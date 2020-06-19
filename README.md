# Security Tips

### Table of Contents
+ [Operating system](#operating-system)
	+ [Windows](#windows)
	+ [Linux based](#linux-based)
	+ [Android](#android)
+ [Surfing on internet](#sufring-on-internet)
	+ [General rules of secure browsing](#general-rules-of-secure-browsing)
		+ [Check if connection is secure](#check-if-connection-is-secure)
		+ [Always check address before login](#always-check-address-before-login)
		+ [Be careful with mails attachments](#be-careful-with-mails-attachments)
	+ [Browser addons](#browser-addons)
+ [Passwords](#passwords)
	+ [Password managers](#password-managers)
	+ [Complexity](#complexity)
	+ [Master password](#master-password)
	+ [2FA](#2fa)
+ [Encryption](#encryption)
+ [SSH Server](#ssh-server)
	+ [Change default port](#change-default-port)
	+ [Disable root login](#disable-root-login)
	+ [Use SSH key pair](#use-ssh-key-pair)
+ [External sites](#external-sites)

# Operating system

+ **Don't use admin account daily.**
+ Use strong password to user account.
+ Lock your screen if you isn't next to computer.
+ Use [encryption](#encryption) of important files.
+ Regualary update your system and applications.
+ Create backups of your data!

## Windows

+ Do not disable UAC.
+ Do not download software from weird insecure sites. Endeavour to download it from Windows Store.
+ Read informations and selected checkboxes in installers!

## Linux based

+ Install software from official repositories.
+ Do not run `sudo` if you can do operation without it.
+ Set relevant permissions to your files. **Never use `chmod 777`**!
+ Never do `curl -s https://example.com/script.sh | bash`! Always read scripts which you execute.
+ If you don't know what command do - don't use it, read the manual before.

## Android

+ Don't download APKs from insecure sites - use Google Play (or Aurora Store) and F-Droid.
+ Don't give permissions which are not required to applications.
+ Don't allow unverified apps to use root perrmisions (if root is unlocked) or don't unlock root
account if isn't good reason to do that.
+ Do not disable encryption if you are moding your phone unless your custom ROM doesn't works well
with encryption.

# Surfing on internet

## General rules of secure browsing

### Check if connection is secure

Avoid sites without correct HTTPS certificate. **Never login to sites when connection isn't encrypted
\- when in address bar you see HTTP instead of HTTPS.** Your login data isn't secure without encryption.
This is easiest way to cracker to intercept your data.

*To website owners: You can get HTTPS certificate for free on [Let's encrypt](https://letsencrypt.org/).
Don't expose users to data loss when you can very simply (at 5 minutes) apply TLS on your site.*

### Always check address before login

You always should checking address before login to website, **especially your bank's site**. You can
make a typo in URL and come in this way to fake website on similar domain. This type of attack is named
[phishing](https://en.wikipedia.org/wiki/Phishing).

### Be careful with mails attachments

Never open attachments in mails from unknow addresses **especially if it's executable file**.

If you are office worker good practice is using mail client inside Virtual Machine separated
from host system. This will protect your main system from malware.

## Browser addons

+ [uBlock Origin](https://github.com/gorhill/uBlock)
+ [HTTPS Everywhere](https://www.eff.org/https-everywhere)
+ [NoScript](https://noscript.net/) (for more advanced users)

# Passwords

Passwords are one of the most important elements to secure your accounts. You need to have
**complex** and **different** passwords to different accounts.

## Password managers

If you still using one
password to all your accounts stop it! Instead use [password manager](https://en.wikipedia.org/wiki/Password_manager)
and use passwords with randomly generated characters.

Recommended password managers:
+ [Bitwarden](https://bitwarden.com/)
+ [KeePassXC](https://keepassxc.org/)

## Complexity

You should use as long password as is possible in registration. If you have password manager
there is no problem to generate password with 128 characters, numbers, letters and special characters
from extended ASCII. You don't need to remember this password. Simply you must copy it from
your manager and paste in login box.

Example of the best type of password:
```
ü²cZê4!åc¯ËÀfæ<Þ=ßàÕmA¦ÌÓ)ð¿\'cà¶NÌµhJbµ,D#¾nT:29
```
Unfortunately some sites don't allow to generate password looks like this but still you can generate
secure password using only accepted characters and with characters limit to 20.

*To website owners: This is very stupid practice to limits password lenght, please don't do that!*
```
q8;>C'j}f~'\&!ts'Em3
```

## Master password

You must have only one password which you must remember. This is master password to your password manager
database. This is very important to make this secure but also easy to remember. To generate such a password
use [diceware](http://world.std.com/~reinhold/diceware.html).

## 2FA

If site have possibility to enable 2FA - do it. You can download authentication app to your smartphone (e.g.
[Aegis](https://getaegis.app/)). All additional steps to make login process more complex are good.

# Encryption

If you don't want your secret data leak you should encrypt it for example with [GPG](https://gnupg.org/)
Encryption. You can encrypt your data only for oneself or via your frind's
public key so only you and your friend can read this.

More information about creating GPG key pair and usage tutorial you can find on
[this](https://dewinter.com/gnupg_howto/english/GPGMiniHowto.html) site.

# SSH Server

## Change default port
Default port of OpenSSH server is 22. Any bots and scanners are always checking this port
and often aren't more. You can change default port in `/etc/ssh/sshd_config`.

```conf
# /etc/ssh/sshd_config

# Change it to custom port, e.g. 3519
Port 22
```
To connect to server with custom port use this command.
```shell
$ ssh ... -p PORT
```

## Disable root login
Do not allow to connect directly to root with SSH.
```conf
# /etc/ssh/sshd_config

PermitRootLogin no
```

Instead create other user without permissions and with weird name (e.g. "d!@#45sagf")
**with password different with root** and log in on it with SSH. To use root use `su -`
and insert root password. This is additional step to better security. If somebody enter
to this user he still can't do anything because don't have root rights.

## Use SSH key pair
Don't log in to SSH via password. Instead use symetric SSH key pair. This is much more
secure and comfortable. You can store password to your key in `ssh-agent` so you can connect
without typing password.

[Generating an SSH key pair](https://wiki.archlinux.org/index.php/SSH_keys#Generating_an_SSH_key_pair).

Disable login with password.
```conf
# /etc/ssh/sshd_config

PasswordAuthentication no
```

# External sites

+ [Have I been pwned?](https://haveibeenpwned.com/) - if you see message not equal to "Good news — no pwnage found!"
after type your e-mail address you should immediately change passwords to your accounts!
+ [PrivacyTools.io](https://PrivacyTools.io) - PrivacyTools provides services, tools and knowledge to protect your privacy against global mass surveillance.
