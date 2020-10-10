# Post-compromise AD password reset 

_Notes copied from https://us-cert.cisa.gov/ncas/alerts/aa20-283a_

If there is an observation of CVE-2020-1472 Netlogon activity or other indications of valid credential abuse detected, it should be assumed the APT actors have compromised AD administrative accounts, the AD forest should not be fully trusted, and, therefore, a new forest should be deployed. Existing hosts from the old compromised forest cannot be migrated in without being rebuilt and rejoined to the new domain, but migration may be done through “creative destruction,” wherein as endpoints in the legacy forest are decommissioned, new ones can be built in the new forest. This will need to be completed on on-premise as well as Azure hosted AD instances.

Note that fully resetting an AD forest is difficult and complex; it is best done with the assistance of personnel who have successfully completed the task previously.

It is critical to perform a full password reset on all user and computer accounts in the AD forest. Use the following steps as a guide.

1. Create a temporary administrator account, and use this account only for all administrative actions
2. Reset the Kerberos Ticket Granting Ticket (krbtgt) password; this must be completed before any additional actions and a second reset will take place in step 5
3. Wait for the krbtgt reset to propagate to all domain controllers (time may vary)
4. Reset all account passwords (passwords should be 15 characters or more and randomly assigned):
5. User accounts (forced reset with no legacy password reuse)
6. Local accounts on hosts (including local accounts not covered by Local Administrator Password Solution [LAPS])
7. Service accounts
8. Directory Services Restore Mode (DSRM) account
9. Domain Controller machine account
10. Application passwords
11. Reset the krbtgt password again
12. Wait for the krbtgt reset to propagate to all domain controllers (time may vary)
13. Reboot domain controllers
14. Reboot all endpoints

The following accounts should be reset:

AD Kerberos Authentication Master (2x)  
All Active Directory Accounts  
All Active Directory Admin Accounts  
All Active Directory Service Accounts  
All Active Directory User Accounts  
DSRM Account on Domain Controllers  
Non-AD Privileged Application Accounts  
Non-AD Unprivileged Application Accounts  
Non-Windows Privileged Accounts  
Non-Windows User Accounts  
Windows Computer Accounts  
Windows Local Admin  
