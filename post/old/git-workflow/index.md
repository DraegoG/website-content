---
title: Git workflow to manage work on multiple branches
description: "My strategy when using Git as the versioning tools for my projects"
date: 2014-04-25T09:07:09+02:00
tags: git
---

I track all my development using Git, and I always follow this strategy.

The strategy is inspired by [A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/).

I have 2 permanent branches: master and develop.

Those are the rules I follow in my daily routine:

When I take on a new issue, or decide to incorporate a feature, there are 2 main roads:

- The feature is a quick one, or subsequent commits I’ll make won’t break the code (or at least I hope so): I can commit on develop, or do a **quick feature branch**, and then merge it to develop.

- The feature will take more than one commit to finish, maybe it will take days of commits before the feature is finished and it gets stable again: **I do a feature branch**, then merge to develop.

---

If something on our **production server requires immediate action**, like a bugfix I need to get solved ASAP, I do a **short hotfix branch**, fix the thing, test the branch locally and on a test machine, then merge it to master and develop.

---

If I need a **quick feature/edit** to be pushed on the production server, the develop branch has some unstable code in it, and I’d like that feature/edit ASAP, I can **skip the develop branch, do a quick feature branch and merge it to both master and develop**, as long as the feature/edit is fast and trivial. If it proves to be something more complicated down the road, it’d be better to wait and stabilise the code on the develop branch.

---

The **develop branch will always be in a state of flux**, that’s why it should be put on a ‘**freeze**’ when preparing a release. The code is tested and every workflow is checked to verify code quality, and it’s prepared for a merge into master.

---

Every time develop or another hotfix branch is merged into master, **I tag it** with a version number, so it’s easy to move back to a previous state if something goes wrong.
