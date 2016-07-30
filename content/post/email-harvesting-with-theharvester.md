+++
author = "Kevin Kirsche"
comments = true
date = "2016-06-30T20:33:16-04:00"
description = "How to harvest emails with theharvester"
draft = false
featured = false
image = "images/theharvester.png"
menu = ""
share = true
slug = "email-harvesting-with-theharvester"
tags = ["email", "harvesting"]
title = "Email Harvesting With theharvester"

+++

Hey everyone, today we're going to be talking about how to find and harvest email addresses on the internet using a tool called `theharvester` which is available within Kali Linux.

## What is Email Harvesting?

Email address harvesting is the process of generating or obtaining a list of email addresses which can be used in a bulk mailing. For the purposes of this, we will say that you have been hired to conduct a legal penetration test of company, and are doing recon for either a phishing attempt to gain access to the network on you're planning on using social engineering. In addition, it also provides general reconnaissance information which you may not have been able to obtain otherwise, such as the pattern used in email addresses for a company (e.g. `first.lastname@company.com`).

Please note that it is or may be **illegal** to use email addresses in this way which you do not have permission to do so!

## What Is theharvester?

`theharvester` is a program which was designed to gather email addresses, subdomains, and employee names. The tool was designed for use by penetration testers who are in the intelligence gathering phase of the penetration testing standard. The goal during this stage is to better understand the target's footprint on the internet.

## How to Use theharvester To Find Email Addresses

Luckily, `theharvester` is simple to use. For example, if we wanted to find email addresses for the domain `facebook.com`, we may use the `-d` flag, short for domain, to search this company. In addition to stating the domain we would like to search, we also have to tell `theharvester` what it should use as it's source. Some of the options include Google, Bing, LinkedIn, Jigsaw, and more.  To define the source, we use the `-b` flag.

### Example

To show our example above:

```
$ theharvester -d facebook.com -b google
*******************************************************************
*                                                                 *
* | |_| |__   ___    /\  /\__ _ _ ____   _____  ___| |_ ___ _ __  *
* | __| '_ \ / _ \  / /_/ / _` | '__\ \ / / _ \/ __| __/ _ \ '__| *
* | |_| | | |  __/ / __  / (_| | |   \ V /  __/\__ \ ||  __/ |    *
*  \__|_| |_|\___| \/ /_/ \__,_|_|    \_/ \___||___/\__\___|_|    *
*                                                                 *
* TheHarvester Ver. 2.7                                           *
* Coded by Christian Martorella                                   *
* Edge-Security Research                                          *
* cmartorella@edge-security.com                                   *
*******************************************************************


[-] Searching in Google:
	Searching 0 results...
	Searching 100 results...


[+] Emails found:
------------------
Friendship@facebook.com

[+] Hosts found in search engines:
------------------------------------
[-] Resolving hostnames IPs...
31.13.73.1:api.facebook.com
31.13.73.1:developers.facebook.com
31.13.73.1:en-gb.facebook.com
31.13.73.37:free.facebook.com
31.13.73.36:m.facebook.com
31.13.73.36:www.facebook.com
```

That's it for now! This is a good start, but let's expand on this. Maybe we want to add more results to our google search. We can do this by using the `-l` flag, short for limit. We may also want to get some more information about other domain names which may be in use. These are possible using the `-n` flag, to perform a reverse DNS query on all IP's we find, the `-t` flag, to perform a DNS TLD expansion discovery. using these flags, we now see:

```
$ theharvester -d facebook.com -b google -l 500 -n -t
*******************************************************************
*                                                                 *
* | |_| |__   ___    /\  /\__ _ _ ____   _____  ___| |_ ___ _ __  *
* | __| '_ \ / _ \  / /_/ / _` | '__\ \ / / _ \/ __| __/ _ \ '__| *
* | |_| | | |  __/ / __  / (_| | |   \ V /  __/\__ \ ||  __/ |    *
*  \__|_| |_|\___| \/ /_/ \__,_|_|    \_/ \___||___/\__\___|_|    *
*                                                                 *
* TheHarvester Ver. 2.7                                           *
* Coded by Christian Martorella                                   *
* Edge-Security Research                                          *
* cmartorella@edge-security.com                                   *
*******************************************************************


[-] Searching in Google:
	Searching 0 results...
	Searching 100 results...
	Searching 200 results...
	Searching 300 results...
	Searching 400 results...
	Searching 500 results...


[+] Emails found:
------------------
Friendship@facebook.com

[+] Hosts found in search engines:
------------------------------------
[-] Resolving hostnames IPs...
31.13.73.1:developers.facebook.com
31.13.73.1:en-gb.facebook.com
31.13.73.37:free.facebook.com
31.13.73.1:graph.facebook.com
31.13.73.36:m.facebook.com
31.13.73.36:www.facebook.com

[+] Starting active queries:
[-]Performing reverse lookup in :31.13.73.0/24
	31.13.73.255Hosts found after reverse lookup:
---------------------------------
31.13.73.1:edge-star-shv-01-mia1.facebook.com
31.13.73.2:edge-atlas-shv-01-mia1.facebook.com
31.13.73.3:edge-mqtt-shv-01-mia1.facebook.com
31.13.73.4:edge-z-shv-01-mia1.facebook.com
31.13.73.5:netprobe-bgp-01-mia1.facebook.com
31.13.73.6:edge-z-m-shv-01-mia1.facebook.com
31.13.73.12:edge-liverail-shv-01-mia1.facebook.com
31.13.73.13:edge-snaptu-http-p1-shv-01-mia1.facebook.com
31.13.73.15:edge-livestream-upload-shv-01-mia1.facebook.com
31.13.73.16:livestream-edgetee-upload-shv-01-mia1.facebook.com
31.13.73.17:edge-secure-shv-01-mia1.facebook.com
31.13.73.18:edge-experimental-1-shv-01-mia1.facebook.com
31.13.73.19:edge-extern-shv-01-mia1.facebook.com
31.13.73.20:livestream-edgetee-shv-01-mia1.facebook.com
31.13.73.21:edge-z-p1-shv-01-mia1.facebook.com
31.13.73.22:edge-livestream-dev-upload-shv-01-mia1.facebook.com
31.13.73.23:edge-livestream-api-upload-shv-01-mia1.facebook.com
31.13.73.24:akamaiprobe-bgp-01-mia1.facebook.com
31.13.73.25:edge-resolver002-bgp-01-mia1.facebook.com
31.13.73.26:edge-resolver001-bgp-01-mia1.facebook.com
31.13.73.27:edge-experimental-2-shv-01-mia1.facebook.com
31.13.73.32:edge-z-mini-shv-01-mia1.facebook.com
31.13.73.33:edge-snaptu-http-mini-shv-01-mia1.facebook.com
31.13.73.34:edge-mqtt-mini-shv-01-mia1.facebook.com
31.13.73.36:edge-star-mini-shv-01-mia1.facebook.com
31.13.73.37:edge-z-m-mini-shv-01-mia1.facebook.com
31.13.73.40:edge-z-1-p2-shv-01-mia1.facebook.com
31.13.73.41:edge-snaptu-http-p2-shv-01-mia1.facebook.com
31.13.73.48:edgeray-shv-01-mia1.facebook.com
31.13.73.53:edge-z-p3-shv-01-mia1.facebook.com
31.13.73.54:edge-turnservice-shv-01-mia1.facebook.com
[-] Starting DNS TLD expansion:
	Searching for: facebook.zw
[+] Hosts found after DNS TLD expansion:
==========================================
```

We now see much more information!
