# Windows Security Log Investigation

## Project Objective

The objective of this project was to investigate simulated Windows Security Event logs and identify suspicious authentication, account, and administrative activity.

## Scenario

A series of Windows security events showed repeated failed administrator logins followed by a successful login, privileged activity, creation of a new user account, and clearing of the Windows Security audit log.

The goal was to correlate these events and determine whether they represented suspicious activity.

## Windows Event IDs Investigated

- Event ID 4624 — Successful logon
- Event ID 4625 — Failed logon
- Event ID 4672 — Special privileges assigned to a new logon
- Event ID 4720 — User account created
- Event ID 1102 — Security audit log cleared

## Tools and Commands Used

- Linux terminal
- `cat`
- `grep`
- `sort`
- `uniq`

Example command used to count Windows Event IDs:

`grep -o 'EventID=[0-9]*' windows-events.log | sort | uniq -c`

## Key Findings

The investigation identified four failed administrator login attempts from the same source IP within a short period.

A successful administrator login followed from the same IP.

The administrator session received elevated privileges and created a new account named `backup_admin`.

The new account later logged in from the same source IP.

Finally, the Windows Security audit log was cleared.

The combined evidence suggests a possible administrator account compromise, persistence through creation of another account, and an attempt to remove evidence.

## Skills Practiced

- Windows security fundamentals
- Windows Event ID analysis
- Log analysis
- Authentication monitoring
- Security event correlation
- Incident timeline reconstruction
- Suspicious account activity identification
- SOC investigation
- Linux command-line analysis

## Project Files

- `windows-events.log` — Simulated Windows Security Event evidence
- `findings.md` — Investigation findings, timeline, and analyst conclusion

## Disclaimer

This project uses simulated security logs in a controlled learning environment. No real system was attacked or accessed.

