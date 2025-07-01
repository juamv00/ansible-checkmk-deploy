# 🚀 Professional Automation of Checkmk Agents with Ansible

This project was built to solve a real-world problem in production environments:  
**automatically install, configure, and secure Checkmk monitoring agents** on Linux servers using TLS and intelligent plugin handling.

With a single command, this playbook:

✅ Installs the Checkmk agent from your own server  
✅ Automatically registers the host securely using TLS  
✅ Detects which services are running (nginx, mysql, docker...)  
✅ Installs only the necessary monitoring plugins for each host  
✅ Automatically installs Python libraries required by each plugin  
✅ Configures the Checkmk server to accept the new agents using encrypted connections  

> 💡 Perfect for teams that want to **standardize monitoring**, **eliminate manual errors**, and **scale infrastructure securely**.

---

## 🔒 Inventory File Security

This project uses a `inventario.ini` file that includes plaintext passwords for simplicity and compatibility with Ansible.  
**We strongly recommend encrypting this file using Ansible Vault in production.**

### 🔐 Ansible Vault basic commands

```bash
# Encrypt the inventory file
ansible-vault encrypt inventario.ini

# Edit the encrypted inventory
ansible-vault edit inventario.ini

# Run playbook with vault password prompt
ansible-playbook -i inventario.ini deploy_cmk.yml --ask-vault-pass
````

> ⚠️ Never commit your real `inventario.ini`. Use only the provided `inventario.example.ini` with fake values for GitHub.

---

## ✨ Problems This Project Solves

**Before:**
🔸 Manual agent installations, each host configured differently
🔸 Unstandardized plugin usage
🔸 Insecure agents exposing port 6556
🔸 Missing or broken Python dependencies
🔸 Manual registration with the Checkmk server

**After:**
✅ Automated, standardized and secure agent deployment
✅ Zero manual intervention once configured
✅ Fully production-ready with secure TLS communication

---

## 🔧 Technologies Used

* **Ansible** as Infrastructure-as-Code automation tool
* **Checkmk RAW 2.4.0** as monitoring system
* **Linux (Debian/Ubuntu)** as target hosts
* **Jinja2** templates for TLS rule generation

---

## 📁 Project Structure

```
ansible-checkmk-deploy/
├── deploy_cmk.yml                 # Main playbook
├── inventario.example.ini        # Example inventory (do not expose real credentials)
├── templates/
│   └── agent_tls_rule.mk.j2      # Jinja2 template for Checkmk TLS rule
└── README.md
```

---

## 🚀 How to Use

1. Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/ansible-checkmk-deploy.git
cd ansible-checkmk-deploy
```

2. Copy and customize the inventory:

```bash
cp inventario.example.ini inventario.ini
nano inventario.ini
```

3. Run the playbook:

```bash
ansible-playbook -i inventario.ini deploy_cmk.yml
```

> 💡 If using Vault encryption, add `--ask-vault-pass` to the command.

---

## 🧠 Technical Highlights

* Auto-detects Debian 10 and applies safe APT source patch
* Uses `service_facts` to detect active services on the host
* Only installs plugins required by those services
* Installs required Python libraries (`pymongo`, `mysqldb`, etc.)
* Registers agent securely using `cmk-agent-ctl` with TLS
* Deploys a global TLS rule on the Checkmk server using Jinja2

---

## 🔐 Security

* TLS communication is enforced by default
* Legacy port 6556 is disabled
* No destructive commands
* Idempotent: you can run the playbook multiple times safely

---

## ✅ Production-Ready

✔️ Compatible with production systems
✔️ Controlled APT updates (Debian 10-specific)
✔️ Supports multiple hosts
✔️ Zero manual setup required after configuration

---

## 📜 License

MIT — Free for personal and commercial use

---

## 🙌 Contribute

Found it useful? Want to improve it?
Pull requests and issues are welcome!
