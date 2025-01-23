# Mongodb-Installation-in-Linux

Here are the steps to install MongoDB on a Linux server:

---

### **Step 1: Update System Packages**
```bash
sudo apt update
```
**Explanation**:  
This command updates the list of available packages and their versions. It's essential to ensure you're downloading the latest version of MongoDB and its dependencies.

---

### **Step 2: Install Required Packages**
```bash
sudo apt install -y gnupg
```
**Explanation**:  
This command installs the `gnupg` package, which is used to manage encryption keys. MongoDB requires signing keys to verify the integrity of the software.

The `-y` flag automatically answers "yes" to any prompts during installation.

---

### **Step 3: Import MongoDB GPG Key**
```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo gpg --dearmor -o /usr/share/keyrings/mongodb-archive-keyring.gpg
```
**Explanation**:  
- `wget -qO -`: Downloads the MongoDB GPG key silently (`-q`) and outputs it (`-O -`) to the standard output.
- `sudo gpg --dearmor`: Converts the ASCII GPG key into binary format, which is required for package verification.
- `-o /usr/share/keyrings/...`: Specifies where the converted GPG key should be saved. This key ensures that the packages are genuine and untampered.

---

### **Step 4: Add the MongoDB Repository**
```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/mongodb-archive-keyring.gpg] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```
**Explanation**:  
- `echo ... | sudo tee ...`: Adds the MongoDB repository details to your system's list of package sources.
- `arch=amd64`: Specifies the architecture for which MongoDB is installed (64-bit in this case).
- `signed-by=...`: Ensures the repository is signed with the GPG key added in the previous step.
- `https://repo.mongodb.org/...`: The URL for MongoDB's official repository.
- `focal`: Refers to the Ubuntu version (change this if using a different distribution).
- `multiverse`: The component where MongoDB is categorized in the repository.

---

### **Step 5: Update System Packages Again**
```bash
sudo apt update
```
**Explanation**:  
After adding the new repository, this command refreshes the package list to include MongoDB.

---

### **Step 6: Install MongoDB**
```bash
sudo apt install -y mongodb-org
```
**Explanation**:  
This installs the MongoDB package from the repository you just added. The `-y` flag ensures automatic confirmation of installation prompts.

---

### **Step 7: Start MongoDB**
```bash
sudo systemctl start mongod
```
**Explanation**:  
This starts the MongoDB service (`mongod` is the name of the MongoDB daemon).

---

### **Step 8: Enable MongoDB to Start on Boot**
```bash
sudo systemctl enable mongod
```
**Explanation**:  
This ensures that MongoDB starts automatically whenever the server is rebooted.

---

### **Step 9: Check MongoDB Status**
```bash
sudo systemctl status mongod
```
**Explanation**:  
Displays the current status of the MongoDB service, confirming whether it is active and running.

---

### **Step 10: Verify MongoDB Installation**
```bash
mongo --version
```
**Explanation**:  
This command checks and displays the installed version of the `mongo` shell, confirming that MongoDB is properly installed.

---

### Optional Step: Connect to MongoDB Shell
```bash
mongo
```
**Explanation**:  
This opens the MongoDB shell where you can interact with your database. If successful, the shell confirms that MongoDB is running correctly.

---

By following these steps, you will have MongoDB installed, running, and ready for use on your Linux server. Let me know if you'd like additional details!
