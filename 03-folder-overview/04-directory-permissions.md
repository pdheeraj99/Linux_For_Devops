# 4. A First Look at Directory Permissions 🚪

Mawa, manam `ls -l` command use chesinappudu, `drwxr-xr-x` lanti oka string chusam. Adi file or directory యొక్క permissions ni represent chestundi.

Permissions anevi Linux lo oka pedda and chala important topic. Manam deeni gurinchi `07-file-permissions` module lo full detail ga nerchukuntam. Kani ippudu, aa permissions oka directory ki apply ayinappudu వాటి meaning ento konchem chuddam.

A directory has three basic permissions for three types of users (owner, group, others):
*   **`r` (read)**
*   **`w` (write)**
*   **`x` (execute)**

Ee permissions files ki unna meaning ki, directories ki unna meaning ki konchem theda undi.

---

### **`r` (Read Permission) on a Directory**

*   **What it means:** If you have read permission on a directory, you can **list the contents** of that directory. Ante, nuvvu aa directory lo `ls` command run cheyagalavu.
*   **If you DON'T have read permission:** Nuvvu `ls` run cheste, neeku "permission denied" error vastundi. Nuvvu aa directory lo em files unnayo chudalenu.

    ```bash
    # Let's create a directory and remove read permission for everyone
    mkdir secret-files
    chmod a-r secret-files
    ls -ld secret-files
    # Output: d-wx-wx-wx 2 jules jules 4096 Sep  2 16:00 secret-files

    # Now, try to list its contents
    ls secret-files
    # Output: ls: cannot open directory 'secret-files': Permission denied
    ```

### **`w` (Write Permission) on a Directory**

*   **What it means:** If you have write permission on a directory, you can **create, delete, and rename files** within that directory. Ee permission file content ni modify cheyadaniki kaadu, directory content (the list of files) ni modify cheyadaniki.
*   **If you DON'T have write permission:** Nuvvu aa directory lo kotha file create cheyalante (`touch`), or unna file ni delete cheyalante (`rm`), neeku "permission denied" vastundi.

    ```bash
    # Let's give read/execute but remove write
    chmod a+rx,a-w secret-files
    ls -ld secret-files
    # Output: dr-xr-xr-x 2 jules jules 4096 Sep  2 16:00 secret-files

    # Now, try to create a file inside it
    touch secret-files/new-file.txt
    # Output: touch: cannot touch 'secret-files/new-file.txt': Permission denied
    ```

### **`x` (Execute Permission) on a Directory**

*   **What it means:** Execute permission on a directory is the most important. It allows you to **enter (or traverse)** that directory. Ante, nuvvu aa directory lo `cd` command use cheyagalavu. It also allows you to access files inside it, *if you know their exact name*.
*   **If you DON'T have execute permission:** Nuvvu aa directory loki `cd` cheyalenu. Nuvvu `ls -l` lanti commands tho aa directory lo unna files metadata ni kuda chudalenu.

    ```bash
    # Let's give read/write but remove execute
    chmod a+rw,a-x secret-files
    ls -ld secret-files
    # Output: drw-rw-rw- 2 jules jules 4096 Sep  2 16:00 secret-files

    # Now, try to enter it
    cd secret-files
    # Output: bash: cd: secret-files: Permission denied
    ```

---
## Summary

| Permission on Directory | Allows you to...                                    |
| ----------------------- | --------------------------------------------------- |
| **`r` (read)**          | List the names of the files in the directory (`ls`). |
| **`w` (write)**         | Create, delete, and rename files in the directory.  |
| **`x` (execute)**       | Enter the directory (`cd`) and access its contents. |

Mawa, idi just a teaser matrame. The combination of these permissions is very powerful. For now, just remember that to do anything with a directory, you almost always need `x` (execute) permission.

Manam `07-file-permissions` module lo `chmod`, `chown`, and inka chala vishayalu detail ga chuddam. For now, let's move on to some exercises to practice what we've learned in this module.
