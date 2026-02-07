## CPU and Memory Monitoring: Monitor CPU and memory usage and log the data.

```bash
┌──(kali㉿kali)-[~/shell_scripting]
└─$ cat cpu-memory~monitoring.sh
#!/bin/bash

LOG_DIR="$HOME/shell_scripting"
LOG_FILE="$LOG_DIR/systemusage.log"

mkdir -p "$LOG_DIR"

DATE=$(date "+%Y-%m-%d %H:%M:%S")
CPU=$(top -bn1 | awk '/Cpu\(s\)/ {printf "%.2f", 100 - $8}')
MEMORY=$(free | awk '/Mem:/ {printf "%.2f", $3/$2 * 100}')

echo "$DATE | CPU:${CPU}% | Memory usage:${MEMORY}%" >> "$LOG_FILE"

```

<img width="572" height="115" alt="image" src="https://github.com/user-attachments/assets/d726786a-672e-4376-968b-692c4cd6e4ec" />

## **Line-by-line explanation**

### **1. `#!/bin/bash`**

- Tells Linux that this script should be run with **Bash**.
- Always at the top of shell scripts.

---

### **2. `LOGFILE="$HOME/system_usage.log"`**

- Creates a variable called **`LOGFILE`** that stores the **path of the log file**.
- **`$HOME`** → your home directory, e.g., **`/home/username`**.

---

### **3. `DATE=$(date "+%Y-%m-%d %H:%M:%S")`**

- **`date`** command gets the **current date and time**.
- **`+...`** formats it as **YYYY-MM-DD HH:MM:SS**.
- **`$()`** → stores the output in variable **`DATE`**.

Example:

```
2026-02-07 14:30:01
```

---

### **4. `CPU=$(top -bn1 | grep "Cpu(s)" | awk '{print 100 - $8}')`**

- **`top -bn1`** → runs the **`top`** command **once in batch mode**.
- **`grep "Cpu(s)"`** → selects only the line containing CPU usage.
- **`awk '{print 100 - $8}'`** → extracts the **idle CPU value ($8)** and calculates **CPU usage = 100 − idle**.
- Stores the result in variable **`CPU`**.

Example:

```
CPU=12.5# CPU usage in percent
```

---

### **5. `MEM=$(free -m | awk '/Mem:/ {printf("%.2f"), $3/$2 * 100}')`**

- **`free -m`** → shows memory usage in **MB**.
- **`awk '/Mem:/ { ... }'`** → selects the line starting with **`Mem:`**.
- **`$3/$2 * 100`** → calculates **used memory percentage** (used ÷ total × 100).
- **`printf("%.2f")`** → formats it to **2 decimal places**.
- Stores the result in variable **`MEM`**.

Example:

```
MEM=41.23# Memory usage in percent
```

---

### **6. `echo "$DATE | CPU: $CPU% | MEM: $MEM%" >> "$LOGFILE"`**

- **`echo`** → prints a formatted string with **date, CPU, and memory usage**.
- **`>> "$LOGFILE"`** → **appends** the output to the log file (does not overwrite it).
- This is what creates a **running log** of your system usage.

Example log line:

```
2026-02-07 14:30:01|CPU:12.5%|MEM:41.23%
```
