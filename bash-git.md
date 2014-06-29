Bash lesson for beginners
========================

My apoligies, for now these lessons are mainly short notes for an instructor, still they have all the commands
covered in the lessons and links to the scripts used.
More extended version of the material covered here on [Software Carpentry](http://software-carpentry.org/v5/)

## Introduction

What it is? command line text only interface to filesystem (like file manager GUI) + execute commands on files (like double clicking or open with menu in file manager GUI)

Ask students not to take notes and show quickly that `ls` is same as file manager GUI, `mkdir` creates a folder that shows up in the file manager GUI, show `cd` in and out a folder.

The purpose here is to show students that never saw a command line interface before what it is.

Motivation: ssh into a supercomputer, bash is the only interface available
Motivation: automate everything, let the computer do boring stuff

## Motivating exercise

We have a tar archive with some data files and some badly formatted files,
we want to learn how to:

* Delete some useless files
* Move bad files in a subfolder
* Rename the good files with a better name
* Apply an plotting script that works on 1 file a time to all data files
* Put this in a bash script so we can automate the process next time we get a data delivery

## First bash commands:

* `pwd` print out current folder
* `ls` lists files in current folder
* `ls targetfolder` lists files in target folder (use only relative paths)
* `ls -F` identifies folders with /
* `cd foldername` changes directory to foldername
* `cd` changes directory to home folder
* `ls ..` lists files in parent folder
* `echo Hello World` print a string


## Shell expansion

It is important students understand that it is performed by the shell, not by the commands,
common misconception is:

`ls *.csv` `ls` filters the files that ends with `csv`.
Wrong! It is the shell that sends to `ls` the list of files that ends with `csv` separated by spaces.

Better only use `*`, unless they ask, then show `?`.

So, don't start with `ls` but just with `echo`:

* `cd` to folder that has `csv` files
* `echo "*csv"` this prints the string `*csv`
* `echo *csv` try this on your machine, what happens? 
* `ls *.csv` here `ls` gets already the list of `csv` files

We can now remove the useless files (first always use `ls` or `echo`):

`ls / rm ._*.csv`

## Command options, manual

Get an example option from `ls` for example `-I --ignore`
(FIXME find bettere example, this doesn't work on MAC)

*exercise*: read manual of `head` and print first 3 lines of gapminder file

    mkdir obsolete
    mv *broken* obsolete/
    ls obsolete

## Batch files renaming

Rename files using:

    for f in *.csv
    do 
        mv $f ${f/-/_2014-06-16_}
    done

needed to explain the weird syntax of `${f/-/_2014-06-16_}`, this is basically
taking the string in`f`` and replacing `-` with `_2014-06-16_`.
Also explain `for`, i.e. we are repeating the `mv` operation for every `csv` file,
quite intuitive.

## Run analysis script

get GNU R script from <https://gist.github.com/zonca/8468f080a93e8164fbe4>,
the easiest way is to copy-paste into editor.

FIXME: `plot_inflammation.r` should not use `ggplot`, only normal plotting,
so we do not need to add the path to `RScript`.
TODO: add Python equivalent

Go quickly through the script, show that the script works with just 1 file,
opens it, plots it and saveas a `png` or `pdf`.

Now use bash to run this on all files:

    for f in *.csv
    do
        /c/Program\ Files/R/R-3.1.0/bin/Rscript.exe plot_inflammation.r $f
    done

Check that all the figures were created.

Move figures to subfolder:

    mkdir figures
    mv *png figures/

## Show integrated bash script

Now ask students not to take notes, explain we just created a text file
that ends in `sh` using the commands we saw before,
go line by line on the script: <https://gist.github.com/zonca/96e7651830f777b070b7>
Just mention that `curl` downloads the data and `unzip` unzips them.

Now run the script and show the students that it automatically performs all the
operations we did during the morning.
Ready to be reproduced and to make a boring task run with 1 command.

Git lesson for beginners
========================

## Motivating exercise

we want to make improvements to the R/Python analysis script and we want
to keep history of changes so we can roll back to any previous version to
reproduce previous results, i.e. when we submitted a paper.

## Git setup

    git init
    git config --global user.name "Firstname Lastname"
    git config --global user.email "yourworkemail@youruniversity.edu"
    git config --global core.editor "notepad.exe" # for windows
    git config --global core.editor "nano" # for MAC and Linux

## Basic git commands

* `git add` # put in the shopping cart
* `git status` # check what is modified, what is ready to be committed
* `git commit` # buy (opens editor to type commit message)
* `git commit -m "Commit message"` # buy (no editor)
* `git log` # show histor

Add `.gitignore` with *.csv to avoid them to show up in `git status`

## Do some commits


* initial commit
* improve comments
* add `.gitignore`
* Add a title, in `ggplot`: `ggtitle(paste("Patient Inflammation figure for ", options[1], sep=""))` *Add syntax error* so we can show debugging with git
* add save png

travel back in history to understand where it is.

Checkout different previous versions and try to run each of them, notice that the commit just before was working, the "Add title" commit breaks the script.

## Github

open github account with same email used in git configuration
create a remote following the instructions on github
git push

make a change from the web interface, that changes nothing locally!
git pull to syncronize

Try another commit locally, push to github

Show different parts of the github GUI, show how research group in the area of the students use github for code or papers.
