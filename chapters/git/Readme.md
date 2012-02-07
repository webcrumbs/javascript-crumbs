# git - the simple guide

### just a simple guide for getting started with git


## setup

* [dowload git for OSX](http://code.google.com/p/git-osx-installer/downloads/list?can=3)
  * or use [homebrew](http://mxcl.github.com/homebrew/):
      * install brew: `$> /usr/bin/ruby -e "$(curl -fsSL https://raw.github.com/gist/323731)"`
      * install git through brew: `$> brew install git`
* [download git for Windows](http://code.google.com/p/msysgit/downloads/list?can=3)
* [download git for Linux](http://book.git-scm.com/2_installing_git.html)


## create a new repository

To create a new git repository,  
create a new directory, open it and perform a 

```
git init
```

## checkout a repository
Create a working copy of a local repository by running the command

```
git clone /path/to/repository
```

When using a remote server, the command will be

```
git clone username@host:/path/to/repository
```


## workflow
Your local repository consists of three "trees" maintained by git: 

* your `Working Directory` which holds the actual files  
* the `Index` which acts as a staging area
* the `HEAD` which points to the last commit you've made

![trees](https://github.com/cvd-lab/javascript-crumbs/raw/master/chapters/git/images/trees.png "trees")


## add & commit
To propose changes (add it to the **Index**) use

```
git add <filename>
```

```
git add *
```

This is the first step in the basic git workflow.  
To actually commit these changes use

```
git commit -m "Commit message"
```

Now the file is committed to the **HEAD**, but not in your remote repository yet.


## pushing changes
Your changes are now in the **HEAD** of your local working copy.  
To send those changes to your remote repository, execute

```
git push origin master
```

Change master to whatever branch you want to push your changes to.  


If you have not cloned an existing repository and want to connect your repository to a remote server, add it with

```
git remote add origin <server>
```

Now you are able to push your changes to the selected remote server.


## branching
Branches are used to develop features isolated from each other.  
The master branch is the "default" branch when you create a repository.  
Use other branches for development and merge them back to the master branch upon completion.

![branches](https://github.com/cvd-lab/javascript-crumbs/raw/master/chapters/git/images/branches.png "branches")

To create a new branch named `feature_x` and switch to it use

```
git checkout -b feature_x
```

switch back to master

```
git checkout master
```

and delete the branch again

```
git branch -d feature_x
```

A branch is not available to others unless you push the branch to your remote repository

```
git push origin <branch>
```


## update & merge
To update your local repository to the newest commit, execute 

```
git pull
```

in your working directory to fetch and merge remote changes.  

To merge another branch into your active branch (e.g. master), use

```
git merge <branch>
```

In both cases git tries to auto-merge changes.  
Unfortunately, this is not always possible and results in conflicts.  
You are responsible to merge those conflicts manually by editing the files shown by git.  
After changing, mark them as merged with

```
git add <filename>
```

Before merging changes, you can also preview them by using

```
git diff <source_branch> <target_branch>
```

## tagging
It's recommended to create tags for software releases.  
This is a known concept, which also exists in SVN.  
To create a new tag named 1.0.0 execute

```
git tag 1.0.0 1b2e1d63ff
```

The *1b2e1d63ff* stands for the first 10 characters of the commit id you want to reference with your tag.  
To get the commit id use 

```
git log
```

You can also use fewer characters of the commit id, it just has to be unique.


## replace local changes
In case you did something wrong (which for sure never happens ;) you can replace local changes using the command

```
git checkout -- <filename>
```

this replaces the changes in your working tree with the last content in HEAD.  
Changes already added to the index, as well as new files, will be kept.  

If you instead want to drop all your local changes and commits,  
fetch the latest history from the server and point your local master branch at it like this

```
git fetch origin
git reset --hard origin/master
```

## useful hints
built-in git GUI

```
gitk
```

use colorful git output

```
git config color.ui true
```

show log on just one line per commit

```
git config format.pretty oneline
```

use interactive adding

```
git add -i
```


#links & resources

graphical clients:

* [GitX (L) (OSX, open source)](http://gitx.laullon.com/)
* [Tower (OSX)](http://www.git-tower.com/)
* [Source Tree (OSX, free)](http://www.sourcetreeapp.com/)
* [GitHub for Mac (OSX, free)](http://mac.github.com/)


guides:

* [Git Community Book](http://book.git-scm.com/)
* [Pro Git](http://progit.org/book/)
* [Think like a git](http://think-like-a-git.net/)
* [GitHub Help](http://help.github.com/)
* [A Visual Git Guide](http://marklodato.github.com/visual-git-guide/index-en.html)


## credits
Roger Duler, @tfnico, @fhd and Namics  

Please report issues on [github](github.com)