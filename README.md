# Welcome to the 5C Blockchain Club
This was written by Ronak Bhatia from Harvey Mudd College. Any questions/edits/concerns can be sent to rbhatia@hmc.edu

This is a public repository for the 5C Cryptocurrency Blockchain. We will post relevant research and related information here! The first step is to create a GitHub account! First, find a profile picture and save it to your computer's desktop. Then, you can create a GitHub account [here](https://github.com/). You can change your profile photo through the following link [here](https://github.com/settings/profile). Make sure that when you click this link, you hit **Upload New Picture**.

Now, assuming that you have set up a GitHub account, you're going to want to set up an editor. Normally, people use something called vim. You can also use a different editor by using the following command in your terminal or command prompt window: `git config --global core.editor <editor-command>`. Now, before I continue on with this tutorial, I'm going to stop assuming base knowledge and explain a few key concepts and tools that will be helpful for this journey. First, I'm going to give an introduction to GitHub and the use of Git. I hope you will have fun learning! :tada::+1: :octocat: 

# A Brief Aside on the Command Line 
Assuming that you have created a GitHub account, you may be wondering how we use GitHub asides from in-browser. One very popular way, and the way that I use, is through the command line (also called the command screen or text interface). This is a user interface that you navigate via typing "prompts" or commands instead of using the mouse (like you might on the GitHub website). The command line is really important for many reasons. One quick example is if you wanted to make or rename 100 files in a directory on your computer, you will be extremely frustrated doing so manually. However, you could do such tasks in under a minute with the command line. Although I would love to discuss the command line and its relevance more, I want to prioritize the use of Git and eventually get to doing some Blockhain work! That being said, I will assume that you have knowledge of some basic commands and know your way around the command line from this point onwards. A good tutorial can be found [here](https://www.davidbaumgold.com/tutorials/command-line/). It will let you know how to find the command line, how to use the command line, and some navigation techniques. Some of the most commonly used  commands are the following. 
*  `ls` which lists the content of directories (files). Think l(i)s(t). 
*  `cd` which lists the contents of the current directory. Think c(urrent) d(irectory). 
*  `pwd` which p(rints) the w(orking) d(irectory), moving you around your computer.  
*  `rm` which r(e)m(oves) the file! It deletes a file permanently, be careful. 
*  `sudo` which stands for super user do. Be careful with this and look it up before using.

For the purposes of this document, I will be using terminal on a Mac. Take your time reading up on the command line before we head into the next step of our journey - Git and GitHub. 

# Git and GitHub
GitHub is a version control system that has Git at its base. GitHub allows people to store files and work together online. In addition, it allows people to keep a live log of everything related to a set of files or code. It's extremely popular worldwide and used in millions of projects, even [Bitcoin](https://github.com/bitcoin/bitcoin). Now, if we want to use Git on the command line, we're going to want to download and install it on our computer. You can also get [GitHub Desktop](https://help.github.com/desktop/guides/getting-started-with-github-desktop/). In order to set up Git, we can do the following steps! 
- [x] [Download and install the latest version of Git](https://git-scm.com/downloads) 
- [x] [Set your username in Git](https://help.github.com/articles/setting-your-username-in-git/) 
- [x] [Set your commit email address in Git](https://help.github.com/articles/setting-your-commit-email-address-in-git/) 
- [ ] [Citing my source for the above information and for more complex set-ups such as Authentication](https://help.github.com/articles/set-up-git/)

## GitHub Terminology and Common Tasks
A repository is a collection of files that share things like who can access them and what changes have been made. In order to makechanges to a repository, you need to make a copy of the files on the computer you're working on (aka cloning the repository). You can do this by navigating to a GitHub repository (like this one!) and clicking on the green *Clone or Download* button, copying the URL that's shown, and then running the following command on the commandline: `git clone https://path.to.repo.git` where the "path.to.repo.git" is the pathway that was copied. Now, let's go over some commands that you may encounter and what they mean! 
* Before we get to modifying files, we add files to a snapshop of the edits we made (commit is the snapshot). 
  * You can use `git add .` or `git add fileName` in order to add a file before committing (please remember this step!). 
* Although git tracks changes to files, it won't remember a new version of them unless you explicitly let it know. 
  * To store a new version of a file, use the commit command along with a message on what you did to change the file! 
  * To run this, use `git commit -m "Added additional information on staying up all nighte" nameOfFile.md`
* Now, even once making changes and committing, Git is still afraid of commitment (jk). You need to share the progress!
  * The copy of your local repository needs to be shared with that on GitHub. 
  * To do this, run `git push`
* Now, let's say that changes are pushed to GitHub that aren't on your local copy (e.g. you have many people on the project)
  * To check for changes that may have been pushed from other users, we use pull. 
  * All you need to do is run `git pull` 
* Checking the status of Git! 
  * If you want to know more about the options of git commands you can run `git help <command>` 
  * Running `git status` lets us know if we're missing something or if things are running smoothly. Very helpful command. 
* Editing your code
  * You can run `vim fileName.md` or `vi fileName.py` where .md or .py is substituted with the file's extension
  * This will open the file (if it's possible!) in the vim editor where you can make changes. 
  * Vim, which I'm using to edit this MarkDown file, takes time to learn. Try [here](https://coderwall.com/p/adv71w/basic-vim-commands-for-getting-started). 
* Merge conflicts occur when working with others and making changes simultaneously. 
  * Try pulling before changing code and pushing after finishing work. 
  * Also, if you want a previous version of the code, you can do something called [roll back](https://blog.github.com/2015-06-08-how-to-undo-almost-anything-with-git/). 
* Consider configuring GitHub with your name, email, editor, etc. 
  * `git config --global user.name "John Doe"`
  * `git config --global user.email jdoe@college.edu`
  * Setting an editor to be Visual Studio: `git config --global core.editor code`

Hopefully this gives a full insight into the command line and using Git! Try cloning this repository and adding an additional linein the space below here. Another thing I haven't mentioned is the use of branches and pull requests. We'll give those their own section in order to wrap up this tutorial.

## Branches 
Now, one of the most powerful features of GitHub is the use of branches. When working in a project, you're going have many different features or ideas in progress. Branches allow you manage all this and the varying levels of completion of such ideas. When you create a branch in the project, you can experiment as much as you want without changing the master branch or your main, completed,and working code. The cool thing is that no commits will have unless it's ready to be reviewed. The main thing to keep note is that the master branch is ready-to-go. More information about branches and their place in the Git flow is available [here](https://guides.github.com/introduction/flow/). 

Now, if we have a project that we're working on in GitHub, we're most likely going to do most of the work in a different branch than the master branch. For example, while editing this MarkDown file, I'm in a seperate branch called "develop" so I can easily revert to a previous, working version of my file if things go wrong while I'm editing at 2:00 A.M. How do we create and use branches?
* Creating a new Branch
  * Creating a branch is done by `git checkout -b [name_of_your_new_branch]`
  * You change the branch you're working in (e.g. from master to develop) by running `$ git checkout [name_of_your_new_branch]`
  * You push the branch onto GitHub through `git push origin [name_of_your_new_branch]`
  * You can see all the branches created using `git branch`
  * For citation and for additional information on branches, I suggest looking [here](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches).  
  * Once you're ready to merge a branch to master, you can do so through command line or through GitHub's browswer itself.  

## Pull Requests
Pull requests let others know about the changes you've pushed to a GitHub respository. Once you send a pull request, people can review the set of changes, discuss modifications, and then push follow-up commits. Once you and those you're working with (or you, if you're doing a solo project) are finished with the modifications, you can merge a pull request to the master branch or a local branch if you're not comfortable with master-merging yet. A good tutorial on this is available [here](https://yangsu.github.io/pull-request-tutorial/). If you really wanted to, you could do a pull request with an edited version of this repository. Don't expect me to accept it though :smiley: 
