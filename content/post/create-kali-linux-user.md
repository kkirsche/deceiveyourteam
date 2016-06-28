+++
author = "Kevin Kirsche"
comments = true
date = "2016-06-28T13:43:33-04:00"
description = "How to create a new standard user account in Kali Linux Rolling release, using the command line."
draft = false
featured = false
image = "images/kali.png"
menu = ""
share = true
slug = "create-new-user-in-kali-linux"
tags = ["kali", "basics"]
title = "Creating a New Standard User in Kali Linux From the Command Line"

+++

Why would you want to run [Kali Linux](https://www.kali.org/) as a non-root user? Honestly, this comes down to one very nice and simple reason: we don't want to have to worry about breaking Kali. So let's just get right to it.

## Confirm version of Kali Linux

First, let's show what version of Kali Linux and Kernel which I'm running on:

```
$ uname -a
Linux kali 4.6.0-kali1-amd64 #1 SMP Debian 4.6.2-1kali1 (2016-06-17) x86_64 GNU/Linux

$ lsb_release -a
No LSB modules are available
Distributor ID: Kali
Description:    Kali GNU/Linux Rolling
Release:        kali-rolling
Codename:       kali-rolling
```

Now, these instructions should work on many older and newer versions of Kali Linux other than this, but this is helpful to show what I am running in case you encounter any issues.

## Creating A New User

Now, let's create a new user. We want this user to have a home directory, specifically in `/home/username`, be a part of the `sudo` group, and use the `/bin/bash` shell. To accomplish this, we use the `-m` or `--create-home` flag to create a home directory, `--gid` or `-g` with a comma separated list of groups the user should belong to, and `--shell` or `-s` to set the shell which the user should use. In the examples below, replace "`username`" with the username which you would like the user to have.

Long:

```
$ groupadd username
$ useradd --create-home --gid username --gid sudo --shell /bin/bash username
```


Short:
```
$ groupadd username
$ useradd -m -g username -g sudo -s /bin/bash username
```


## Setting A Password For The User

By default, a new user account is disabled. To enable it, we need to add a password. To do this, we use the `passwd username` command followed by the password which we would like created:

```
$ passwd username
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

With that, we have a successfully set up new user account for us to use!
