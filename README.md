# Ansible ELK Stack (Docker)

Deploy a complete **ELK Stack (Elasticsearch, Logstash, Kibana)** using **Ansible** and **Docker Compose**, following Ansible best practices and a clean role-based structure.

This repository is designed to be:

* ✅ Educational
* ✅ Public & review-friendly
* ✅ Close to real-world production patterns (with clear security notes)

---

## ✨ Features

* Ansible role-based structure
* Docker Compose–based ELK deployment
* Templated configurations (Jinja2)
* Secure secret management using **Ansible Vault**
* Idempotent playbooks
* Easy customization via variables

---

## 🧩 Technology Stack

| Component | Version                      |
| --------- | ---------------------------- |
| Ansible   | **2.19.5**                   |
| Ubuntu    | **24.04**                    |
| ELK Stack | **2.9.9**                    |
| Docker    | Latest (Engine + Compose v2) |

> ⚠️ Versions are tested and known to work together. Using other versions may require adjustments.

---

## 📂 Project Structure

```
.
├── ansible.cfg
├── playbooks/
│   └── site.yml
├── roles/
│   └── elk/
│       ├── defaults/
│       ├── handlers/
│       ├── meta/
│       ├── tasks/
│       ├── templates/
│       └── vars/
│           └── vault.yml   # encrypted
└── README.md
```

---

## ⚙️ Prerequisites

Make sure the target system has:

* Ubuntu 24.04
* Docker installed and running
* Docker Compose v2
* Ansible 2.19.5 installed on the control node
* SSH access to the target host

---

## 🚀 Quick Start

### 1️⃣ Clone the repository

```bash
git clone https://github.com/hamid-rch/ansible-elk-docker.git
cd ansible-elk-docker
```

---

### 2️⃣ Inventory setup

Edit your inventory file to point to the target host:

```ini
[elk]
elk-server ansible_host=YOUR_SERVER_IP ansible_user=YOUR_USER
```

---

### 3️⃣ Run the playbook

This project uses **Ansible Vault** for sensitive variables.

```bash
ansible-playbook -i inventory/hosts playbooks/site.yml --ask-vault-password
```

---

## 🔐 Secrets Management (Important)

### How secrets are handled

* Sensitive variables (e.g. `elastic_password`) are **NOT** stored in plaintext
* They are stored in an encrypted file:

```
roles/elk/vars/vault.yml
```

* This file **is committed to Git**, but only in encrypted form

---

### ⚠️ Demo Vault Password (Read Carefully)

> 🚨 **SECURITY WARNING**

For demonstration and learning purposes **only**, the current Vault password is:

```
123
```

⚠️ **This is intentionally insecure and must NEVER be done in real projects.**

In real-world usage:

* Vault passwords must never be stored in Git
* Vault passwords must never appear in README files
* Use environment variables, CI secrets, or secure password files instead

This repository explicitly documents this **bad practice** so reviewers can understand the Vault workflow without setup friction.

---

### Viewing Vault contents (local only)

If you know the Vault password:

```bash
ansible-vault view roles/elk/vars/vault.yml
```

If the Vault password is lost:

* The file **cannot be recovered**
* A new Vault file must be created

---

## 🔄 Configuration Notes

### Startup timing & retries

Depending on the system resources (CPU, RAM, disk speed):

* Elasticsearch and Kibana containers may take time to become healthy
* Health checks may fail on slower systems

If you encounter startup failures, you can safely increase retry values in the role tasks, for example:

```yaml
retries: 30
delay: 10
```

This is **not an error**, but a normal behavior on resource-constrained machines.

---

## 🧪 Verification

After a successful run:

* Elasticsearch should be available on port `9200`
* Kibana should be available on port `5601`

Example:

```bash
curl http://localhost:9200
```

---

## 🛠️ Customization

You can customize the deployment by overriding variables:

* Via `defaults/main.yml` (non-sensitive values only)
* Via Vault (`vault.yml`) for secrets
* Via extra-vars if needed

---

## 🧠 Design Decisions

* Secrets are decrypted **only at runtime**
* No plaintext credentials exist in the repository
* Role structure follows Ansible best practices
* Docker Compose files are templated for flexibility

---

## 📌 Disclaimer

This project is:

* A **learning & demonstration repository**
* Not intended to be production-ready without further hardening

Security shortcuts are clearly documented and intentional.

---

## 📄 License

MIT License

---

## 🙌 Author

Created and maintained by **Hamid**

If you find this project useful, feel free to ⭐ the repository.
