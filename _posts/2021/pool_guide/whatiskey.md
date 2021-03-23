---
title: What is ssh key-keygen
layout: single
author_profile: true
read_time: true
comments: true
share: false
related: true
categories:
- pool
tag:
- ssh
- linux
toc: true
toc_sticky: true
toc_label: Table
description: 없음
article_tag1: #https://en.wikipedia.org/wiki/SSH_(Secure_Shell)
article_tag2: #https://www.ssh.com/ssh/command/
article_tag3: #태그3
article_section: 
meta_keywords: #
last_modified_at: '2021-03-23 12:00:00 +0800'
---

## 1. What is ssh??

It is called SSH or Secure Shell. They are cryptographic network protocol for operating network services securely over an unsecured network. Typical application include remote CLI, login, remote command execution. Any net work service can be secured with SSH

## 2. What is `ssh-keygen`?

Ssh-keygen is a tool for creating new authentication key pairs for SSH. Such key pairs are used for automating logins, single sign-on, and for authenticating hosts.

## 3. How they work?

The SSH protocol uses public key cryptography for authenticating hosts and users. The authentication keys, called SSH keys, are created using the keygen program.

SSH introduced public key authentication as a more secure alternative to the older .rhosts authentication. It is improved security by avoiding the need to have password stored in files, and eliminated the possiblity of a compromised server stealing the user's password.

However, SSH keys are authentication credentials just like passwords. Thus, they must be managed somewhat analogously to user name and passwords. They shoud have a proper termination process so that key are removed when no longer needed

## 4. Including 

When you command `ssh-keygen`, tool asked where to save the file. SSH keys for user authentication are usually stored in the user's `.ssh` directory under the home directory. The defualt key file name depends on the algorithm, in this case `id_rsa` when using the default RSA algroithm.

Then it asks to enter a passphrase. The passphrase is used for encrypting the key, so that it cannot be used event if someone obtains the private key file.

## Commands option

- -b "Bits" this option specifies the number of bits in the key.
- -e "Export" This option allows reformatitting of existing keys between the OpenSSH key file format and the format documetned in RFC 4716
- -p "Change the passphrase" This option allows changing the passphrase of a private key with [-O old_passphrase] and [-N new_passphrase], [-f keyfile].
- -t "Type" This option specifies the type of key to be created. Commonly used values are rsa for RSA keys -dsa for DSA keys -ecdsa for elliptic curve DSA keys
- -i "input" When ssh-keygen is required to access an exisiting key, this option designates the file.
- -f "File" Specifies name of the file in which to store the created key.
- -N "New" Provieds a new passphrase for the key.
- -P "Passphrase" Provides the (old) passphrase when reading a key
- -p Change the passphrase of a private key file

https://www.tecmint.com/13-basic-cat-command-examples-in-linux/(cat -e option stadns for)