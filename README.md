
---

# 🧰 Server Configuration & Automation using Ansible

This project automates the provisioning and configuration of servers using **Ansible roles**.
It installs and configures **Docker**, **Nginx**, and applies **basic security hardening** automatically.

All configurations are modularized into individual roles and can be published or reused via **Ansible Galaxy**.

---

## 🚀 Features

✅ Automated setup of server environments
✅ Installs and configures **Docker** and **Nginx**
✅ Applies **security hardening** (UFW, Fail2ban, SSH lockdown)
✅ Modular structure — roles can be reused independently
✅ Easy to extend or integrate into CI/CD pipelines

---

## 🏗️ Project Structure

```
ansible-server-automation/
├── ansible.cfg
├── inventory/
│   └── hosts.ini
├── playbooks/
│   └── site.yml
└── roles/
    ├── docker/
    │   ├── tasks/main.yml
    │   ├── meta/main.yml
    │   └── README.md
    ├── nginx/
    │   ├── tasks/main.yml
    │   ├── meta/main.yml
    │   └── README.md
    └── security/
        ├── tasks/main.yml
        ├── handlers/main.yml
        ├── meta/main.yml
        └── README.md
```

---

## ⚙️ Roles Overview

| Role         | Description                                                           |
| ------------ | --------------------------------------------------------------------- |
| **docker**   | Installs and configures Docker CE from the official repository.       |
| **nginx**    | Installs Nginx and deploys a simple homepage.                         |
| **security** | Applies firewall rules, installs Fail2ban, and locks down SSH access. |

---

## 🔧 Prerequisites

* Ubuntu / Debian-based system
* Python 3 + Ansible installed
* (Optional) SSH access to a remote server

Install Ansible:

```bash
sudo apt update
sudo apt install -y ansible
```

---

## 📋 Configuration

### **ansible.cfg**

Defines Ansible defaults (inventory path, roles path, etc.)

### **inventory/hosts.ini**

Specify target hosts:

```
[web]
localhost ansible_connection=local
```

You can also use remote servers by replacing `localhost` with IPs.

---

## ▶️ Usage

Run the main playbook:

```bash
ansible-playbook playbooks/site.yml
```

### Example Output:

```
TASK [docker : Install Docker] **************************
TASK [nginx : Install nginx] ****************************
TASK [security : Enable firewall and fail2ban] **********
PLAY RECAP **********************************************
localhost : ok=20  changed=10  unreachable=0  failed=0
```

After execution:

* Docker and Nginx will be installed
* Nginx homepage available on port **80**
* Firewall (UFW) enabled and SSH hardened

---

## 🪣 Publishing Roles to Ansible Galaxy

1. Push the repository to GitHub:

   ```bash
   git add .
   git commit -m "Initial commit - Docker, Nginx, Security roles"
   git push origin main
   ```

2. Go to [https://galaxy.ansible.com/](https://galaxy.ansible.com/)
   → Log in with GitHub
   → Click **Import** → Select this repository.

3. Once imported, roles can be installed anywhere via:

   ```bash
   ansible-galaxy role install albinraju.docker
   ansible-galaxy role install albinraju.nginx
   ansible-galaxy role install albinraju.security
   ```

---

## 🧱 Example Playbook for Reuse

```yaml
---
- name: Configure server with Docker, Nginx, and Security Hardening
  hosts: web
  become: yes
  roles:
    - albinraju.docker
    - albinraju.nginx
    - albinraju.security
```

---

## 🧑‍💻 Author

**Albin Raju**
MCA Student | DevOps & Cloud Enthusiast
[GitHub](https://github.com/albinraju) • [LinkedIn](https://linkedin.com/in/albinraju)

---

