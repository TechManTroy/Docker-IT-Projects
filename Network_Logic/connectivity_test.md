### 📄 02_Validation/connectivity_tests.md

# Phase 5: Isolation Validation

## Terminal Verification
**Test 1: Sandbox to Default Gateway**
```
ping -I enp0s3.10 10.10.10.1
```
**Result:** 100% Packet Loss (Expected: Isolation successful).
**Test 2: Sandbox to Home PC**
```
ping -I enp0s3.10 192.168.1.67
```
**Result:** 100% Packet Loss (Expected: Segmentation successful).

## Hardware Verification
* **Source:** Netgear Monitoring > Port Statistics.
* **Observation:** Port 2 showed `41180` Bytes Sent during tagged ping attempts, confirming the switch received and correctly dropped the unauthorized cross-VLAN traffic.
