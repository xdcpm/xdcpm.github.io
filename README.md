xdcpm.github.io
==============

XDCPM: eXtra Dynamic Critical Path Method of Project Management; CPM re-engineered

Workflow (draft)
----------------

Parallel development of a git repository

To explain practical, common git processes, let's use an existing scenario for an example.

http://github.com/openacs/openacs-core is a release (read-only) repository.

Additional assumptions for this example:

*. xdcpm/openacs-core, other-dev1/openacs-core, and other-dev2/openacs-core are forks of openacs/openacs-core
*. xdcpm-dev is an account of a developer with read/write permissions for xdcpm/openacs-core.
*. other-dev1 and other-dev2 are accounts of independent developers with read permission for xdcpm/openacs-core; 

First time, each developer has cloned the repository:

    git clone https://github.com/xdcpm/openacs-core.git

Each developer has subsequently made changes to be contributed back to xdcpm.

Diagram xdcpm-parallel-dev-process1.dia only shows arrows of expected common code flow related to developing and publishing xdcpm/openacs-core:

*. openacs/openacs-core to xdcpm-dev/openacs-core
*. other-dev1/openacs-core to xdcpm-dev/openacs-core
*. other-dev2/openacs-core to xdcpm-dev/openacs-core
*. xdcpm/openacs-core to xdcpm-dev/openacs-core

The code flow might be initiated by developer other than the target (as a pull request) or as the developer.  Only fetches from the perspective of an xdcpm developer (xdcpm-dev) are discussed.

When a repository is cloned, the default branch is "master";

An alias "origin" is created locally that points to the remote repository just cloned.

Any git command defaults to the most recent local branch referred to with "git checkout <branch-name>".

Any remote reference defaults to point to the "master" branch unless specified otherwise.

Setup remote aliases to simplify commands. ( http://gitref.org/remotes/ and http://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes )

    git remote add openacs https://github.com/openacs/openacs-core.git
    git remote add xdcpm https://github.com/xdcpm/openacs-core.git
    git remote add other-dev1 https://github.com/other-dev1/openacs-core.git
    git remote add other-dev2 https://github.com/other-dev2/openacs-core.git

To see list of remotes:

    git remote -v 

Alias "origin" is automatically added. For xdcpm-dev, this would be equivalent to:

    git remote add origin https://github.com/xdcpm-dev/openacs-core.git


### How to import changes from xdcpm/openacs-core to xdcpm-dev/openacs-core

Before beginning any remote transaction, make sure current repository does not have any pending commits or edits. If there are any, xdcpm-dev commits and pushes as needed to bring own remote repository up-to-date.

Verify with:

    git status

Variations on 'git log' are also handy. See http://gitref.org/branching/#log

    git branch foobar1
    git checkout foobar1
    git fetch xdcpm
    
Merge onto branch foobar1 

    git merge xdcpm/master
    
*. If any conflicts, edit files, git add and git commit as needed. 
*. If the merge required edits/conflict resolutions, follow up with: ```git push``` 

Once conflicts are merged to a local private branch (foobar1), merge to local master

    git checkout master
    git merge foobar1

*. If any conflicts, edit files, git add and git commit as needed. 
*. If the merge required edits/conflict resolutions, follow up with: ```git push``` 



### How to import changes from openacs/openacs-core to xdcpm-dev/openacs-core

To import changes from openacs/openacs-core:

Make sure to start with the latest xdcpm version.

Follow instructions for xdcpm/openacs-core to xdcpm-dev/openacs-core
then:

    git branch foobar2
    git checkout foobar2
    git fetch openacs

Merge onto branch foobar2 

    git merge openacs/master

*. If any conflicts, edit files, git add and git commit as needed. 
*. If the merge required edits/conflict resolutions, follow up with: ```git push``` 

Once conflicts are merged to a local private branch (foobar2), merge to local master

    git checkout master
    git merge foobar2

*. If any conflicts, edit files, git add and git commit as needed. 
*. If the merge required edits/conflict resolutions, follow up with: ```git push``` 


### How to import changes from other-dev1/openacs-core to xdcpm-dev/openacs-core

To import changes from other-dev1/openacs-core:

Make sure to start with the latest xdcpm version.

Follow instructions for xdcpm/openacs-core to xdcpm-dev/openacs-core
then:

    git branch foobar2
    git checkout foobar2
    git fetch other-dev1

Merge onto branch foobar2

    git merge other-dev1/master

*. If any conflicts, edit files, git add and git commit as needed. 
*. If the merge required edits/conflict resolutions, follow up with: ```git push``` 

Once conflicts are merged to a local private branch (foobar2), merge to local master

    git checkout master
    git merge foobar2

*. If any conflicts, edit files, git add and git commit as needed. 
*. If the merge required edits/conflict resolutions, follow up with: ```git push``` (git push origin/master)


### Naming branches locally.

Branches can be called most anything, but these names will be recorded and shared when pushed. 

*. If a branch is planned to be shared, try to keep it meaningful (and unique if appropriate).
*. If including a date in a branch name, use the format yyyymmddhh to the resolution needed.
*. If branch is a contribution from an external person, include their github username or other uniquely recognizable reference.
