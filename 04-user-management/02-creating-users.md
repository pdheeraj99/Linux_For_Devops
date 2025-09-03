# 2. Managing User Accounts: `useradd`, `usermod`, `userdel` 🧑‍🔧

Mawa, manam user concepts nerchukunnam. Ippudu, aa users ni actually create cheyadaniki, modify cheyadaniki, and delete cheyadaniki use chese core commands ni chuddam. Ee commands anni normal ga `root` user or `sudo` privileges tho matrame run cheyagalam.

---

### **`useradd`**: Creating a New User

*   **Purpose:** To create a new user account on the system.
*   **Basic Usage:**
    ```bash
    # Create a new user named 'ravi'
    sudo useradd ravi
    ```
    Ee command `ravi` ane user ni create chestundi, kani konni important things miss avtayi (like home directory, password). Anduke, manam eppudu "power-ups" tho kalipi vadali.

*   **Common "Power-ups" (Options):**
    *   `-m` (create home): User ki `/home/username` lo oka home directory create chestundi. **Idi almost eppudu use cheyali.**
    *   `-s <shell_path>` (shell): User ki login shell set chestundi. Default ga `/bin/sh` untundi, kani manam normal ga interactive users ki `/bin/bash` istham.
    *   `-c "<comment>"` (comment): User gurinchi oka description ivvadaniki. Usually user yokka full name or role.
    *   `-g <group>`: User yokka **primary group** set cheyadaniki.
    *   `-G <groups>`: User ki **secondary groups** (comma-separated list) assign cheyadaniki.
    *   `-d /path/to/home`: Custom home directory path set cheyadaniki.

*   **Real-World Usage (Putting it all together):**
    ```bash
    # Create a new developer named 'sita' with a home directory,
    # a bash shell, a comment, and add her to the 'devops-team' group.
    sudo useradd -m -s /bin/bash -c "Sita, Developer" -G devops-team sita

    # Verify that the user was created by checking /etc/passwd
    grep sita /etc/passwd
    ```
*   **Sample Output (`grep sita /etc/passwd`):**
    ```text
    sita:x:1003:1003:Sita, Developer:/home/sita:/bin/bash
    ```
*   **Setting a Password:** `useradd` password set cheyadu. User create chesaka, manam `passwd` command tho password set cheyali.
    ```bash
    sudo passwd sita
    # It will prompt you to enter and re-enter the new password.
    ```

---

### **`usermod`**: Modifying an Existing User

*   **Purpose:** Already unna user account properties ni change cheyadaniki.
*   **Common "Power-ups" (Options):** Eevi `useradd` options laage untayi.
    *   `-aG <groups>`: **A**ppend to **G**roups. User ni kotha secondary groups ki add cheyadaniki. `-a` (append) lekunda vadithe, user existing groups nunchi remove aipotadu. **This is very important!**
    *   `-l <new_name>`: User yokka login **l**name ni change cheyadaniki.
    *   `-s <shell_path>`: User yokka shell ni change cheyadaniki.
    *   `-L` (Lock): User account ni lock cheyadaniki (disable login).
    *   `-U` (Unlock): Lock chesina account ni unlock cheyadaniki.

*   **Real-World Usage:**
    ```bash
    # Add our user 'sita' to the 'testers' group as well.
    # Use -a to append, otherwise she will be removed from 'devops-team'.
    sudo usermod -aG testers sita

    # Lock sita's account temporarily
    sudo usermod -L sita

    # Unlock her account
    sudo usermod -U sita
    ```

---

### **`userdel`**: Deleting a User

*   **Purpose:** To delete a user account.
*   **Common "Power-ups" (Options):**
    *   `-r` (remove): **Ee option chala important.** Idi user account tho paatu, valla home directory and mail spool ni kuda delete chestundi. Ee option lekunda delete cheste, aa user files system lo anadhaga migilipotayi.
*   **Real-World Usage:**
    ```bash
    # Delete the user 'ravi' and all of their files.
    sudo userdel -r ravi
    ```

---

## Viewing User Information

Ippudu, users gurinchi information ela chudalo nerchukundam. Ee commands ki normal ga `sudo` avasaram ledu.

*   **`id <username>`**: Shows a user's UID, primary GID, and all secondary groups.
    ```bash
    id sita
    # Output: uid=1003(sita) gid=1003(sita) groups=1003(sita),100(devops-team),101(testers)
    ```
*   **`who`**: System lo evaru log in ayyaro chupistundi.
*   **`w`**: `who` kanna detailed output istundi. User entha sepati nunchi idle ga unnadu, em command run chestunnadu lanti details chupistundi.
*   **`last`**: Recent logins yokka history chupistundi.
*   **`finger <username>`**: User gurinchi inkonni details (Full Name, shell, etc.) chupistundi. (Konni systems lo install cheyali).
*   **`getent passwd <username>`**: `/etc/passwd` file ni query cheyadaniki correct way. It also works with network-based user databases like LDAP.
    ```bash
    getent passwd sita
    # Output: sita:x:1003:1003:Sita, Developer:/home/sita:/bin/bash
    ```

Mawa, ee commands tho nuvvu user accounts ni full control cheyochu. Next file lo, manam groups ni inka detail ga ela manage cheyalo chuddam.
