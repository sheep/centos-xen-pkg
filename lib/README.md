
How to use `git subtree` with merged history
---------------------------------------------

# First time setup

First checkout one of the branches, then:

    git checkout xen-48
    git subtree split -P lib --rejoin -b centos-repo-lib

The subtree `centos-repo-lib` will have the full history of the `lib/`
directory. Then --rejoin will merge this new history back into the main branch,
e.g. `xen-48`. That will result in every commit in `lib/` been duplicated in
the history.

# update main tree

When there are new commits in the *subtree*, simply apply them to the branch
(e.g. `xen-48`) with:

    git subtree merge -P lib centos-repo-lib

This will produce a merge between the subtree and the main branch.

# push main tree commits to subtree

When changes have been made in `xen-48` in the `lib/` directory, in order to
push them into the subtree, this command can be used:

    git subtree split -P lib --rejoin -b centos-repo-lib

New commits will be duplicated in the main branch history, like for first time
use.
