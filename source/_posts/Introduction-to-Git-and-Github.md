title: Introduction to Git and Github
date: 2015-08-03 12:16:18
---
Here I just list few common issues for now I encountered when I use Git and Github.

### How to get a Git repository

For example, I need to get the [Jacman](https://github.com/wuchong/jacman) theme for this blog.
I need to get to my blog's local themes folder:

``` bash
$ cd blog/themes
$ git clone https://github.com/wuchong/jacman.git jacman 
```

### How to update files from Git repository
For example, I want to update Jacman theme, I can:
``` bash
$ cd blog/themes/jacman
$ git pull origin master
```
<!--more-->

### How to manage projects in remote Github repository
For example, I want to upload my blog's source files to remote Github repository
1. I need to create a repository on Github named blog first. (same as your local blog folder)
2. Get to your local blog folder and create local git repository:
``` bash
$ cd blog
$ git init		//initial repository
$ git add .		//add all files to the index
$ git commit -m "add all files"		//commit files to repository
//Tip: you have to add at least one file to the repository before committing
```
3. Set the remote address of git repository: (get the address when you create the repository on Github)
``` bash
$ git remote add origin git@github.com:woaij007/blog.git 
```
4. upload files to remote Github repository
``` bash
$ git push origin master
```

### How to update changes to remote Github repository
For example, I made some changes to my local blog files and I need to update them to my Github repository:
1. check the changes of your local repository:
``` bash
$ cd blog
$ git status
```
2. For example I get message from git like: "modified:   source/_posts/Test.md", then I will need to:
``` bash
$ git add source/_posts/Test.md
$ git commit -m "update test file"
$ git push origin master
```

### How to update changes from remote Github repository to local project folder
``` bash
$ git pull origin master
or 
$ git fetch origin master
//Tip: In the simplest terms, git pull does a git fetch followed by a git merge.
```

## Difference between Git and Github

And the last issue is that what's the difference between Git and Github we mentioned above: (Below is what I get from stackoverflow)

Git is a revision control system, a tool to manage your source code history. GitHub is a hosting service for Git repositories. So they are not the same thing: Git the tool, GitHub the service for projects that uses Git.

## What is Git:
{% blockquote %}
"Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency"
{% endblockquote %}
## What is GitHub:
{% blockquote %}
"GitHub is a web-based Git repository hosting service, which offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features."
{% endblockquote %}
{% blockquote %}
Github provides access control and several collaboration features such as wikis, task management, and bug tracking and feature requests for every project.

You do not need GitHub to use Git.

Git = Local (on you computer), GitHub = Remote (web).

Github allows you to:
1. Share your repositories with others.
2. Access other user's repositories.
3. Store remote copies of your repositories (github servers) as backup of your local copies.
{% endblockquote %}
