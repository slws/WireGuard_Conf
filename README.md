# WireGuard_Conf

Guide to Fetch NordVPN WireGuard Config Manually on Windows
This guide provides step-by-step instructions to manually obtain and configure NordVPN WireGuard settings on a Windows machine.

Prerequisites
A NordVPN subscription
Windows operating system
Internet access

Steps to Fetch NordVPN WireGuard Configuration
Step 1: Generate an Access Token
Go to the Nord Account Dashboard.
Log in to your account.
Create an access token.

Step 2: Save the Access Token
Copy the generated access token.
Open Notepad and paste the token for safekeeping.

Step 3: Launch Command Prompt
Click on the Start menu.
Type cmd in the search bar.
Right-click on "Command Prompt" and select "Run as administrator."

Step 4: Navigate to the Git Directory
In the Command Prompt, enter the following command:
cd c:\program files\git\mingw64\bin\

Step 5: Fetch User Credentials
Enter the following command, replacing <ACCESS_TOKEN> with your actual access token:
curl -s -u token:<ACCESS_TOKEN> https://api.nordvpn.com/v1/users/services/credentials
Copy the output and paste it into Notepad.

Step 6: Locate the Private Key
In Notepad, search for nordlynx_private_key.
Save the value you find for later use.

Step 7: Fetch Recommended Server
Enter the following command in Command Prompt:
curl -s "https://api.nordvpn.com/v1/servers/recommendations?&filters[servers_technologies][identifier]=wireguard_udp&limit=1"
Copy the output and paste it into Notepad.

Step 8: Extract Required Values
In Notepad, search for public_key and save this value.
Then search for station and save this value as well.

Step 9: Create the Configuration File
Open a new Notepad window.
Use the following template to create your configuration file, replacing placeholders with the values you saved:

[Interface]
PrivateKey = <PRIVATE_KEY> # from step 6
Address = 10.5.0.2/32 # this IP is always the same
DNS = 1.1.1.1 # your favorite DNS server

[Peer]
PublicKey = <PUBLIC_KEY> # from step 8
AllowedIPs = 0.0.0.0/0, ::/0 # route everything
Endpoint = <ENDPOINT>:51820 # station or IP from step 9, the port is always the same
Save the file with a .conf extension (e.g., nordvpn.conf).

Step 10: Connect to NordVPN
Use your VPN client that supports WireGuard to import the configuration file you created.
