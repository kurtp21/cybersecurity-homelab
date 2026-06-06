# IR-001 - Account Lockout Investigation

## Summary

- A user account lockout was detected after multiple failed authentication attempts against the account HOMELAB\cjames. Investigation confirmed the account lockout was triggered by the configured Active Directory lockout policy and was generated as part of a controlled homelab security monitoring exercise

## Incident Details

| Field            | Value              |
|------------------|--------------------|
| Incident ID      | IR-001             |
| Detection Date   | June 6, 2026       |
| Affected User    | HOMELAB\cjames     |
| Affected Systems | WIN10-CLIENT, DC01 |
| Severity         | Low                |
| Status           | Closed             |
| Detection Source | Wazuh SIEM         |
| Analyst          | Kurt               |

## Detection

- The event was investigated through Wazuh Threat Hunting

### Failed Authentication Event

| Field          | Value                                        |
|----------------|----------------------------------------------|
| Event ID       | 4625                                         |
| Target Account | HOMELAB\cjames                               |
| Description    | Logon Failure - Unknown user or bad password |
| Event Type     | Failed Authentication                        |
| Source System  | WIN10-CLIENT                                 |
| Timestamp      | Jun 6, 2026 @ 02:20:37.672                   |

### Account Lockout Event

| Field          | Value                                           |
|----------------|-------------------------------------------------|
| Event ID       | 4740                                            |
| Target Account | HOMELAB\cjames                                  |
| Description    | User account locked out (multiple login errors) |
| Event Type     | Failed Authentication                           |
| Source System  | DC01                                            |
| Timestamp      | Jun 6, 2026 @ 02:20:42.594                      |

## Investigation

- During the investigation it was determined that there were multiple login attempts generated against the account *cjames* from the *WIN10-CLIENT* endpoint
- Review of the Domain Controller Security logs confirmed Event ID 4740, indicating that Active Directory enforced the configured account lockout policy after the failed authentication threshold was exceeded.
- There was no malicious intent as this was intentionally generated as part of a homelab authentication monitoring exercise

## Timeline

| Time     | Event                                   |
|----------|-----------------------------------------|
| 02:20:30 | Failed login attempt agains user cjames |
| 02:20:37 | Failed login attempt agains user cjames |
| 02:20:42 | User account cjames locked out          |

## Action Taken

- Went into Active Directory and found user account cjames. Reset password to default and unlocked account
- Confirmed that the account was unlocked and that a new secure password was set

## Root Cause

- Intentional failed login attempts performed during security monitoring and Active Directory testing

## Lessons Learned

- Failed authentication events can originate from endpoints while lockout events are recorded on the Domain Controller
- Active Directory is responsible for enforcing account lockout policies
- Effective security monitoring requires collecting logs from both endpoints and infrastructure systems
- Wazuh can be used to correlate authentication events across multiple systems

## Recomendations

- Continue monitoring authentication events through Wazuh
- Create dashboards for failed logins and account lockouts
- Develop custom detection rules for excessive failed authentication attempts
- Expand monitoring to include privileged account activity

## Conclusion

- This exercise successfully demonstrated end-to-end authentication monitoring within the homelab environment. Failed login attempts originating from WIN10-CLIENT were correlated with Active Directory account lockout events generated on DC01, validating log collection and event correlation through Wazuh
