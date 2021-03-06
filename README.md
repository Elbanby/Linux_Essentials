# Linux Essentials

## About
These are some of the commands from the linux essential training for
the LPI linux certification. I am not pursuing the certification as of now. However, I am studying the material for my personal development.

Here I am not covering all the material/commands taught. I have previous experience with Linux, hence, I am only gonna be including a few things like extra flags that I have just learnt about, and find interesting.


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
  
`mkdir path/{dir1,dir2}`
This will create dir1 and dir2 on the path you specify. Note that there are no spaces allowed. 

`cmd 2>&1` 
`cmd &> output.txt`
To redirect stderror to stdout

`cmd 2> /dev/null`
To ignore error

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


## SSH Keys

~/.ssh/id_rsa

`ssh-keygen -p` reset your ssh password 

# Chrooted env Demo 

1- Create the dir that you would like to chroot. 

`mkdir /usr/user1`

2- Create the lib folder for that user 

`mkdir /usr/user1/{bin,lib64}`

3- Copy the command you want the user to be able to execute 

`cp /usr/bin/ls /usr/user1/bin`

4- Get the shared libraries required by each program

`ldd /bin/bash`

5- Move all the libraries specifed by step 4 output to /usr/user1/lib64 

6- Now lets chroot it! This will put us inside the chrooted directory. Which will make that path act likes a root

`chroot /usr/user1 /bin/bash`

## Chrooted ssh enviroment demo (very basic intro)

This will create a chrooted ssh env for user. 

1- Create a group for users to share 

`groupadd controlledEnv`

2- Create the user(s) that will enable the ssh for 

`useradd -g controlledEnv JaiedUserName`

3- Open the ssh config file (Use whatever editor you perfer. I am using vim!)

`vim /etc/ssh/sshd_config`

4- Add the following to the sshd_config file at the bottom (for simplicity)

```
Match group controlledEnv
      ChrootDirectory /usr/user1
      X11Forwarding no 
      AllowTCPForwarding no
```

5- Restart your sshd service

`systemctl restart sshd`

6- Give your user a password 

`passwd JaiedUserName`

7- to test ssh using the username and password

`ssh JaiedUserName@<ip here>`


## Space and usage 

To profile your root system and sort them 
`du -h / | sort -rh | head -10`

To show human readble space usage of a devive 
`df -H /dev/<name>`

To see all the block storage 
`lsblk`

partitioning tool interactive
`sudo fdisk /dev/sda`

displays partition information
`sudo parted -l`


## Memory 

To see all the Dirty cache 
`cat /proc/meminfo`

To write cache to disk
`sync`


## Systemd 

To get the current release of Systemd
`systemctl --version`

To get boot process duration
`systemd-analyze`
 
To get the time spent by each task during the boot process
`systemd-analyze blame`

To get all systemd units
`systemctl list-units`

To get all systemd services
`systemctl list-units | grep .service`

To get a service status
`systemctl status <service-name.service>`

N.B: you need sudo to minapulate services

To disable a service
`sudo systemctl disable <service-name.service>`

To enable a service
`sudo systemctl enable <service-name.service>`

To stop a service 
`sudo systemctl stop <service-name>`

List services that failed when starting system
`systemctl --failed`

To restart a service
`sudo systemctl restart <service-name>`

To check if a service is running 
`systemctl is-enabled <service-name>`

To reboot the system 
`systemctl reboot`

To shutdown the system 
`systemctl poweroff`

To suspend machine to ram 
`systemctl suspend`

To get the boot chain
`systemd-analyze critical-chain`
 
 To get the boot chain of a specific service 
`systemd-analyze critical-chain <service-name>`


## journalctl 

To see all logs
`journalctl`

To see log meassages from this boot 
`journalctl -b`

To see all the logs from a unit 
`journalctl -u <service-name>`

