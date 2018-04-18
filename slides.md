theme: Franziska, 9
footer: Replacing Traditional Backup Systems with ZFS — BSDCan 2018
autoscale: true

[.hide-footer]

# Replacing Traditional Backup Systems with ZFS
## BSDCan 2018
## Calvin Hendryx-Parker
### Six Feet Up

---

# Backups will be done when it is easy

---

# [fit] Backstory

AMANDA 1999-2012
Bacula 2007, 2012-2018

---

# AMANDA

## The Advanced Maryland Automatic Network Disk Archiver

Project started in the early 90s
Uses native tools (tar, dump)

^ Written in C and Perl
  BSD style and GPL license
  Currently backed and supported by Zmanda
  My First, used it at my first sysadmin job in 1999

^ Due to the native tool usage, we were able to recover, painfully, from an accidental deletion of AMANDA's index data.

---

Stopped using Amanda due to the age of our current pacakges installed.
They didn't support ZFS well at the time.
The upgrade to AMANDA 3 was rough and did not inspire confidence due to all the moving pieces, changed uid and perms, timeouts, random hangs
AMANDA would commonly bring down some machines that were short on disk space

---

# Bacula

* Filesystem level backup
* ~~GPLv2~~ AGPLv3 or Proprietary license

---

> However, if you are new to Unix systems or do not have offsetting experience with a sophisticated backup package, the Bacula project does not recommend using Bacula as it is much more difficult to setup and use than tar or dump.
-- The Bacula Website

---

[The Hidden Cost of Creating Open Source Code](https://blog.bacula.org/110/)

^ Block level available in the Enterprise version
  Enterprise version 5.1 released in 2011 included Incremental/Differential Block Level Difference Backup, but it is not in the Open Source version still to this day.

---

Difficult to configure
At one point, our configs got so bad that we only had a once a week backup of some of our files

Requires a DB backend to index the files backed up
Lots of care and feeding to make sure it is always running smoothly
Slow to backup, leverages a File Daemon on each box and a Storage Daemon to do the writing, Director to conduct
Custom Python code to generate the configurations for all the various hosts to backup

---

# [fit] There has to be a
# [fit] better way

---

# [fit] I :heart: ZFS

---

What if there were a way for all of our VMs and Jails to be backed by a filesystem or block device that supported

* snapshots
* replication
* compression
* data integrity

---

# [fit] FreeBSD
## (or any OS that supports ZFS) just works:tm:

and we are a FreeBSD shop already!

---

# Goals

1. Reliable
1. Grainular
1. Integrity
1. Few Dependancies
1. Easy to Configure
1. Runs with little care and feeding

---

Show number of config lines comparison


