**Disk Usage Monitoring: Write a script to check disk usage and alert if it exceeds a threshold.** 

```bash
┌──(kali㉿kali)-[~/shell_scripting]
└─$ cat diskusage.sh  
#!/bin/bash

THRESHOLD=35

USAGE=$(df / | grep / | awk '{print $5}' | sed 's/%//')

if [ "$USAGE" -ge "$THRESHOLD" ];then
        notify-send echo "warning Disk usage exceeded over ${THRESHOLD}%! "
else
        echo "Disk usage under control"
fi

```

<img width="512" height="289" alt="image" src="https://github.com/user-attachments/assets/1123f287-9fbc-45f2-8a04-3d66f8f2605c" />

for notification :

- install - libnotify-bin
- add  **“notify-send”** before the echo command

for automation :

```bash
* * * * * DISPLAY=:0 /home/kali/shell_scripting/diskusage.sh
That means:
		*   *   *   *      *
minute hour day month weekday

# for 10 minute 

*/10 * * * * DISPLAY=:0 /home/kali/shell_scripting/diskusage.sh

```

### `THRESHOLD=35`

- Defines a shell variable named `THRESHOLD`
- Stores the value `35`
- Used later as the comparison limit for disk usage
- In Bash, variables are untyped; `35` is treated as a string but used numerically when compared

---

### `USAGE=$(df / | grep / | awk '{print $5}' | sed 's/%//')`

- Uses **command substitution**: `$(...)`
- Bash executes everything inside and assigns the final output to `USAGE`

Step-by-step inside the pipeline:

- `df /`
    
    Displays disk usage statistics for the root (`/`) filesystem
    
- `grep /`
    
    Filters lines that contain `/` to isolate the filesystem entry
    
- `awk '{print $5}'`
    
    Extracts the 5th whitespace-separated column, which is the disk usage percentage (e.g. `42%`)
    
- `sed 's/%//'`
    
    Removes the `%` symbol, leaving only the numeric value
    

Final result:

`USAGE` contains a number like `42`

---

### `if [ "$USAGE" -ge "$THRESHOLD" ]; then`

- Starts a conditional statement
- `[ ... ]` is the `test` command
- `ge` performs a numeric “greater than or equal to” comparison
- Evaluates whether disk usage is greater than or equal to the threshold

If the condition is true, the next block executes

---

### `notify-send echo "warning Disk usage exceeded over ${THRESHOLD}%! "`

- Attempts to send a desktop notification
- `notify-send` is a command used in Linux graphical environments
- `"warning Disk usage exceeded over ${THRESHOLD}%!"` is the message text
- `${THRESHOLD}` expands to the value of the variable

Bash expands the variable **before** running the command

---

### `else`

- Defines the alternative branch
- Executes only if the `if` condition evaluates to false

---

### `echo "Disk usage under control"`

- Prints a message to standard output
- Indicates disk usage is below the threshold

---

### `fi`

- Ends the `if` conditional block
- Required to close every `if` statement in Bash
