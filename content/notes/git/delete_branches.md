---
title: "Delete branches"
date: 2024-09-04T15:02:44-05:00
draft: false
weight: 210
menu:
  notes:
    name: Delete branches
    identifier: notes-git-deletebranches
    parent: notes-git
    weight: 10
---




{{< note title="Git: Delete local branches that no longer exist on origin" >}}

Fetch the latest updates from the remote

```shell
git fetch --prune
```

List branches that have been deleted on the remote but still exist locally

```shell
git branch -vv | grep ': gone' | awk '{print $1}'
```

Delete the local branches that no longer exist on the remote

```shell
git branch -vv | grep ': gone' | awk '{print $1}' | xargs git branch -d
```


{{< /note >}}
