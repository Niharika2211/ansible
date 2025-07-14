# Ansible for DevOps Engineers — Interview Ready Guide

---

## 📐 Ansible Architecture & Components

**Key Components:**

* **Control Node**: Where Ansible is installed and executed.
* **Managed Nodes**: Target systems Ansible manages (via SSH).
* **Inventory**: List of target systems (static file or dynamic script).
* **Modules**: Units of work (e.g., `yum`, `copy`, `user`).
* **Playbooks**: YAML files defining automation tasks.
* **Tasks**: Individual actions (like installing packages).
* **Roles**: Reusable, structured playbook components.
* **Handlers**: Triggered only when notified (e.g., restart nginx).

🧪 *Interview Tip:* "How does Ansible communicate with remote machines?"

> Ansible uses SSH by default to connect to managed nodes and executes tasks using modules.

---

## 📘 Playbooks vs Roles vs Tasks vs Handlers

* **Playbooks**: Define *what* to automate — usually a list of plays.

  ```yaml
  - name: Install nginx
    hosts: web
    tasks:
      - name: Install package
        yum:
          name: nginx
          state: present
  ```
* **Roles**: Help reuse and organize code. Each role has its own `tasks`, `handlers`, `vars`, etc.
* **Tasks**: Individual instructions inside a play.
* **Handlers**: Run only when notified (ideal for restarting services).

🧪 *Real-time Use Case:* Deploying a Flask app:

* Role 1: `common` (create users, update system)
* Role 2: `nginx` (install and configure web server)
* Role 3: `app` (clone repo, install Python packages)

🧪 *Interview Tip:* "When would you use a handler?"

> When you need to restart a service **only if** a config file changes.

---

## 📂 Inventory Management (Static & Dynamic)

* **Static Inventory**: Defined in INI or YAML files

  ```ini
  [web]
  server1 ansible_host=192.168.0.10
  ```
* **Dynamic Inventory**: Useful for cloud infra (e.g., AWS EC2)

  * Uses plugins or external scripts to fetch live hosts
  * Example: EC2 instances with a specific tag

🧪 *Real-time Use Case:* Use dynamic inventory with `aws_ec2` plugin to deploy apps across tagged EC2 instances.

🧪 *Interview Tip:* "Why is dynamic inventory preferred in cloud environments?"

> Because infrastructure changes frequently (e.g., auto-scaling), dynamic inventory adapts in real time.

---

## 🔐 Ansible Vault (Secrets Management)

Used to encrypt sensitive data like passwords or tokens.

* Encrypt a file: `ansible-vault encrypt secrets.yml`
* Edit a file: `ansible-vault edit secrets.yml`
* Use in playbook:

  ```yaml
  vars_files:
    - secrets.yml
  ```

🧪 *Real-time Use Case:* Encrypt database credentials used in a playbook.

🧪 *Interview Tip:* "How do you manage secrets securely in Ansible?"

> Use Ansible Vault to encrypt variables and use `vars_files` in playbooks.

---

## ⚙️ Ad-hoc Commands vs Playbooks

* **Ad-hoc**: Quick one-liners for one-time tasks

  ```bash
  ansible all -m ping
  ansible web -m yum -a "name=git state=present"
  ```
* **Playbooks**: Structured, repeatable automation

🧪 *Real-time Use Case:* Use ad-hoc to install `htop` on all servers quickly.

🧪 *Interview Tip:* "When would you use an ad-hoc command over a playbook?"

> For one-time or urgent operations, like checking uptime or restarting a single service.

---

## 🛠️ Real-world Examples

1. **Install nginx**

```yaml
- name: Install and configure nginx
  hosts: web
  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present

    - name: Start nginx
      service:
        name: nginx
        state: started
        enabled: yes
```

2. **Deploy Python App**

```yaml
- name: Deploy Flask app
  hosts: app
  vars:
    app_dir: /opt/flask
  tasks:
    - name: Clone repo
      git:
        repo: https://github.com/user/repo.git
        dest: "{{ app_dir }}"

    - name: Install dependencies
      pip:
        requirements: "{{ app_dir }}/requirements.txt"
```

---

## ✅ Best Practices & Interview Q\&A

* Use **roles** for modularity
* Encrypt sensitive data with **Vault**
* Keep inventory files **organized**
* Use **tags** for selective task runs
* Always test with `--check` or `--diff`

🧪 *Interview Tip:* "How do you structure your Ansible projects?"

> I use role-based structure, separate inventory files per environment, and encrypted Vaults for secrets.

---

## 🪛 Troubleshooting Tips

* Use `-v`, `-vv`, or `-vvv` for verbose output
* Check `/var/log/ansible.log` if logging is enabled
* Confirm SSH access and Python availability on remote nodes
* Use `ansible-playbook --check` for dry runs

---

## 🗂️ Role-Based Directory Structure

```
site.yml
inventory/
  production
  staging
roles/
  nginx/
    tasks/
    handlers/
    templates/
    defaults/
    vars/
    files/
    meta/
```

Each role contains:

* `tasks/` — main logic
* `handlers/` — service restarts, etc.
* `templates/` — Jinja2 configs
* `vars/`, `defaults/` — variables
* `files/` — static files (e.g., tarballs)

🧪 *Interview Tip:* "Why use roles in Ansible?"

> Roles help make playbooks clean, reusable, and maintainable — critical for large-scale infra.

---

