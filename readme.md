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
