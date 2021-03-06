# GIT BASICS
It is tough to work without Git in this world of uncertainties. You never know when you
desktop goes down and BOOM you lost all your projects. It is recommended for every
developer to be committed to git ;)
>Git is a software that allows you to keep track of changes made to a project over time.
Git works by recording the changes you make to a project, storing those changes, then
allowing you to reference them as needed.

## Few key concepts
Git is a distributed and decentralised source control system. Most operations
are local. Internet is required when changes are to be pushed to a remote repository.
Each **commit** is identified with SHA1 hash. **HEAD** is pointer to last commit
in current branch. **Remote** is a related repository that is not local.

## Going to some depth
A git project has three main parts:
1. **Working directory**: This is the place where the user make changes to the
file in the project. A folder is converted to a git repository using ```git init```.
To clone(bring to local system) a git repository ```git clone <repo_url>``` is executed.
2. **Staging area**: This is the place where all the changes the project are
listed. Local changes are moved to staging area using ```git add <file/folder names>```.
3. **Git Repository**: all latest files/folders are saved as a different version in the
project.This is done using ```git commit -m<message for the commit>```. Adding message
to the commit is mandatory.

***NOTE***: As shortcut to add and commit all changes in tracked files in working
directory is
```shell
git commit -am \"<message>\"
```
Local changes to Remote repository: ```git push```  
Remote repository changes to Local: ```git pull```

>In git workflow, changes are made in the working directory, files are added to
the staging area and saved in the repository.

## Important git commands
**Get Help**  
```shell
git help
```
This shows the different options available in git. ```git help <command>``` will show the
documentation of the specified command only.  

**Configuring Git**  
Git must have the owner's name and email ID. This is preferably the user name and
email ID that is linked to online VCS like Github or BitBucket.
```shell
git config --global user.name "<username>"
git config --global user.email "<email address>"
```
These details can be viewed using ```git config --global --list```. The configuration
settings are saved in the working directory in a file name **.gitconfig**.

**Creating a folder along with git initialisation**  
```shell
git init <project-folder-name>
```
A **.git** folder is created whenever git is initialised.

**Status of changed files**  
```shell
git status
```
Untracked files mean the files has some changes but git has not started tracking them.

**Add a file to staging area**  
```shell
git add filename #OR
git add * #OR
git add . #OR
git add filename_1 filename_2 #OR
git add -A
```
Here, each command has their own importance and may behave different in
different situations.

**See the changes made to a staged file**  
```shell
git diff filename
```

**View all commits**  
Git stores history of commits of a branch in chronologically order in repository.
This is helpful when a reference to previous versions of project is required.
```shell
git log
```
This has SHA1 key, author, date and message for each commit. Flags can be added
to have a more concise view of the commits. Try this:
```shell
git log --oneline --graph --decorate --color
```

**Move files to different directory inside repository**  
Here *index.html* is moved from the root directory to a directory named *web* inside root.
```shell
git mv index.html web
```

## Gitignore
Git provides user an option to exclude files or filename following a pattern from
being added to staging area. This is done by creating a file named **.gitignore**.
One pattern per line. Here is a sample *.gitignore* file.
```text
__pycache__/*
.idea/*
*/__pycache__/*
```

## Backtracking
As mentioned earlier, **HEAD** is the current commit. To look for changes in it:
```shell
git show HEAD
```
The output is same as _git log_ plus changes made to file.

**Removing file from staging area**
```shell
git rm --cached filename
```
Git will stop tracking this file, as well.

**Removing file from current commit**  
```shell
git reset HEAD filename
```
Git will keep tracking this file but removes it from latest commit.

**Revert back to the content before the latest commit**  
```shell
git checkout HEAD filename
```
There is a shortcut to this command:
```shell
git checkout -- filename
```
The first 7 characters of the sha of last commit can also be used to unstag changes.
```shell
git reset 96g12673
```

### Git Branching
The default branch that we work is _master_. Git provides option to create branches to experiment with versions of the project. The main project will be _MASTER_ branch. The other branches need to merged to MASTER to update the main repository. New branch is a different version of the Git project. It will have all commits from MASTER. To check the current branch:
```shell
git branch
```
The output will be the list of all branches with asterisk(\*) mark on the current branch. To create a new branch:
```shell
git branch new_branch
```
To switch to another branch:
```shell
git checkout branch_name
```
After switching, staging and commiting is done in the same way as before. To merge the changes with MASTER branch, first switch to master branch using _git checkout master_, then:
```shell
git merge branch_name
```
There will be merge conflicts if the same file is edited in master as well as any other.
Many branches can be created in a Git project. But, the end requirements reflecting all changes into the _master_ branch. After merging the branches can be deleted:
```shell
git branch -d branch_name
```
If a branch is not merged to _master_, then to delete that branch, run:
```shell
git branch -D branch_name
```

## Generating SSH keys
* Open command prompt and navigate to root user directory. E.g. /User/aanisha/
* Move into *.ssh* folder. If it does not exist, create one : ```mkdir .ssh```.
* ```ssh-keygen -t rsa -C "aanisha.mishra05@gmail.com"``` to create a new SSH key.
* It will ask for a file name to save the details and a password to protect. Give the details as per requirement.
Now, two file are created based on the name given by user. One of them has *.pub* extension.
This file has the content that can be copied into on of the VCS cloud clients like Github.
The key generated will be unique to your laptop.

Now, come back to the same cmd session, and run ```ssh -T git@github.com```(provided you
have added the key to your GitHub profile). Your  laptop and GitHub and now in mutual connection.
This process is recommended for remote works.

## Working with collaborates
>A __remote__ is a shared Git repository that allows multiple collaborators to work on the same Git project from different locations. Collaborators work on the project independently, and merge changes together when they are ready to do so.

To contribute to a remote project, the project first needs to be cloned to local. This is done as:
```shell
git clone remote_location clone_name
```
_repo_location_ is address of the place where the repository is. It can be a file path or URL. _clone_name_ is the name of the directory where Git project is cloned. By default, git names the remote connection as __origin__. All remotes can be views using:
```shell
git remote -v
```

#### Push an existing directory to remote
* Create a repository in remote.
* Copy the SSH link of the repository
* Open command prompt inside the local directory and run ```git remote add origin <the link copied>```.
* Git pull to bring all remote changes to local.

## Git Remote  Command while collaborating
To reflect changes in git to you system:
```shell
git fetch
```
This will not update the local repository but will bring the changes to remote branch.
To integrate origin (master) into local repository, __git mergin origin/master__ is used.

To push changes to the origin:
```shell
git push origin branch_name
```
After pushing the changes to a branch, they can then be merged with master.

***Sources: Udemy, Codecademy***
