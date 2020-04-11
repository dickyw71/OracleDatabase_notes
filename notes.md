# My Oracle database learning journey
## Introduction
I was tasked with upgrading an 20+ year old obsolete Oracle database 7 server and the Windows client applications. The requirements specified that the new system should be on a virtual machine (VM) that could be hosted in a datacentre. The system vendor however insisted that all the system elements would need to remain 32-bit to assure compatability with their other systems used in our environment. This became a problem because the datacentre only offered a 64-bit build of the Red Hat 6 OS for VMs.  
To move the project on, it was decided that a 32-bit OS and Oracle 11g database would be deployed on a HP DL120 Gen7 physical server. The Windows client was ported to a newer version of PowerBuilder to match the Oracle 11g database. The new system elements were all more modern than the originals, but they all had supportability and obsolecense issues. The server hardware, OS and database were all End-Of-Life (EOL) and the PowerBuilder framework version was not supported by the developer.  
These project outcomes were poor because the system was not on supported platforms and there was no upgrade path for the 32-bit RHEL 6 OS.

## What I did
### Phase 1 - Build a 32-bit CentOS 6 server and Oracle 11g database in a VM on my laptop 
- Restart supplier server in run-level 1 (single user).
- Create new OS user with super-user (sudo) access rights.
- Login with new sudoer user under OS run-level 3 (multi-user no GUI).
- Switch to oracle user.
- Export the logical backup of database schema for specific users with the EXP utility.
- Build a replica of the Oracle 11g 32-bit database server on a RHEL6/CentOS6 32-bit server using VirtualBox.
    - Configure VM hardware in VirtualBox
    - Attach CentOS 6 32-bit OS ISO media to VM CD-drive.
    - Install CentOS 6 32-bit OS (minimal server).
    - Create and mount filesystems in OS replicating supplier server filesystem
    - Setup for Oracle database install
        - Install prerequisite RPM packages for Oracle 11g database
        - Set kernel parameters
        - Create oracle, sys and system OS users
        - Create oinstall OS group and add to oracle user a primary group
        - Configure oracle user bash profile
        - Change mode of SELINUX to permissive   
    - Install Oracle 11.2.0.1 32-bit database with Oracle Universal Installer (OUI)
        - Using X-Windows (xterm) from another host with a GUI. 
    - Create an empty database with DataBase Creation Assistant (DBCA)
    - Added a tablespace.
    - Created Users and granted them permissions.
    - Created database indexes.
- Imported the logical database schemas for users with the IMP utility.
    - Found missing object synonyms and created them.
    - Recompiled Views.
- Started Oracle Listener
- Opened Listener tcp port
- Connected to database server from an Oracle 11g client on another host.
### Phase 2 - Install Oracle 11g database onto a 64-bit RHEL 7 VM using Oracle Optimal Flexible Architecture (OFA)

## Why I did it

