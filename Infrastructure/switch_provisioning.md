# Phase 3: Hardware Discovery & Provisioning

## Hardware Identity
* **Device:** Netgear GS108Ev3 8-Port Smart Managed Plus Switch.
* **Firmware:** V2.06.17EN.

## Recovery & Discovery
1. **Factory Reset:** Performed a manual reset to clear legacy configurations.
2. **IP Discovery:** Used Advanced IP Scanner to locate the device at `192.168.1.30` on the local subnet.
3. **Static Hardening:** Disabled DHCP and assigned a permanent management IP of `192.168.1.250`.

## Connectivity Verification
Successfully confirmed the path from the Ubuntu VM to the switch management interface.
* **Command:** `ping 192.168.1.250`
* **Result:** 0% Packet Loss; Avg RTT 2.8ms.
