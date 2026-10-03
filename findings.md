# Windows Security Log Investigation — Findings

## Investigation Summary

I analyzed simulated Windows Security Event logs to identify suspicious authentication and account activity.

The evidence suggests that the administrator account may have been compromised. Multiple failed login attempts were followed by a successful login from the same source IP. Administrative privileges were then observed, a new account was created, and the Windows Security audit log was later cleared.

## Evidence

### Repeated Failed Logins

Four Event ID 4625 events occurred against the administrator account from source IP 192.168.1.77.

The attempts occurred approximately four seconds apart.

This pattern could indicate automated password guessing or brute-force activity.

### Successful Administrator Login

Event ID 4624 showed a successful administrator login from 192.168.1.77 shortly after the failed attempts.

This made the earlier authentication failures more suspicious.

### Administrative Privileges

Event ID 4672 appeared shortly after the successful administrator login.

This indicated that special privileges were assigned to the new logon session.

### New Account Created

Event ID 4720 showed that the administrator account created a new account named backup_admin.

The new backup_admin account later successfully logged in from 192.168.1.77.

This could represent an attempt to establish persistent access.

### Security Audit Log Cleared

Event ID 1102 showed that the Windows Security audit log was cleared by the administrator account.

In the context of the preceding suspicious activity, this could indicate an attempt to remove evidence or cover the attacker's tracks.

## Incident Timeline

- 08:32:10–08:32:22 — Four failed administrator logins
- 08:32:30 — Successful administrator login
- 08:33:05 — Administrative privileges assigned
- 08:36:41 — backup_admin account created
- 08:40:12 — backup_admin successfully logged in
- 08:45:51 — Windows Security audit log cleared

## Analyst Conclusion

The system appears to have been under attack. The evidence suggests that an attacker may have gained access to the administrator account, created another account to maintain access, and then attempted to cover their tracks by clearing the Security audit log.

## Skills Practiced

- Windows Event ID analysis
- Authentication log analysis
- Security event correlation
- Incident timeline reconstruction
- Brute-force pattern identification
- Persistence identification
- SOC investigation
