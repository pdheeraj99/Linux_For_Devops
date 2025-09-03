# 6. Password Policies and User Details 🔐

Mawa, manam user accounts create chesam, kani vaati security ni inka improve cheyochu. Ee file lo, manam password policies ni ela enforce cheyalo and user account details ni ela change cheyalo nerchukundam.

---

### **`passwd`**: Changing Passwords

Manam ee command ni already chusam, but let's look at it again.

*   **Purpose:** To change a user's password.
*   **Usage:**
    *   `passwd`: Changes the password for the **current** user.
    *   `sudo passwd <username>`: A sysadmin can use this to change the password for **any** user. It's also used to set the password for a newly created account for the first time.
*   **Real-World Usage:**
    ```bash
    # As a sysadmin, reset the password for user 'ravi'
    sudo passwd ravi
    # Enter new password:
    # Retype new password:
    # passwd: password updated successfully
    ```

---

### **`chage`**: Managing Password Aging

*   **Purpose:** `chage` (change age) anedi oka powerful command. Deenitho, manam oka user yokka password eppudu expire avvalo, expire ayye mundu enni rojulu warning ivvalo, lanti rules set cheyochu. This is a key tool for security compliance.
*   **Common "Power-ups" (Options):**
    *   `-l <username>` (**l**ist): Shows the current password aging policies for a user.
    *   `-m <days>`: Sets the **m**inimum number of days between password changes.
    *   `-M <days>`: Sets the **M**aximum number of days a password is valid.
    *   `-W <days>`: Sets the number of **W**arning days before a password expires.
    *   `-d 0`: Forces the user to change their password on their next login.
*   **Real-World Usage:**
    Let's set a policy for the user `sita`.
    ```bash
    # First, let's see the current policy for 'sita'
    sudo chage -l sita

    # Now, let's set a policy:
    # Minimum 7 days, Maximum 90 days, Warning 14 days before expiry
    sudo chage -m 7 -M 90 -W 14 sita

    # Let's verify the new policy
    sudo chage -l sita
    ```
*   **Sample Output (`chage -l sita` after update):**
    ```text
    Last password change                                    : Sep 02, 2025
    Password expires                                        : Dec 01, 2025
    Password inactive                                       : never
    Account expires                                         : never
    Minimum number of days between password change          : 7
    Maximum number of days between password change          : 90
    Number of days of warning before password expires       : 14
    ```

---

### **`chsh`**: Changing the Login Shell

*   **Purpose:** To **ch**ange a user's default login **sh**ell.
*   **Common "Power-ups" (Options):**
    *   `-s <shell_path>`: Sets the new shell.
    *   `-l` (**l**ist): Lists all available shells on the system (from `/etc/shells`).
*   **Real-World Usage:**
    A user `ravi` was created with the default `/bin/sh`, but now he needs `bash`.
    ```bash
    # See available shells
    chsh -l

    # Change ravi's shell to /bin/bash
    sudo chsh -s /bin/bash ravi

    # Verify the change in /etc/passwd
    grep ravi /etc/passwd
    ```
*   **Sample Output (`grep ravi`):**
    ```text
    ravi:x:1004:1004::/home/ravi:/bin/bash
    ```
    You can also disable a user's login ability by setting their shell to `/sbin/nologin`.

---

### **`chfn`**: Changing User Information

*   **Purpose:** To **ch**ange a user's "finger" i**n**formation. This is the information that appears in the comment field of `/etc/passwd`.
*   **How it works:** Running `chfn <username>` will interactively prompt you to enter the user's Full Name, Room Number, Work Phone, and Home Phone.
*   **Real-World Usage:**
    Our user `sita` was created with the comment "Sita, Developer". Let's add more details.
    ```bash
    # Change info for sita
    sudo chfn sita
    # It will then ask you for the details one by one.

    # Let's see the result
    finger sita
    ```
*   **Sample Output (`finger sita`):**
    ```text
    Login: sita                             Name: Sita, Developer
    Directory: /home/sita                   Shell: /bin/bash
    ...
    ```

---
Mawa, ee commands tho nuvvu user accounts ni inka secure ga and detailed ga manage cheyochu. Ee module tho, you now have a strong foundation in user and group management.

This concludes Module 04! As per our autonomous mode, I will now proceed to submit this module and then start the plan for the next one: Module 05 - File Management.
