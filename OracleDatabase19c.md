# Installing Oracle Database 19c on Red Hat Enterprise Linux 7 VM

X Windows is required to run the Oracle Universal Installer (OUI), Database Configuration Assistant (dbca) and Database Upgrade Assistant (dbua) applications.

I started an XTerm on my RHEL 8 Gnome desktop and SSH'd into my Oracle server using:

`$ ssh -X oracle@hostname`

I needed to set the `$DISPLAY` environment variable value so that X Windows would display the applications on a remote X client.

For Oracle Database 19c installation I also found that I needed to set a Java option to correctly display the window contents.

`export _JAVA_OPTION='Dsun.java2d.xrender=false'`
