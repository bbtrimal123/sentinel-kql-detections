# Detection Testing Guide

## Overview

This document describes how I plan to test and validate the KQL detection queries in this repository using authorised Microsoft Sentinel lab data.

## 1. Password Spray Detection

**MITRE ATT&CK:** T1110.003 – Password Spraying

**Objective:** Detect multiple failed sign-in attempts against different user accounts from a single source IP address.

### Expected behaviour

The query should identify:

- At least 20 failed sign-in attempts.
- At least 10 distinct targeted user accounts.
- Activity occurring within a 15-minute window.

### Testing approach

1. Prepare synthetic Microsoft Entra ID sign-in records.
2. Include failed sign-ins across multiple test accounts.
3. Run the detection query against the appropriate lab table.
4. Check whether the expected IP address is identified.
5. Adjust the detection thresholds if necessary.

### False positives

- Legitimate authentication failures caused by shared network addresses.
- Misconfigured applications or automated sign-in processes.
- Multiple users experiencing authentication problems behind the same NAT address.

## 2. Suspicious Successful Sign-in Detection

**MITRE ATT&CK:** T1078 – Valid Accounts

**Objective:** Identify successful sign-ins following repeated authentication failures for the same user and source IP address.

### Expected behaviour

The query should identify:

- Five or more failed sign-in attempts.
- A subsequent successful sign-in.
- Activity involving the same user account and IP address.
- Failures occurring within 30 minutes before the successful sign-in.

### Testing approach

1. Prepare synthetic failed and successful sign-in events.
2. Run the KQL query against lab data.
3. Verify that failures occurring after a successful sign-in are excluded.
4. Check the returned user, IP address and timestamps.
5. Review possible false positives.

## 3. Validation Checklist

- [ ] Query executes without syntax errors.
- [ ] Required tables and columns are available.
- [ ] Expected test events are detected.
- [ ] Benign test events are excluded where appropriate.
- [ ] False positives are documented.
- [ ] Results and limitations are recorded.

## 4. Current Status

**Status:** Testing planned.

These queries have been created as learning exercises. They have not yet been validated against a Microsoft Sentinel lab environment or production dataset.

## 5. Security and Privacy

All testing must use authorised lab environments and synthetic or appropriately sanitised data. No employer logs, credentials, customer details, or confidential information will be uploaded to this repository.
