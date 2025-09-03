# 5. Disk Usage Commands & Practice Exercises 🧠

Mawa, manam directories ni create cheyadam, move cheyadam, and delete cheyadam nerchukunnam. Kani, aa directories entha space teesukuntunnayo teluskovadam kuda chala important. As a DevOps engineer, disk space monitoring anedi oka critical task.

Ee section lo, manam disk space ni check cheyadaniki use chese konni powerful commands nerchukundam.

---

## Commands to Analyze Disk Space

### **`du` (Disk Usage)**

*   **Purpose:** To find out how much space a specific directory (and its sub-directories) is using.
*   **Common "Power-ups" (Options):**
    *   `-h` (human-readable): Ee option output ni `K` (kilobytes), `M` (megabytes), `G` (gigabytes) lo chupistundi. Chala useful.
    *   `-s` (summarize): Ee option total size matrame chupistundi, prathi sub-directory size ni chupinchadu.
    *   `-a` (all): Directories tho paatu, individual files yokka size ni kuda chupistundi.
    *   `--max-depth=N`: Entha level of sub-directories varaku velli size chupinchalo cheptundi. `--max-depth=1` ante current directory lo unna prathi file/folder size ni chupistundi.
*   **Real-World Usage:**
    ```bash
    # /var/log directory entha space teesukuntundo chudu
    du -sh /var/log

    # Find the largest sub-directories in your current location
    du -h --max-depth=1 . | sort -rh | head -n 5

    # The above command first gets the sizes, then sorts them in reverse
    # human-readable order, then shows the top 5. Chala powerful!
    ```
*   **Sample Output (`du -sh /var/log`):**
    ```text
    512M    /var/log
    ```

### **`df` (Disk Free)**

*   **Purpose:** `du` anedi oka specific folder size kosam, kani `df` anedi motham filesystem (or hard drive) lo entha space free ga undi, entha used undi anedi chupistundi.
*   **Common "Power-ups" (Options):**
    *   `-h` (human-readable): Most important option. Sizes ni GB, MB lo chupistundi.
    *   `-T` (type): Filesystem type ni kuda chupistundi (e.g., `ext4`, `xfs`).
    *   `-i`: Disk space tho paatu, **inode** usage ni chupistundi. Konni sarlu disk space unna, inodes aipotayi (if there are millions of tiny files), appudu ee command useful.
*   **Real-World Usage:**
    ```bash
    # Check the disk space on all mounted filesystems in a readable format
    df -h
    ```
*   **Sample Output (`df -h`):**
    ```text
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/sda1        50G   20G   30G  40% /
    tmpfs           1.9G     0  1.9G   0% /dev/shm
    /dev/sdb1       100G   50G   50G  50% /data
    ```

### **`ncdu` (NCurses Disk Usage)**

*   **Purpose:** Idi `du` ki oka interactive, user-friendly version. Nuvvu `ncdu` run cheste, adi nee directories ni scan chesi, aey folder entha space teesukuntundo oka nice interface lo chupistundi. You can navigate through directories and quickly find what's eating up your disk space.
*   **Installation:** `ncdu` default ga undadu. `sudo apt install ncdu` or `sudo yum install ncdu` tho install cheyali.
*   **Real-World Usage:**
    ```bash
    # Analyze the disk usage of the current directory interactively
    ncdu

    # Analyze the entire root filesystem (might take time)
    # sudo ncdu /
    ```
*   **Sample Output:** It will open a full-screen interactive menu where you can use arrow keys to navigate.

---

## Practice Exercises

Mawa, ippudu ee module lo nerchukunna commands anni kalipi practice cheddam.

1.  **Project Setup:**
    *   Nee home directory lo, `learning-project` ane oka directory create cheyi.
    *   `learning-project` lopala, `mkdir -p` use chesi, `src/components`, `assets/images`, and `docs` ane nested directories ni okke command tho create cheyi.
    *   `tree` command tho nee project structure ni verify cheyi.

2.  **Directory Juggling:**
    *   `pushd` use chesi, `assets/images` loki vellu.
    *   `pushd` use chesi, `docs` loki vellu.
    *   Ippudu, `dirs -v` tho nee directory stack ni chudu.
    *   `pushd +1` lanti command use chesi, stack ni rotate chesi `assets/images` ki jump cheyi.
    *   `popd` use chesi stack nunchi directories ni remove cheyi, until you are back in the `learning-project` directory.

3.  **Cleanup Mission:**
    *   `learning-project` lopala, `temp-stuff` ane oka kotha directory create cheyi.
    *   `rmdir` tho daanini delete cheyadaniki try cheyi. It should work.
    *   Ippudu, `docs` directory ni `documentation` ga rename cheyi.
    *   `assets` directory ni `static` ane kotha directory loki move cheyi.
    *   Final ga, chala jagrathaga, `rm -r` use chesi `static` directory ni delete cheyi.

4.  **Disk Space Investigation:**
    *   `du -sh` use chesi, nee home directory (`~`) entha space use chestundo kanukko.
    *   `df -h` use chesi, nee root (`/`) filesystem lo entha space available ga undo chudu.

Ee exercises complete chesthe, neeku directory management meeda full command vastundi. Good luck!
