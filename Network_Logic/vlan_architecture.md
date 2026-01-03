# Phase 4: Network Segmentation & Trunking

## VLAN Definition
* **VLAN 1 (Default):** Home network traffic and switch management.
* **VLAN 10 (Sandbox):** Isolated lab environment for Docker containers.

## Physical Port Configuration (802.1Q)
* **Port 2 Trunking:** * VLAN 1: Untagged (U).
    * VLAN 10: Tagged (T).
    * PVID: 1 (Ensures host Windows traffic remains on the primary network).

## Guest OS Tagging (Ubuntu)
The following commands were executed to enable the "Sandbox Lane" on the shared cable:


## Create the virtual VLAN 10 interface
```bash
sudo ip link add link enp0s3 name enp0s3.10 type vlan id 10
```
## Activate the interface
```bash
sudo ip link set dev enp0s3.10 up
```
## Assign static Sandbox IP (No DHCP available)
```bash
sudo ip addr add 10.10.10.5/24 dev enp0s3.10
```
