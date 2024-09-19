# Commands

Quick commands

| Command | Full Name |
| --- | --- |
| ls | listing |
| cd | change directory |
| cat | concatenate - output contents of a file |
| pwd | print working directory |
| whoami | current user |
| ls -a | All filles including hidde |
| cp | copy |
| grep | search though a file |
| - - help | List all possible operators for the command |
| man | Manual e.g. ‘man ls’ |
| touch | create a file |
| mkdir | create a folder |
| mv | move a file or folder |
| rm | remove a file or folder |
| file | identify file type |
| su | switch user |
| su - l | new users home |
| sudo | use root permissions  |
| ps | view list of running processors  |
| ps aux |  Processors run by other uses and processes that don't run from a session  |
| top | Real time stats about running processes |
| kill {PID} | Kill the process  |
| apt | add repo, gets checked for updates when system updates |

Searching files:

Find a file if you know the doc name:

`find -name test.txt`

Find files with certain extension

`find -name *.txt`

Find contents in a file:

wordcount 

**`wc -l access.log`**

Grep to search in a file:

**`grep "12.123.111.11" access.log`**

Operators:

Take the output from a command we run and send that output to somewhere else

> 

 Rather than overwriting any contents within a file, for example, it instead just puts the output at the end.

>>

SSH

`ssh account@111.111.111.11`

Downloading files

wget - download files from web via http

**`wget https://assets.test.com//linux/myfile.txt`**

Transfer files though SSH

SCP  Secure Copy - Unlike the regular cp command, this command allows you to transfer files between two computers using the SSH protocol to provide both authentication and encryption

**`scp secure.txt ubuntu@192.168.1.10:/home/ubuntu/transferred_secure.txt`**

can be reversed to copy files from teh remote computer to local:

**`scp ubuntu@192.168.1.10:/home/ubuntu/secure.txt local_secure.txt`**