# 1. Creating Directories with `mkdir` 📂

Mawa, manam directories lo navigate cheyadam nerchukunnam. Ippudu, manaki కావలసినట్టు kotha directories ni ela create cheyalo chuddam. The primary command for this is `mkdir` (make directory).

---

## The `mkdir` Command

*   **Purpose:** To create one or more new directories.
*   **Basic Usage:**
    ```bash
    # Create a single directory named 'projects' in the current location
    mkdir projects

    # Create multiple directories at the same time
    mkdir scripts images backups
    ```
*   **Important Note:** By default, `mkdir` will give an error if you try to create a directory that already exists, or if the parent directory doesn't exist. Ee kindi "power-ups" aa problems ni solve chestayi.

---

### **Power-up: `-p` (parents)**

This is probably the most useful option for `mkdir`.

*   **Purpose:** To create a nested directory structure. If the parent directories don't exist, `-p` will create them for you. It also suppresses the error if the directory already exists, making it safe to use in scripts.
*   **Real-World Usage:**
    Imagine you need to create a directory structure like `project-alpha/src/components`. If you just run `mkdir project-alpha/src/components`, it will fail because `project-alpha` and `src` don't exist yet.

    ```bash
    # This will fail!
    # mkdir project-alpha/src/components
    # Output: mkdir: cannot create directory ‘project-alpha/src/components’: No such file or directory

    # This is the correct way - it creates the entire path
    mkdir -p project-alpha/src/components

    # Let's verify with the tree command
    tree project-alpha
    ```
*   **Sample Output:**
    ```text
    project-alpha
    └── src
        └── components

    2 directories, 0 files
    ```
*   **DevOps Scenario:** When writing an automation script, you often need to ensure a specific directory exists before writing a file to it. Using `mkdir -p` is the standard, safest way to do this.

    ```bash
    # A script to ensure a log directory exists
    LOG_DIR="/var/log/my-app"
    echo "Ensuring log directory exists at $LOG_DIR"
    mkdir -p "$LOG_DIR"
    echo "Log directory is ready."
    ```

---

### **Power-up: `-m` (mode)**

*   **Purpose:** To set the file permissions (mode) for the new directory at the time of creation. Manam permissions gurinchi `07-file-permissions` module lo inka detail ga nerchukundam, but this is a useful shortcut.
*   **Real-World Usage:**
    You need to create a directory that only you (the owner) can access. The permission mode `700` gives read, write, and execute permissions only to the owner.

    ```bash
    # Create a directory with permissions 700
    mkdir -m 700 my-private-stuff

    # Let's check the permissions with ls -ld
    ls -ld my-private-stuff
    ```
*   **Sample Output:**
    ```text
    drwx------ 2 jules jules 4096 Sep  2 15:00 my-private-stuff
    ```
    Notice the `drwx------`. The `rwx` is only for the first set (the user/owner).

---

### **Power-up: `-v` (verbose)**

*   **Purpose:** To print a message for each directory created. Idi `-p` tho kalipi use cheste, aey directories create ayyayo clear ga chupistundi.
*   **Real-World Usage:**
    ```bash
    # Create a nested path and see what's happening
    mkdir -pv new-project/assets/images
    ```
*   **Sample Output:**
    ```text
    mkdir: created directory 'new-project'
    mkdir: created directory 'new-project/assets'
    mkdir: created directory 'new-project/assets/images'
    ```

Mawa, `mkdir -p` anedi nee rojuvari workflow lo chala important command avtundi. Get used to it! Next, manam directories madhyalo efficiently navigate cheyadaniki konni advanced techniques chuddam.
