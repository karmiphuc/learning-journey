---
layout: post
summary: "INodes and its problem"
tags: linux programming troubleshoot
---
One of our development servers went down today.

Problems started with deployment script that claimed “No space left on device”although partition was not full (`df -h`).

If you ever run into such trouble – most likely you have too many small or 0-sized files on your disk, and while you have enough disk space, you have exhausted all available Inodes.

Below is the solution for this problem: http://www.ivankuznetsov.com/2010/02/no-space-left-on-device-running-out-of-inodes.html

---

> The definition of INodes also makes me feel curious
>
> Below is the copy of INodes definition on http://www.linfo.org/inode.html

An _inode_ is a [_data structure_](data_structure.html) on a [_filesystem_](filesystem.html) on [Linux](linuxdef.html) and other [Unix-like](unix-like.html) [operating systems](operating_system.html) that stores all the [information](information.html) about a [_file_](file.html) except its name and its actual [data](data.html).

A data structure is a way of storing data so that it can be used efficiently. Different types of data structures are suited to different types of applications, and some are highly specialized for specific types of tasks.

A filesystem is the hierarchy of directories (also referred to as the [_directory tree_](directory_tree.html)) that is used to organize files on a [computer](computer.html). On Unix-like operating systems, the directories start with the [_root directory_](root_directory.html) (designated by a [forward slash](forward_slash.html)), which contains a series of subdirectories, each of which, in turn, may contain further subdirectories, etc. A variant of this definition is the part of the entire hierarchy of directories or of the directory tree that is located on a single [hard disk drive](hdd.html) (HDD) or other [_storage_](storage.html) device or on a single [_partition_](partition.html) (i.e., a logically independent section of a HDD).

A file is a named collection of related information that appears to the user as a single, contiguous block of data and that is retained in storage. It does not automatically contain information about itself (e.g., its size, when it was created or where it is located on the system), unless some human purposely adds in such data. Such information _about_ a file, in contrast to the data contained _in_ a file, is its [_metadata_](metadata.html) (i.e., data about data).

Storage refers to computer devices or media that can hold data for relatively long periods of time (e.g., years or decades), such as disk drives and magnetic tape. A directory (referred to as a _folder_ on some operating systems) in Unix-like operating systems is merely a special type of file that associates file names with a collection of inodes.

When a file is created, it is assigned both a name and an _inode number_, which is an integer that is unique within the filesystem. Both the file names and their corresponding inode numbers are stored as entries in the directory that appears to the user to contain the files. That is, the directory associates file names with inodes.

Whenever a user or a [program](program.html) refers to a file by name, the operating system uses that name to look up the corresponding inode, which then enables the system to obtain the information it needs about the file to perform further operations. That is, a file name in a Unix-like operating system is merely an entry in a table with inode numbers, rather than being associated directly with a file (in contrast to other operating systems such as the Microsoft Windows systems). The inode numbers and their corresponding inodes are held in _inode tables_, which are stored in strategic locations in a filesystem, including near its beginning.

This detaching of a file's name from its other metadata is what allows the system to implement _hard links_ and thus have multiple names for any file. A hard link is an entry in a directory that contains a _pointer_ directly to the inode bearing the file's metadata. When a new hard link to a file is created, both links share the same inode number because the link is only a pointer, not a copy of the file.

The concept of inodes is particularly important to the recovery of damaged filesystems. When parts of the inode are lost, they appear in the _lost+found_ directory within the partition in which they once existed.

Whereas a file contains only its own content and a directory holds only the names of the files that appear to the user to be contained in it and their inode numbers, an inode contains all the other information describing a file. This metadata includes (1) the size of the file (in [bytes](byte.html)) and its physical location (i.e., the addresses of the blocks of storage containing the file's data on a HDD), (2) the file's owner and group, (3) the file's access [_permissions_](permissions.html) (i.e., which users are permitted to read, write and/or execute the file), (4) [timestamps](timestamp.html) telling when the inode was created, last modified and last accessed and (5) a reference count telling how many hard links point to the inode.

The operating system obtains a file's inode number and information in the inode through the use of the [_system call_](system_call.html) named _stat_. A system call is a request in a Unix-like operating system by an _active [process](process.html)_ for a service performed by the [_kernel_](kernel.html) (i.e., the core of the operating system), such as input/output (I/O) or process creation. System calls can also be viewed as clearly-defined, direct entry points into the kernel through which programs request services from it. A process is an [instance](instance.html) of a program in execution, and an active process process is one which is currently progressing in the [CPU](cpu.html) (central processing unit).

Space for inodes must be set aside when an operating system (or a new filesystem) is installed and that system does its initial structuring of the filesystem. Within any filesystem, the maximum number of inodes, and hence the maximum number of files, is set when the filesystem is created.

There are two ways in which a filesystem can run out of space: it can consume all the space for adding new data (i.e., to existing files or to new files), or it can use up all the inodes. The latter can bring computer use to a sudden stop just as easily as can the former, because exhaustion of the inodes will prohibit the creation of additional files even if sufficient HDD space exists. It is particularly easy to run out of inodes if a filesystem contains a very large number of very small files. A typical system, however, runs out of file space first, because the average file size on most system is larger than two kilobytes.

The decision as to how many inodes to create is made on Linux using an [_algorithm_](algorithm.html) (i.e., a set of precise and unambiguous rules that specify how to solve some problem or perform some task) that considers the size of the partition and the average file size. The default setting creates an inode for every 2K bytes contained in the filesystem, but the number can be adjusted by the user when creating the filesystem. For example, it can be wise to create fewer inodes when setting up a filesystem that will contain just a few large files. Similarly, for a filesystem intended for mostly small files, it is advisable to allocate more space to inodes and less to file contents.

A file's inode number can easily be found by using the _ls_ [command](command.html), which by default lists the _objects_ (i.e., files, links and directories) in the [_current directory_](current_directory.html) (i.e., the directory in which the user is currently working), with its _-i_ [option](option.html). Thus, for example, the following will show the name of each object in the current directory together with its inode number:

> `ls -i`

Additional information can be obtained about the inodes on a system by using the [_df_](df.html) command. This command by default shows the names and sizes of each [_mounted_](mounting.html) (i.e., logically connected to the main filesystem) filesystem as well as how much of each is used and unused. One of df's most useful options is _-h_, which formats the information in _human readable_ form (i.e., in terms of kilobytes, megabytes and [gigabytes](gigabyte.html)). Thus the following provides a nice display of both the currently available space and the used space for each filesystem or partition:

> `df -h`

df's _-i_ option instructs it to supply information about inodes on each filesystem rather than about available space. Specifically, it tells df to return for each mounted filesystem the total number of inodes, the number of free inodes, the number of used inodes and the percentage of inodes used. This option can be used together with the -h option as follows to make the output easier to read:

> `df -hi`

The exact story behind the creation of the term _inode_ has been lost, but it is very likely that the _i_ originally stood for _index_ and/or _information_.

Created June 6, 2005\. Updated September 15, 2006.  
Copyright © 2005 - 2006 The Linux Information Project. All Rights Reserved.
