# Firewall Task - Windows Defender Firewall Configuration

## 📌 Overview
This repository contains my completed **Firewall Task** using **Windows Defender Firewall**.  
The objective was to create, test, and remove a firewall rule that blocks Telnet (port 23) while keeping SSH (port 22) allowed.

---

## 📂 Contents
- **firewall_full_prep_and_walkthrough_windows.pdf** – Detailed report with interview prep answers and step-by-step task explanation (Windows version).
- **Screenshots/** – Visual proof of each step (before rule creation, after enabling, testing block, restoring defaults).
- **Restoration Proof** – Screenshot showing rule removed and firewall restored.

---

## 🛠 Task Description
### **Objective**
1. Block inbound Telnet connections (port 23).
2. Keep SSH (port 22) allowed to prevent remote lockout.
3. Test the rule to confirm the block.
4. Remove the rule and restore defaults.

### **Steps Performed**
1. **Open Windows Defender Firewall (Advanced Settings)**
   - Press `Win + R`, type:
     ```
     wf.msc
     ```
     and press **Enter**.

2. **Create a new inbound rule**
   - Go to **Inbound Rules** → **New Rule**.
   - Choose **Port** → **TCP** → Specific local ports: `23`.
   - Action: **Block the connection**.
   - Profile: Select all (Domain, Private, Public).
   - Name: `Block Telnet (Port 23)`.

3. **Allow SSH (if needed)**
   - Ensure there is an **Allow Rule** for TCP port 22.
   - If not, create one using the same steps but choose **Allow the connection**.

4. **Verify the new rule**
   - List inbound rules in the GUI or run in PowerShell:
     ```powershell
     Get-NetFirewallRule | Where-Object {$_.DisplayName -like "*Telnet*"}
     ```

5. **Test the block**
   - From another device, attempt to connect to this machine using Telnet:
     ```powershell
     Test-NetConnection -ComputerName <Your_IP> -Port 23
     ```
     - Expected result: TCP test failed (blocked).

6. **Remove the block rule**
   - In **Windows Defender Firewall with Advanced Security**, find the `Block Telnet (Port 23)` rule.
   - Right-click → **Delete**.

7. **Verify removal**
   ```powershell
   Get-NetFirewallRule | Where-Object {$_.DisplayName -like "*Telnet*"}
