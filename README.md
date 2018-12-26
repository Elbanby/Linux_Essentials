# Linux Essentials

## About
These are some of the commands from the linux essential training for
the LPI linux certification. I am not pursuing the certification as of now. However, I am studying the material regardless for my personal development.

Here I am not covering all the material/commands taught, as I have previous experience with Linux. Hence I am only gonna be including few things like extra flags that I have just learnt about, that are interesting to me.


# Commands starts here. Happy learning!

## General 

`su -`
switch to root user


`shutdown`
Check out the flags available in this one. to reboot and such

`whoami` = `$LOGNAME`


`uname`  
tells us what Kernal we use

`uname -r`
What Kernal version we are using

`uname -m`
What machine type we are using

`uname -p`
processor info  

`uname -o`
Official name

`uname -a`
Shows all the above info

`$HISTFILESIZE`
This available is used for how many commands can your history file store

`$HISTCONTROL`
Controls how bash stores your command history.

`cd -`
Takes you back to the previous directory you were on.

`export <variableName>`
Makes a variable global

`PATH=$PATH:/<opt>`
To add anything to the path. Be carful that this will only be during the current session.

`locate <searchValue>`
Only works if the locate Database is effective.

`find <searchValue>`
Searches in the current directory.

`ls -r`
Show all the subdirectories and there content.

`ls -t`
Show files/folders based on when last edited.

`whereis <commandName>` = `man -f <commandName>`
Show where a command lives

`apropos <commandName>` = `man -k <commandName>`
Searches the manual for the command

N.B: when on the man pages and you would like to search by a keyword. Click '/<searchKeyword>' then click ENTER then use letter 'n' to go for next occurrence.

## Archiving and/or Compression

`tar -cf <For_Name> <dirPath>`
-c is for archiving
-f for renaming

`tar -tf <For_Name>`
To have a look inside the archived directory without unarchive

`tar -xf <For_Name>`
to unarchive

`tar -czf <For_Name> <dirPath>`
To archive and compress using gzip (-z flag).
Be careful that order matters in this command.
Typically extension is .tar.gz

`tar -xzf <For_Name>`
To unarchive and decompress a gzip archived file

`tar -cjf <For_Name> <dirPath>`
To archive and compress using bzip2 (-j flag).
Be careful that order matters in this command.
Typically extension is .tar.bz2

`tar -xjf <For_Name>`
To unarchive and decompress a bzip2 archived file

N.B: You can use the -v flag when decompressing and unarchiving, to show the process. `tar -xvjf <For_Name>`

`zip -r <For_Name> <dirPath>`
Using the -r flag is to recursively zip the folder and its content.

`unzip <For_Name>`
To unzip a folder/file

`zip <fileName>` `unzip <fileName>`
`gzip <fileName>` `gunzip <fileName>`
`bzip2 <fileName>` `bunzip2 <fileName>`
For single file Compression and decompression using the respective technology.

## File Viewing

`less <fileName>`

`head <fileName>`
This will show the first 10 lines of a file.

`head -n <AnyNumber> <fileName>`
This will show any specified number of lines from the top of the file.

`tail <fileName>`
This will show the last 10 lines of a file.

`tail -n <AnyNumber> <fileName>`
This will show any specified number of lines from the bottom of the file.

`tail -f <fileName>`
This will show the bottom of the file constantly as it updates.
Used to track a file that continuously update.

## processes

`ps -e`
To view all processes.

`ps -eH` = `ps -e --forest`
To view all processes and there hierarchy.

`ps -efH`
shows all arguments a command is using while its running

`top`
you can use top standalone to find processes info in real time
use letter k then provide a process id to kill a process while in the top view.

## Log files

`cd /var/log`
important log files are
  1. secure
  2. message
  3. boot

`dmesg <hardWareLogFile>`
To have a look at a hardware log file.

## Networking

`ip addr show` = `ifconfig`
Shows the ip address info.

`ip route show` = `route` = `netstat -r`
Shows the gateway ip address

`cat etc/resolve.conf`
Shows the DNS address.

`cat etc/hosts`
This file contains the loop back address and any extra user added address as well. Used it in the past to add my docker containers ip addresses to be able to access their exposed ip.

`host <siteName>`
This will return the ip address from the DNS. DNS resolution

`pin -c 3 <ipAddress/HostName>`
using the -c flag will specify the number of packets we would like to send. Else, we would send unlimited number of packets.

## Privileges  

`who`
Shows who is currently logged in the server.

`w`
This will show who is logged in the server but also there usage and extra info.

`cat etc/sudoers`
This file will contain the groups and the commands that a group could use that requires a 'sudo' access.

`cat etc/passed`
Shows users and passwords for users in the system

`cat etc/shadow`
Shows the users and there password (encrypted)

`cat etc/groups`
Shows users and passwords for their group.

`groupadd`
To create a group.

`useradd -G <groupNum> -m -c "<Comment>" <userName> `
This is to create a user
-G for a group
-m to create home directory
-c for comment usually for full name

`passwd <userName>`
To change a user's password.

`last`
Shows who last logged in the system.

`chmod o+t <folderName>` = `chmod 1777 <folderName>`
To add a sticky bit to a directory. This means only the user created the file or folder would be able to erase it.

## Hardware

`cat /proc/cpuinfo`
Cpu info

`free -h`
Shows available ram space. The -h flag is for the human readable sizes instead of Bytes.

`dmidecode`
Info about the motherboard

`lsblk`
Shows the hard drives attached to the system

`df -h`
Shows space available in the desk.

`ls dev/`
Any <sda[0..9]> will mean there is a hard-drive attached.
