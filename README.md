## About this repository
This is a learning repository.  The repository structure
described in this file is in this repository.  The commit
IDs have changed, but the basic structure of commits is
here.  You can follow along with the commands to learn
this command---in fact, it's encouraged.

This repository is part of [Travis Swicegood's][] talk
titled, Git's Meat Cleavers.  If you'd like to learn more
about Git, you can see Travis talk around the country on
the topic, or pick up either of his books:

* [Pragmatic Version Control using Git][tsgit] - An
  introduction to version control and the concepts of Git.
* [Pragmatic Guide to Git][pggit] - A quick-start guide for
  those familiar with version control for those looking to
  transition to Git from another tool.

[Travis Swicegood's]: http://travisswicegood.com/
[tsgit]: http://pragprog.com/titles/tsgit/
[pggit]: http://pragprog.com/titles/pg_git/


Rebasing
========
Rebasing takes one series of commits--normally a branch--and
replays them on top of another commit, also normally a branch.

Consider a repository that looks like this when you run
`git log --oneline --graph --all`:

    prompt> git log --oneline --graph --all
    * ce38ccb f
    | * 5a2eaf3 e
    | * 5a00102 d
    |/
    * 2b449a0 c
    * 1674c67 b
    * 0f5f8d0 a
    * c1d1e5d README driven development

Commits `e` and `f` are on a branch called `other`.  It's
created from commit `c` on the `master` branch, which later
had a commit `f` added to it.

Rebasing `other` on top of `master`, takes the two commits
from `other` and replays them after the last commit inside
the `master` branch.  It looks something like this:

    prompt> git checkout other
    Switched to branch 'other'
    prompt> git rebase master
    * 19b43c5 e
    * 519c589 d
    * ce38ccb f
    * 2b449a0 c
    * 1674c67 b
    * 0f5f8d0 a
    * c1d1e5d README driven development

Now, `e` and `f` come after the latest commit in `master`.


Warning
-------
Be careful with rebase.  Git uses the parent of a commit as
part of it's commit ID calculation.  Rebasing changes that
ID, which leads to trouble when you share code with other
developer's that has been rebased.

The rule of thumb is to rebase code to your heart's content,
*until* you've shared your code.  Once you've pushed your
code to another server, don't rebase that part of your
repositories.

Put another way, never rebase a branch that you've shared,
but go to town rebasing your local branches on top of that
shared code.
