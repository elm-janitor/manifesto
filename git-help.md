# To set up a new forked core repo.

Using elm/core version 1.0.5 as an example.

    git remote add upstream git@github.com:elm/core.git

    git pull upstream master
    git checkout -b upstream-master
    git push --set-upstream origin upstream-master

    git checkout -b upstream-1.0.5 1.0.5
    git push --set-upstream origin upstream-1.0.5

    git checkout -b stack-1.0.5
    git push --set-upstream origin stack-1.0.5
