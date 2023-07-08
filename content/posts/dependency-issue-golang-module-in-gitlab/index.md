---
title: "Dependency issue golang Module in Gitlab"
date: 2021-09-24T15:12:39+07:00
# draft: true
categories: ["git", "golang"]
tags: ["golang","go module","gitlab"]
# resources:
# - src: images/github-env.png
#   title: Github environment look like
# - src: images/gitlab-env.png
#   title: Gitlab environment look like
Description: Handle Dependency issue in golang Module within private Gitlab like a bos
---

Manage dependency in golang is quite easy, the module path like `git.company.com/product/tools/adapter/db/mongo` can 

When you hosting your code privately in gitlab.com or your company (e.g: git.company.com) 

Most of the time people who using github.com as their base for Go module don't have this issues.
How do you get it work with Go modules (privately!)

Common issue for private module, triggered by `go mod tidy`
```sh
fatal: unable to update url base from redirection:
25 	  asked for: http://git.company.com/product/tools.git/info/refs?service=git-upload-pack
26 	   redirect: https://git.company.com/users/sign_in
```

### Create access token for gitlab authorization
The details you can read details [here](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html)
Create access token here https://git.company.com/profile/personal_access_tokens
![Personal Access Token](images/personal-access-token.png "Make sure check api and read repository")

### Create or edit netrc file
On linux/Mac the location is on `~/.netrc` on windows is on `~/_netrc` 

Here's the contents:
```sh
machine git.company.com
login yourUserName
password YourPersonalAccessToken
```

### Set GOPRIVATE on
`go env -w GOPRIVATE=git.company.com`

### Set Redirect properly for git
```
git config --global url.https://oauth2:YourPersonalAccessToken@git.company.com.insteadOf git.company.com

git config --global url.https://oauth2:YourPersonalAccessToken@git.company.com.insteadOf http://git.company.com
```

This command will force git to always redirect to https