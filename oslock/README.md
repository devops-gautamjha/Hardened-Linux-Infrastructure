oslock
=======

An Ansible role to perform system hardening on Debian/Ubuntu servers, including user creation, SSH hardening, Fail2ban and auditd setup, kernel network hardening, and firewall configuration.

Requirements
------------

- Control node: Ansible 2.9+
- Managed nodes: Debian or Ubuntu-based systems
- Python installed on managed nodes (provided by default on most distros)

Role Variables
--------------

The following variables are defined in `defaults/main.yml` and can be overridden:

```yaml
# defaults/main.yml
NEW_USER: "oslock"         # Name of the user to create
USER_PASSWORD: "P@ssw0rd"  # Initial password (will be hashed)
NEW_SSH_PORT: 6500          # SSH daemon port for key-based login
```

**Mandatory variable** (must be provided by the caller):

```yaml
SSH_PUBLIC_KEY: "<your-public-ssh-key>"  # User's SSH public key to install
```

Dependencies
------------

This role has no external Ansible role dependencies.

Example Playbook
----------------

```yaml
- hosts: all
  become: true
  roles:
    - role: oslock
      SSH_PUBLIC_KEY: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}"
      # Optional overrides:
      NEW_USER: "deploy"
      USER_PASSWORD: "Str0ngP@ss!"
      NEW_SSH_PORT: 6500
```

License
-------

MIT

Author Information
------------------

Developed by Gautam Jha

