# Chapter 3

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
    * -> 0 or more
    ? -> 1 character
    touch file-{1..9}{1..9}{1..9}
    ls *[13]*
    ls file??[34]
    [!abc...] -> any character not in brackets
    [^abc...] -> any character not in brackets

## Variables
```bash
x=50
echo ${x}
echo Time and data is $(data)
```