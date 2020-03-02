---
layout: "post"
title: "How to Set Up SSH Keys on Ubuntu and Putty"
categories: "ssh ubuntu"
permalink: "/:categories/:year/:month/:day/:title.html"
---

These are the steps to setup putty login profile:
=================================================
- ssh-keygen -t rsa -b 2048 -f mykey -C "my-email@example.com"
- copy the content of mykey.pub to ~/.ssh/authorized_keys on the ubuntu server
- chmod 700 ~/.ssh
- chmod 644 ~/.ssh/authorized_keys
- start puttygen -> conversion -> import key
- select download mykey.ppk
- start puttygen -> connection -> auth
- browse and then choose the previous generated key (mykey.ppk)
- go back to session
- save the session
