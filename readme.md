# **Chapter 3**

## various notes
- rm command but interactively use `rm -ri`

## Hard links
`ln filename hardlink_name`
- point at the inode number of the original file
- if the original file is removed, the hard link can access the original content
- work only on files and not directories
- work on the same file system

## Soft links
`ln -s filename softlink_name`
- point at the name of the original file
- if the original file is removed, dangling occurs
### show inode number
`ls -i`
### show file system
`df`

## Expansions

| Syntax                          |          Description          |
| :------------------------------ | :---------------------------: |
| `touch file-{1..9}{1..9}{1..9}` |  touch file-111 to file-999   |
| *                               |           0 or more           |
| ?                               |          1 character          |
| `ls *[13]*`                     |  any file containing 1 or 3   |
| `ls file??[34]`                 |  any file ending with 1 or 3  |
| [!abc...]                       | any character not in brackets |
| [^abc...]                       | any character not in brackets |

## Variables
```bash
x=50
echo ${x}
echo Time and data is $(data)
```

# **Chapter 4**

## man page
`man command`

## search command
`man -k command`

## list files related to the command (binary, man page, ...)
`whereis command`

## info page
`pinfo command`

**NOTE:** man pages are located at <em>/usr/share/man<em/>

# **Chapter 5**
## redirection

| Syntax                                              |                     Description                      | stdout display | error display |
| :-------------------------------------------------- | :--------------------------------------------------: | :------------: | :-----------: |
| `find /etc -name passwd > output_file`              |  redirect **output** of command to file (overwrite)  |       no       |      yes      |
| `find /etc -name passwd >> output_file`             |   redirect **output** of command to file (append)    |       no       |      yes      |
| `find /etc -name passwd 2> errors_file`             |        redirect **errors** of command to file        |      yes       |      no       |
| `find /etc -name passwd 2> /dev/null`               |      ignore errors (don't save or display them)      |      yes       |      no       |
| `find /etc -name passwd > passwd_out 2> passwd_err` | redirect output to a file and errors to another file |       no       |      no       |
| `find /etc -name passwd &> both`                    |     redirect output and errors to the same file      |       no       |      no       |

## pipelining
pass output of first command to second command

`ls -l /usr/bin | less`

redirect output of first command to file and pass it to second command

`ls -l /usr/bin | tee output_file | less`

## vim editor
`vim filename`

![alt text](images/vim-modes.png?raw=true)

## shell variables
`EDITOR=vi`
- only accessible from current shell session
## environmental variables
````bash
EDITOR=vi
export $EDITOR
# you can also use
export $EDITOR=vi
````
## path
`echo $PATH`

add <em>/home/user/sbin<em/> to path

`export PATH=${PATH}:/home/user/sbin`

list environmental variables

`env`

variables can be added to ~/.bashrc
````bash
# open .bashrc
vim ~/.bashrc
# add your variables
export EDITOR=vi
````

## unsetting and unexporting variables
````bash
# unset variable
unset VARNAME
# unexport without unsetting (unexport from environmental variables)
export -n VARNAME
````

# **Chapter 6**
## types of users
| super user |                        system user                         |       regular user       |
| :--------: | :--------------------------------------------------------: | :----------------------: |
|    root    |                          daemons                           | day-to-day<br /> limited |
|   UID 0    | system processes UID 1-200 <br/> unpriveledged UID 201-999 |        UID 1000+         |

## check UID and ownership
```bash
# my id
id
# id of user
id username
# display ownership
ls -l
ls -ld
```
## check process PID and user
`ps -au`

## switching user
```bash
# switching to username
su - username
# switching to root
su -
```

## adding a user to sudoers
this can be done by:
- adding a file in /etc/sudoers.d/ with the same format of /etc/sudoers file
- using `visudo` command which is used to edit /etc/sudoers file

## user actions
```bash
# add user
useradd username
# modify user
usermod [options] username
# delete user
userdel username
userdel -r username # delete with user's files
```

## adding password to a user
`passwd username`

## some usermod options
![alt text](images/usermod.jpg?raw=true)

## group actions
```bash
# add group
groupadd groupname
groupadd -g GID groupname # specify GID
groupadd -r groupname # add system group

# modify group
groupmod [options] groupname

# delete group
groupdel groupname
```
