---
title: "Hugo Blog Using Hugoplate Template"
meta_title: ""
description: "this is meta description"
date: 2022-04-04T05:00:00Z
image: "/images/image-placeholder.png"
categories: ["Application", "Data"]
author: "John Doe"
tags: ["nextjs", "tailwind"]
draft: false
---

## Updating Hugo Blog Workflow Utilizing Hugoplate Theme

`brew install hugo`
No need to install go

check version of hugo installed using
`brew list --version hugo`

I am using the Hugoplate theme which has go and node as a dependency. Otherwise installing hugo should have sufficed.

Install go using `brew install go`
Note that the synonyms are golang, go@1.21, google-go
Check the version by `go version`
Note the lack of -- before the version
It will output `$ go version go1.21.6 darwin/amd64`

Follow the instructions to setup hugoplate template

Setup remote repo so that source is original/main, which gets pulled to main. And the other local branch to work on is master which is then pushed to the target as origin/master
`git branch -a`
main
master
remotes/origin/master
remotes/original/main

Checking the remote branches is as following
`git remote -v`
origin	git@github.com:doctopus/doctopus.github.io.git (fetch)
origin	git@github.com:doctopus/doctopus.github.io.git (push)
original	git@github.com:zeon-studio/hugoplate.git (fetch)
original	git@github.com:zeon-studio/hugoplate.git (push)


### Workflow

**Fetch Updates from `original/main`:**
Start by fetching the latest changes from `original/main`.


```
git fetch original main
```

**Update Local `main`:**
Update your local `main` branch with the changes from `original/main`.

```
git checkout main 
git merge original/main`
```

**Create and Checkout Local `master`:**
Create a local `master` branch and switch to it.

```
git checkout master
```

**Merge Changes from `main` into `master`:**
Merge the changes from `main` into your local `master`.

```
git merge main
```
Resolve any merge conflicts if they occur.

**Work on Local `master`:**
Make your changes on the local `master` branch.

```
# Make changes 
git add .
git commit -m "Your commit message"
```

**Push Changes to `origin/master`:**
Push your changes to the `origin/master` branch.

`git push origin master`

> This workflow ensures that your `main` branch always reflects the changes from `original/main`, and you work on your modifications in the local `master` branch. The changes made in `master` can be pushed to `origin/master` when you are ready.

Remember to resolve any conflicts that may arise during merges and ensure that your local branches are in sync with the remote branches before making any updates.
