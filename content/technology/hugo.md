---
title: "Hugo on GitHub Pages with Travis"
date: 2019-06-18T18:32:59+08:00
author:
  name: "Jane"
comments: true
description: "Hugo on GitHub Pages with Travis CI"
keywords: ["hugo","github","Travis","CI"]
images:
tags:
  - hugo
  - Travis
  - CI
---

### Preparation steps

1.Install hugo on your local system.

2.Create a bot user account on GitHub.

### create two repositories on Github

use two repositories: one for sources and another for publishing

- publishing repositories named like **\<user/org name>\.github.io** for your HTML content,and if you hava domain,you can go to **Settings** fill in your Custom domain and enable **Enforce HTTPS**.

- sources repositories named like **Blog**.

### Put your secrets to travis settings
1.New personal access token

In your github [New personal access token](https://github.com/settings/tokens/new),**Token description** fill in token name and enable all about **repo**,then get token ,copy it.

2.Setting Travis CI

In order to get the HTML content pushed to GitHub Pages, you have to create a secret variable in the Travis CI settings of your repository, which contains hugo source files.

- Login [Travis CI](www.tracis.eu) with github account,then you will find your github repositories in Travis.
- Turn on **Blog** repositories and click **Settings**.
- Environment Variables：Name fill in "GITHUB_TOKEN",Value fill in your github token.
- click **Add**.


{{<figure src="//images/hugo-travis1.png" alt="hugo-travis1">}}

{{<figure src="//images/hugo-travis2.png" alt="hugo-travis2">}}
### Revise config.toml
### Create travis configuration
```yml
language: go
go:
  - master # This uses automatically the latest version of go
# Specify which branches to build using a safelist
# branches:
#   only:
#     - master 
install:
  - wget https://github.com/gohugoio/hugo/releases/download/v0.55.5/hugo_0.55.5_Linux-64bit.deb
  - sudo dpkg -i hugo*.deb
  # themes
  # - git clone https://github.com/rhazdon/hugo-theme-hello-friend-ng.git themes/hello-friend-ng


script:
  # run hugo
  - hugo
after_script:
  # 部署
  - cd ./public
  - git init
  - git config user.name "github user name"
  - git config user.email "github email" 
  - git add .
  - git commit -m "Update Blog By TravisCI With Build $TRAVIS_BUILD_NUMBER"
  # Github Pages
  - git push --force --quiet "https://$GITHUB_TOKEN@${GH_REF}" master:master
  # Github Pages
  - git push --quiet "https://$GITHUB_TOKEN@${GH_REF}" master:master --tags


env:
 global:
   # Github Pages
   - GH_REF = "github.com/your/your.github.io"

deploy:
  local_dir: public # Default static site output dir for Hugo
  repo: your/your.github.io 
  provider: pages
  target-branch: master
  skip_cleanup: true
  github_token: $GITHUB_TOKEN # This is the authentication which you will setup in the next step in travis-ci dashboard
  email: your
  name: "your"
  fqdn: https://your.com # domain
  keep-history: true # 
  on:
    branch: master  
```
### Create .gitignore 
```
public/*
themes/*
resources/*
```