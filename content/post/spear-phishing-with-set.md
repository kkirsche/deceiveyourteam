+++
author = "Kevin Kirsche"
comments = true
date = "2016-06-21T18:30:44-04:00"
description = "How to go spear phishing on Kali Linux with the Social Engineering Toolkit"
draft = false
featured = false
image = ""
menu = ""
share = true
slug = "spear-phishing-with-set"
tags = ["phishing", "kali"]
title = "Spear Phishing With SET on Kali Linux"

+++

If you are new to security research, you may not be familiar with the [Social Engineering Toolkit (SET)](https://www.trustedsec.com/social-engineer-toolkit/) by [TrustedSec](https://www.trustedsec.com/). Today, we'll be discussing how SET can be used to take advantage of humans during a penetration test.

# What Is Social Engineering?

Social engineering is the activity of manipulating people into performing an action (such as clicking on a link to a malicious website) or divulging confidential information (such as sharing a customer's account information).

In general, social engineering takes advantage of cognitive biases, sometimes referred to as bugs in human hardware, are exploited to create a number of different attack techniques. Today, we'll be talking about spear phishing.

# Spear Phishing and It's Difference From Phishing

Spear phishing is a form of phishing which usually involves an attacker who is knowledgable about their target. These emails perform best when the attacker knows the end user's name, email address, and at least a little about you — such as where you work, who you are friends with, or what companies you interact with.

So how does the attacker get this information? Often, attacker's are able to learn about you with information that you put on the internet, often via your laptop or smart phone. They may learn about you via social media services such as Twitter, Facebook, or LinkedIn and use information such as friend's lists or current employer to their advantage.

# How Can We Craft A Spear Phishing Campaign

Today, we'll be using [Kali Linux](https://www.kali.org/), a linux distribution by [Offensive Security](https://www.offensive-security.com/) focused on penetration testing. So let's get started!

## Prepare the Phishing Email

First things first, we need to open the toolkit. To do this, we simply run the following command:

```
$ se-toolkit
```

This will open the main menu:

![Social Engineering Toolkit Main Menu](/images/set-main-screen.png)

From here, we select the first option by selecting `1` for Social-Engineering Attacks and hit enter. This will present the Social Engineering Toolkit attack menu:

![Social Engineering Toolkit Attack Menu](/images/set-attack-menu.png)

From here, we select the first option again using `1` then hitting enter to enter the Spear-Phishing Attack Vectors. This will open the Spear-Phishing submenu.

![Spear-Phishing Submenu](/images/set-spear-phishing-submenu.png)

For the purpose of this, we'll select the first option to begin a mass email attack. To select this, enter `1` again and then hit enter. This will open the email payload menu.

![Spear-Phishing Payload Menu](/images/set-spear-phishing-payload.png)

From this submenu, we select number `13`, `Adobe PDF Embedded EXE Social Engineering (NOJS)`. This is the default payload for this option. From here, you can either provide SET with a PDF which you would like to embed the payload in or you can use a blank PDF. For the purpose of this tutorial we will use option `2` to select the Built In Blank PDF. You'll then be presented with an options screen to select what type of payload you would like to embed:

![Spear-Phishing PDF Exploit Selection Menu](/images/spear-phishing-pdf-exploit-selection.png)

We'll select the second option which uses a `Windows Meterpreter Reverse_TCP`. This means that when the victim opens the PDF that we send, the PDF will create a reverse shell which connects back to our machine. This allows us to bypass many firewalls, as they often block inward connections, not outbound. After selecting this, you'll be asked for the IP address which the reverse shell should connect back to. This should be your machine's routable IP address from the victim machine. In this example, I will be using RFC1918 space to which will only work within my internal network.  

Next, we'll provide SET with our target port. We'll use the exploit default of port 443. SET will then create the payload for us. You'll then be asked if we want to set a filename. For this example, we'll use the default filename, in a real penetration test or spear phishing campaign, you would want to change the filename to something which the victim would actually look at. We select our choice of `1`, which represents the "Keep the filename, I don't care" option.

![SET Spear Phishing Exploit Creation](/images/set-spear-phishing-exploit-creation.png)

Next, we need to select how we plan to send this — either to one email address or as a large mass-mailer campaign. We'll be sending our phishing email to a single email address by selecting `1`. You'll then be asked if you would like to craft the email's design or use a built-in template. For simplicity, we will use a built in template using option `1`.

![SET Email Template](/images/set-template.png)

Available templates:
![SET Email Template Options](/images/set-email-template-options.png)

For simplicity, we'll choose option `10` — Status Report. Depending on the victim, this may or may not work for your needs. Next, we are prompted for the email address we would like to send to. For this, we'll to an example address: deceiver[at]deceiveyour[dot]team. You'll then be asked if you would like to use gmail to send the email or use your own server. We want to use gmail to send our email. We will be prompted for a gmail address and password. You'll then be asked if you want to set this as a high priority email, which more often than not we do not.

Next, you'll be prompted to start the listener. Next, just wait for the user to open the PDF and you've successfully gotten a meterpreter shell on the victim's machine.
