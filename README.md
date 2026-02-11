# File Backup Automation Script (Bash)

```bash
#!/bin/bash

# Variables
SOURCE="Documents"
BACKUP="Backup"

# Check if source folder exists
if [ -d "$SOURCE" ]; then
    echo "Backing up files..."

    mkdir -p "$BACKUP"

    # Loop through files
    for file in "$SOURCE"/*
    do
        if [ -f "$file" ]; then
            cp "$file" "$BACKUP"
        fi
    done

    echo "Backup completed."

else
    echo "Source folder not found."
fi

```

### Description of the Script

### a) Shebang Line

`#!/bin/bash`

Specifies that the script should be executed using the Bash shell interpreter.

---

### b) Variables

- `SOURCE="Documents"`
    
    Defines the source directory from which files will be copied.
    
- `BACKUP="Backup"`
    
    Defines the destination directory where files will be stored.
    

Using variables improves flexibility and maintainability of the script.

---

### c) Conditional Statement

`if [ -d "$SOURCE" ]; then`

- The `d` test checks whether the specified directory exists.
- If the directory exists, the backup process begins.
- If not, an error message is displayed.

This prevents errors that may occur if the source directory is missing.

---

### d) Directory Creation

`mkdir -p "$BACKUP"`

- Creates the backup directory.
- The `p` option ensures no error occurs if the directory already exists.

---

### e) Loop

`for file in "$SOURCE"/*`

- Iterates through all files inside the source directory.
- Each file path is stored temporarily in the variable `file`.

---

### f) File Check

`if [ -f "$file" ]; then`

- Ensures only regular files are copied.
- Prevents copying subdirectories unintentionally.

---

### g) File Copy Operation

`cp "$file" "$BACKUP"`

Copies each file from the source directory to the backup directory.

---

### Working Procedure

1. The script defines source and backup directories.
2. It verifies whether the source directory exists.
3. If available, it creates the backup directory (if needed).
4. It loops through all files in the source directory.
5. Each file is copied to the backup directory.
6. Displays completion message.

---

### Key Concepts Demonstrated

- Shell scripting structure
- Variable declaration and usage
- Conditional statements (`if-else`)
- Looping mechanism (`for` loop)
- Basic file operations (`cp`, `mkdir`)
