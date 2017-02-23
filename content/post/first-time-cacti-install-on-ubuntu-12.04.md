---
title: "First time Cacti install on Ubuntu 12.04"
description: "A fresh install of Cacti on Ubuntu 12.04"
tags: [ "cacti", "monitoring", "graphing", "ubuntu", "howto" ]
date: "2012-12-12"
categories:
  - "monitoring"
---

Networks are great when they work but when they don't, how do you know you've fixed things properly? How are you going to be sure that everything is back to normal? You can do this with graphs and you can do it relatively cheaply with an application called [Cacti][3]. So today I'm going to show you just how easy it is to get Cacti up and running on Ubuntu server. First you'll need to download Cacti from your local repository.

{{< highlight shell >}}
pete@ubuntu:~$ sudo apt-get install cacti [sudo] password for pete:
{{< /highlight >}}

Cacti does require a database but don't let that scare you off. The first prompt during the installation process is to choose whether you set one up your self or alternatively (what I do for home) let dbconfig-common take care of the heavy work.

![01 configure databse][4]

Creating a database for cacti doesn't take long and you'll be quickly prompted to enter an admin password for the newly created MySQL database. In a production environment this password would likely need to be super strong but this is my home box so I'll admit I'm pretty lax.

![02 choose database admin pw][5]

You've just set the database admin password but now the database cacti account needs one too. The database cacti account is created automagically and you have the option to leave the password field blank in which case a password will be generated for you or you can create one yourself. I choose to create one myself here because… I can.

![03 cacti steps][6]

It'd suck if you miss typed your password and I guess that's why I write my more tricky passwords out and then copy and paste it in using [shift+insert][7]. However there's some inbuilt checks and balances during this process so you'll need to enter that password in again.

![04 cacti steps][8]

You've created all your accounts, now it's time to install a web server so you can get to your Cacti front page. I've used Apache2 in the past and it just worked so that's my go to default web server but if you have a preference then by all means use what you're most comfortable with.

![05 cacti steps][9]

That's the last of the prompts and by the end of it you'll be left with a CLI that looks something like this.

{{< highlight shell >}}
pete@ubuntu:~$ sudo apt-get install cacti
Reading package lists... Done
Building dependency tree
Reading state information... Done
Suggested packages:
  php5-ldap
The following NEW packages will be installed:
  cacti
0 upgraded, 1 newly installed, 0 to remove and 10 not upgraded.
Need to get 1,891 kB of archives.
After this operation, 4,766 kB of additional disk space will be used.
Get:1 ftp://ftp.iinet.net.au/linux/ubuntu/ precise/universe cacti all 0.8.7i-2ubuntu1 [1,891 kB]
Fetched 1,891 kB in 2s (919 kB/s)
Preconfiguring packages ...
Selecting previously unselected package cacti.
(Reading database ... 52860 files and directories currently installed.)
Unpacking cacti (from .../cacti_0.8.7i-2ubuntu1_all.deb) ...
Setting up cacti (0.8.7i-2ubuntu1) ...
dbconfig-common: writing config to /etc/dbconfig-common/cacti.conf

Creating config file /etc/dbconfig-common/cacti.conf with new version
Replacing config file /etc/cacti/debian.php with new version
granting access to database cacti for cacti@localhost: success.
verifying access for cacti@localhost: success.
creating database cacti: success.
verifying database cacti exists: success.
populating database via sql...  done.
dbconfig-common: flushing administrative password
 * Reloading web server config apache2
apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1 for ServerName  
{{< /highlight >}}

Hopefully everything went according to plan for you and you've just successfully installed Cacti. From here on in you'll need to fine tune the setup from the Cacti webpage. You can now access Cacti on  where x.x.x.x is your servers IP address.

For this blog post my servers IP was 172.16.0.46 so my cacti URL was . When you access cacti for the first time you'll be prompted with the welcome screen seen below. Click Next > >

![06 cacti][10]

Secondly you're prompted to select if this is a new install or an upgrade. We're installing this from scratch so new install it is. Click Next > >

![07 cacti][11]

This is where things can get a bit hairy. I remember when I first installed Cacti not all of these paths were found successfully but it seems to have worked fine with my Ubuntu server 12.04 setup. Everything appears to be super green. Click Next > >

![08 cacti][12]

Default password fun times off the starboard bow. The first time you log in your details are as follow;

Username: **admin**  
Password: **admin**

![09 cacti steps][13]

Once you've logged in with the defaults it's time to secure things a bit so enter in a new admin password.

![10 cacti steps][14]

You're logged into Cacti using the admin account and that's it. You've successfully installed and set up Cacti.

![11 cacti steps][15]

More blog posts to come on how to add your Cisco or Juniper network devices. I look forward to hearing how your install went.

[1]: http://blog.network2501.com/2012/12/12/first-time-cacti-install-on-ubuntu-12.04/#disqus_thread
[2]: http://blog.network2501.com/categories/monitoring
[3]: http://www.cacti.net/ "Cacti"
[4]: http://blog.network2501.com/images/01-configure-databse-768x337.png
[5]: http://blog.network2501.com/images/02-choose-database-admin-pw-768x337.png
[6]: http://blog.network2501.com/images/03-cacti-steps-768x336.png
[7]: http://network2501.com/bite/shift-into-gear/
[8]: http://blog.network2501.com/images/04-cacti-steps.png
[9]: http://blog.network2501.com/images/05-cacti-steps.png
[10]: http://blog.network2501.com/images/06-cacti.png
[11]: http://blog.network2501.com/images/07-cacti.png
[12]: http://blog.network2501.com/images/08-cacti-steps.png
[13]: http://blog.network2501.com/images/09-cacti-steps.png
[14]: http://blog.network2501.com/images/10-cacti-steps.png
[15]: http://blog.network2501.com/images/11-cacti-steps.png

