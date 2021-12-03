---
layout: post
title: Github CommandLineInterface
date: 2019-02-26 20:13:12
categories: WebApplication
desc: A general post about CLI vs GUI interface of github
---

**Post after long time**  

During the time when i publish this blog on github.  
I doesnt feel any challenge, its just like a cake walk(I forked a repository and make changes online whenever i feel that i want to make a post)  
When i tried to install git on my local machine then i came through across some challengses and lot of questions. Which all are posted here   

**Why command line?**  

Eventhough there are plenty of GUI available online. Make your hand dirty by working on CLI.  
When you are a beginner then its ok but when it comes to developers(if you're planned to) then you must be familiar with CLI
1. CLI will helps in automate your work  
2. CLI is only option for certain task(SSH tunnel into remote server)  
3. You know about what you going through.  
4. If you need some help from community, most of the solutions are available for CLI users(because there are plenty of GUI out there)  
5. It really feels good(Trust me :-)  

**Connecting to Github from CLI?**  

If you don't want to reenter your passphrase every time you use your SSH key, you can add your key to the SSH agent, which manages your SSH keys and remembers your passphrase.
1. Please make sure you are already having a ssh key, if you already have one use that one itself.
2. Else you can generate a new one and use that.
3. Use the following command to generate ssh key  
```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
4. It will prompt you to enter a passphrase.

**Then you need to add this ssh key to your ssh agent. To do that** 

1.  Start the ssh agent in the background
```
$ eval "$(ssh-agent -s)"
```
2. Add your ssh key to the ssh agent. Default it is present in the `~/.ssh/id_rsa`

3. Copy your public key (By default it is present in the following location `~/.ssh/id_pub`  
Then go to your github settins option, select SSH key and then click add ssh key  
Paste your public key there.

**`Getting & Creating Projects`**  

Initialize a local Git repository  
 
```console 
$ git init
```
Create a local copy of a remote repository  

```console
$ git clone ssh://git@github.com/[username]/[repository-name].git
```

### Basic Snapshotting

To check the status  
```console
$ git status
```
Add a file to the staging area
```
$ git add [filename.txt]
```
Commit changes
```
$ git commit -m "[commit message]
```
Remove a file
```
$ git rm -r [filename.txt]
```

**`Sharing & Updating Projects`**  

Push a branch to your repository  
```
$ git push origin [branch name]
```

Delete a remote branch
```
$ git push origin --delete [branch name]
```

Update local repository to the newest commit
```
$ git pull
```
Pull changes from remote repository
```
$ git pull origin [branch name]
```
**`Inspection & Comparison`**  

View chanes
```
$ git log
```
View changes in detailed manner
```
$ git log --summary
```
Preview changes from merging  
```
$git diff [source branch] [target branch]
```



