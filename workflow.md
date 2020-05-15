## Workflow

This project treats the `master` branch as the current deployment branch (rather than having a separate `production` or `release` branch). The `master` branch is protected and allows for merging pull requests only after atleast one code review and passing builds on Travis.

This document illustrates the workflow that should be followed while starting to develop a _new feature_.

1. Begin by gettin the latest code from Github to your local `master` branch : `git pull origin master`
2. Checkout a new branch : `git chcekout -b feature-branch`
3. Write code.
4. Commit code with meaningful commit messages.

### Pull Requests

Once your feature is complete, before making a pull request please `rebase` your `feature-branch` with `origin/master`.

#### Rebasing

Let's say, while you are working on your feature-branch, new stuff is integrated onto the `master` branch. So the history might look like this:

```
1 - 2 - 3 - 5 (master)
    \
     4 - 6 - 7 - 8 (feature-branch)
```

If you simply create a pull-request and the `master` branch maintainer would have to merge it, he would need to deal with potential conflicts -- bad for the maintainer.

If you rebase the `feature-branch` branch onto `master` and resolve potential conflicts before submitting the pull-request the history would look like this : 

```
1 - 2 - 3 - 5 (master)
             \
              4 - 6 - 7 - 8 (feature-branch)
```

For details on how to rebase please refer [here](https://www.atlassian.com/git/tutorials/merging-vs-rebasing).

5. Squash commits into meaningful feature commits.
6. `git push origin feature-branch`
7. Go to [Github](https://github.com/mc-internship/covid19visualizer) and create a pull request.
8. Make sure your code passes all Travis builds.
9. Ask for reviews.
10. Merge PR.
11. Repeat

### Cherry-picking

Sometimes in the interest of time you may need to cherry-pick some commits and land them to `master` before your `feature` is complete to help fellow developers.

An example:

```

dd2e86 - 946992	- 9143a9 - a6fd86 - 5a6057 [master]
           \
            76cada - 62ecb3	- b886a0 [feature]

```

Let’s say you’ve written some code in commit `62ecb3` of the feature branch that is very important right now. It may contain a bug fix or code that other people need to have access to now. Whatever the reason, you want to have commit `62ecb3` in the master branch right now, but not the other code you’ve written in the feature branch.

Here comes git cherry-pick. In this case, `62ecb3` is the cherry and you want to pick it!

```
git checkout master
git cherry-pick 62ecb3
```
That’s all. `62ecb3` is now applied to the master branch and commited (as a new commit) in master. cherry-pick behaves just like merge. If git can’t apply the changes (e.g. you get merge conflicts), git leaves you to resolve the conflicts manually and make the commit yourself.

### Force Pushing

Never `--force` push changes to github. These re-write your commit history and can potentially introduce complications that may become difficult to track. Consider [squashing](https://medium.com/@slamflipstrom/a-beginners-guide-to-squashing-commits-with-git-rebase-8185cf6e62ec) instead.

### Issues

Please open issues if you find something that needs to be addressed by someone else or by you later.

