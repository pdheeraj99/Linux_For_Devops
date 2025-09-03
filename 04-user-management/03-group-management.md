# 3. Group Management: Collaboration and Permissions 🤝

Mawa, manam users ni create cheyadam chusam. Ippudu, aa users ni groups lo petti, permissions ni easy ga ela manage cheyalo nerchukundam. Oka project lo pani chese antha mandi developers ni `developers` ane group lo pedithe, manam aa okka group ki permissions isthe saripotundi, prathi individual user ki ivvalsina avasaram ledu. This is the power of groups.

---

### **`groupadd`**: Creating a New Group

*   **Purpose:** To create a new group on the system.
*   **Basic Usage:**
    ```bash
    # Create a new group called 'developers'
    sudo groupadd developers

    # Create another group called 'automation'
    sudo groupadd automation
    ```
*   **Common "Power-ups" (Options):**
    *   `-g <GID>`: Manually specify the **G**roup **ID** (GID). Normal ga system automatic ga next available GID ni istundi.
*   **Verification:** You can verify that the group was created by checking the `/etc/group` file.
    ```bash
    grep developers /etc/group
    ```
*   **Sample Output:**
    ```text
    developers:x:1004:
    ```

---

### **`groupmod`**: Modifying a Group

*   **Purpose:** Already unna group properties ni change cheyadaniki.
*   **Common "Power-ups" (Options):**
    *   `-n <new_name>`: Group యొక్క **n**ame ni change cheyadaniki.
    *   `-g <new_GID>`: Group యొక్క **G**ID ni change cheyadaniki.
*   **Real-World Usage:**
    ```bash
    # Let's rename the 'automation' group to 'cicd-team'
    sudo groupmod -n cicd-team automation

    # Verify the change
    grep cicd-team /etc/group
    ```
*   **Sample Output:**
    ```text
    cicd-team:x:1005:
    ```

---

### **Adding Users to a Group**

This is the most common group management task. As we saw in the last file, we use the `usermod` command for this.

*   **Command:** `usermod -aG <groupname> <username>`
*   **The Golden Rule:** **Always use `-a` (append)!** Ee option lekunda `-G` vadithe, user existing secondary groups anni poyi, kotha group matrame add avtundi. `-a` ensures you are **a**ppending the new group to the user's list of groups.
*   **Real-World Usage:**
    Let's add our user `sita` (from the previous lesson) to the new `developers` and `cicd-team` groups.

    ```bash
    # Add sita to the 'developers' group
    sudo usermod -aG developers sita

    # Add sita to the 'cicd-team' group as well
    sudo usermod -aG cicd-team sita

    # Now, let's verify which groups sita belongs to
    id sita
    ```
*   **Sample Output (`id sita`):**
    ```text
    uid=1003(sita) gid=1003(sita) groups=1003(sita),100(devops-team),101(testers),1004(developers),1005(cicd-team)
    ```
    You can see `developers` and `cicd-team` have been added to her list of groups.

---

### **`groups`**: Viewing a User's Groups

*   **Purpose:** To quickly see all the groups a specific user belongs to.
*   **Usage:**
    ```bash
    # See which groups the current user belongs to
    groups

    # See which groups the user 'sita' belongs to
    groups sita
    ```
*   **Sample Output (`groups sita`):**
    ```text
    sita : sita devops-team testers developers cicd-team
    ```

---

### **`groupdel`**: Deleting a Group

*   **Purpose:** To delete an existing group.
*   **Important Note:** You cannot delete a group if it is the primary group for any user. First, you must change that user's primary group or delete the user.
*   **Real-World Usage:**
    ```bash
    # Let's delete the 'testers' group we created earlier
    sudo groupdel testers

    # Verify it's gone
    grep testers /etc/group
    # (This command should produce no output)
    ```

Mawa, group management anedi user management tho kalisi chala powerful combination. Ee rendu concepts tho, nuvvu nee system lo permissions ni chala granular ga control cheyochu.

Next, manam `sudo` ane oka magical command gurinchi nerchukundam, adi normal users ki temporary ga superuser powers ela istundo chuddam.
