.. _data_git_intro:

Git introduction
================

Overview
--------

`Git <https://en.wikipedia.org/wiki/Git_(software)>`_ is a distributed revision 
control system with an emphasis on speed, data integrity,
and support for distributed, non-linear workflows. Git was initially designed and
developed by Linus Torvalds for Linux kernel development in 2005, and has since
become one of the most widely adopted version control systems for software development.


Git Installation
----------------

Installing Git is pretty straightforward, refer to `this <https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>`_
page for instructions on how to install it on your Operating System.

Git configuration
-----------------

Before you start using Git set your name and email address::

    git config --global user.email email@yourdomain.com
    git config --global user.name 'Name Surname'

Setup a new project
-------------------

You can either start from scratch or `clone` an existing Git `repository`.
Lets create a new Git repository::

    mkdir testproject
    cd testproject
    git init

This will initialize a new Git repository in your project folder

Clone an existing repository
----------------------------

If instead of starting from scratch you want to work on an existing repository,
`clone` it using the `git clone` command. For example to clone this documentation
repository::

    git clone https://github.com/geosolutions-it/doc-cread.git
    cd doc-cread

For more information on how to `clone` a remote repository 
refer to `the clone doc page <http://git-scm.com/docs/git-clone>`_

Setup a repository on GitHub
----------------------------

`GitHub <http://www.github.com>`_ is a very popular hosting provider for Git repositories.
Hosting your repository `in the could` makes it easier to cooperate with other people.

`Create <https://github.com/join>`_ a new account on GitHub if you haven't already.

Login into your account and `create a new repository <https://help.github.com/articles/create-a-repo/>`_

Clone your repository locally as explained above to start working on it

Make changes
------------

Create a new file called `test.txt` and edit it with your favorite editor::

    vim test.txt

Save changes to the file and run `git status`::

    git status

    On branch master

    Initial commit

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

    	test.txt

    nothing added to commit but untracked files present (use "git add" to track)

Git detects the new file in your project. Now add it to Git to start tracking the changes
to the file

Commit the changes
------------------

To commit the changes, run the following command::

    git add test.txt

If you run `git status` now ::

    git status
    On branch master

    Initial commit

    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)

    	new file:   test.txt

You can see the new file added to `the staging area` waiting to be committed.
Lets commit the changes to make them "permanent"::

    > git commit 'first commit'
    [master (root-commit) 16542aa] first commit
     1 file changed, 1 insertion(+)
     create mode 100644 test.txt

All your changes have benn committed to your local repository. Run `git log`
to view the commit history of the repository::

    > git log
    commit 16542aa9810c50b6af7729c2375ebfa77364c68d
    Author: Alessandro Parma <alessa.parma@gmail.com>
    Date:   Mon Aug 24 18:35:58 2015 +0200

        first commit

For more information on `git commit` refer to this document <http://git-scm.com/docs/git-commit>`_

`Push` to a remote repository
-----------------------------

If you cloned the repository from GitHub you may want to upload your work to the online
repository. The command you need to use is ``git push`` ::

    git push origin master

where `origin` is the default name given to the remote repository and `master` is
the name of the branch you want to push to.

For more information on `pushing` to a remote repository refer to `this document <http://git-scm.com/docs/git-push>`_

`Pull` from a remote repository
-------------------------------

A remote repository may change over time, for example someone may have pushed commits
to it, and you may want to `synchronize` your local repository with the remote one.
The way you do it is by running `git pull`. All the changes made to the remote repository
will be applied to your local repository and the two will have the exact same changes.

It is important to do a `git pull` before you try to push to a remote repository.
The local and remote repository need to have a `common anchestor` to be able to push.

For more information on `pulling` from a remote repository refer to `this document <http://git-scm.com/docs/git-pull>`_
