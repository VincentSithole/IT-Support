# Ticket 1: Printer Offline

## The Problem
A user from the finance department submitted a ticket stating, "My computer says the printer is offline, and I have invoices to print for the end of the month."

## Troubleshooting Steps
1. **Verify Physical Connections:** Asked the user to check if the printer's power cable and network (Ethernet) cable were securely plugged in. (They were).
2. **Check Network Connectivity:** Asked the user to ping the printer's IP address (`ping 192.168.1.50`). The request timed out.
3. **Check Printer Status:** Walked the user through checking the printer's display screen. It showed an IP conflict error.
4. **Resolve IP Conflict:** Logged into the router, found a new device had been assigned the printer's old IP. 
5. **Action:** Assigned a static IP to the printer (192.168.1.250) so this won't happen again. Reconfigured the printer port on the user's Windows PC.

## Resolution
The user was able to print the invoices successfully. The printer is now on a static IP to prevent future conflicts.

## Cloud/DevOps Tie-In
In a corporate environment, instead of managing local IPs, I would use a print management server (like Windows Server Print Services) or a cloud printing solution (like Google Cloud Print or Microsoft Universal Print) to ensure seamless connectivity.
