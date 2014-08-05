## Collaborating

* Open account on github
* Follow instructions for adding remote and pushing

Exercise: add other source files, commit locally, push to github and check they
show up on the web interface

* clone to another folder
* make change in other folder and push (Create README.md)

## Conflicts

* Make 2 conflicting changes in the two local clones (change printf phrase)
* push one
* try to push other
* `git pull origin master`
* fix merge conflict
* `git push origin master`

## Branching
http://software-carpentry.org/v5/novice/extras/01-branching.html

* create new branch `test-num_threads`
* develop there
* merge back to master: `git checkout master` `git merge test-num_threads`
* OR push branch and create pull request on github