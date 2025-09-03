# 5. Switching Users: `su` vs. `sudo` 🎭

Mawa, manam different users ni create chesam. Ippudu, oka user nunchi inkoka user ga ela maaralo chuddam. Idi oka server ni manage chestunnappudu or oka specific user tho problem ni debug chestunnappudu chala avasaram avtundi.

There are a few ways to do this, each with a slightly different, but very important, outcome.

---

### **`su <username>`** (Switch User)

*   **Purpose:** To switch to another user account. If you don't provide a username, it defaults to switching to the `root` user.
*   **How it works:** Ee command run cheste, adi aa destination user yokka password adugutundi. For example, `su ravi` run cheste, adi `ravi` yokka password adugutundi. `su` run cheste, adi `root` password adugutundi.
*   **The Problem:** `su` switches the user, but it **keeps your original environment**. Ante, nee `PATH`, `HOME` variable, and other shell settings maaravu. This can lead to a lot of confusion and unexpected behavior.
*   **Real-World Usage:**
    ```bash
    # Let's switch to the 'ravi' user
    su ravi
    Password:  #<-- Enter ravi's password here

    # Now, let's check who we are and where we are
    whoami
    # Output: ravi

    pwd
    # Output: /home/jules  <-- See? We are still in jules's home directory! This is confusing.
    ```
    Because of this confusion, `su` by itself is **not recommended**.

---

### **`su -`** or **`su -l <username>`** (Login Shell)

*   **Purpose:** This is the **correct way** to use `su`. It switches to another user and also starts a **new login shell** for that user.
*   **How it works:** The `-` or `-l` (login) flag makes a huge difference. It completely resets the environment to what the new user would get if they logged in directly. The `HOME` directory changes, the `PATH` is reloaded from their profile files (`.bashrc`, `.bash_profile`), etc.
*   **Real-World Usage:**
    ```bash
    # Let's switch to the 'ravi' user the RIGHT way
    su - ravi
    Password:  #<-- Enter ravi's password here

    # Now, let's check who we are and where we are
    whoami
    # Output: ravi

    pwd
    # Output: /home/ravi  <-- Much better! We are now in ravi's home.
    ```
    To become the `root` user with a full login shell, you would run `su -`.

---

### **`sudo -i`** (Interactive)

*   **Purpose:** To get a full, interactive login shell as the `root` user.
*   **How it works:** Idi `su -` ki chala similar, kani oka pedda advantage undi: idi **nee own password** adugutundi, `root` password kaadu. This is much more secure because you don't need to share the root password with anyone.
*   **Real-World Usage:**
    If you need to run many commands as root, instead of typing `sudo` for every command, you can just become `root` temporarily.
    ```bash
    # Become root
    sudo -i
    [sudo] password for jules:  #<-- Enter YOUR (jules's) password

    # Now check who you are
    whoami
    # Output: root
    ```

---

### **`sudo -u <username> <command>`**

*   **Purpose:** To run a **single command** as another user, without fully switching to them.
*   **How it works:** This is useful for testing or running processes as a specific application user.
*   **Real-World Usage:**
    Let's say you are the `root` user, but you want to check how a command would behave for the user `sita`.
    ```bash
    # As root or a sudoer, run the 'ls -la' command as if you were 'sita'
    sudo -u sita ls -la /home/sita
    ```
    This is very useful in scripts where you need to run a specific task with a specific user's permissions.

---

## Summary: Which One to Use?

| Command                 | Switches to... | Asks for...         | Environment             | Best For...                                         |
| ----------------------- | -------------- | ------------------- | ----------------------- | --------------------------------------------------- |
| `su <user>`             | `<user>`       | `<user>`'s password | Keeps original          | **Not Recommended**                                 |
| **`su - <user>`**       | `<user>`       | `<user>`'s password | Full login shell        | Switching to a user when you know their password.   |
| **`sudo -i`**           | `root`         | **Your** password   | Full login shell        | Becoming `root` for an extended period. (Preferred) |
| **`sudo -u <user>`**    | `<user>`       | **Your** password   | For one command only    | Running a single command as another user.           |

Mawa, ee differences ardam cheskovadam chala important for both security and functionality. Most of the time, you will be using `sudo -i` or `sudo -u`.

Next up, we'll look at how to manage password policies and other user details.
