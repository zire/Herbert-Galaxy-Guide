# Git Handbook

## Basic usage

```
$ git add .
$ git commit -m "write something meaningful"
$ git push
```

## Update Remote URL

When remote URL has changed, git push still works, but the following message will appear：

```
remote: This repository moved. Please use the new location:
remote: git@github.com:joesmith/new-remote-name.git
```

First, check what is the current remote origin

```
$ git remote -v
```

Then, delete the outdated remote origin and add the new remote origin

```
$ git remote rm origin
$ git remote add origin git@github.com:joesmith/new-remote-name.git
```

It will take the next git push to make this effective. During the next git push, do this:

```
$ git push --set-upstream origin master
```

Then carry on with git push to complete the full loop.

***

[Back to HitichHikder's Guide by Herbert](README.md)