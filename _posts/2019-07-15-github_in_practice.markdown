---
layout: post
title:      "GitHub In Practice"
date:       2019-07-16 01:36:29 +0000
permalink:  github_in_practice
---

GitHub can seem deceptively simple when everything is going according to plan. After learning the basics early on in the Flatiron curriculum, I was able to keep track of my repositories, make commits, and share my code fairly easily. It was only when my projects started to get more complicated that I remembered just how powerful, and complex, GitHub is.

**Sidenote**
Although my simple use of GitHub involved only a minimal amount of typing in Terminal, I started using the [Atom GitHub Package](https://github.atom.io/) to make the process even easier. The provided Git integration makes it extraordinarily easy to write different commit messages for changes in different files and even different code blocks within the same file. The package also makes it easy to create new branches, switch between branches, and pull/fetch/push to the online repository. It's a great tool that makes it easier to focus on your code instead of version control. 

Simply put, GitHub is a version control system. Version control systems (VCS) really shine when multiple people are working on the same resource at the same time. They're also perfect for a person who wants to experiment with a resource while knowing that they can always revert back to an earlier working version. The key to these use cases is that GitHub allows users to integrate changes to a resource in a controlled (and reversible) way. 

[GitHub Guides](https://guides.github.com/introduction/flow/) has a great flowchart showing how a team might use GitHub branches to work on and collaborate on a repository together. In it, they outline how a team member may create a new branch, make a few commits, and then submit a pull request to their colleagues. Those colleagues would then be able to review all of the commits made on the new branch and suggest changes before ultimately merging the new branch with the master branch. 

Ultimately though, this scenario is just one of many that GitHub manages to facilitate. There could be multiple branches with pull requests at the same time or users could be working off of different copies of the master. The end goal is the same- to retain a working resource in the master branch and allow users to contribute in a way that doesn't cause errors or make someone else's work redundant. 

Fortunately, GitHub has a bunch of resources to help explain some of it's more complex use cases. There's a nifty [cheatsheet of Terminal commands ](https://github.github.com/training-kit/downloads/github-git-cheat-sheet/), an [e-book](https://git-scm.com/book/en/v2), and a whole collection of [learning resources](https://help.github.com/en/articles/git-and-github-learning-resources). It's nice to know that as teams grow and projects get more complicated, GitHub has the capacity to effectively manage every necessary version. 
