---
title: "Github Actions Hugo Deploy"
date: 2021-08-17T22:50:06-05:00
draft: false
toc: false
images:
tags:
  - untagged
---
After some quick tinkering the gitops style deployment is complete. Ran into an issue where the custom domain was being overwritten due to the publish directory generated from Hugo not containing the CNAME file.

To restore the site I had to drill into the pages settings again and set the domain and check enforce https. In order to fix it for future deployments, I've added the `finnp/create-file-action@master` action to create the CNAME file on each deployment.

Workflow action example.

```yaml
name: hugo CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true
          fetch-depth: 1

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'

      - name: Build
        run: hugo --minify

      # Setup CNAME
      - uses: "finnp/create-file-action@master"
        env:
          FILE_NAME: "./public/CNAME"
          FILE_DATA: "domain.com"

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          personal_token: ${{ secrets.PERSONAL_TOKEN }}
          external_repository: username/username.github.io
          publish_branch: main
          publish_dir: ./public
```
