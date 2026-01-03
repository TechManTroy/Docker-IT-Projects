# Persistent VLAN Configuration (Netplan)

To ensure the Sandbox interface (`enp0s3.10`) survives a reboot, the manual `ip link` commands must be converted into a Netplan configuration file.

## Step 1: Locate the Config File
Navigate to the netplan directory:
`ls /etc/netplan/`
*Commonly named `50-cloud-init.yaml` or `01-netcfg.yaml`.*

## Step 2: Edit the Configuration
Use `sudo nano` to edit your file. Update it to match the structure below, which preserves your primary DHCP connection while adding the VLAN 10 tagging logic.

```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: true  # Home Network (VLAN 1 Untagged)
  vlans:
    enp0s3.10:
      id: 10
      link: enp0s3
      addresses: [10.10.10.5/24] # Sandbox Network
