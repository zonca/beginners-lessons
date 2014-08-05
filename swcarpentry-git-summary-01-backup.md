## Setting up

Use your work email address

    $ git config --global user.name "Vlad Dracula"
    $ git config --global user.email "vlad@tran.sylvan.ia"
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

## Recovering Old Versions

    rm file
    git checkout file
    
## Ignoring things

    nano .gitignore