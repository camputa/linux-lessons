# Comprehensive Guide to Common Built-In Linux Commands on Ubuntu 20.04

Welcome to the world of Linux! If you're new to Linux or just looking to deepen your understanding, this guide is here to help you navigate some of the most common built-in commands. We'll explore their options and configurations, providing you with the knowledge and confidence to use these powerful tools effectively. Let’s dive in and make your Linux journey enjoyable and enriching!

## Understanding the Basics

Linux commands are the building blocks of your interaction with the system. They help you manage files, navigate directories, monitor system performance, and much more. In this guide, we’ll cover the following commands:
- `ls`
- `pwd`
- `cd`
- `cp`
- `mv`
- `rm`
- `mkdir`
- `rmdir`
- `ln`
- `unlink`
- `chmod`
- `chown`

Each command comes with various options that enhance its functionality, allowing you to perform tasks efficiently and effectively.

## `ls` - List Directory Contents

The `ls` command lists the contents of a directory. It’s one of the most frequently used commands.

### Common Options

- `-l`: Long format listing, showing detailed information about files and directories.
- `-a`: Show all files, including hidden ones (those starting with a dot).
- `-h`: Human-readable format, making file sizes easier to understand.

### Example Usage

```bash
ls -l
```
This command will list the files and directories in the current directory in a detailed format, including permissions, owner, file size, and modification date.

```bash
ls -lah
```
Combining options to list all files (including hidden ones) in a detailed, human-readable format.

## `pwd` - Print Working Directory

The `pwd` command prints the current working directory, helping you keep track of your location within the file system.

### Example Usage

```bash
pwd
```
Simply typing `pwd` will display the full path to the current directory, ensuring you know exactly where you are in the file system.

## `cd` - Change Directory

The `cd` command changes the current directory to another directory specified by the user.

### Common Options

- `cd ..`: Move up one directory level.
- `cd /path/to/directory`: Move to a specific directory.

### Example Usage

```bash
cd /var/log
```
This command changes the current directory to `/var/log`, where system log files are stored.

```bash
cd ~
```
Moves to the home directory of the current user.

## `cp` - Copy Files and Directories

The `cp` command copies files and directories from one location to another.

### Common Options

- `-r`: Recursively copy directories.
- `-i`: Interactive mode, prompting before overwrite.
- `-u`: Copy only when the source file is newer than the destination file or when the destination file is missing.

### Example Usage

```bash
cp file.txt /backup/file.txt
```
This command copies `file.txt` to the `/backup/` directory.

```bash
cp -r /source_directory /backup/
```
Recursively copies the entire `source_directory` to the `/backup/` directory.

## `mv` - Move (or Rename) Files and Directories

The `mv` command moves or renames files and directories.

### Common Options

- `-i`: Interactive mode, prompting before overwrite.
- `-u`: Move only when the source file is newer than the destination file or when the destination file is missing.

### Example Usage

```bash
mv oldname.txt newname.txt
```
This command renames `oldname.txt` to `newname.txt`.

```bash
mv file.txt /backup/file.txt
```
Moves `file.txt` to the `/backup/` directory.

## `rm` - Remove Files and Directories

The `rm` command deletes files and directories.

### Common Options

- `-r`: Recursively remove directories and their contents.
- `-i`: Interactive mode, prompting before each removal.
- `-f`: Force removal without prompting.

### Example Usage

```bash
rm file.txt
```
This command deletes `file.txt`.

```bash
rm -rf /tmp/test_directory
```
Forcefully and recursively removes the `test_directory` and its contents in `/tmp`.

## `mkdir` - Make Directories

The `mkdir` command creates new directories.

### Common Options

- `-p`: Create parent directories as needed.

### Example Usage

```bash
mkdir new_directory
```
This command creates a new directory named `new_directory`.

```bash
mkdir -p /new/path/to/directory
```
Creates the specified directory along with any necessary parent directories.

## `rmdir` - Remove Empty Directories

The `rmdir` command deletes empty directories.

### Example Usage

```bash
rmdir empty_directory
```
This command removes the `empty_directory` if it is empty.

## `ln` - Create Links

The `ln` command creates hard and symbolic links.

### Common Options

- `-s`: Create a symbolic (soft) link.
- `-f`: Force creation by removing existing destination files.

### Example Usage

```bash
ln -s /path/to/file.txt symlink.txt
```
This command creates a symbolic link `symlink.txt` pointing to `/path/to/file.txt`.

```bash
ln /path/to/file.txt hardlink.txt
```
Creates a hard link `hardlink.txt` pointing to `/path/to/file.txt`.

## `unlink` - Remove Symbolic Links

The `unlink` command removes symbolic links.

### Example Usage

```bash
unlink symlink.txt
```
This command removes the symbolic link `symlink.txt`.

## `chmod` - Change File Permissions

The `chmod` command changes the permissions of files or directories.

### Common Options

- `u`: User (owner) permissions.
- `g`: Group permissions.
- `o`: Other (world) permissions.
- `a`: All permissions (user, group, and others).
- `r`: Read permission.
- `w`: Write permission.
- `x`: Execute permission.
- `+`: Add a permission.
- `-`: Remove a permission.
- `=`: Set exact permissions.

### Example Usage

```bash
chmod u+x script.sh
```
This command adds execute permission for the user (owner) to the file `script.sh`.

```bash
chmod g-w file.txt
```
Removes write permission for the group from `file.txt`.

## `chown` - Change File Owner and Group

The `chown` command changes the owner and group of a file or directory.

### Common Options

- `user`: Specify the new owner.
- `:group`: Specify the new group.
- `-R`: Recursively change ownership for all files and directories.

### Example Usage

```bash
chown user:group file.txt
```
This command changes the owner of `file.txt` to `user` and the group to `group`.

```bash
chown -R user:group /path/to/directory
```
Recursively changes the ownership of all files and directories within `/path/to/directory`.

## Conclusion

Congratulations on exploring the common built-in Linux commands! Understanding these commands is essential for efficient system management and daily tasks on Ubuntu 20.04. Each command has its unique options and configurations, offering powerful ways to interact with your system. Keep practicing, stay curious, and continue your journey in the fascinating world of Linux. Happy learning!