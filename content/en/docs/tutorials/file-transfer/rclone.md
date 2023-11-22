---
title: "Rclone on Rivanna"
linkTitle: "Rclone"
weight: 30
description: >-
     Using Rclone to upload and download from cloud services
tags:
- rivanna
- linux
- filetransfer
---

# Using the Rclone Module on Rivanna

Rclone is a useful tool to upload and download from cloud
services such as Google Drive by using the commandline.
However, a web browser is required for initial setup,
which can be done from the computer that logs into Rivanna.

## Setup Rclone on Rivanna

First, load the newer version of module; otherwise, Rivanna
loads an incompatible, older version by default. Then, initialize
a new rclone configuration and enter the following inputs:

```bash
$ module load rclone/1.61.1
$ rclone config
n/s/q> n
name> gdrive
Storage> drive
```

A client ID is required to create a provision that interfaces
with Google Drive. Follow the instructions at
<https://rclone.org/drive/#making-your-own-client-id> to create
a client ID and then input the values into Rivanna.

```bash
client_id> myCoolID..
client_secret> verySecretClientSecret..
scope> 2 # read only
service_account_file> # just press enter
Edit advanced config?
y) Yes
n) No (default)
y/n> n
Use web browser to automatically authenticate rclone with remote?
y/n> n
```

## Install Rclone on Client Computer

If the computer used to log on to Rivanna is running Windows,
and the computer has Chocolatey, then download Rclone using an 
administrative Git Bash instance with 

```bash
$ choco install rclone -y
```

Otherwise, for Linux and macOS, use

```bash
$ sudo -v ; curl https://rclone.org/install.sh | sudo bash
```

Then, after opening a new instance of the terminal, paste the command given
into Git Bash and follow the instructions.

## Rclone Authentication

In the web browser, click Advanced when google says that they 
have not verified this app; it is safe and expected. Then click 
Go to rclone, then Continue.

When Rclone gives the config token, ensure that all new line
characters are removed. This can be done by pasting the code
into an application such as Notepad and manually ensuring that
all characters are on the same line. Otherwise, the code will
be split across new prompts, breaking the setup.

This is bad:
```bash
sjgnkajdfnkj
fdnskjafnkad
asdfnasjkffd
```

This is good:
```bash
sjgnkajdfnkjfdnskjafnkadasdfnasjkffd
```

Paste the fixed token into Rivanna.

```bash
config_token> myCoolCodeThatHasNoNewLineCharacters
Configure this as a Shared Drive (Team Drive)?

y) Yes
n) No (default)
y/n> n
Keep this "gdrive" remote?
y) Yes this is OK (default)
y/e/d> y
q) Quit config
e/n/d/r/c/s/q> q
```

An example command to use Rclone is as follows.
The flag `--drive-shared-with-me` restricts the scope to
only shared files.

```bash
$ rclone copy --drive-shared-with-me gdrive:Colab\ Datasets/EarthquakeDec2020  /scratch/$USER/EarthquakeDec2020 -P
```
