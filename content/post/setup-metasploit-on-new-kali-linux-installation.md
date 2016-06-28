+++
author = "Kevin Kirsche"
comments = true
date = "2016-06-28T14:15:39-04:00"
description = "How To Setup Metasploit On A Fresh Kali Linux Installation"
draft = false
featured = false
image = "images/metasploit.jpg"
menu = ""
share = true
slug = "metasploit-setup-fres-kali-installation"
tags = ["metasploit", "kali"]
title = "How To Setup Metasploit On A Fresh Kali Linux Installation"

+++

Luckily, the team at [Offensive Security](https://www.offensive-security.com/) has made the process of setting up [Metasploit](https://www.metasploit.com/) on a fresh [Kali Linux](https://www.kali.org/) installation nice and simple. By default, Kali linux begins no services which could use network connectivity. This means that databases are not started on boot. To get Metasploit setup with database support, there are three steps:

## Start the PostgreSQL Database Service

Metasploit leverages [PostgreSQL](https://www.postgresql.org/) as it's database of choice in Kali. So we start it with:

```
$ service postgresql start
```

Note that depending on your user's permissions, you may need to use `sudo`.

Next, we verify that PostgreSQL started correctly using `ss -ant | grep 5432`. The `ss` command is short for socket statistics, and we use the flags `-a`, `-n`, and `-t`. These flags state the following:

* `-a` | `--all`: Display all sockets
* `-n` | `--numeric`: Do not try to resolve service names
* `-t` | `--tcp`: Display only TCP sockets

We then use `grep`, a command which is used to search for patterns. When it finds a line which matches a pattern. We are searching for port `5432`, the default port of PostgreSQL. The output should look something like so:

```
$ ss -ant | grep 5432
LISTEN  0 128 127.0.0.1:5432  *:*
LISTEN  0 128 ::1:5432        :::*
```

This means that PostgreSQL is successfully started and listening.

## Initialize the Metasploit Database

With PostgreSQL successfully started, we need to create the `msf` database for Metasploit. This is done with:

```
$ msfdb init
```

## Launch the Metasploit Console
Lastly, with PostgreSQL running and the database setup, we can launch Metasploit's CLI Console and verify that it was able to connect to the database:

```
$ msfconsole
msf > db_status
[*] postgresql connected to msf
msf >
```
