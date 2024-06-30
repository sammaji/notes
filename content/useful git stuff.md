---
title: useful git stuff
tags:
  - git
  - tips-and-tricks
draft: false
---
### git alias
```
git config --global alias.[ALIAS_NAME] 'COMMAND'
---
git config --global alias.staash 'stash --all'

# run non git commands using a "!" before it
git config --global alias.bb '!better_search.sh'
```

### log history of code

this code will show you which commits modified a file and what is modified after each commit.

```
git log -L 15,26:/path/to/file

-- or --

git log -L :File:/path/to/file
```

## blame, but ignore white-spaces and code movements

to ignore white-space changes.
```
git blame -w
```

to ignore code movements.
```
git blame -C
```

one `-C` -> ignore all code movements in that commit.
two `-C` -> ignore all code movements in that commit or the commit that created the file.
three `-C` -> ignore all code movements in all commits.

so, to ignore code movements (copy or delete) across all commit, in git blame, use this command.
```
git blame -C -C -C
```

## log with regex
the command below is used to search logs using a regex.
```
git log -S REGEX -p
```

## git word diff
shows the diff, in the same line, instead of two lines.
```
git diff --word-diff
```

### auto-resolve same merge conflicts
if git sees a merge conflict, it will remember it and then try to auto resolve it, next time it encounters it.
```
git config --global rerere.enabled true
```

### make repository faster
run this command to make your git repository faster. if you do this in a repo, git will run a cron job regularly (probably, hourly), and make that repo faster.
```
git maintenance start
```
# SOURCE

<iframe width="560" height="315" src="https://www.youtube.com/embed/aolI_Rz0ZqY?si=5rrVc9c31o3hTL15" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Md44rcw13k4?si=EoMf-Q3BJFKVZMw6" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>