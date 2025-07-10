# Ansible & Configuration Management

---

## 🧠 What is Configuration Management?

**Configuration Management (CM)** is the process of systematically handling changes to ensure a system maintains integrity over time. In a DevOps context, it's used to automate the setup and maintenance of infrastructure and applications.

### 🔧 Provisioning a Server (Example Workflow)

1. Install system packages (e.g., `curl`, `git`, `nginx`)
2. Install programming runtimes (e.g., `python`, `nodejs`, `java`)
3. Create necessary users, groups, and directory structures
4. Download application code (from Git, S3, etc.)
5. Install dependencies (e.g., `pip install -r requirements.txt`)
6. Configure services (e.g., `systemd` unit files)
7. Start and enable the application service

---

## 🚀 Deployment Workflow

1. **Stop the existing service**
2. **Remove the old version** (optional: backup if needed)
3. **Deploy the new version**
   - Pull latest code
   - Install dependencies
4. **Start the service again**

---

## ⚠️ Problems with Manual Scripts

Traditional shell scripts for CM can lead to the following issues:

| Disadvantage | Explanation |
|--------------|-------------|
| ❌ Not idempotent | Scripts may run the same action multiple times causing conflicts (e.g., re-creating users) |
| ❌ Poor error handling | Manual scripts may not gracefully handle failures |
| ❌ Not scalable | Hard to run on 10s/100s of servers without orchestration |
| ❌ Limited portability | May work only for specific OS or distributions |
| ❌ Hard syntax | Bash scripting can be error-prone and hard to maintain |
| ❌ Weak secrets management | Passwords often stored in plain text |

---

## 🔧 Configuration Management Tools

Popular CM tools include:

- **Ansible** (agentless, YAML, SSH-based)
- **Chef** (Ruby DSL, client-server model)
- **Puppet** (declarative language, agent-based)
- **SaltStack** (Python, scalable event-driven automation)
- **Rundeck** (orchestration and job scheduling)

---

## 💡 Why Ansible?

Ansible is widely adopted because it is:

- **Agentless** – Uses SSH, no agent installation needed
- **Idempotent** – Ensures consistent end state
- **Declarative** – Describe *what* you want, not *how* to do it
- **YAML-based** – Easy to read and write
- **Modular** – Support for Roles, Modules, Vaults, Collections
- **Scalable** – Works across many servers via inventory files or dynamic inventories

---

💬 *"Can you describe how you used Ansible in your last project?"*

> "Yes, I used Ansible for provisioning EC2 instances on AWS. We used dynamic inventory via EC2 tags and playbooks to automate the entire application stack: nginx, Python, PostgreSQL. Roles were created for reusable components like monitoring and log rotation. We also used Ansible Vault for securing database credentials."

---

Feel free to contribute more or expand each section!
