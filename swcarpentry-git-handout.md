* Git reference: http://software-carpentry.org/v5/novice/ref/02-git.html
* Show current git branch in your bash prompt: https://github.com/magicmonty/bash-git-prompt
* Any questions? [Open an issue in the repository](https://github.com/zonca/beginners-lessons/issues/new)

Software Carpentry lesson that covers first part of the class:
http://software-carpentry.org/v5/novice/git/01-backup.html

## Setting up

Use your work email address

    $ git config --global user.name "Your Name"
    $ git config --global user.email "your@email.com"
    $ git config --global color.ui "auto"
    $ git config --global core.editor "nano"
    
## Creating a Repository

    cd $HOME/SI2014/INTRO
    git init
    ls -a
    
    git status

## Tracking Changes to Files

    git add hello_hybrid.c
    git status
    
    git commit -m "First version of hello_hybrid"
    
    git status
    git log

Changes are saved in the `.git` folder.

## Changing a File

Edit file with `vim` or `nano`

Add "world" after "Hello"

    git status
    git diff
    git commit -m "Added world after Hello"

Other commits: 

* Refactor initializations
* Add hello from process
* Add goodbye from process


	git log
    
## Exploring History

    git diff HEAD~2
    git log 
    git diff refspec
    
    git tag -a paper-submitted -m "Paper submitted to Journal"

## Recovering Old Versions

    rm file
    git checkout file
    
## Ignoring things

    nano .gitignore
    
## Collaborating

http://software-carpentry.org/v5/novice/git/02-collab.html

* Open account on github
* Follow instructions for adding remote and pushing

Exercise: add other source files, commit locally, push to github and check they
show up on the web interface

* clone to another folder
* make change in other folder and push (Create README.md)

## Conflicts

http://software-carpentry.org/v5/novice/git/03-conflict.html

* Make 2 conflicting changes in the two local clones (change printf phrase)
* push one
* try to push other
* `git pull origin master`
* fix merge conflict by modifying file, adding and committing
* `git push origin master`

## Branching
http://software-carpentry.org/v5/novice/extras/01-branching.html

Code in master should always work!

* create new branch `test-num_threads`
* develop there
* Now decide you want to make other changes, so go back to master and create an isolated branch:

        git checkout master
        git checkout -b rename-np
        # make changes
        # merge them to master
        git checkout master
        git merge rename-np
        
* Now go back to your feature branch and finish implementation

        git checkout test-num_threads
        git commit -am "added num_threads"

* Need to incorporate new changes from master to the feature branch

        git merge master
        
* push branch to github `git push origin test-num_threads`
* create pull request with web interface on github
