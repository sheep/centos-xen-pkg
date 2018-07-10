
How to use `git subtree` with squashed history
----------------------------------------------

# First time setup

First checkout one of the branches, then:

    git subtree split -P lib -b centos-repo-lib
    git rm -r lib
    git commit -m 'will add subtree'
    git subtree add -P lib --squash  centos-repo-lib

The subtree `centos-repo-lib` will have the full history of the `lib/`
directory. Then, when adding it back into the e.g. `xen-48` branch, git will
create a commit will all history squashed.

# update main tree

When there are new commits in the *subtree*, simply apply them to the branch (e.g. `xen-48`) with:

    git subtree merge -P lib --squash centos-repo-lib

This will produce a squashed commit with everything that changed since the last
one.  The merge it.

# push main tree commits to subtree

When changes have been made in `xen-48` in the `lib/` directory, in order to
push them into the subtree, these commands needs to happen:

    # switch to subtree
    git checkout centos-repo-lib
    git cherry-pick $all_new_lib_commits
    # back to main tree
    git checkout xen-48
    git subtree merge -P lib --squash centos-repo-lib

