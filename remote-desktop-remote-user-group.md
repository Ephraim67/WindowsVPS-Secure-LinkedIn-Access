To add a user to the **Remote Desktop Users** group on a Windows VPS, follow these steps:

### **Method 1: Using Computer Management (GUI)**
1. **Log into your Windows VPS** using an Administrator account via **Remote Desktop (RDP)**.  
2. **Open Computer Management**  
   - Press `Win + R`, type `compmgmt.msc`, and press **Enter**.  
3. **Go to Local Users and Groups**  
   - In the left panel, navigate to:  
     `System Tools` → `Local Users and Groups` → `Groups`  
4. **Find the Remote Desktop Users Group**  
   - In the right panel, double-click **"Remote Desktop Users"**.  
5. **Add a New User**  
   - Click **"Add"**, then enter the username of the user you want to grant RDP access.  
   - If unsure of the username, click **"Advanced" → "Find Now"** to select the correct user.  
6. **Click OK and Apply Changes**  
7. **Restart the VPS** (if necessary) and test login with the new user.


### **Method 2: Using Command Prompt (CMD)**
1. **Open Command Prompt as Administrator**  
   - Press `Win + R`, type `cmd`, and press **Ctrl + Shift + Enter** to run as **Administrator**.  
2. **Run the following command:**  
   ```
   net localgroup "Remote Desktop Users" <username> /add
   ```
   Example:  
   ```
   net localgroup "Remote Desktop Users" VAUser /add
   ```
3. **Verify the user was added:**  
   ```
   net localgroup "Remote Desktop Users"
   ```
4. **Test login with the new user via RDP.**


### **Method 3: Using PowerShell**
1. **Open PowerShell as Administrator**  
   - Press `Win + R`, type `powershell`, and press **Ctrl + Shift + Enter**.  
2. **Run the following command:**  
   ```powershell
   Add-LocalGroupMember -Group "Remote Desktop Users" -Member "<username>"
   ```
   Example:  
   ```powershell
   Add-LocalGroupMember -Group "Remote Desktop Users" -Member "VAUser"
   ```
3. **Confirm the user was added:**  
   ```powershell
   Get-LocalGroupMember -Group "Remote Desktop Users"
   ```
4. **Test the new user login via RDP.**


### **Final Steps**
- Ensure the user has a **password** (Windows does not allow RDP login for users without passwords).
- Open **Windows Firewall** and ensure **RDP (port 3389) is allowed** for the new user.
- If using AWS, update **Security Group Rules** to allow RDP connections from your trusted IP.  
