---
title: "Create infomall.org"
linkTitle: "Create infomall"
weight: 100
description: >-
     Description on how to create infomall.org
tags: 
- hugo
---

We assume you have hugo installed and cloudmesh-vpn is installed

You need to have python 3

| computer> |
| --- |
```
python -m venv ~/ENV3
source ~/ENV3/bin/activate  # if windows in gitbash source ~/ENV3/Scripts/activate
pip install cloudmesh-vpn -U
cms help
```

## Creating a draft

To create a new version of the code from the repository use

| rivanna terminal 1> |
| --- |
```bash
git clone git@github.com:DSC-SPIDAL/infomall-org-uva.git
make serve
```

To view the content say

| rivanna terminal 2> |
| --- |
```bash
make view
```

## Publish

The Web site is currently published by Gregor as follows. No other person must publish it.

| computer> |
| --- |
```bash
cms vpn info # make sure vpn is set tu UVA
cms vpn connect # only needed if vpn is off
make huge
make rsync
cms vpn disconnect #optional to make sure vpn is off
```

