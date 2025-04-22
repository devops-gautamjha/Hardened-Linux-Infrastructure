Hardened Linux Infrastructure
=================

Repository containing the **oslock** Ansible role alongside sample inventory, configuration, and playbook files to harden Debian/Ubuntu servers.

Repo Structure
--------------

```text
.
├── ansible.cfg           # Ansible configuration
├── host.ini              # Inventory file with target host definitions
├── my-playbook.yaml      # Root playbook that invokes the oslock role
├── variables.yaml        # Variable overrides for the playbook
└── oslock/               # oslock role directory (defaults, tasks, templates, etc.)
```

### ansible.cfg

```ini
[defaults]
host_key_checking = False
remote_user = root
ansible_python_interpreter = "/usr/bin/python3"
become = true
become_method = sudo
deprecation_warnings = False
```

### host.ini

Define your target node here:

```ini
<Node-Name> ansible_host=<YOUR_NODE_IP> ansible_user=<LOGIN_USER>
```

Replace `<Node-Name>`, `<YOUR_NODE_IP>`, and `<LOGIN_USER>` with your values.

### variables.yaml

Override default role variables and supply the mandatory SSH key:

```yaml
NEW_USER: "gautam"
USER_PASSWORD: "mypassword"
NEW_SSH_PORT: 6500
SSH_PUBLIC_KEY: "<YOUR_PUBLIC_SSH_KEY>"
```

Be sure to replace `<YOUR_PUBLIC_SSH_KEY>` with the contents of your `~/.ssh/id_rsa.pub` (or equivalent).

### my-playbook.yaml

This playbook calls the **oslock** role using your inventory and variable overrides:

```yaml
- hosts: all
  become: true
  any_errors_fatal: true
  roles:
    - oslock
```

Usage
-----

1. **Clone** the repository:

   ```bash
   git clone https://github.com/devops-gautamjha/Hardened-Linux-Infrastructure.git
   cd Hardened-Linux-Infrastructure
   ```

2. **Edit** `host.ini` with your target host details.

3. **Edit** `variables.yaml` to set `NEW_USER`, `USER_PASSWORD`, `NEW_SSH_PORT`, and **mandatory** `SSH_PUBLIC_KEY`.

4. **Run** the playbook:

   ```bash
   ansible-playbook -i host.ini my-playbook.yaml -e @variables.yaml
   ```

5. **Verify** that the hardening tasks completed successfully by checking the playbook output and SSHing to the new port with your key.

Role Variables
--------------

The **oslock** role defines defaults in `oslock/defaults/main.yml`:

```yaml
NEW_USER: "oslock"
USER_PASSWORD: "P@ssw0rd"
NEW_SSH_PORT: 6500
```

You can override these in `variables.yaml` or by passing `-e NEW_USER=...` on the command line.

License
-------

MIT

Author Information
------------------

Developed by Gautam Jha

