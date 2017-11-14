<b>It is tough to work without Git in the worl of uncertainities. You never know when you desktop goes down and BOOM you lost all your projects. It is recommended for every developer to be committed to git ;) </b>
Git is a software that allows you to keep track of changes made to a project over time. Git works by recording the changes you make to a project, storing those changes, then allowing you to reference them as needed.

To make a (existing) repository into git project: git init

A git project has three main parts:
1) working directory: this is the place where the user make changes to the file in the project.
2) Staging area: this is the place where all the changes the project are listed.
3) Repository: all latest files/folders are saved as a different version in the project.

In git workflow, changes are made in the working directory, files are added to the staging area and saved in the repository.

Status of changed files: <i>git status</i></br>
Untracked files mean the files has some changes but git has not started tracking them.</br>

To add a file to staging area: <i>git add filename</i> or <i>git add *</i> to add all files to staging area.
    
To unstage a file:  <i>git rm --cache filename</i></br>
    
To see the changes made to a staged file: git diff <filename>

Commit is the last part of Git workflow. This permanently saves changes in the staging area to repository. 
