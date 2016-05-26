# Deploy to Siteground with git
An easy solution for deploying to Siteground with Git

### Prerequisites:
1. Configure SSH access from your local computer to Siteground. You need to have SSH access from you computer without entering a password. Use PuTTY Authentication Agent. How to do this: [Tutorial](https://www.siteground.com/tutorials/ssh/). Open the SSH Console.
2. Workstation with a local git Repository containig your website to deploy. It does not matter how the repo it is setup.
3. An empty directory for your public website. For this tutorial we call it `mysite.com` and place it at the root of the Siteground home directory.
3. Open cPanel File Manager at Siteground.

### Preparation
1. cPanel File Manger: Create a server git repository directory for your website for example `mysite.git` at the root of the Siteground home directory.
3. SSH Console: Change to `mysite.git`. Type `git init --bare`. This initializes an empty git repository at your site.
4. cPanel File Manger: Change to `mysite.git/hooks` and add a New File named `post-receive`.
5. cPanel File Manager: Edit `post-receive` and insert following code (adjust for your environment). This tells Siteground-Git to checkout to your public website directory after you push to it.
```
#!/bin/sh
GIT_WORK_TREE=/home/userxx/mysite.com git checkout -f
```

6. cPanel File Manger: Change Permissions for `post-receive`: Allow Execute to User, Group, and World.
7. Workstation: Add a remote site to your git Repository: `git remote add mysite ssh://userxx@am27.siteground.biz:18765/home/userxx/mysite.git` (Adjust for your environment)

### Deploy
1. Workstation: `git push mysite master' this pushes the master branch to your site

This procedure is based on:
[Caio Vaccaro](https://www.digitalocean.com/community/tutorials/how-to-set-up-automatic-deployment-with-git-with-a-vps)

[Abhijit Menon-Sen ](http://toroid.org/git-website-howto)
