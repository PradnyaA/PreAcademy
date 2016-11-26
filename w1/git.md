# Working with git repositories

## The community effect
Imagine a community of 4 people, where everyone has a design and shares it. The balance is positive for all of them, since each one gives one and receives 3. The **most important** feature in sharing communities is that knowledge is amplified and **you always receive more that you give**.

In Fab Academy **we are working with git repositories**. Every lab has a git repository where students push their work and pull other people's work. The advantages of working with repositories rather than simple file sharing are countless: you can create branches, roll back changes, delete other people's files and many other things that you will ~~hate~~ love very soon.

## Downloading from Github
[Github](github.com) is a web-based Git repository hosting. You don't need a github account or any software to download a repository.

> Exercise: Visit GitHub and download a repository. Think of the inconveniences of proceeding that way.

## Installing git
For the next part of the course we will need to install [git](https://git-scm.com/). In Ubuntu type in a terminal window:

`sudo apt-get install git`

> Exercise: Install git in your laptop.

## Configuring git
Set some basic config and tell git who you are. Maybe I don't have to say that, but replace **yourname** with your actual name and **youremail** with your email address.

```
cd ~/folder_name # replace this with your repository folder
git config --global user.name "yourname" #set name for commits
git config --global user.email "youremail" #set email for commits
git config --global push.default simple #default push only the current branch
git config --global core.editor atom #set the editor
```
> Exercise: Configure git with your personal data

## Cloning a repository
> **Note:** From now on you will need your [fablabs.io](fablabs.io) account.

To clone a repository you must type in a terminal window:

`git clone REPOSITORY_ADDRESS`

You can specify 2 kind of address depending on the connection used: HTTPS or SSH.

HTTPS authentication will require login/password for each connection if the project is private. You can use the credential helper to cache these for some time (15 min by default). This will require an extra config step:

`git config --global credential.helper cache # Set git to use the credential memory cache`

To change the default timeout

`git config --global credential.helper 'cache --timeout=3600' # Set the cache to timeout after 1 hour (setting is in seconds)`

> Exercise: Clone the prefab repository using the https address:  
http://git.fabacademy.org/fabacademyx/preacademy2017.git  
Did you need to authenticate? What does it mean?

Hopefully you will have a folder called `preacademy2017` in your home folder now.

> Exercise: What happens if you move the folder to another location? What happens if you rename the folder?

## Generating SSH Keypair
We usually use SSH connection in git, that way we are not messing with logins and passwords. A SSH connection needs a SSH keypair, one public key and one private key. These two together will allow you to connect. You generate a ssh keypair use this tutorial.

## Cloning a repository using a SSH connection
Please find below the SSH address to clone the repository. In your computer, inside a terminal window, navigate to where you want to clone the repository (**recommended your home directory**):

```
cd ~
git clone git@git.fabacademy.org:fabacademyx/preacademy2017.git
```


> Exercise: Clone the prefab repository in your computer.

## Basic git workflow
This is the basic git workflow. Once you have made all changes to your website (hopefully daily), upload those changes to the repository. **Very important:** Do not miss any step, and do them in order.
```
cd ~/folder_name          # go to the repository folder
git pull                  # pull other students changes
git add --all             # add your changes
git commit -m "message"   # write a meaningful message
git push
```
This is the manual workflow of updating your page. You can also write a script and  [automate this process](.w1d2.md).

## Where is the webpage?


## Troubleshooting

### SSH connection not working
Sometimes git asks for the repository password even if you have specified to use SSH keys. So what you should do is check if the keys are in the **ssh-agent**:
```
$ ssh-add -l
Could not open a connection to your authentication agent.
```
In this case the **ssh-agent** is not running, so start it using:
```
$ eval `ssh-agent -s`
Agent pid 3032
```
Check again:
```
$ ssh-add -l
The agent has no identities.
```
Now the problem is that the agent has no identities. List the keys in your `.ssh` folder:
```
$ ls ~/.ssh
academy  academy.pub  config  known_hosts
```
I add your key, which is the key you added in gitlab
```
$ ssh-add ~/.ssh/your_key
Identity added: ~/.ssh/your_key (~/.ssh/your_key)
```
Check again:
```
$ ssh-add -l
2048 SHA256:D0Yg6HyzIzD9mIIpytearRhVc2YMYEtIpqP664EjEzU ~/.ssh/your_key (RSA)
```
An then, git pull and push using SSH works again.
---
[Back to Summary](../summary.md)