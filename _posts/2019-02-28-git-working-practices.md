---
layout: post
title: Git and Github working practices, a reflective approach
author: David Jones
slug: 2019-02-28-git-working-practices
date: 2019-02-28 12:00:00 UTC+00:00
tags: git vcs
category: tutorials
link:
description:
type: text
---

# Observing a git repo

By observing an existing git repo we can
form qualitative assessments of a group's working processes, and
determine and prioritise which best practices a group should adopt next.

Consider the git repo for this blog: https://github.com/RSE-Sheffield/RSE-Sheffield.github.io

I'm going to use GitHub's _network_ tool to
examine the commit structure of this repo.
The network tool is available on the *Insights* tab.

![A screenshot of github, with the Insights tab and Network tool selected](
assets/images/github-working/github-working00network.png){: .img-fluid}

In the beginning, life is good;
commits either appear on the _master_ branch or
on a series of short lived development branches.

Later on we see something like this:

![A screenshot of the Network tool showing a blue branch that has a node merging from a black branch and several nodes merging to the black branch]

The black branch is the _master_ branch.
The blue branch is a long-lived development branch.

Once a development branch has been merged into its parent branch
(_master_ in this case), there is no need to keep using it.

A new branch should be create from the fresh commit on _master_.
There are several ways to do this,
the most conceptually clean is to
delete the old branch and start a new one.
You can keep the same name if you like.

If you think deleting a branch and creating a new one is a bit tedious,
and you want to re-use the branch name
(which I suppose you are free to do so),
then you can use `rebase` to catch-up your branch:

    git fetch --prune --all
    git checkout me/my-fave-branch
    git rebase origin/master

If you've already caught up `master` to `origin/master` then you can go

    git rebase master


## Some notes

### After merging on GitHub, catchup your master

If you merge on GitHub (via a Pull Request), then
your `master` branch will be behind GitHub's `master` branch.
You can "catch up" by fetching and using `rebase` to
fast-forward:

    # Assuming origin is the name of your github remote
    git fetch origin --prune --all
    git checkout master
    git rebase
    # You will now be on your newly caught up master branch



