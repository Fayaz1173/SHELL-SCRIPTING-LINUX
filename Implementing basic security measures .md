# Implementing basic security measures 

1. Aim
    
    To implement basic security measures in a Linux system and document the steps clearly.
    
2. Introduction
    
    Linux is a multi-user operating system. To keep the system secure, we must control who can read, write, and execute files. Basic security mainly involves setting correct file permissions, managing ownership, and limiting unnecessary access.
    
3. Restricting File Permissions

Step 1: Create a file

```
touch confidential.txt
```

Step 2: Give permission only to the owner

```
chmod 600 confidential.txt
```

Step 3: Verify

```
ls -l confidential.txt
```

Result:

Only the owner can read and write the file. Others cannot access it.

Purpose: Protect sensitive data from unauthorized users.

1. Securing Script Files

Step 1: Create a script

```
touch backup.sh
```

Step 2: Allow only the owner to use it

```
chmod 700 backup.sh
```

Step 3: Verify

```
ls -l backup.sh
```

Result:

Only the owner can read, write, and execute the script.

Purpose: Prevent other users from running or modifying the script.

1. Using Groups for Secure Access

Step 1: Create a group

```
sudo groupadd projectgrp
```

Step 2: Assign group to a directory

```
sudochgrp projectgrp project/
```

Step 3: Set group permissions

```
chmod 770 project/
```

Step 4: Verify

```
ls -ld project/
```

Result:

Owner and group members have full access. Others have no access.
