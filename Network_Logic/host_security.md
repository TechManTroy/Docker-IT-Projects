## 📂 Phase 7: Management & Access Hardening

**File Path:** `/IT-Projects/01_Network_Logic/host_security.md`

### 🔑 1. Dedicated Key Generation

To avoid conflicts with existing keys used for other services, a unique, high-entropy identity was generated for this server.

* **Command**: `ssh-keygen -t ed25519 -f ~/.ssh/id_docker_server`
* **Algorithm**: ED25519 (chosen for its speed and higher security compared to RSA).
* **Pathing**: The key was explicitly saved to the Windows user profile path to ensure portability across terminal sessions.

### 🛡️ 2. Password Authentication Prevention

Once the public key was transferred to the server via `ssh-copy-id`, the "password door" was locked to prevent brute-force attacks.

* **Configuration File**: `/etc/ssh/sshd_config`
* **Key Settings Applied**:
* `PasswordAuthentication no`: Disables the ability to log in using a standard password.
* `PubkeyAuthentication yes`: Forces the system to only accept authorized SSH keys.
* `PermitRootLogin no`: Prevents direct root access, requiring a standard user to escalate privileges via `sudo`.


* **Enforcement**: Applied via `sudo systemctl restart ssh`.

### 🚀 3. Easy SSH Configuration (Automation)

To streamline management from the Windows host (`TroysHomeBase`), a client-side config file was created to map the server's nickname to its hardened parameters.

* **Config Path**: `~/.ssh/config` (on the Windows Host)
* **Implementation**:
```text
Host ubuntu-lab
    HostName 192.168.1.231
    User adminuser
    IdentityFile ~/.ssh/id_docker_server

```
Having secure SSH access from both your laptop and host Windows PC is a major milestone in establishing a professional management plane for your lab. This "Dual-Homed" connectivity allows you to maintain the server without needing direct console access.

Following your request for documentation, here is the updated networking and management log for your project files.

---

## 📂 Phase 7.1: Network Logic & Management



### 🛡️ SSH Access Matrix

The server is now configured for "Key-Only" access, which is a critical security layer that prevents password-guessing (brute-force) attacks.

| Client Device | Connection Alias | Identity File (Private Key) | Authorization Status |
| --- | --- | --- | --- |
| **Windows Host** | `ubuntu-lab` | `id_docker_server` (ED25519) | **Active** |
| **Laptop Client** | `ubuntu-lab` | `id_laptop_docker` (ED25519) | **Active** |

### 🔑 Key-Based Authentication Implementation

1. **Password Lockdown**: Modified `/etc/ssh/sshd_config` to set `PasswordAuthentication no`.
2. **Public Key Whitelisting**: Both client public keys have been appended to the server’s `~/.ssh/authorized_keys` file.
3. **Permissions Enforcement**: Applied `chmod 600 ~/.ssh/authorized_keys` to ensure the file is only readable by the `adminuser` account, a requirement for SSH to trust the keys.

### 🚀 Management Automation (Client-Side)

Both the Windows Host and Laptop now use a `~/.ssh/config` entry to automate logins:

```text
Host ubuntu-lab
    HostName 192.168.1.231
    User adminuser
    IdentityFile ~/.ssh/[Specific_Key_Filename]

```

---
