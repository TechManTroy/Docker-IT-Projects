# Phase 1: Virtualization & OS Deployment

## Overview
The foundation of this project is a virtualized server environment running on a Windows 11 host.

## Virtual Machine Specifications
* **Hypervisor:** VirtualBox.
* **Guest OS:** Ubuntu 24.04.3 LTS.
* **Hostname:** `docker-ubuntu-server`.
* **Primary Interface (enp0s3):** Bridged to the physical Ethernet controller to allow direct communication with the Netgear switch.

## Remote Management
* **Method:** SSH via MINGW64 Terminal.
* **Target:** `adminuser@192.168.1.231`.
* **Credentialing:** Verified ED25519 fingerprint `SHA256:ZE2YrE9EQoTElYUlw5oi/X/zleNYT40zp19QIkvusU8`.
