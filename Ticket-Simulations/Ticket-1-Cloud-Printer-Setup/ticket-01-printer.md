# Ticket 01: Setting up a Cloud Print Server (CUPS on AWS EC2)

## 📌 Issue Summary
The local on-premise server (32-bit Debian) lacked the hardware architecture to install and run modern 64-bit print server software (CUPS). The objective was to migrate the print service to a cloud environment to ensure compatibility and availability.

## 🛠️ Environment & Tools Used
*   **Cloud Provider:** AWS (Amazon Web Services)
*   **Compute:** EC2 (t2.micro running Ubuntu 22.04 LTS)
*   **Software:** CUPS (Common UNIX Printing System)
*   **Networking:** SSH, TCP Port 631, AWS Security Groups

## 🚀 Troubleshooting & Resolution Steps

1.  **Provisioned the Cloud Server:** 
    Launched a free-tier AWS EC2 instance running Ubuntu (64-bit) to bypass local hardware limitations. 
2.  **Connected Securely:** 
    Used SSH with a `.pem` key pair (`chmod 400`) to securely connect to the server from a local Debian machine.
3.  **Installed the Software:** 
    Updated the package repository (`sudo apt update`) and successfully installed CUPS (`sudo apt install cups -y`).
4.  **Configured Remote Access:** 
    By default, CUPS only listens to localhost. Ran `sudo cupsctl --remote-any` to allow external connections.
5.  **Troubleshot Connectivity (The Cloud Firewall):** 
    Attempting to access the web interface via `http://<Public-IP>:631` resulted in a connection timeout. 
    *   **Root Cause:** AWS Security Groups act as a virtual firewall and block all ports by default.
    *   **Resolution:** Went to the AWS EC2 Console > Security Groups > Added an Inbound Rule for **Custom TCP on Port 631** with the source `0.0.0.0/0`.
6.  **Verification:** 
    Ran `sudo ss -tulpn | grep 631` to verify CUPS was listening on `0.0.0.0:631`. Successfully accessed the CUPS web interface via a browser.

## 🎓 Key Learnings
*   Cloud networking requires a layered security approach. You must open the port in both the Cloud Firewall (AWS Security Group) and the local application config (`cupsd.conf`).
*   Migrating services to the cloud solves physical hardware limitations.

## 📸 Proof of Work (Screenshots)

Here is the visual proof of the deployment:

### 1. Ubuntu Server Installation & CUPS Setup
![Ubuntu Installation](ubuntu%20installation.jpg)
![Installation of CUPS](installation%20of%20cups.jpg)

### 2. Server IP & Web Interface
![CUPS Host](cups%20host.jpg)
![CUPS Website](cups%20website.jpg)
