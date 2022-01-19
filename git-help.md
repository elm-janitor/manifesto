# General advice.

Each patch will be tracked in its own branch. Many patches will consist of a
single commit too, but there is no hard rule about this. Larger patches may
be better presented as several commits, so long as each commit makes sense on
its own.

Avoid using `git merge --squash` as this does not track merges, so it gets hard
to figure out what is merged or not. It can also overwrite the author of a patch
so the original author may lose attribution.

Work in a local branch until you have a patch absolutely correct. That way, you
can always delete it without rewriting the git history on GitHub where others
can see it.

# To set up a new forked core repo.

Using elm/core version 1.0.5 as an example.

Fork on Github then:

    git remote add upstream git@github.com:elm/core.git

    git pull upstream master
    git checkout -b upstream-master
    git push --set-upstream origin upstream-master

    git checkout -b upstream-1.0.5 1.0.5
    git push --set-upstream origin upstream-1.0.5

    git checkout -b stack-1.0.5
    git push --set-upstream origin stack-1.0.5

# To start work on a Pull Request

Work on a Pull Request in a local branch only. Do not push your branch until
you have it all correct.

Pull the patch from the upstream pull request into a local branch:

    git fetch upstream pull/992/head:pr-992

At this point the PR may not have been built on the version that we are patching.
Look at the logs or maybe `git diff upstream-1.0.5` to check this.

If the PR is based behind or ahead of 1.0.5, rebase it with:

    git rebase --onto upstream-1.0.5 upstream-master

That should find the common ancestor of the PR on the upstream master branch,
cut off the commits that are just on the PR, then re-apply them relative to
the upstream 1.0.5 release tag.

Running the above rebase command will do nothing if the PR is already in the
correct position.

# To prepare a Pull Request into a patch ready for adding.

Many Pull Requests will just be a single commit with a small change in it, that
is already in good shape for adding.

Some may be made up of lots of commits, or may be incorrectly formatted.

In particular if `elm-format` has been run there may be a large amount of
whitespace diff that is not relevant to the actual patch. Evan does not use
`elm-format` on the core packages, preferring a 2 space indent instead. Adjust
the formatting until the patch is correct and commit the changes on the pr
branch.

Once the patch is in good shape, you may want to rebase the commit history,
either down to a single commit, or a smaller number of commits that provide
a better view of the patch in the commit history. A single commit is ideal for
small patches, larger ones may be condensed down to 2 or 3 as appropriate. I
recommend squashing any reformatting.

    git rebase -i upstream-1.0.5

Will let you reorganize the commit history.

# If you made a mistake.

If things end up in a mess and you just want to try again making a clean patch.

    git checkout master
    git branch -D pr-992

Work on a Pull Request in a local branch only. Do not push your branch until
you have it all correct. The above deletes the local branch and you can try
again.

# To add the Pull Request to the stack.

Check your patch will merge cleanly onto the patch stack.

    git checkout stack-1.0.5
    git merge --no-commit --no-ff pr-992

You may find some conflicts and need to go back and sort them out. Assuming the
above went cleanly, you can push the patch.

    git push origin pr-992
    git push origin stack-1.0.5

Note that the pr branch was pushed too. It is worth saving the pr branch for
future reference or in case we decide to revise or remove the patch at a
later time.

# To remove a Pull Request from the stack.
