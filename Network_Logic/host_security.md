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
