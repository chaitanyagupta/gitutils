gitutils
========

submodule-hooks
---------------

* pre-commit -- Check whether any submodule is about to be updated
  with the commit. Ask the user for confirmation. To use, copy to
  $GIT_DIR/hooks/ and make it executable.

* post-merge-checkout -- Check if any submodule has been updated post
  git-merge (git-pull) or a branch checkout. If so, ask if user wants
  to run git-submodule update. To use, copy to
  $GIT_DIR/hooks/post-checkout and/or $GIT_DIR/hooks/post-merge and
  make them executable.

There's an install script inside the submodule-hooks directory
(install.sh); you can use this script to install submodule-hooks in
your git working directory.

git-track-remote
----------------

Sets up an existing branch to track a remote branch.

Usage:

    git track-remote origin/branch
    git track-remote branch origin/branch

Runs the following git-config commands:

    git config branch.$local_branch.remote $remote_repo
    git config branch.$local_branch.remote refs/heads/$remote_branch

git-new
-------

git-new will display a (git) log of all commits which are in the
remote tracking branch but not in the local branch. All options are
passed to git-log. Most useful after a `git fetch`.

Usage:

    git new
    git new --oneline
    git new -p

Note: You need to add this file *and* ./new-revs to your $PATH for it
to work.

to-utf8
-------

to-utf8 tries to detect the encoding of the given file using `file`
and then prints its contents to stdout, converted to utf-8. The
command `iconv` is required to perform the conversion to utf-8.

to-utf8 is useful as a git-diff driver for text files not encoded
using ascii or utf-8. To configure this as a diff driver,

1. Add `to-utf8` to your $PATH

2. Configure it as diff driver in your git config using:

        git config diff.to-utf8.textconv to-utf8

3. In your project's `.gitattribues`, configure the relevant path to
use this diff driver. e.g.

        *.strings diff=to-utf8    /* Cocoa Strings files */
