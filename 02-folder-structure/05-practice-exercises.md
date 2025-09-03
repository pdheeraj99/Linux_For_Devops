# 5. New Tools & Practice Exercises 🏋️

Mawa, manam ee module lo filesystem structure gurinchi chala nerchukunnam. Ippudu, aa structure ni inka better ga explore cheyadaniki konni kotha, powerful commands nerchukundam. Tarvata, ee module lo nerchukunna concepts ni practice cheyadaniki konni exercises cheddam.

---

## New Commands for Filesystem Exploration

### **`tree`**

*   **Purpose:** Directories and files ni oka "tree-like" format lo chupinchadaniki. Idi directory structure ni visualize cheyadaniki chala powerful tool.
*   **Installation:** `tree` command konni minimal systems lo default ga undadu. Ubuntu lo `sudo apt update && sudo apt install tree` tho install cheyochu.
*   **Common "Power-ups" (Options):**
    *   `-L <level>`: **L**evel of depth. Entha deep ga tree chupinchalo cheptundi. `tree -L 2` ante current directory and daani sub-directories (2 levels) matrame chupistundi.
    *   `-d`: Only show **d**irectories, files ni skip chey.
    *   `-f`: Print the **f**ull path prefix for each file.
*   **Real-World Usage:**
    ```bash
    # See the structure of your current project, up to 2 levels deep
    tree -L 2

    # See only the directory structure of the /etc folder
    tree -d /etc
    ```
*   **Sample Output (`tree -L 2`):**
    ```text
    .
    ├── 01-filesystem-hierarchy.md
    ├── 02-root-directories.md
    ├── 03-absolute-vs-relative-paths.md
    ├── 04-hidden-files.md
    └── 05-practice-exercises.md

    0 directories, 5 files
    ```

### **`file`**

*   **Purpose:** Oka file asalu aey type o cheppadaniki. Adi text file aa, image aa, directory aa, leka oka executable program aa anedi `file` command cheptundi. It looks at the file's content, not just its extension.
*   **Real-World Usage:**
    ```bash
    # What type of file is .bashrc?
    file ~/.bashrc

    # What is /bin/ls?
    file /bin/ls

    # What is the current directory?
    file .
    ```
*   **Sample Output:**
    ```text
    /home/jules/.bashrc: ASCII text
    /bin/ls:             ELF 64-bit LSB pie executable, x86-64, ...
    .:                   directory
    ```

### **`stat`** (Status)

*   **Purpose:** `ls -l` kanna inka ekkuva, detailed metadata ni oka file gurinchi chupinchadaniki.
*   **Information Provided:**
    *   **File:** File name
    *   **Size:** File size in bytes
    *   **Blocks:** Disk blocks occupied
    *   **Device:** Device number
    *   **Inode:** Inode number (a unique ID for the file on the filesystem)
    *   **Links:** Number of hard links
    *   **Access/Modify/Change times:** Last access time (`Access`), last content modification time (`Modify`), and last metadata/permission change time (`Change`).
*   **Real-World Usage:**
    ```bash
    # Get all possible status information for a file
    stat /etc/passwd
    ```
*   **Sample Output:**
    ```text
      File: /etc/passwd
      Size: 2369            Blocks: 8          IO Block: 4096   regular file
    Device: 10302h/66306d    Inode: 131074      Links: 1
    Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
    Access: 2023-09-02 10:00:00.000000000 +0000
    Modify: 2023-08-15 12:00:00.000000000 +0000
    Change: 2023-08-15 12:00:00.000000000 +0000
     Birth: -
    ```

### Path Manipulation Commands

Ee commands oka full path nunchi file name or directory name ni extract cheyadaniki chala useful, especially in scripts.

### **`basename`** & **`dirname`**

*   **Purpose:**
    *   `basename`: Full path nunchi kevalam **file name** ni matrame istundi.
    *   `dirname`: Full path nunchi kevalam **directory path** ni matrame istundi.
*   **Real-World Usage (in a script):**
    ```bash
    FULL_PATH="/var/log/nginx/access.log"

    # Get just the filename
    LOG_FILE=$(basename "$FULL_PATH")
    echo "Log file name is: $LOG_FILE"

    # Get just the directory
    LOG_DIR=$(dirname "$FULL_PATH")
    echo "Log directory is: $LOG_DIR"
    ```
*   **Sample Output:**
    ```text
    Log file name is: access.log
    Log directory is: /var/log/nginx
    ```

### **`realpath`** & **`readlink`**

*   **Purpose:**
    *   `realpath`: Oka relative path or a path with symbolic links (`../` or symlinks) ni teeskoni, daani complete, absolute physical path ni istundi.
    *   `readlink -f`: Similar to `realpath`, it follows all symbolic links recursively and gives the final canonical path.
*   **Real-World Usage:**
    ```bash
    # Suppose you have a symbolic link
    # ln -s /usr/bin/python3.8 /home/jules/python

    cd ~
    # Get the real path of the link
    realpath ./python

    # Get the real path of a complex relative path
    realpath ./Documents/../Pictures
    ```
*   **Sample Output:**
    ```text
    /usr/bin/python3.8
    /home/jules/Pictures
    ```

---

## Practice Exercises

Mawa, ippudu konni assignments chesi, nee knowledge ni test chesko.

1.  **Map the City:**
    *   Root directory (`/`) ki navigate avvu.
    *   `ls -l` command use chesi, andulo unna main directories ni chudu.
    *   Ee kindi directories lo ki `cd` command tho velli, `pwd` tho mee current location ni confirm chesko:
        *   The directory for system configuration files.
        *   The directory where log files are usually stored.
        *   The directory that holds essential commands for all users.

2.  **Path Detective:**
    *   Nee home directory (`~`) nunchi, `/var/log` directory యొక్క content ni **relative path** use chesi list cheyadaniki try cheyi. (Hint: `cd ../../var/log`)
    *   `/tmp` directory lo undi, nee home directory lo unna `Downloads` folder content ni **absolute path** use chesi list cheyi.

3.  **The Hidden World:**
    *   Nee home directory lo, `.my_configs` ane oka hidden directory create cheyi.
    *   `ls -a` use chesi, adi create ayyindo ledo verify cheyi.

4.  **File Forensics:**
    *   `/bin/bash` ane file aey type o `file` command tho kanukko.
    *   `/etc/passwd` file యొక్క complete status information ni `stat` command tho chudu. Last time aa file eppudu access chesaro cheppu.

5.  **Tree Vision:**
    *   Nee home directory lo `tree -L 1` command run cheyi. Output em vastundo chudu.
    *   `tree -d -L 2 /usr` command run chesi, `/usr` loni directory structure ni ardam cheskovadaniki try cheyi.

Good luck, mawa! Ee exercises complete chesthe, neeku filesystem navigation meeda manchi confidence vastundi.
