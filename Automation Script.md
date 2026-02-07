**1.Bulk file renaming**

```bash
┌──(kali㉿kali)-[~/shell_scripting]
└─$ cat [rename.sh](http://rename.sh/)
#!/bin/bash
cd new_folder ||exit

PREFIX="new_"

for file in *.txt; do
mv "$file" "${PREFIX}${file}"
done

echo "renaming completed"
```

**2.Temperory files removing**

```bash
┌──(kali㉿kali)-[~/shell_scripting]
└─$ cat tmp_clearing.sh   
#!/bin/bash

echo "clearing temporary files"

sudo rm -rf /var/tmp/*
sudo rm -rf /tmp/*
sudo rm -rf ~/.cache/*

echo "cleared"

```

**3.Updating and upgrading the linux system**

```bash
┌──(kali㉿kali)-[~/shell_scripting]
└─$ cat update.sh   
#!/bin/bash

echo "updating and upgrading your linux"

sudo apt update
sudo apt upgrade

echo "Done"
           
```
