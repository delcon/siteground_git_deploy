# Deploy to Siteground with Git
A Tutorial for deploying to Siteground with Git

### Prerequisites:
- You must have basic Git knowledge.
- Configure SSH access from your local computer to Siteground. You need to have SSH access from you computer without entering a password. Use PuTTY Authentication Agent. [Siteground Tutorial](https://www.siteground.com/tutorials/ssh/) on this topic. 
- Open the SSH Console. Test you SSH Connection `ssh sitegroundXYZ.biz` and do `ls` and `git --version`. Adjust for your environment. Leave your console open.
- Workstation with a local git Repository containig your website to deploy. It does not matter how the Repository it is setup.
- An empty directory for your public website. For this tutorial we call it `mysite.com` and place it at the root of the Siteground home directory.
- Open cPanel File Manager at Siteground.

### Preparation
- cPanel File Manger: Create a server git repository directory for your website for example `mysite.git` at the root of the Siteground home directory.
- SSH Console: Change to `mysite.git`. Type `git init --bare`. This initializes an empty git repository at your site.
- cPanel File Manger: Change to `mysite.git/hooks` and add a New File named `post-receive`.
- cPanel File Manager: Edit `post-receive` and insert following code (adjust for your environment). This tells Siteground-Git to checkout to your public website directory after you push to it.
```
#!/bin/sh
GIT_WORK_TREE=/home/userXX/mysite.com git checkout -f
```

- cPanel File Manger: Change Permissions for `post-receive`: Allow Execute to User, Group, and World.
- Workstation: Add a remote site to your git Repository: `git remote add mysite ssh://userxx@amXYZ.siteground.biz:18765/home/userxx/mysite.git` (Adjust for your environment)

### Deploy
-  Workstation: `git push mysite master` this pushes the master branch from your local Repository to your Site.


##### Note:
This tutorial is written for general Git deployment to Siteground Sites. If you use a CMS (WP/Drupal....) Siteground has SG-Git and Staging specifically for these taks.


This procedure is based on:

[Caio Vaccaro](https://www.digitalocean.com/community/tutorials/how-to-set-up-automatic-deployment-with-git-with-a-vps) and 
[Abhijit Menon-Sen ](http://toroid.org/git-website-howto)
