# File Types

> 📌 Linux considers every thing as a file.

There are three main classifications of files in Linux / Unix:
1. Regular Files
2. Directory Files
3. Special Files. Special Files further have 5 subcategories.

> 💡 The `ls -l` command can be used to identify a file type.

## Inode

Before moving onto files we'll learn about Inodes.

The **inode** is a data structure in a Unix-style file system which describes a filesystem object such as a file or a directory. Each inode stores the attributes and disk block location(s) of the object’s data. Filesystem object attributes may include metadata (times of last change, access, modification), as well as owner and permission data.

> 💡 Use `ls -i` to get the inode number.

## Regular Files

Examples of regular files are - readable files, binary files, image files, compressed files, etc. These files are indicated with `-` (in the first column) in `ls -l` command output. 

> 💡 Use a combination of `grep` and `ls -l` to list regular files : `ls -l | grep ^-`

## Directory Files

These type of files contains regular files/folders/special files stored on a physical device.  The number of symbolic links for a directory file is $\geq 2$. 

Directories are lists of names assigned to inodes. A directory contains an entry for itself, its parent, and each of its children. These files are indicated with `d` (in the first column) in `ls -l` command output. 

> 💡 Use a combination of `grep` and `ls -l` to list directory files : `ls -l | grep ^d`

## Special Files

#### **Device Files**

1. **Character** : Provides a serial stream of input or output. Terminals are classic example for this type of files. These files are indicated with `c` (in the first column) in `ls -l` command output. 

   > 💡 Use a combination of `grep` and `ls -l` to list directory files : `ls -l | grep ^c`
2. **Block** : These files are hardware files and most of them are present in `/dev`. These files are indicated with `b` (in the first column) in `ls -l` command output. 

   > 💡 Use a combination of `grep` and `ls -l` to list directory files : `ls -l | grep ^b`

#### Link Files

These are files linked to other files. They are either Directory/Regular File.  The inode number for this file and its parent files are same. 

There are two types of link files available in Linux/Unix ie Soft Link and Hard Link : 
1. **Hard Link** - A hard link is merely an additional name for an existing file on Linux or other Unix-like operating systems. Hard links can be created for other hard links but cannot be created for directories or files in another partition.
2. **Soft Link** - Soft links is a special kind of file that points to another file, much like a shortcut. Unlike a hard link, a symbolic link does not contain the data in the target file. It simply points to another entry somewhere in the file system. Soft links allows link to directories, or to files on remote computers. Also, when you delete a target file, symbolic links to that file become unusable, whereas hard links preserve the contents of the file.

These files are indicated with `l` (in the first column) in `ls -l` command output. Hard link files and soft links files can be told apart from each other in the `ls` command by checking their inode numbers and comparing them to the original file's inode. Hard link files and the original files have the same inode while the soft link file and the original files have different inodes.

> 💡 Use a combination of `grep` and `ls -l` to list directory files : `ls -l | grep ^l`

For more detailed explanation read this article on [Medium](https://blog.usejournal.com/what-is-the-difference-between-a-hard-link-and-a-symbolic-link-8c0493041b62).

#### Pipe Files

> TODO - Open for Contributiong

#### Socket Files

> TODO - Open for Contribution

----
