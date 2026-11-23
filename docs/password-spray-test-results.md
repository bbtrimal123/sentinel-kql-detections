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
## Negative Detection Test

**Test date:** 23 November 2026

**Objective:** Confirm that authentication activity below the configured detection thresholds does not generate an alert.

### Test Configuration

- Failed sign-ins: 5
- Distinct targeted users: 5
- Source IP address: 203.0.113.10
- Minimum failure threshold: 20
- Minimum distinct users: 10
- Detection window: 15 minutes

### Observed Results

The KQL query executed successfully and returned zero detection rows.

**Result: PASS — Negative detection test**

## Overall Test Results

| Test Scenario | Expected Result | Actual Result | Status |
|---|---|---|---|
| Positive: 25 failures, 12 users | 1 detection | 1 detection | PASS |
| Negative: 5 failures, 5 users | 0 detections | 0 detections | PASS |

## Limitations

Testing was performed using synthetic data in Azure Data Explorer.

The detection has not been validated against live Microsoft Sentinel logs or deployed as a production analytics rule.

Further testing is recommended for time-window boundaries and false positives.
