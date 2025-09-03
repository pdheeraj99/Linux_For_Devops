# 1. Fundamental File Operations 📄

Mawa, manam directories tho pani cheyadam nerchukunnam. Ippudu, aa directories lopala unde files tho ela pani cheyalo chuddam. Files ni create cheyadam, copy cheyadam, move cheyadam, and delete cheyadam anedi Linux lo most common tasks.

---

### **`touch`**: Creating Empty Files and Updating Timestamps

*   **Purpose:** To create a new, empty file. If the file already exists, `touch` will update the file's access and modification timestamps to the current time.
*   **Basic Usage:**
    ```bash
    # Create a single empty file
    touch new-file.txt

    # Create multiple empty files at once
    touch index.html style.css script.js
    ```
*   **Common "Power-ups" (Options):**
    *   `-a`: Change only the **a**ccess time.
    *   `-m`: Change only the **m**odification time.
    *   `-d "<string>"`: Use a specific **d**ate string instead of the current time.
    *   `-r <ref_file>`: Use the timestamp of another **r**eference file.
*   **Real-World Usage:**
    ```bash
    # Create a file to start writing a script
    touch backup-script.sh

    # You made some changes to a config file and want to "mark" it
    # without actually changing the content.
    touch /etc/nginx/nginx.conf

    # Make file.txt have the same timestamp as file.log
    touch -r file.log file.txt
    ```

---

### **`cp`** (Copy) & **`mv`** (Move/Rename)

Ee commands files ki and directories ki similar ga pani chestayi, kani files tho konni extra details untayi.

*   **Purpose:**
    *   `cp <source> <destination>`: Copies a file.
    *   `mv <source> <destination>`: Moves a file.
    *   `mv <old_name> <new_name>`: Renames a file.
*   **Common "Power-ups" (Options):**
    *   `-i` (interactive): Overwrite chese mundu confirmation adugutundi. (Most systems lo `cp` and `mv` ki idi default alias.)
    *   `-v` (verbose): Em jarugutundo cheptundi.
    *   `-p` (preserve): `cp` tho use cheste, it preserves the original file's metadata (permissions, ownership, timestamps). Idi backups ki chala important.
    *   `-a` (archive): `cp -a` anedi `-r` (recursive) and `-p` (preserve) kalipi. It's the best way to copy a directory with all its properties intact.
*   **Real-World Usage:**
    ```bash
    # Create a backup of a configuration file before editing it
    sudo cp /etc/fstab /etc/fstab.bak

    # Rename a downloaded file to something more meaningful
    mv downloaded_file_123.zip ubuntu-22.04.iso

    # Move all .log files to a 'logs' directory
    mkdir logs
    mv *.log logs/
    ```

---

### **`rm`** (Remove) & **`shred`** (Secure Remove)

*   **Purpose:**
    *   `rm <file>`: To permanently delete a file.
    *   `shred <file>`: To securely delete a file by overwriting it with random data first, making it almost impossible to recover.
*   **🔥 WARNING! 🔥**
    `rm` is permanent. There is no "Recycle Bin". Use it carefully.
*   **Common "Power-ups" (`rm`):**
    *   `-i` (interactive): Asks for confirmation before deleting each file.
    *   `-f` (force): Deletes without asking for confirmation. Dangerous but useful in scripts.
*   **Real-World Usage:**
    ```bash
    # Delete a temporary file (will ask for confirmation on most systems)
    rm temp.txt

    # Forcefully delete a file without a prompt
    rm -f old-log.log

    # If you have a very sensitive file, shred it first, then delete.
    shred -vzu sensitive-data.txt
    # -v: verbose, -z: add a final overwrite with zeros, -u: deallocate and remove file after overwriting
    ```

---

## Comparing File Contents

Oka DevOps engineer ga, manam config files lo or code lo changes ni compare cheyalsina avasaram eppudu untundi.

### **`diff`**

*   **Purpose:** To compare two files line by line and show the differences.
*   **Common "Power-ups" (Options):**
    *   `-u` (unified format): Shows the differences with a few lines of context, which is much easier to read. This is the format used in Git and other version control systems.
    *   `-i`: **I**gnore case differences.
    *   `-w`: Ignore all **w**hite space.
    *   `-r`: **R**ecursively compare all files in two directories.
*   **Real-World Usage:**
    You have two versions of a config file, `nginx.conf.v1` and `nginx.conf.v2`.
    ```bash
    diff -u nginx.conf.v1 nginx.conf.v2
    ```
*   **Sample Output:**
    ```diff
    --- nginx.conf.v1       2025-09-02 18:00:00.000000000 +0000
    +++ nginx.conf.v2       2025-09-02 18:01:00.000000000 +0000
    @@ -1,5 +1,5 @@
     server {
    -    listen 80;
    +    listen 8080;
         server_name example.com;
    -    root /var/www/html;
    +    root /var/www/v2;
     }
    ```
    (`-` lines are from the first file, `+` lines are from the second file).

### **`cmp`** & **`comm`**

*   **`cmp` (compare):**
    *   **Purpose:** To check if two files are identical or not. `diff` anedi differences chupistundi, `cmp` anedi just different aa kaada ani cheptundi. It stops at the first difference, so it's very fast.
    *   **Usage:** `cmp file1 file2`. If they are identical, it produces no output. If they differ, it reports the line and byte number where the first difference occurs.
*   **`comm` (common):**
    *   **Purpose:** To compare two **sorted** files line by line.
    *   **Output:** It produces three columns. Column 1: lines only in file1. Column 2: lines only in file2. Column 3: lines common to both files.

Mawa, ee file operations anevi Linux lo bread and butter lanti vi. Veetini baaga practice cheyi. Next, manam different types of files gurinchi and vaati integrity ni ela check cheyalo chuddam.
