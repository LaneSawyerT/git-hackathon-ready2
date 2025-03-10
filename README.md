# README: How to Collaborate on a GitHub Project

## 📌 Introduction
This guide explains how to contribute to a GitHub project, step by step. Follow these instructions to fork, clone, make changes, and submit a pull request.

---
# How to collaborate in a GitHub project:
- Review collaboration policy in the project
- Fork the repo
- Clone forked repo
- Update master branch
- Create a branch
- Make our improvements
- Create a pull request
- Sync a fork
- Rebasing a pull request


## It's important to take a look to documentation related with collaboration in the project in which we want to contribute

## Fork the repo in which you want to collaborate lets say this repo: 

[https://github.com/jmsampayo/gazelle-analyser-api.git](https://github.com/jmsampayo/gazelle-analyser-api.git)

## Clone our fork:

`git clone https://github.com/neklaf/gazelle-analyser-api.git`

## Let's add the URL from the original repository:

`git remote add upstream https://github.com/jmsampayo/gazelle-analyser-api.git`

Let's check if everything is in its place:
```
git remote -v
origin	https://github.com/neklaf/gazelle-analyser-api.git (fetch)
origin	https://github.com/neklaf/gazelle-analyser-api.git (push)
upstream	https://github.com/jmsampayo/gazelle-analyser-api.git (fetch)
upstream	https://github.com/jmsampayo/gazelle-analyser-api.git (push)
```

## Update master branch:

Update to the last changes in the repo:

```
git pull -r upstream master
From https://github.com/jmsampayo/gazelle-analyser-api.git
```

## Create a new branch to contain our changes:

`git checkout -b my-collaboration-feature`

## Make our changes:

```
vim README.md
git status -s
  M README.md
```
### Let's commit our changes:

```
git add README.md
git commit -m 'Added my awesome new feature to the project in which I collaborate'
```

### And push them:
```
git push --set-upstream origin my-collaboration-feature
Already up to date.
```

## It's needed to create a pull request and you should considered to link that PR with an opened issue (from GitHub web interface)

## Sync a fork
### Fetch branches and commits
Get branches and their commits from the upstream repository. Commits to master will be stored in a local branch, upstream/master

```
$ git fetch upstream
...
> From https://github.com/jmsampayo/gazelle-analyser-api.git
>  * [new branch]      master     -> upstream/master
```
### Check out your fork's local master branch
```
$ git checkout master
> Switched to branch 'master'
```
### Merge the changes from upstream/master into your local master branch
`$ git merge upstream/master`

If your local branch didn't have any unique commits, Git will instead perform a "fast-forward":
```
$ git merge upstream/master
> Updating xxx..yyy
> Fast-forward
>  README.md                 |    3 ++-
>  1 file changed, 3 insertions(+), 1 deletion(-)
```

## Rebase a pull request
(As a reference)[https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request]

### Prepare fork for rebasing
It's needed to ensure your fork is synchronized with the upstream repo (take a look to Sync a fork)

### Rebasing
Checkout the branch from which we originally created the PR. You could execute `git fetch` if you no longer have your branch locally.
`$ git checkout my-collaboration-feature` 

Run the rebase on top of our development branch.
`$ git rebase upstream/master`

The last step is to force push the changes. This will ensure your rebase will replace the outdated PR.
`$ git push -f`

### What if there are changes required in your PR?
A best practice is to have only one commit in your PR. Of course you could make several commits, but be sure to squash your changes.

To squash the last N consecutive commits into a single commit (this works better when you're working with feature branches and can’t commit to master:

```
$ git reset --soft HEAD~5
$ git commit -m "ID-1234 | Improve code quality"
```
And, since we’ve already pushed changes to the remote previously, we could do:

`$ git push origin +my-collaboration-feature`
The + signs basically acts as a force push to rewrite history.

- References:
(https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)[https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History]
(http://stackoverflow.com/a/5201642/295797)[http://stackoverflow.com/a/5201642/295797]
(https://feeding.cloud.geek.nz/posts/combining-multiple-commits-into-one/)[https://feeding.cloud.geek.nz/posts/combining-multiple-commits-into-one/]

NOTE: This will create a git nb alias that will create a new branch tracking the current branch and checking it out. You can then use it like that:
`$ git config --global alias.foo '!git checkout --track $(git config branch.$(git rev-parse --abbrev-ref HEAD).remote)/$(git rev-parse --abbrev-ref HEAD) -b'`

