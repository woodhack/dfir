# Permissions

In Linux, every file and folder (also known as directories) has specific permissions that determine what actions users can perform on them. These permissions are divided into three main categories: **read**, **write**, and **execute**. Additionally, permissions are set for three distinct groups: the **owner** (user), the **group**, and **others** (everyone else).

### Permission Types

1. **Read (r)**: This permission allows the user to view the contents of a file or list the contents of a directory.
    - For a file: Read permission allows you to open and view the file.
    - For a directory: Read permission allows you to list the files inside the directory.
2. **Write (w)**: This permission allows the user to modify a file or directory.
    - For a file: Write permission allows you to edit, modify, or delete the file.
    - For a directory: Write permission allows you to add, delete, or rename files inside the directory.
3. **Execute (x)**: This permission allows the user to execute a file or access a directory.
    - For a file: Execute permission allows you to run the file as a program or script.
    - For a directory: Execute permission allows you to "enter" the directory, meaning you can access its contents.

### Permission Structure

Permissions are represented using either symbolic or numeric notation.

### Symbolic Representation:

Permissions are displayed in a string of 10 characters. For example:

`-rwxr-xr--`

The first character represents the file type:

- `` for a regular file.
- `d` for a directory.
- `l` for a symbolic link.

The next nine characters are divided into three sets of three, representing the permissions for:

1. The **owner** (user who owns the file).
2. The **group** (users who belong to the file’s group).
3. **Others** (everyone else).

In the above example, `rwxr-xr--`:

- **rwx**: The owner has read, write, and execute permissions.
- **r-x**: The group has read and execute permissions.
- **r--**: Others only have read permission.

### Numeric Representation (Octal Notation):

Permissions can also be represented numerically, using octal (base-8) numbers. Each permission is represented by a digit (4 for read, 2 for write, and 1 for execute), and the sum of these digits gives the final permission value.

For example:

- **7 (rwx)**: Read (4) + Write (2) + Execute (1) = 7
- **6 (rw-)**: Read (4) + Write (2) = 6
- **5 (r-x)**: Read (4) + Execute (1) = 5
- **4 (r--)**: Read (4) = 4

Permissions are grouped into three numbers representing the owner, group, and others. For example:

`chmod 755 filename`

This sets:

- **7 (rwx)** for the owner.
- **5 (r-x)** for the group.
- **5 (r-x)** for others.

### Changing Permissions

The `chmod` command is used to change file or directory permissions. You can use either symbolic or numeric notation to modify the permissions.

- **Symbolic Example**:
    
    `chmod u+rwx,g+rx,o+r filename`
    
    This grants:
    
    - The owner (u) read, write, and execute permissions.
    - The group (g) read and execute permissions.
    - Others (o) read permissions.
- **Numeric Example**:
    
    `chmod 755 filename`
    
    This gives:
    
    - Owner full access (rwx).
    - Group and others read and execute permissions (r-x).

### Ownership

Every file and directory in Linux has an associated owner and group. The **owner** is usually the user who created the file, and the **group** is a set of users who share the same group privileges. You can change ownership using the `chown` command.

- **Changing owner**:
    
    `sudo chown newowner filename`
    
- **Changing group**:
    
    `sudo chgrp newgroup filename`
    
- **Changing both owner and group**:
    
    `sudo chown newowner:newgroup filename`
    

### Special Permissions

In addition to the basic read, write, and execute permissions, there are special permissions in Linux:

1. **Setuid (Set User ID)**: When applied to an executable file, the process runs with the privileges of the file’s owner, not the user who runs it. Represented by an `s` in the owner’s execute permission (e.g., `rws`).
2. **Setgid (Set Group ID)**: When applied to an executable file, it causes the file to be executed with the privileges of the file’s group. For directories, files created inside the directory inherit the group ID. Represented by an `s` in the group’s execute permission (e.g., `rwxr-sr-x`).
3. **Sticky Bit**: When applied to a directory, it allows only the file's owner (or root) to delete or modify files within the directory, regardless of the directory’s write permissions. Represented by a `t` in others’ execute permission (e.g., `rwxrwxrwt`).