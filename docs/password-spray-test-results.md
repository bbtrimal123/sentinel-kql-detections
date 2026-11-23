# Password Spray Detection — Test Results

**Test date:** 23 November 2026  
**Environment:** Azure Data Explorer, public help/SampleLogs connection  
**Data:** Synthetic Microsoft Entra ID-style sign-in events  
**MITRE ATT&CK:** T1110.003 — Password Spraying

## Test Objective

Validate that the KQL password-spray detection identifies multiple failed authentication attempts against distinct user accounts from a single IP address within a 15-minute time window.

## Test Configuration

| Parameter | Value |
|---|---|
| Simulated failed sign-ins | 25 |
| Distinct targeted accounts | 12 |
| Source IP address | 203.0.113.10 |
| Minimum failure threshold | 20 |
| Minimum distinct users | 10 |
| Detection window | 15 minutes |

## Observed Results

The KQL query executed successfully and returned one matching detection row.

- FailedAttempts: 25
- TargetedUsers: 12
- IPAddress: 203.0.113.10

**Result: PASS — Positive detection test**

## Limitations

Testing used synthetic data created inside the KQL query, not live Microsoft Sentinel sign-in logs.

This test confirms the positive detection scenario only. Additional testing is required for benign activity, threshold boundaries, time-window boundaries, and false positives.

## Next Steps

- Test activity below the detection thresholds.
- Test events crossing 15-minute time-bin boundaries.
- Validate the query against a dedicated Microsoft Sentinel lab when available.
- Document investigation and response procedures.
