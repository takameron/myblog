---
title: "OpenStack Horizonを使ってConoHaを使う（ログインするところだけ）"
date: 2025-07-21T20:08:00+09:00
lastmod: 2025-07-21T20:08:00+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1752922017/Blog-personal/conoha_with_openstack_horizon/thumbnail.png"]
categories: ["プログラミング"]
tags: ["ConoHa","OpenStack Horizon"]
archives: ["2025","2025-07"]
description: "OpenStack HorizonでConoHaの公開APIを使ってログインするところだけ試してみました。"
toc: true
draft: false
---

[ConoHa](https://www.conoha.jp/)のVPSでは、クラウド基盤であるOpenStackの機能を用いた[API](https://doc.conoha.jp/reference/api-vps3/)が公開されています。
OpenStackのCLIコマンドを用いてリソースを表示したり操作したりできます（[リファレンス](https://doc.conoha.jp/reference/openstack-cli/)）。

OpenStackのAPIが公開されているということは、OpenStack公式のGUIツールである[OpenStack Horizon](https://docs.openstack.org/horizon/latest/)が使えるのではと思い、試してみました。

Dockerコンテナとして構築します。

Dockerファイルは下記の通りです（注：このままだと動きません）。
openstack-dashboardで一通り入りますが、キャッシュに用いられているmemcachedもインストールします。

```Dockerfile
FROM ubuntu/apache2:2.4-24.04_edge

RUN apt-get update && apt-get upgrade -y \
&& apt-get install -y memcached openstack-dashboard

EXPOSE 80
```

docker-compose.ymlファイルは下記の通りです。
[ドキュメント](https://doc.conoha.jp/reference/openstack-cli/openstack-cli-install/)とConoHaにログインして確認できる情報から値を設定しました。

```docker-compose.yml
services:
  horizon:
    build: .
    container_name: horizon
    environment:
      - OS_AUTH_URL=https://identity.c3j1.conoha.io/v3
      - OS_USER_DOMAIN_NAME=gnc
      - OS_PROJECT_DOMAIN_ID=gnc
      - OS_PROJECT_ID='YOUR_TENANT_ID'
      - OS_PROJECT_NAME='YOUR_TENANT_NAME'
      - OS_USERNAME='YOUR_USERNAME'
      - OS_PASSWORD='YOUR_PASSWORD'
      - OS_REGION_NAME=c3j1
      - OS_INTERFACE=public
      - OS_IDENTITY_API_VERSION=3
    ports:
      - '8000:80'
```

`docker compose up` でコンテナを起動し http://localhost:8000/horizon を開くとOpenStack Horizonのページが開きます。

### 調査方法編 {#research-methodology}

Visual Studio Codeを使い、「Container Tools」というMicrosoft公式の拡張機能を使いました。
コンテナ内のどのディレクトリにどのファイルがあるのか、ファイルの内容の確認や編集がローカルと同じようにできます。
特にDockerコンテナのような使えるコマンドがとても少ない環境でとても便利です。

コンテナを調査するには下記のコマンドを使用します。

| 内容 | コマンド |
| :--- | :--- |
| コンテナの起動 | `docker compose up` |
| コンテナ内のシェルを開く | `docker compose exec horizon /bin/bash` |
| コンテナ内のログを表示する | `docker compose logs horizon` |

UbuntuにおいてOpenStack Horizonの認証に関係するのは下記のファイル・ディレクトリです。

| ファイル・ディレクトリ | 内容 |
| :--- | --- |
| `/etc/openstack-dashboard/local_settings.py` | OpenStack Horizonの設定ファイル |
| `/usr/lib/python3/dist-packages/openstack_auth` | 認証関係のロジック |

その他として下記のディレクトリがあります。

| ファイル | 内容 |
| :--- | --- |
| `/usr/share/openstack-dashboard` | ユーザが使用するコマンド |
| `/var/lib/openstack-dashboard` | OpenStack HorizonのUI部分 | 
| `/usr/lib/python3/dist-packages/openstack` |  |
| `/usr/lib/python3/dist-packages/openstack_dashboard` |  |
| `/usr/lib/python3/dist-packages/openstackclient` | [python-openstackclient](https://pypi.org/project/python-openstackclient/) |

デバッグのためにログを出力するようにします。
`/etc/openstack-dashboard/local_settings.py` を開き、 `DEBUG` をTrueにします。

```diff {linenos=false}
-- DEBUG = False
++ DEBUG = True
```

また、 `loggers` → `horizon.operation_log` の `level` を `INFO` から `DEBUG` に変更します。

```diff {linenos=false}
    'loggers': {
        'horizon': {
            'handlers': ['console'],
            'level': 'DEBUG',
            'propagate': False,
        },
        'horizon.operation_log': {
            'handlers': ['operation'],
--          'level': 'INFO',
++          'level': 'DEBUG',
            'propagate': False,
        },
```

末尾にあるコメントアウトされている設定のコメントを外し、 `OPERATION_LOG_ENABLED = True` も追記します。

```diff {linenos=false}
--  # OPERATION_LOG_OPTIONS = {
--  #     'mask_fields': [],
--  #     'target_methods': ['POST'],
--  #     'ignored_urls': ['/js/', '/static/'],
--  #     'format': ("[%(domain_name)s] [%(domain_id)s] [%(project_name)s]"
--  #         " [%(project_id)s] [%(user_name)s] [%(user_id)s] [%(request_scheme)s]"
--  #         " [%(referer_url)s] [%(request_url)s] [%(message)s] [%(method)s]"
--  #         " [%(http_status)s] [%(param)s]"),
--  # }
++  OPERATION_LOG_ENABLED = True
++  OPERATION_LOG_OPTIONS = {
++      'mask_fields': [],
++      'target_methods': ['POST'],
++      'ignored_urls': ['/js/', '/static/'],
++      'format': ("[%(domain_name)s] [%(domain_id)s] [%(project_name)s]"
++          " [%(project_id)s] [%(user_name)s] [%(user_id)s] [%(request_scheme)s]"
++          " [%(referer_url)s] [%(request_url)s] [%(message)s] [%(method)s]"
++          " [%(http_status)s] [%(param)s]"),
++  }
```

変更は下記のコマンドで反映されます。

```sh {linenos=false}
service apache2 reload
```

ここでキャッシュ関係（memcached）のエラーが発生した場合は、まずは `service memcached restart` を実行します。

それで解決しない場合は `python3 /usr/share/openstack-dashboard/manage.py compress` を実行することで解決できます。
これで解決した場合は今後もエラーが発生しやすく、高速化のためだけにあるので、無効化するには `/etc/openstack-dashboard/local_settings.py` の上部にある `COMPRESS_ENABLED = not DEBUG` や `COMPRESS_OFFLINE = not DEBUG` のコメントをはずします。

```diff {linenos=false}
    # This setting controls whether or not compression is enabled. Disabling
    # compression makes Horizon considerably slower, but makes it much easier
    # to debug JS and CSS changes
--  #COMPRESS_ENABLED = not DEBUG
++  COMPRESS_ENABLED = not DEBUG

    # This setting controls whether compression happens on the fly, or offline
    # with `python manage.py compress`
    # See https://django-compressor.readthedocs.io/en/latest/usage/#offline-compression
    # for more information
--  #COMPRESS_OFFLINE = not DEBUG
++  COMPRESS_OFFLINE = not DEBUG
```

また、下部にある `COMPRESS_OFFLINE = True` をコメントアウトします。

```diff {linenos=false}
    # Compress all assets offline as part of packaging installation
--  COMPRESS_OFFLINE = True
++  #COMPRESS_OFFLINE = True
```

これで `service apache2 reload` を実行すると反映されます。

ConoHaでのログインを試すと、[OpenStackのIdentity API](https://docs.openstack.org/api-ref/identity/v3/)ではパスワード認証に加えてトークン認証やプロジェクトの一覧の取得など様々なAPIが存在しますが、[ConoHaで公開されているIdentity API](https://doc.conoha.jp/reference/api-vps3/api-identity-vps3/)ではパスワード認証でトークンを発行するAPIしか公開されていないことがわかりました。
OpenStack Horizonでは、 `openstack` コマンドとは違うPOSTパラメータであったり様々なAPIを使用していたりするため、認証エラーや404が返ってくるAPIへのアクセスが発生して認証が完了しない状態でした。
それを回避するためソースコードを変更する必要があります。

これを調べるのに、 [requestでPOSTした送信内容(data)を確認したい！ #Python - Qiita](https://qiita.com/takky_0330/items/63083dec97125cdbff9d)の記事にあるプログラムを使用し、ローカルでPythonのHTTPサーバをたて、ソースコード中の認証URLを設定している処理をローカルのURLに置き換えることで、どのようなリクエストを送っているかを確認しながら調査しました。
この変更でも、もちろん `service apache2 reload` で変更を反映させます。

OpenStack HorizonのUI上に表示されるエラーメッセージは[exeptions.py](https://github.com/openstack/horizon/blob/stable/2025.1/openstack_auth/exceptions.py)に定義されています。
エラーに対応した例外クラスを探し、その例外を発生させているコードをGitHub上などで探すことでエラーの原因を探しました。

調査にあたっては下記のサイトが参考になりました。

* [OpenStack API Documentation](https://docs.openstack.org/api-ref/identity/v3/)
* [keystoneclient.v3 package](https://docs.openstack.org/python-keystoneclient/latest/api/keystoneclient.v3.html)
* [keystoneauth1](https://docs.openstack.org/keystoneauth/2025.1/api/modules.html)

また、OpenStack Horizonは[プラグインを作る](https://docs.openstack.org/horizon/latest/contributor/tutorials/plugin.html)ことで機能を拡張することができます。
今回はプラグインの作成のみで対応するのが難しそうだったため、ソースコードを直接書き換えています。

### 実践編 {#practice}

前提として、 `openstack` コマンドを使うと[ドキュメント](https://doc.conoha.jp/reference/openstack-cli/openstack-cli-install/)の通り認証に成功します。
コンテナ内で `openstack` コマンドを使えるようにするには、 `apt install python3-openstackclient` を実行してインストールします。

`openstack` コマンドは環境変数から認証情報を与えられますが、OpenStack Horizonでは `local_settings.py` ファイルを編集する必要があります。

`/etc/openstack-dashboard/local_settings.py` ファイルの末尾に下記を追加します。

```py {linenos=false}
OPENSTACK_KEYSTONE_DEFAULT_DOMAIN = "gnc"
DEFAULT_SERVICE_REGIONS = {
    '*': 'c3j1',
    OPENSTACK_KEYSTONE_URL: 'c3j1',
}
```

また、下記のように書き換えます。

```diff {linenos=false}
    OPENSTACK_HOST = "127.0.0.1"
--  OPENSTACK_KEYSTONE_URL = "http://%s/identity/v3" % OPENSTACK_HOST
++  OPENSTACK_KEYSTONE_URL = "https://identity.c3j1.conoha.io/v3"
```

`service apache2 reload` を実行した上でホスト側で http://localhost:8000/horizon にアクセスし、ConoHaで作成したAPIユーザーでログインします。
そうすると「An error occurred authenticating. Please try again later.」というエラーメッセージが表示され失敗します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1752931738/Blog-personal/conoha_with_openstack_horizon/error1.png" alt="「An error occurred authenticating. Please try again later.」と表示されているログイン画面" caption="ログインが失敗した画面" >}}

この時にOpenStack Horizonでは下記のようなリクエストボディは

```json {linenos=false}
{"auth": {"identity": {"methods": ["password"], "password": {"user": {"password": "YOUR_PASSWORD", "name": "YOUR_USERNAME", "domain": {"name": "gnc"}}}}, "scope": "unscoped"}}
```

`openstack` コマンドでは下記のようなリクエストボディとなっており、 `scope` の値が違います。

```json {linenos=false}
{"auth": {"identity": {"methods": ["password"], "password": {"user": {"password": "YOUR_PASSWORD", "name": "YOUR_USERNAME", "domain": {"name": "gnc"}}}}, "scope": {"project": {"id": "YOUR_TENANT_ID"}}}}
```

原因としては[passwordプラグイン](https://github.com/openstack/horizon/blob/stable/2025.1/openstack_auth/plugin/password.py#L43)においてscopeが渡されていないことが原因です。
[keystoneauth1.identity.v3.passwordモジュール](https://docs.openstack.org/keystoneauth/2025.1/api/keystoneauth1.identity.v3.password.html)モジュールではスコープを指定することができます。

`/usr/lib/python3/dist-packages/openstack_auth/plugin/password.py` を下記のように書き換えて、 `unscoped=True` を消し、スコープにproject_idを追加します。

```diff {linenos=false}
    class PasswordPlugin(base.BasePlugin):
        """Authenticate against keystone given a username and password.

        This is the default login mechanism. Given a username and password inputted
        from a login form returns a v2 or v3 keystone Password plugin for
        authentication.
        """

        def get_plugin(self, auth_url=None, username=None, password=None,
--                  user_domain_name=None, **kwargs):
++                  user_domain_name=None, project_id=None, **kwargs):
            if not all((auth_url, username, password)):
                return None

            LOG.debug('Attempting to authenticate for %s', username)

            return v3_auth.Password(auth_url=auth_url,
                                    username=username,
                                    password=password,
                                    user_domain_name=user_domain_name,
--                                  unscoped=True)
++                                  project_id=project_id)
```

プラグインにproject_idを渡すため、[forms.py](https://github.com/openstack/horizon/blob/stable/2025.1/openstack_auth/forms.py#L123)のauthenticateメソッドに引数を追加します。

`/usr/lib/python3/dist-packages/openstack_auth/forms.py` を下記にように変更します。

```diff {linenos=false}
    @sensitive_variables()
    def clean(self):
        default_domain = settings.OPENSTACK_KEYSTONE_DEFAULT_DOMAIN
        username = self.cleaned_data.get('username')
        password = self.cleaned_data.get('password')
        domain = self.cleaned_data.get('domain', default_domain)
        region_id = self.cleaned_data.get('region')
        try:
            region = get_region_endpoint(region_id)
        except (ValueError, IndexError, TypeError):
            raise forms.ValidationError("Invalid region %r" % region_id)
        self.cleaned_data['region'] = region
++      project_id = settings.OPENSTACK_KEYSTONE_PROJECT_ID

        if not (username and password):
            # Don't authenticate, just let the other validators handle it.
            return self.cleaned_data

        try:
            self.user_cache = authenticate(request=self.request,
                                           username=username,
                                           password=password,
                                           user_domain_name=domain,
--                                         auth_url=region)
++                                         auth_url=region,
++                                         project_id=project_id)
            LOG.info('Login successful for user "%(username)s" using domain '
                     '"%(domain)s", remote address %(remote_ip)s.',
                     {'username': username, 'domain': domain,
                      'remote_ip': utils.get_client_ip(self.request)})
        except exceptions.KeystonePassExpiredException as exc:
            LOG.info('Login failed for user "%(username)s" using domain '
                     '"%(domain)s", remote address %(remote_ip)s: password'
                     ' expired.',
                     {'username': username, 'domain': domain,
                      'remote_ip': utils.get_client_ip(self.request)})
            if utils.allow_expired_passowrd_change():
                raise
            raise forms.ValidationError(exc)
        except exceptions.KeystoneTOTPRequired as exc:
            LOG.info('Login failed for user "%(username)s" using domain '
                     '"%(domain)s", remote address %(remote_ip)s: TOTP'
                     'required.',
                     {'username': username, 'domain': domain,
                      'remote_ip': utils.get_client_ip(self.request)})
            if settings.OPENSTACK_KEYSTONE_MFA_TOTP_ENABLED:
                raise
            raise forms.ValidationError(exc)
        except exceptions.KeystoneAuthException as exc:
            LOG.info('Login failed for user "%(username)s" using domain '
                     '"%(domain)s", remote address %(remote_ip)s.',
                     {'username': username, 'domain': domain,
                      'remote_ip': utils.get_client_ip(self.request)})
            raise forms.ValidationError(exc)
        return self.cleaned_data
```

`/etc/openstack-dashboard/local_settings.py` ファイルの末尾に下記を追加します。

```py {linenos=false}
OPENSTACK_KEYSTONE_PROJECT_ID = 'YOUR_TENANT_ID'
```

この対応をして `service apache2 reload` を実行した後で再度ログインを試すと、「Unable to retrieve authorized projects.」というエラーで失敗します。

認証処理をしているのは[こちら](https://github.com/openstack/horizon/blob/stable/2025.1/openstack_auth/backend.py#L96)であり、 `openstack token issue` コマンドに相当する処理が行われるのは下記の箇所です。

```py {linenos=false}
# the recent project id a user might have set in a cookie
recent_project = None
if request:
    # Grab recent_project found in the cookie, try to scope
    # to the last project used.
    recent_project = request.COOKIES.get('recent_project')
unscoped_auth_ref = plugin.get_access_info(unscoped_auth,
                                            session=session)
```

その後に続く下記の箇所で[get_domain_scoped_auth](https://github.com/openstack/horizon/blob/stable/2025.1/openstack_auth/plugin/base.py#L212)と[get_project_scoped_auth](https://github.com/openstack/horizon/blob/stable/2025.1/openstack_auth/plugin/base.py#L162)というメソッドを呼び出し、それらのメソッド内でConoHaの公開APIには存在しないAPIを呼び出しているためエラーになっています。

```py {linenos=false}
domain_name = kwargs.get('user_domain_name', None)
domain_auth, domain_auth_ref = plugin.get_domain_scoped_auth(
    unscoped_auth, unscoped_auth_ref, domain_name, session=session)
scoped_auth, scoped_auth_ref = plugin.get_project_scoped_auth(
    unscoped_auth, unscoped_auth_ref, recent_project=recent_project,
    session=session)
```

OpenStack Horizonの挙動としては、まずはパスワード認証でトークンを発行後、トークン認証でドメインまたはプロジェクトをスコープに設定して認証しようとしますが、ConoHaの公開APIではパスワード認証しかできません。

そのためすでに認証済みの情報を最後まで使い回す必要があります。
下記のように `get_domain_scoped_auth` と `get_project_scoped_auth` を呼び出している箇所をコメントアウトし、 `scoped_auth_ref` を使っている箇所を `unscoped_auth_ref` に置き換えます。

```diff {linenos=false}
    def authenticate(self, request, auth_url=None, **kwargs):
        """Authenticates a user via the Keystone Identity API."""
        LOG.debug('Beginning user authentication')

        if not auth_url:
            auth_url = settings.OPENSTACK_KEYSTONE_URL

        auth_url, url_fixed = utils.fix_auth_url_version_prefix(auth_url)
        if url_fixed:
            LOG.warning("The OPENSTACK_KEYSTONE_URL setting points to a v2.0 "
                        "Keystone endpoint, but v3 is specified as the API "
                        "version to use by Horizon. Using v3 endpoint for "
                        "authentication.")

        plugin, unscoped_auth = self._get_auth_backend(auth_url, **kwargs)

        client_ip = utils.get_client_ip(request)
        session = utils.get_session(original_ip=client_ip)

        # the recent project id a user might have set in a cookie
        recent_project = None
        if request:
            # Grab recent_project found in the cookie, try to scope
            # to the last project used.
            recent_project = request.COOKIES.get('recent_project')
        unscoped_auth_ref = plugin.get_access_info(unscoped_auth,
                                                   session=session)

        # Check expiry for our unscoped auth ref.
        self._check_auth_expiry(unscoped_auth_ref)

--      domain_name = kwargs.get('user_domain_name', None)
--      domain_auth, domain_auth_ref = plugin.get_domain_scoped_auth(
--          unscoped_auth, unscoped_auth_ref, domain_name, session=session)
--      scoped_auth, scoped_auth_ref = plugin.get_project_scoped_auth(
--          unscoped_auth, unscoped_auth_ref, recent_project=recent_project,
--          session=session)
--
--      # Abort if there are no projects for this user and a valid domain
--      # token has not been obtained
--      #
--      # The valid use cases for a user login are:
--      #    Keystone v2: user must have a role on a project and be able
--      #                 to obtain a project scoped token
--      #    Keystone v3: 1) user can obtain a domain scoped token (user
--      #                    has a role on the domain they authenticated to),
--      #                    only, no roles on a project
--      #                 2) user can obtain a domain scoped token and has
--      #                    a role on a project in the domain they
--      #                    authenticated to (and can obtain a project scoped
--      #                    token)
--      #                 3) user cannot obtain a domain scoped token, but can
--      #                    obtain a project scoped token
--      if not scoped_auth_ref and domain_auth_ref:
--          # if the user can't obtain a project scoped token, set the scoped
--          # token to be the domain token, if valid
--          scoped_auth = domain_auth
--          scoped_auth_ref = domain_auth_ref
--      elif not scoped_auth_ref and not domain_auth_ref:
--          msg = _('You are not authorized for any projects or domains.')
--          raise exceptions.KeystoneNoProjectsException(msg)
--
--      # Check expiry for our new scoped token.
--      self._check_auth_expiry(scoped_auth_ref)

++     # domain_name = kwargs.get('user_domain_name', None)
++     # domain_auth, domain_auth_ref = plugin.get_domain_scoped_auth(
++     #     unscoped_auth, unscoped_auth_ref, domain_name, session=session)
++     # scoped_auth, scoped_auth_ref = plugin.get_project_scoped_auth(
++     #     unscoped_auth, unscoped_auth_ref, recent_project=recent_project,
++     #     session=session)
++     #
++     # # Abort if there are no projects for this user and a valid domain
++     # # token has not been obtained
++     # #
++     # # The valid use cases for a user login are:
++     # #    Keystone v2: user must have a role on a project and be able
++     # #                 to obtain a project scoped token
++     # #    Keystone v3: 1) user can obtain a domain scoped token (user
++     # #                    has a role on the domain they authenticated to),
++     # #                    only, no roles on a project
++     # #                 2) user can obtain a domain scoped token and has
++     # #                    a role on a project in the domain they
++     # #                    authenticated to (and can obtain a project scoped
++     # #                    token)
++     # #                 3) user cannot obtain a domain scoped token, but can
++     # #                    obtain a project scoped token
++     # if not scoped_auth_ref and domain_auth_ref:
++     #     # if the user can't obtain a project scoped token, set the scoped
++     #     # token to be the domain token, if valid
++     #     scoped_auth = domain_auth
++     #     scoped_auth_ref = domain_auth_ref
++     # elif not scoped_auth_ref and not domain_auth_ref:
++     #     msg = _('You are not authorized for any projects or domains.')
++     #     raise exceptions.KeystoneNoProjectsException(msg)
++     #
++     # # Check expiry for our new scoped token.
++     # self._check_auth_expiry(scoped_auth_ref)
     
        # We want to try to use the same region we just logged into
        # which may or may not be the default depending upon the order
        # keystone uses
        region_name = None
--      id_endpoints = scoped_auth_ref.service_catalog.\
++      id_endpoints = unscoped_auth_ref.service_catalog.\
            get_endpoints(service_type='identity')
        for id_endpoint in id_endpoints['identity']:
            if auth_url in id_endpoint.values():
                region_name = id_endpoint['region']
                break

        if settings.OPENSTACK_KEYSTONE_ENDPOINT_TYPE:
            interface = settings.OPENSTACK_KEYSTONE_ENDPOINT_TYPE
        else:
            interface = settings.OPENSTACK_ENDPOINT_TYPE

--      endpoint = scoped_auth_ref.service_catalog.url_for(
++      endpoint = unscoped_auth_ref.service_catalog.url_for(
            service_type='identity',
            interface=interface,
            region_name=region_name)

        # If we made it here we succeeded. Create our User!
        unscoped_token = unscoped_auth_ref.auth_token

        user = auth_user.create_user_from_token(
            request,
--          auth_user.Token(scoped_auth_ref, unscoped_token=unscoped_token),
++          auth_user.Token(unscoped_auth_ref, unscoped_token=unscoped_token),
            endpoint,
            services_region=region_name)

--       if request is not None:
--           # if no k2k providers exist then the function returns quickly
--           utils.store_initial_k2k_session(auth_url, request, scoped_auth_ref,
--                                           unscoped_auth_ref)
--           request.session['unscoped_token'] = unscoped_token
--           if domain_auth_ref:
--               # check django session engine, if using cookies, this will not
--               # work, as it will overflow the cookie so don't add domain
--               # scoped token to the session and put error in the log
--               if utils.using_cookie_backed_sessions():
--                   LOG.error('Using signed cookies as SESSION_ENGINE with '
--                             'OPENSTACK_KEYSTONE_MULTIDOMAIN_SUPPORT is '
--                             'enabled. This disables the ability to '
--                             'perform identity operations due to cookie size '
--                             'constraints.')
--               else:
--                   request.session['domain_token'] = domain_auth_ref
--
--           request.user = user
--           timeout = settings.SESSION_TIMEOUT
--           token_life = (user.token.expires -
--                         datetime.datetime.now(datetime.timezone.utc))
--           session_time = min(timeout, int(token_life.total_seconds()))
--           request.session.set_expiry(session_time)
--
--           keystone_client_class = utils.get_keystone_client().Client
--           scoped_client = keystone_client_class(session=session,
--                                                 auth=scoped_auth)
--
--           # Support client caching to save on auth calls.
--           setattr(request, KEYSTONE_CLIENT_ATTR, scoped_client)

++      # if request is not None:
++      #     # if no k2k providers exist then the function returns quickly
++      #     utils.store_initial_k2k_session(auth_url, request, scoped_auth_ref,
++      #                                     unscoped_auth_ref)
++      #     request.session['unscoped_token'] = unscoped_token
++      #     if domain_auth_ref:
++      #         # check django session engine, if using cookies, this will not
++      #         # work, as it will overflow the cookie so don't add domain
++      #         # scoped token to the session and put error in the log
++      #         if utils.using_cookie_backed_sessions():
++      #             LOG.error('Using signed cookies as SESSION_ENGINE with '
++      #                       'OPENSTACK_KEYSTONE_MULTIDOMAIN_SUPPORT is '
++      #                       'enabled. This disables the ability to '
++      #                       'perform identity operations due to cookie size '
++      #                       'constraints.')
++      #         else:
++      #             request.session['domain_token'] = domain_auth_ref
++
++      #     request.user = user
++      #     timeout = settings.SESSION_TIMEOUT
++      #     token_life = (user.token.expires -
++      #                   datetime.datetime.now(datetime.timezone.utc))
++      #     session_time = min(timeout, int(token_life.total_seconds()))
++      #     request.session.set_expiry(session_time)
++
++      #     keystone_client_class = utils.get_keystone_client().Client
++      #     scoped_client = keystone_client_class(session=session,
++      #                                           auth=scoped_auth)
++
++      #     # Support client caching to save on auth calls.
++      #     setattr(request, KEYSTONE_CLIENT_ATTR, scoped_client)

        LOG.debug('Authentication completed.')
        return user
```

これで、ひとまずはログインできました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1752922017/Blog-personal/conoha_with_openstack_horizon/thumbnail.png" alt="OpenStack Horizonのログイン後のページ。右上にエラーが並んでいる。" caption="OpenStack Horizon" >}}

右上にエラーが並んでいるように、HTTPのステータスコードが400や404のエラーが多く、一通りのページを確認したところほとんど使い物になりませんでした。

さらにソースコードの変更が必要そうですが、この記事ではここまでとします。
