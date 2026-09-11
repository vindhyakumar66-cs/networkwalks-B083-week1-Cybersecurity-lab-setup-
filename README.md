🖥️ Week 1 – Cybersecurity Lab Environment Setup

Internship: Cybersecurity Internship — Batch B083 Organization: Networkwalks Academy Tools: Oracle VirtualBox • Kali Linux • NAT Network

🎯 Lab Purpose

This project sets up an isolated cybersecurity testing lab on a local machine using Oracle VirtualBox and Kali Linux. Running the attacking machine inside a sandboxed virtual environment allows security tools and configurations to be practiced safely, without any risk to the host system or the actual network. If something goes wrong, the lab can simply be reset from a snapshot instead of being rebuilt from scratch.

📋 Task Requirements

The lab was set up to meet the following specification:

Oracle VirtualBox (latest recommended version) as the virtualization platform
Kali Linux configured as the attacking/hacker machine
Custom NAT Network on subnet 10.0.0.0/24
Kali Linux assigned a static IP of 10.0.0.2/24
Clipboard sharing and file drag-and-drop enabled between host and guest
Shared folder enabled, mapping the host's /downloads folder into the VM
Full internet access confirmed on the Kali Linux machine
🧩 Lab Environment
Component	Configuration
Virtualization Platform	Oracle VirtualBox
Guest OS	Kali Linux
Network Mode	NAT Network
Subnet	10.0.0.0/24
Kali Linux IP Address	10.0.0.2/24
Shared Folder	/downloads (host → guest)
Clipboard & Drag/Drop	Enabled
Internet Access	Full access confirmed
🪜 Step-by-Step Build
Step 1: VirtualBox Installation

Installed the latest version of Oracle VirtualBox on the host machine as the hypervisor for the lab.
<img width="1600" height="897" alt="VM BOX INstallation" src="https://github.com/user-attachments/assets/7d7233a6-f21a-4984-b70a-c776e36aac51" />









Step 2: Kali Linux Setup

Set up Kali Linux as a guest VM to act as the attacking/hacker machine for future exercises.
<img width="1600" height="769" alt="Kali Linux setup" src="https://github.com/user-attachments/assets/40565279-b16b-4efa-9098-2ec3a3b0723a" />


Step 3: NAT Network Configuration

Configured a custom NAT Network on subnet 10.0.0.0/24, instead of using the default NAT adapter. A NAT Network was required (rather than plain NAT) so the VM could be given a fixed, predictable IP while still retaining outbound internet access.

(add screenshot)

Step 4: VM Settings — Clipboard, Drag/Drop & Shared Folder

Enabled bidirectional clipboard sharing and drag-and-drop in the VM settings, and set up a shared folder mapping the host's /downloads folder into Kali Linux, for easy file transfer between host and guest.

(add screenshot)

Step 5: Static IP Configuration

Assigned Kali Linux a static IP address of 10.0.0.2/24 within the NAT Network and verified internet connectivity.

(add screenshot)

Step 6: Snapshot

Took a VM snapshot once the network configuration was confirmed working, to use as a clean recovery point for future exercises.

(add screenshot)

🐞 Problems Faced & Solutions
Problem 1: Network option missing in VirtualBox settings

Issue: Under VirtualBox Tools, the Network option wasn't visible under Basic settings. Solution: Switched from Basic Mode to Expert Mode in VirtualBox, which revealed the Network configuration option.

Problem 2: No "Edit Connection" option in Kali Linux

Issue: Kali Linux's network settings didn't show a direct edit-connection option through the standard GUI path. Solution: Opened the connection editor manually using nm-connection-editor, then went to the wireless/wired connection and selected Edit from there. This initially assigned the IP 10.0.0.3 instead of the required 10.0.0.2, so the address had to be corrected manually to match the task requirement.

Problem 3: Connection not applying after IP change

Issue: After updating the IP address, the connection wasn't coming up properly. Solution: Resolved it from the terminal using nmcli:

bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"

Disabling the duplicate-address-detection timeout and cycling the connection down/up applied the new IP correctly.

💡 What I Learned This Week
The difference between VirtualBox's Basic and Expert view, and where key settings like Network configuration are hidden in each
How a custom NAT Network differs from a default NAT adapter, and why it's needed for a controllable, addressable lab VM
How to manually configure and troubleshoot network connections in Kali Linux using both nm-connection-editor and nmcli
Why static IP assignment matters for a lab environment, and how to fix an incorrectly assigned address
The value of taking a clean snapshot right after a working setup, so any future misconfiguration can be undone in seconds instead of rebuilding the VM
🔐 Security & Ethical Use

This lab is set up strictly for personal learning and authorized practice on a system I own. It is not used against any third-party or unauthorized network or system.

📸 Screenshots

Screenshots for each step above are added in the screenshots/ folder and linked inline.

👤 Author

Vindhya Cybersecurity Intern — Batch B083 Networkwalks Academy
