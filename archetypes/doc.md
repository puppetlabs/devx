---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
description: "ENTER DESCRIPTION HERE"
github_repo: "https://github.com/puppetlabs/pdkgo"
draft: true
---

**Insert Lead paragraph here.**

## New Cool Posts

{{ range first 10 ( where .Site.RegularPages "Type" "cool" ) }}
* {{ .Title }}
{{ end }}