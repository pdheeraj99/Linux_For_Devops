# 2. Advanced Navigation: The Directory Stack 📚

Mawa, manam `cd` command tho directories ela maaralo chusam. Kani, manam frequent ga konni specific directories madhyalo switch avvalsina paristhithi vastundi. For example, oka project lo `/etc/nginx/sites-available` ki, `/var/log/nginx` ki, and `~/my-project/src` ki repeatedly vellalsi raavochu.

Prathi sari full path type cheyadam or `cd -` use cheyadam antha efficient kaadu. Anduke, shell manaki oka powerful feature istundi: the **Directory Stack**.

---

## What is the Directory Stack?

The directory stack is a temporary, in-memory list of directories you've been to. You can add directories to this list, view the list, and quickly jump to any directory in the list.

It works on a **LIFO (Last-In, First-Out)** principle, like a stack of plates. The last directory you add (`push`) is on top of the stack, and the first one you can remove (`pop`) is the one from the top.

Ee stack ni manage cheyadaniki manaki a మూడు commands unnayi: `pushd`, `popd`, and `dirs`.

---

### **`pushd` (Push Directory)**

*   **Purpose:** Ee command rendu panulu chestundi:
    1.  It "pushes" (adds) a directory onto the top of the stack.
    2.  It immediately `cd`s you into that directory.
*   **Real-World Usage:**
    Let's say you are in your home directory (`~`) and want to work on your web server configuration.

    ```bash
    # Check our current location
    pwd
    # Output: /home/jules

    # Push the Nginx config directory onto the stack and go there
    pushd /etc/nginx/sites-available

    # Now check our location
    pwd
    # Output: /etc/nginx/sites-available
    ```

### **`dirs` (Directories)**

*   **Purpose:** To display the current directory stack. The directory at the top of the stack (index 0) is your current working directory.
*   **Common "Power-ups" (Options):**
    *   `-v`: **V**erbose. Shows the stack with an index number for each directory, which is much more useful.
*   **Real-World Usage:**
    Continuing from the previous example...

    ```bash
    # Let's see what's on our stack
    dirs -v
    # Output:
    #  0  /etc/nginx/sites-available
    #  1  /home/jules

    # Now, let's push the Nginx log directory onto the stack
    pushd /var/log/nginx

    # Let's check the stack again
    dirs -v
    # Output:
    #  0  /var/log/nginx
    #  1  /etc/nginx/sites-available
    #  2  /home/jules
    ```
    As you can see, the stack is growing. The most recent directory is always at the top (index 0).

### **`popd` (Pop Directory)**

*   **Purpose:** Ee command kuda rendu panulu chestundi:
    1.  It "pops" (removes) the top directory from the stack.
    2.  It immediately `cd`s you into the new top directory.
*   **Real-World Usage:**
    We are currently in `/var/log/nginx`.

    ```bash
    # Let's pop the top directory from the stack
    popd

    # Where are we now?
    pwd
    # Output: /etc/nginx/sites-available

    # Let's check the stack. /var/log/nginx should be gone.
    dirs -v
    # Output:
    #  0  /etc/nginx/sites-available
    #  1  /home/jules
    ```

### Jumping Between Directories in the Stack

You can also use `pushd` to jump to any directory already in the stack by using its index number (from `dirs -v`).

*   **Purpose:** To rotate the stack and bring any directory to the top.
*   **Real-World Usage:**
    Our stack is `0 /etc/nginx/sites-available` and `1 /home/jules`. We are currently in the nginx directory. Let's jump to our home directory.

    ```bash
    # Jump to the directory at stack index 1
    pushd +1

    # Check our location and the stack
    pwd
    # Output: /home/jules
    dirs -v
    # Output:
    #  0  /home/jules
    #  1  /etc/nginx/sites-available
    ```
    Notice how the stack was rotated? The directory at index 1 came to the top.

---
Mawa, `pushd`, `popd`, and `dirs` anevi terminal lo mee productivity ni chala penchutayi. When you find yourself switching between the same 3-4 directories repeatedly, remember to use the directory stack!

Next up, we'll learn how to copy, move, and delete the directories we've been creating.
