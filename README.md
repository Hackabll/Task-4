# Task-4
Windows Firewall with Advanced Security (the standard tool for Windows) and UFW (Uncomplicated Firewall) for Linux, as the steps vary significantly between the two operating systems.
💻 1. Windows Firewall (GUI Method)
This is the easiest way to manage the firewall on a standard Windows machine.
Steps 1 & 2: Open Tool and List Rules
  Press the Windows key and type Windows Firewall with Advanced Security, then click to open it.
  In the left pane, click Inbound Rules to see the list of current rules (your "list").
Step 3: Add a Rule to Block Port 23 (Telnet) 
  In the right pane, click New Rule...
  Rule Type: Select Port, then click Next.
  Protocol and Ports: Select TCP and Specific local ports. Type 23 (the port for Telnet). Click Next.
  Action: Select Block the connection. Click Next.
  Profile: Check all three boxes (Domain, Private, Public). Click Next.
  Name: Give it a memorable name like Test Block Telnet 23. Click Finish.
Step 4: Test the Block Rule 
  Open Command Prompt (CMD)
  Type the test command: telnet 127.0.0.1 23 (If Telnet Client isn't installed, you'll need to install it first via "Turn Windows features on or off").
   Expected Result: The connection attempt should fail or time out, confirming the rule is blocking traffic.
Step 6: Remove the Test Block Rule 
  Go back to Windows Firewall with Advanced Security > Inbound Rules.
  Find the rule named Test Block Telnet 23.
  Right-click on it and select Delete. This restores the original state.
 2. Linux Firewall (UFW - Terminal Method)
UFW is the easiest firewall tool for most modern Linux distributions (like Ubuntu/Debian).
Steps 1 & 2: Open Tool and List Rules
  Open your Terminal.
  To check if UFW is active and see current rules:
   sudo ufw status verbose

Step 3: Add a Rule to Block Port 23 (Telnet) 
  Execute the following command to block all incoming traffic on TCP port 23:
   sudo ufw deny 23/tcp

Step 5: Add a Rule to Allow SSH (Port 22) 
Crucial Safety Step: If you are connecting to this machine remotely (via SSH), you must ensure SSH traffic is allowed before making any changes, or you might lock yourself out.
   sudo ufw allow ssh 
# OR the specific port number:
sudo ufw allow 22/tcp

Step 4: Test the Block Rule 
  From a different machine on the same network (or a different terminal window on the same machine), try to connect:
   telnet <Your_IP_Address> 23

  Expected Result: The connection should be refused or timeout, confirming the block.
Step 6: Remove the Test Block Rule 
  First, list the rules with their assigned numbers:
   sudo ufw status numbered

  Find the number next to the DENY 23/tcp rule (let's say it's 3).
  Delete the rule by its number (replace 3 with the number you found):
   sudo ufw delete 3

 7. Document Commands/GUI Steps
  Windows: Used the New Inbound Rule wizard to select Port, TCP 23, and the Block the connection action.
  Linux (UFW):
    List rules: sudo ufw status verbose
    Block Telnet: sudo ufw deny 23/tcp
    Allow SSH: sudo ufw allow 22/tcp
    Delete rule: sudo ufw delete <rule number>
 8. Summarize How Firewall Filters Traffic
A firewall is like a security guard at the entrance of your computer or network.
  It examines every piece of incoming and outgoing data, which is called a packet.
  It checks the packet against a set of predefined rules (the ones you listed and created).
  These rules often look at the port number (like an apartment number) and the source/destination IP address (like a street address).
  If the packet matches a rule that says "DENY" or "BLOCK" (like your Port 23 rule), the security guard immediately drops or rejects the packet.
  If the packet matches a rule that says "ALLOW" (like your SSH rule), the packet is let through to the proper program.
  This process effectively filters traffic, only allowing legitimate and authorized data to enter or leave your system, preventing unauthorized access (like from Telnet).
