---
layout: post
title: "Azure Tips and Tricks Part 171 - SAP on Azure in Plain English Part 2 of 2"
excerpt: "Learn about SAP hosted on Azure"
tags: [azure, sap, portal, tipsandtricks]
share: true
comments: true
---
 
**NEW:** Get your copy of the BEST Azure Tips and Tricks of all time in this FREE [eBook](http://ebook.azuredev.tips) now!
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}
 
## SAP on Azure in Plain English Part 2 of 2
 
In this series, I take a look at SAP coming from someone who hasn't used it before. 

* [Part 1](http://www.michaelcrump.net/azure-tips-and-tricks170)
* [Part 2 - This Post](http://www.michaelcrump.net/azure-tips-and-tricks171)

## Yesterday on Azure Tips and Tricks

Yesterday, we took a look at SAP on Azure and learned a little about the history and what offerings were available. We set up a VM using the **SAP HANA express edition (Server + Applications)** image and left off with a deployed SAP VM. Today, we'll take a look at connecting to the instance and configuring it. 

## Connecting to our VM

Once Azure has created the VM and configured the storage and virtual network you can connect to the server via RDP or SSH.

<img style="border:3px solid #021a40" src="/files/azure-sap-connect.png">

In my case, I'm using SSH. 

<img style="border:3px solid #021a40" src="/files/azure-sap-connect-to-vm.png">

Below shows how I configured SAP Hana, you can follow along with what I did if you want. 

**Pro Tip** The default password is `HXEHana1` if you have any trouble logging in via the `su - hxeadm` login. 
{: .notice--primary}

SSH into the Linux VM with `sh hxehost@<the ip provided from azure portal>`

```text
mbcrump@sapexpressed:~> ssh hxehost@<the ip provided from azure portal>
The authenticity of host 'x (x)' can't be established.
ECDSA key fingerprint is SHA256:XxQpKdpxiwzEo27E+dkFc7HPE4a4iP00sYNqprWzDmA.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'x' (ECDSA) to the list of known hosts.
Password:
SUSE Linux Enterprise Server 12 SP3 x86_64 (64-bit)

As "root" (sudo or sudo -i) use the:
  - zypper command for package management
  - yast command for configuration management

If you are using extensions consider to enable the auto-update feature
of the extension agent and restarting the service. As root execute:
  - sed -i s/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/ /etc/waagent.conf
  - rcwaagent restart

Management and Config: https://www.suse.com/suse-in-the-cloud-basics
Documentation: https://www.suse.com/documentation/sles-12/
Forum: https://forums.suse.com/forumdisplay.php?93-SUSE-Public-Cloud

Have a lot of fun...
```

Now run the `sudo -i` command to gain Sys Admin access with the password you entered earlier.

```text
xehost@SAPTestMC:~> sudo -i

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for hxehost:
```

Run `su - hxeadm` to log into the express edition and use `HXEHana1` for the password and configure as shown below.

```text
SAPTestMC:~ # su - hxeadm
Password:
##############################################################################
# Welcome to SAP HANA, express edition 2.0.                                  #
#                                                                            #
# The system must be configured before use.                                  #
##############################################################################


Password must be at least 8 characters in length.  It must contain at least
1 uppercase letter, 1 lowercase letter, and 1 number.  Special characters
are allowed, except \ (backslash), ' (single quote), " (double quotes),
` (backtick), and $ (dollar sign).

New HANA database master password:
Confirm "HANA database master" password:

Do you need to use proxy server to access the internet? (Y/N): n

XSA configuration may take a while.  Do you wish to wait for XSA configuration to finish?
If you enter no, XSA will be configured in background after server completes.

Wait for XSA configuration to finish (Y/N) [Y] : y
```

You'll now see the Summary. 

```text

##############################################################################
# Summary before execution                                                   #
##############################################################################
HANA, express edition
  Host name                            : SAPTestMC
  Domain name                          : x.dx.internal.cloudapp.net
  Master password                      : ********
  Log file                             : /var/tmp/hdb_init_config_2018-10-19_04.00.52.log
  Wait for XSA configuration to finish : Yes
  Proxy host                           : N/A
  Proxy port                           : N/A
  Hosts with no proxy                  : N/A

Proceed with configuration? (Y/N) : y
```

Press `y` to proceed and you'll see a log similar to the following.


```text
Please wait while HANA server starts.  This may take a while...

tartService
OK
OK
Starting instance using: /usr/sap/HXE/SYS/exe/hdb/sapcontrol -prot NI_HTTP -nr 90 -function StartWait 2700 2


21.10.2018 00:56:08
Start
OK

21.10.2018 00:56:18
StartWait
OK

Change SYSTEM user password on SystemDB database...
Change SYSTEM user password on HXE database...



##############################################################################
# Security keys change summary                                               #
##############################################################################
  HANA system ID            : HXE
  HANA instance number      : 90
  system password           : ********
  root key backup password  : ********
  root key backup directory : /usr/sap/HXE/home/root_key.bck


#############################
# Changing SSFS Master keys #
#############################
Re-encrypt master key of the instance SSFS...
Record Statistics
=============================================
Encrypted and readable                : 8
Encrypted and not readable            : 0
Plaintext                             : 7
Removed by compacting                 : 0

Add new entry to global.ini file...

Re-encrypt the system PKI SSFS with new key...
Record Statistics
=============================================
Encrypted and readable                : 3
Encrypted and not readable            : 0
Plaintext                             : 0
Removed by compacting                 : 0

#########################################
# Change root key for SystemDB database #
#########################################
Root key backup password set for SYSTEMDB!
Root key generated for data volume of SYSTEMDB!
Root key generated for redo log of SYSTEMDB!
Root key generated for internal application of SYSTEMDB!
Root key for SYSTEMDB is backed up to /usr/sap/HXE/home/root_key.bck/SYSTEMDB.rkb!
Root key activated for data volume of SYSTEMDB!
Root key activated for redo log of SYSTEMDB!
Root key activated for internal application of SYSTEMDB!
###########################################
# Change root key for tenant database HXE #
###########################################
Root key backup password set for HXE!
Root key generated for data volume of HXE!
Root key generated for redo log of HXE!
Root key generated for internal application of HXE!
Root key for HXE is backed up to /usr/sap/HXE/home/root_key.bck/HXE.rkb!
Root key activated for data volume of HXE!
Root key activated for redo log of HXE!
Root key activated for internal application of HXE!


Collecting garbage...
Collect garbage on "hdbnameserver"...
Shrink resource container memory on "hdbnameserver"...
Collect garbage on "hdbindexserver"...
Shrink resource container memory on "hdbindexserver"...
Collect garbage on "hdbcompileserver"...
Shrink resource container memory on "hdbcompileserver"...
Collect garbage on "hdbdiserver"...
Shrink resource container memory on "hdbdiserver"...
Collect garbage on "hdbwebdispatcher"...
Shrink resource container memory on "hdbwebdispatcher"...

Total in use HANA processes heap memory (MB)
============================================
Before collection : 2726
After  collection : 2457

Free and used memory in the system
==================================
Before collection
-------------------------------------------------------------------------
             total       used       free     shared    buffers     cached
Mem:           27G        18G       8.7G        68M       331M       7.7G
-/+ buffers/cache:        10G        16G
Swap:         4.0G         0B       4.0G
After  collection
-------------------------------------------------------------------------
             total       used       free     shared    buffers     cached
Mem:           27G        16G        11G        68M       332M       7.7G
-/+ buffers/cache:       8.2G        19G
Swap:         4.0G         0B       4.0G

Please wait while XSA starts.  This may take a while...OK
Change XSA_ADMIN user password on SystemDB database...
Change XSA_DEV user password on SystemDB database...


Collecting garbage...
Collect garbage on "hdbnameserver"...
Shrink resource container memory on "hdbnameserver"...
Collect garbage on "hdbindexserver"...
Shrink resource container memory on "hdbindexserver"...
Collect garbage on "hdbcompileserver"...
Shrink resource container memory on "hdbcompileserver"...
Collect garbage on "hdbdiserver"...
Shrink resource container memory on "hdbdiserver"...
Collect garbage on "hdbwebdispatcher"...
Shrink resource container memory on "hdbwebdispatcher"...

Total in use HANA processes heap memory (MB)
============================================
Before collection : 2482
After  collection : 2494

Free and used memory in the system
==================================
Before collection
-------------------------------------------------------------------------
             total       used       free     shared    buffers     cached
Mem:           27G        16G        11G        68M       334M       7.8G
-/+ buffers/cache:       8.2G        19G
Swap:         4.0G         0B       4.0G
After  collection
-------------------------------------------------------------------------
             total       used       free     shared    buffers     cached
Mem:           27G        16G        11G        68M       336M       7.9G
-/+ buffers/cache:       8.1G        19G
Swap:         4.0G         0B       4.0G

Change telemetry technical user (TEL_ADMIN) password on SystemDB database...
===============================================================================
Change telemetry technical user password on "SystemDB" database
===============================================================================

Password must be at least 8 characters in length.  It must contain at least
1 uppercase letter, 1 lowercase letter, and 1 number.  Special characters
are allowed, except \ (backslash), ' (single quote), " (double quotes),
` (backtick), and $ (dollar sign).

Login to XSA services...
Check/Wait for Cockpit app to start...

Waiting for apps: cockpit-persistence-svc, cockpit-hdb-svc, cockpit-xsa-svc, cockpit-collection-svc, cockpit-telemetry-svc, cockpit-adminui-svc, cockpit-admin-web-app
   cockpit-collection-svc: ready
Waiting for apps: cockpit-persistence-svc, cockpit-hdb-svc, cockpit-xsa-svc, cockpit-telemetry-svc, cockpit-adminui-svc, cockpit-admin-web-app.......................
   cockpit-xsa-svc: ready
Waiting for apps: cockpit-persistence-svc, cockpit-hdb-svc, cockpit-telemetry-svc, cockpit-adminui-svc, cockpit-admin-web-app.....................
   cockpit-adminui-svc: ready
Waiting for apps: cockpit-persistence-svc, cockpit-hdb-svc, cockpit-telemetry-svc, cockpit-admin-web-app.................
   cockpit-admin-web-app: ready
OK

Create role collections...
Role collections created.
Get authentication token from UAA...
"HXE" database is registered to Cockpit.


Collecting garbage...
Collect garbage on "hdbnameserver"...
Shrink resource container memory on "hdbnameserver"...
Collect garbage on "hdbindexserver"...
Shrink resource container memory on "hdbindexserver"...
Collect garbage on "hdbcompileserver"...
Shrink resource container memory on "hdbcompileserver"...
Collect garbage on "hdbdiserver"...
Shrink resource container memory on "hdbdiserver"...
Collect garbage on "hdbwebdispatcher"...
Shrink resource container memory on "hdbwebdispatcher"...

Total in use HANA processes heap memory (MB)
============================================
Before collection : 3151
After  collection : 2468

Free and used memory in the system
==================================
Before collection
-------------------------------------------------------------------------
             total       used       free     shared    buffers     cached
Mem:           27G        26G       1.1G        68M       507M        13G
-/+ buffers/cache:        12G        14G
Swap:         4.0G         0B       4.0G
After  collection
-------------------------------------------------------------------------
             total       used       free     shared    buffers     cached
Mem:           27G        25G       1.6G        68M       507M        13G
-/+ buffers/cache:        12G        15G
Swap:         4.0G         0B       4.0G



*** Congratulations! SAP HANA, express edition 2.0 is configured. ***
See https://www.sap.com/developer/tutorials/hxe-ua-getting-started-vm.html to get started.

hxeadm@saprg:/usr/sap/HXE/HDB90> HDB info
USER          PID     PPID  %CPU        VSZ        RSS COMMAND
hxeadm      11316    11315   0.0      16616       6300 -bash
hxeadm      25032    11316   0.0      13656       3468  \_ /bin/sh /usr/sap/HXE/HDB90/HDB info
hxeadm      25063    25032   0.0      37296       2992      \_ ps fx -U hxeadm -o user:8,pid:8,ppid:8,pcp
hxeadm       6937        1   0.0      21732       2920 sapstart pf=/usr/sap/HXE/SYS/profile/HXE_HDB90_hxe
hxeadm       6975     6937   0.0     211916      57196  \_ /usr/sap/HXE/HDB90/hxehost/trace/hdb.sapHXE_HD
hxeadm       6994     6975  18.2    3760444    3179184      \_ hdbnameserver
hxeadm       7150     6975   0.9    1385044     363288      \_ hdbcompileserver
hxeadm       7171     6975   6.4    3429060    2352128      \_ hdbindexserver -port 39003
hxeadm       7380     6975   0.6    1356504     333676      \_ hdbdiserver
hxeadm       7382     6975   0.6    1593184     549284      \_ hdbwebdispatcher
hxeadm       7384     6975   4.1     788348     362572      \_ /hana/shared/HXE/xs/bin/../sapjvm_8/bin/ja
hxeadm       9619     7384   0.4    1174860     272520      |   \_ /hana/shared/HXE/xs/router/webdispatch
hxeadm       7386     6975  15.7     781300     302356      \_ /hana/shared/HXE/xs/bin/../sapjvm_8/bin/ja
hxeadm       9900     7386   0.6     930264     197944      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      10164     7386   1.5     703292     284292      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      10165     7386   0.5     799672     143036      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      10184     7386   2.0     732348     322612      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      10339     7386   0.0    1299964      53368      |   \_ node index.js
hxeadm      10707     7386   0.0    1306104      63532      |   \_ node application.js
hxeadm      10978     7386   0.9    1422236     440296      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      11250     7386   0.0    1312192      56980      |   \_ node node_modules/@sap/approuter/appro
hxeadm      11407     7386   0.0    1311956      55900      |   \_ node node_modules/approuter/approuter.
hxeadm      11756     7386   0.0      13400       3080      |   \_ /bin/sh ./startup.sh
hxeadm      12803    11756   0.0    1326508      63864      |   |   \_ sinopia
hxeadm      12108     7386   0.0    1280508      39376      |   \_ node start.js
hxeadm      12221     7386   1.8    1238612     381144      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      12935     7386   0.0    1280532      46124      |   \_ node start.js
hxeadm      13102     7386   0.0    1308644      60024      |   \_ node node_modules/@sap/approuter/appro
hxeadm      14494     7386   0.1    1334952      72836      |   \_ node node_modules/@sap/approuter/appro
hxeadm      14672     7386   1.3    1485488     442512      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      14991     7386   0.1    1325884      71616      |   \_ node application.js
hxeadm      15292     7386   0.0    1319708      55052      |   \_ node node_modules/@sap/approuter/appro
hxeadm      15815     7386   0.5     787236     127164      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      16079     7386   0.0    1280020      44124      |   \_ node server.js
hxeadm      16836     7386   3.9     736540     304172      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      16974     7386   3.0    1742528     637948      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      17607     7386   0.1    1303440      56208      |   \_ node application.js
hxeadm      17773     7386   0.1    1303368      55112      |   \_ node application.js
hxeadm      17868     7386   0.2    1337404      73636      |   \_ node --harmony server.js
hxeadm      18023     7386   0.1    1309320      62820      |   \_ node --harmony application.js
hxeadm      18131     7386   0.0    1287276      52956      |   \_ node start.js
hxeadm      18353     7386   5.4    1285856     498360      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      18487     7386   1.8    1403840     410568      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      18969     7386   0.1    1318772      53876      |   \_ node node_modules/@sap/approuter/appro
hxeadm      19194     7386   2.9     975916     283896      |   \_ META-INF/.sap_java_buildpack/sapjvmjdk
hxeadm      22984     7386   6.3    1469408     523404      |   \_ META-INF/.sap_java_buildpack/sapjvm/bi
hxeadm      23663     7386   0.9    3849144     119500      |   \_ node main.js
hxeadm       7424     6975   3.3    1843108     723612      \_ /hana/shared/HXE/xs/bin/../sapjvm_8/bin/ja
hxeadm       2049        1   0.0     495028      33628 /usr/sap/HXE/HDB90/exe/sapstartsrv pf=/usr/sap/HXE
hxeadm       1840        1   0.0      36760       4568 /usr/lib/systemd/systemd --user
hxeadm       1843     1840   0.0      85944       1552  \_ (sd-pam)
hxeadm@saprg:/usr/sap/HXE/HDB90>
```

Once complete open up your browser and go to the **Public IP Address** with port 8090. You should now see XSEngine is up and running! 

<img style="border:3px solid #021a40" src="/files/azure-sap-browser.png">

## Before I go - A Managed Solution is available

For a completely managed solution, [SAP Cloud Platform (CP) on Azure](https://azure.microsoft.com/en-us/blog/agile-sap-development-with-sap-cloud-platform-on-azure/) is a platform-as-a-service implementation that is completely managed by SAP but hosted in the Azure cloud. This arrangement still offers Azure integration so that you can connect with Event Hubs, Azure SQL, Cosmos DB, etc. With this approach, applications are deployed via SAP CP Cockpit, which is a marketplace of apps and components.

## Wrap-up

Whether you are looking at how to manage a SAP NetWeaver system in Azure, or you want to migrate to a more flexible, cloud-first, SAP HANA system, you'll find a lot more detailed information, along with case studies, on the [SAP for Azure website](https://azure.microsoft.com/en-us/solutions/sap/). 


**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
 
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.