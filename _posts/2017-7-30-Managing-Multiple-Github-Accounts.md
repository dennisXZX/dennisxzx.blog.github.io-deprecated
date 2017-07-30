---
layout: post
title: Managing Multiple Github Accounts
categories: [Github]
---

Sometimes you would have to set up multiple Github accounts on your computer when you need to work with both personal and work Github accounts. Here is a walk through on how to achieve that.

1. Set up SSH keys for your Github accounts

```
// enter the hidden .ssh folder
$ cd ~/.ssh

// create a SSH key for your personal account and save it as id_rsa_personal when prompted
$ ssh-keygen -t rsa -C "your_email@associated_with_githubPersonal.com"

// create a SSH key for your personal account and save it as id_rsa_work when prompted
$ ssh-keygen -t rsa -C "your_email@associated_with_githubWork.com"
```

The above commands will set up the following files.

The above commands setup the following files, which you can check by using `ls -al ~/.ssh` in your Ternimal.

id_rsa_personal
id_rsa_personal.pub
id_rsa_work
id_rsa_work.pub

2. Add the SSH keys to your Github accounts

```
// copy the key to your clipboard
$ pbcopy < ~/.ssh/id_rsa_personal.pub
```

Then go to Github 'SSH keys' section and paste the key into it.

3. Create a configuration file to manage the separate keys

Make sure you are in `~/.ssh/` folder, then create a config file by typing `touch config`.

Paste the following content into the config file:

```
# githubPersonal
Host personal
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_personal

# githubWork
Host work
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_work
```

4. Update stored identities

```
// clear the currently stored identities
$ ssh-add -D

// add new keys
$ ssh-add id_rsa_personal
$ ssh-add id_rsa_work

// test to make sure the keys are stored
$ ls -al

// test to make sure Github recognizes the keys
$ ssh -T personal
$ ssh -T work
```

5. Test push and pull
On Github, create a new repo in your personal account called test-personal.

```
$ touch readme.md
$ git init
$ git add .
$ git commit -am "first commit"
// notice it is using the custom account, git@personal, instead of git@github.com
$ git remote add origin git@personal:githubPersonal/test-personal.git
$ git push origin master

// make some change to the readme.md then test pull
$ git pull origin master
```

You can do the same testing for your work Github account and it should work just fine.