---
title: How to use Git
---

# Intro to Git and github

## Adding locally hosted code to GitHub

The most straight forward way to push your locally stored code to a new repository is to first -

### Initialize a Git repository

**NOTE.** Make sure that you're using the latest version of Git (2.28.0)

1. Using Git Bash, navigate to the root directory where your code is stored.

2. Inside the directory, we can now initialize our local directory as a Git repository, which means that we're marking this location to be a recognized (which we then can link to a remote Git repository which we will push our local code to later on).  

Initialize the Git repository with this command: 

```bash
git init -b main
```
*Your default branch is set with the -b flag*

**(Optional) For a more detailed rundown:** when we initialize a new Git repository with ``git init`` we create a ``.git`` folder inside your local directory. This folder contains all the information that Git needs to track changes to your codebase.
- HEAD: A file that points to the current branch.
- config: A file which stores configuration options.
- description: Displays a repository description.
- index: A file that represents the staging area.
- objects/: A directory that stores all the "objects" which include blobs(files), trees(directories) and commits(reference to a tree, parent commit, etc.).
- refs/: Contains pointers to commit objects.
- info/: Directory which contains a file for ignored patterns.
- hooks/: Contains example scripts

These files and directories are basically there to ensure that Git functions properly. They track history of changes, manage branches and commmits and it stores configuration settings. By copying the ``.git`` folder inside your local directory, you can essentially clone your repository. But do note that altering the ``.git`` folder manually without knowing what you're doing might be risky as it could corrupt your Git repository.

3.  We can now add the desired files to our freshly made local repository. (This stages them for the first commit. Staging refers to having marked a modified file in its current version to go into your next commit snapshot.)

```bash
git add .
# . notation adds ALL of our files in the local repository (specify using the filename if you want to add them individually).
``` 

In this step we're staging our desired files to commit later. We can unstage a file using: 
```bash
git reset HEAD example_file'
```

4. Now we can commit the files that we've added(staged) to our local repository.
```bash
git commit -m "I did a commit :)"
``` 

This commits the tracked changes and prepares them to be pushed to a remote repository later on. (If needed, to remove this commit and modify the file we can use ``git reset --soft HEAD~1`` and commit and add the file again) 

What staging and commiting does is that when "staging" (git add...) we're previewing what files that will go into our next commit, think of it as a preview of the changes that will be included in the commit. In this step, we can unstage if we realized that we've added the wrong files or made a mistake in our files. "Committing" is when we're taking a snapshot of the file's (or set of files) current state which is then permanently stored in the Git database.  

## Adding our local repository to GitHub using Git

1. Create a new repository on GitHub.com and to avoid hassle, don't add anything extra to your repository unless you know what you need to add. You can always add these files later on after you've pushed your code/project to GitHub.

2. After creating your repository, go to the top of the repo and copy the remote repository URL. 

3. Open up Git Bash and locate your working directory of your code/project and add the URL for the remote repository which is where your local repository's content will be pushed. Run the following command and replace ``remote-url`` with your remote repository's URL (the one we already copied) 

```bash
git remote add origin remote-url
```
4. Afterwards, verify that you've set the remote URL correctly by running

```bash
git remote -v
```

5. Now to push our changes in our local repository to GitHub.com. We run the following command
```bash
git push origin main
```
If it's the case that your default branch isn't named "main", replace it with the name of your default branch.

## Troubleshooting

In recent years GitHub has foregone the usage of any and all passwords for committing and has now implemented personal access tokens both for authorizing the commit for the first time. One upside with personal access tokens is the added security of having no need for a password and you instead store it on your machine locally. Although it can be a hassle, it is how it is now.

These tokens are used to push a change to any GitHub repository and they can be generated on the website by going to your account settings - developer mode - and in the Personal Access Token (Beta), generate your token with the permission settings needed (usually just ticking every tick is adequate enough).

1. Now In the case where you're using a  freshly made token, generated in a while, you do as per usual: After a commit/push to GitHub, the terminal prompts you to input your GitHub username as instructed and when asked for your password, you copy the generated token url and use that as your password input.

If your Git has been setup with a credential manager(which is usually installed with Git the first time), you will store the access token that you've generated so to not do it every- single- time- that you're committing.

## Troubleshooting 2

If you've made changes in your online repository then you might have problems if your local repository is behind.
If so then you have to ``git pull`` to get up to date with the online repo before you can push your changes.

or ...

you might also have to do ``git branch --set-upstream-to=origin/<branch> main``, if you're not in a different branch then you can just omit ``<branch>``.



