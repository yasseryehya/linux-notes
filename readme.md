# **miscellaneous**
- rm command but interactively use `rm -ri`
 
# **Chapter 3**

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
- adding a file in /etc/sudoers.d/ with the same format of /etc/sudoers
- using `visudo` command which is used to edit /etc/sudoers

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

## setting password to a user
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

## managing passwords

## /etc/shadow
![alt text](images/shadow.jpg?raw=true)

## encrypted password
![alt text](images/encrypted_password.jpg?raw=true)

## password aging
![alt text](images/password_aging.jpg?raw=true)

## display password aging
`chage -l username`

## modify password configurations
`chage -m 0 -M 90 -W 7 -I 14 username`

## force update password
`chage -d 0 username`

## expire user
```bash
chage -E 2022-07-01
# hint: you can use the following command to get the date
date -d "+45days" -u
```

## restricting user (lock/unlock)
```bash
# lock user
usermod -L username
# lock and set expiry date
usermod -L -e 2022-12-05 username

# unlock user
usermod -U username
```

# **Chapter 10**
## remote access via ssh
```bash
ssh username@remotehost
ssh remotehost # use the current username
```

## execute commands remotely
`ssh username@remotehost pwd`

## known hosts and keys location
known hosts located at:
- /etc/ssh/ssh_known_hosts
- ~/.ssh/known_hosts

public/private keys located at:
- /etc/ssh/

##  keys permissions
- 600 for the private key
- 644 for the public key

## generate ssh keys and copy it to remote host
```bash
# generate key
ssh-keygen
ssh-keygen -f filename # specify file

# copy it to remote host (adding publickey to knownhosts of the remote system)
ssh-copy-id -i publickey.pub remote_user@remotehost
```

## authenticate to remote system using certain key
```ssh -i .ssh/privatekey remote_user@remotehost```

## using ssh-agent for non-interactive authentication
```bash
eval $(ssh-agent)
ssh-add key_filename
```

## customizing OpenSSH service configurations
`vim /etc/ssh/sshd_config`

most important edits are
```
PermitRootLogin no
PubkeyAuthentication yes
```