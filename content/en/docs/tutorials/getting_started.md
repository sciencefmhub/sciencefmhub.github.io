---
title: "Getting Started with the bii_dsc_community"
linkTitle: "Getting Started"
weight: 1
description: >-
     Getting Started     
tags:
- rivanna
---

## Contributing your tutorial and experiences

Please contribute to infomall.org as your experiences 
will help. Please remember that technology evolves fast,
and we like to stay up to date by improving information.

Each page as an edit here feature, that you ca use to propose changes.
The changes will be reviewed by Gregor and are not automatically posted 
online.

Once a change is accepted, the Web site will be published and 
updates are visible. Send an e-mail to Gergor for urgent updates. 

## Activating your account

Do the following while sending an e-mail to Gregor:


**Subject**: Activate my account <Lastname>, <Firstname>

**Body:** (fill in lastname and firstname. Do not use all caps)

```
Firstname: 
Lastname:
e-mail:
github.com:

* [ ] Please add me to the `discord` 
* [ ] Please add me to the unix groups:
  * [ ] `biocomplexity`
  * [ ] `nssac_students`
  * [ ] `bii_dsc_community`
```

## Preparing your computer for research

Seee the documentation at

* [Configuring Windows for Research](https://github.com/cybertraining-dsc/reu2022/blob/main/project/windows-configuration.md)
* [Using Git Bash on Windows](https://github.com/cybertraining-dsc/reu2022/blob/main/project/git-bash-pseudo-console.md#using-git-bash-on-windows)

## Using Docker on your computer

To isolate your computer form changes and to develop portable code we recommend 
using docker images. This is especially the case when using GPUs on your computer 
as this is these days the default distribution mechanism for NVIDIA software for 
research.

## Using Singularity on your computer

As Rivanna is using singularity, it is also beneficial to use singularity on 
your loacl computer as this can be used to create images for rivanna. However, 
note that due to the transfer speeds to rivanna the experience may be limited
For that reason. we recommend you visit our 
[https://infomall.org/uva/docs/tutorial/singularity/](Tutorial on Singularity on Rivanna)

## Getting an account on Rivanna

Please read

* [See our infomall.org tutorials about rivanna](https://infomall.org/uva/docs/tutorial/)
* [Configuring Windows for Research](https://github.com/cybertraining-dsc/reu2022/blob/main/project/windows-configuration.md)
* [Using Git Bash on Windows](https://github.com/cybertraining-dsc/reu2022/blob/main/project/git-bash-pseudo-console.md#using-git-bash-on-windows)
* [Rivanna doc: Secure Shell access to Rivanna](https://www.rc.virginia.edu/userinfo/rivanna/login/#secure-shell-access-ssh)
* [Rivanna doc](https://www.rc.virginia.edu/userinfo/rivanna/logintools/rivanna-ssh/)

* [Please attend RIVANNA TUTORIAL ](https://www.rc.virginia.edu/support/) See 
  section "New to rivanna" on that page.
  If you can not attend, ask if they have recording of it. If you know the 
  recording link, please add it here.


**Do not make your account insecure**. On Rivanna's documentation you will find
a statement that we do **NOT RECOMMEND TO FOLLOW** as it is not 
best security practice and can be handled in almost all cases differently.
The statement on the official UVA Rivanna Web Site states:

> Sometimes you will need to enable passwordless ssh. 
> We allow passwordless ssh to frontend nodes from UVA 
> IP addresses. Key authentication works by matching two 
> halves of an encrypted keypair. The “public” key is 
> placed within your home directory on the remote server 
> and the “private” key is kept safely on your own workstation. 
> You should treat private keys as securely as you would any password."

Instead you need to use
| computer> |
| --- |
```
  eval `ssh-agent`
  ssh-add
```

## Using Python

When using anaconda, be careful as it takes over your python instalation and may not
provide a level of inconsistant libraries when you do more complex stuff.
Evaluate if you need anaconda or not. IN many cases it is best to just use vanilla 
python and use pip.

You can also switch between anaconda and regular python. for that you **DO NOT USE**

```conda init```

Fix or outcomment anaconde from your .bashrc or .zshrc files.

If you are a conda expert, give us some tips and tutorials on this topic.

Always check if you use the correct version of python with

| computer> |
| --- |
```bash
  which python
  python --version
```

Please keep in mind: When attending university classes some teachers may give 
you convenient but inssuficcient instructions on how to use python. They are 
typically designed to make the use 
of python easy for a specific class and not necessarily easy for research. 

Please keep in mind that you may have python versions that do not work properly 
on your computer if you have attended classes some years back. You will likely 
need to update your python. Often its good to unisntall your previous verison 
and reinstall.

If you need multiple python versions such as teacher A wants version X and 
wants version Y, this is possible. Just use python virtual environments, 
containers, or virtual machines. What you chose is your choice.

## Using Rivanna

Read 

* [Using Rivanna](https://infomall.org/uva/docs/tutorial/rivanna/)

* Copy Files

* rsync
* scp
* sftp
* [sshfs](https://github.com/libfuse/sshfs#sshfs)
* [Copy files with rclone](Rclone on Rivanna)
* [Copy files with globus](https://infomall.org/uva/docs/tutorial/globus/)

## Using Singularity on Rivanna

Read 

* [Using singularity on Rivanna](https://infomall.org/uva/docs/tutorial/singularity/)

### Using Docker on Rivanna via Singularity

Which they do not document but we do on infomall.org

I will go into this in tutorial. If you already have created a passwordless key, 
please redo it with a password ....

## Onramping Tutorial with Gregor

If you need help on assessing your computer for research you can optionally 
send the folloing info to me.

email to gregor@virginia.edu
```
os:
size ram:
size hdd/ssd:
free space on hdd/ssd
date purchased:
```

We observed that when using chrome and pycharm and zoom you may need lots of 
memory. Shut down all over applications. We recommend 16GB ram these days. 
However, many students have 8GB which may lead to slowing things down in 
some cases as you may hit the memory 

For example, when Gregor runs chrome and 
pycharm he uses up 8.1GB RAM, so if you were to have an 8GB machine it would 
slow down. However, your usage of the RAM may vary dependent on what plugins and 
which version of software as well as the OS you use. 

* Please make sure to have some space on your computers HDD, send me how much 
  free space you have
* if windows, please install gitbash before meeting
* if windows I recommend chocolatey, but be careful what you install 
* make sure you know how to use UVA vpn
* set up ssh key with ssh-keygen and use password WRITE PASSWORD DOWN
* set up ~/.ssh/config as 
* upload sshkey to github

Make sure you employ backup strategy on external HDD or google or something 
like that. I have seen to many computer HDD break and this is standard best 
practice. We can discuss in meeting.

If anythinig unclear or you have questions let me know we will also go through 
the sshkey things 
if you do not understand.

## Editor

* use pycharm (best) on your local computer alternatively vscode
* learn commandline edtor for rivanna emacs best. alternatives nano, pico, vim

## Cloudmesh is useful

You will see that cloudmesh has many features that you will find useful. 
We focus here on a number of libraries useful for rivanna.

Please create venv, this depends on your os on how to do.

Name it ~/ENV3 (if you do conda do it in whatever fashion conda does, as I do 
not use conda you can help us writing documentation about it)

activate it and do

| computer> |
| --- |
```bash
  python -m venv ~/ENV3
  source ~/ENV3
  pip install pip -U
  pip install cloudmesh-common
  pip install cloudmesh-sbatch
  pip install cloudmesh-rivanna
  cms help
```

On rivanna 

| computer> |
| --- |
```
  python -m venv /project/bii_dsc_community/$USER/ENV3
  source /project/bii_dsc_community/$USER/ENV3
  pip install pip -U
  pip install cloudmesh-common
  pip install cloudmesh-sbatch
  pip install cloudmesh-rivanna
  pip install cloudmesh-gpu
  cms help
```

Make sure you are in Gregors discord

In future learn how to do cloudmesh StopWatch so you conveniently augment 
your code with timers

Gregor von Laszewski
laszewski@gmail.com
