---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
lastmod: {{ .Date }}
author: "{{ .Site.Author.name }}"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1580351936/Blog-personal/thumbnail/default.jpg"]
categories: ["category1"]
tags: ["tag1","tag2"]
archives: ["{{ dateFormat "2006" .Date }}","{{ dateFormat "2006-01" .Date }}"]
toc: true
draft: true
---

