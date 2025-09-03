# 3. Directory Operations: Moving, Copying, and Deleting 📦

Mawa, manam directories create cheyadam and vaatilo navigate cheyadam nerchukunnam. Ippudu, aa directories ni move cheyadam, copy cheyadam, and delete cheyadam elaago chuddam. Ee operations ki manam `mv`, `cp`, and `rm` lanti commands ni use chestam, kani directories kosam konni specific options vaadali.

---

### **`mv` (Move / Rename)**

The `mv` command is used for both moving and renaming directories.

*   **Purpose 1: Renaming a Directory**
    ```bash
    # Let's create a directory named 'work'
    mkdir work

    # Now, let's rename 'work' to 'projects'
    mv work projects

    # Verify the change
    ls
    ```
*   **Purpose 2: Moving a Directory**
    ```bash
    # Let's create a 'backups' directory
    mkdir backups

    # Now, let's move the 'projects' directory inside the 'backups' directory
    mv projects backups

    # Verify with tree
    tree backups
    ```
*   **Sample Output:**
    ```text
    backups
    └── projects

    1 directory, 0 files
    ```
*   **Common "Power-ups" (Options):**
    *   `-i` (interactive): Move chese mundu confirmation adugutundi, especially when overwriting. **Important:** Chala modern Linux systems lo, `mv` anedi default ga `mv -i` ki alias chesi untundi. Anduke manaki confirmation prompt vastundi.
    *   `-f` (force): Asks for no confirmation. It will forcefully overwrite the destination if it exists. Use with caution!
    *   `-n` (no-clobber): Destination lo already ade peru tho file/directory unte, overwrite cheyadu and error ivvadu. Idi `-f` ki opposite and scripts lo chala safe.
    *   `-v` (verbose): Em jarugutundo cheptundi.

---

### **`cp -r` (Copy Directory)**

The `cp` command needs a special "power-up" to copy directories.

*   **Purpose:** To copy a directory and all of its contents (files and sub-directories) to a new location.
*   **The Magic Power-up: `-r` or `-R` (recursive)**
    *   Ee option lekunda, `cp` command directory ni copy cheyaledu. `-r` tells `cp` to go inside the directory, copy all the files, go inside every sub-directory, copy all their files, and so on, until everything is copied.
*   **Real-World Usage:**
    ```bash
    # Let's create a project structure
    mkdir -p my-app/src
    touch my-app/src/main.js

    # Now, let's create a version 2 by copying the original
    cp -r my-app my-app-v2

    # Verify with tree
    tree
    ```
*   **Sample Output:**
    ```text
    .
    ├── my-app
    │   └── src
    │       └── main.js
    └── my-app-v2
        └── src
            └── main.js

    4 directories, 2 files
    ```
*   **Important Note:** If the destination directory (`my-app-v2` in this case) already exists, `cp -r` will copy the source directory *inside* the destination directory.

---

### **`rmdir` (Remove Directory)**

*   **Purpose:** To delete **empty** directories.
*   **Key Limitation:** Ee command ਕੇవలం empty directories ni matrame delete cheyagaladu. Directory lo okka file unna, `rmdir` fail avtundi.
*   **Real-World Usage:**
    ```bash
    # Create an empty directory
    mkdir temporary-folder

    # Remove it
    rmdir temporary-folder

    # Create a directory with a file inside
    mkdir not-empty
    touch not-empty/file.txt

    # This will fail!
    rmdir not-empty
    ```
*   **Sample Output (for the failed command):**
    ```text
    rmdir: failed to remove 'not-empty': Directory not empty
    ```
    This is a safety feature. `rmdir` is a very safe command to use.

---

### **`rm -r` (Remove Recursively) - The DANGEROUS Command**

Mawa, ee command chala jagrathaga use cheyali. It's extremely powerful and can wipe out your entire system if used incorrectly.

*   **Purpose:** To delete a directory and **everything** inside it, including all sub-directories and files.
*   **The `-r` (recursive) option:** Tells `rm` to delete recursively.
*   **The `-f` (force) option:** Tells `rm` to ignore non-existent files and never prompt for confirmation. `rm -rf` is the combination of these two.
*   **Real-World Usage (with caution):**
    ```bash
    # We have the 'not-empty' directory from the last example
    # Let's delete it and everything inside it
    rm -r not-empty

    # To avoid any confirmation prompts (be very careful!)
    # rm -rf not-empty
    ```
*   **🔥 WARNING! 🔥**
    *   There is **no undo** for `rm -rf`. There is no "Recycle Bin". Once it's gone, it's gone forever.
    *   **NEVER, EVER** run a command like `rm -rf /` or `rm -rf *` in a system directory unless you know EXACTLY what you are doing. It can destroy your entire Linux system.
    *   Always double-check your `pwd` before running `rm -rf`.
    *   Many people add an alias for `rm` to be `rm -i` (interactive) in their `.bashrc` file to prevent accidental deletion.

Mawa, directory operations anevi fundamental. Practice them well. Next, manam directory permissions gurinchi konchem తెలుసుకుందాం.
