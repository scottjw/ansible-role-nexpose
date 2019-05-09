Nexpose
=========
[![Galaxy](https://img.shields.io/badge/galaxy-scottjw.ansible_role_nexpose-blue.svg?style=flat)](https://galaxy.ansible.com/scottjw/ansible_role_nexpose)

Based on / forked from [Sam Doran's project](https://github.com/samdoran/ansible-role-nexpose)

Setup a [Nexpose](http://www.rapid7.com/products/nexpose/) ~~Console~~ or Engine.

Console deployment is not complete.

This role is in no way assosiated with [Rapid7](http://www.rapid7.com) and they do not endorse this role. 

Requirements
------------

Open HTTPS port in firewall on host.
Target system must meet the [minimum hardware requirements](http://www.rapid7.com/products/nexpose/system-requirements.jsp).

Role Variables
--------------
| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `nexpose_download_url` | `http://download2.rapid7.com/download/NeXpose-v4/NeXposeSetup-Linux64.bin"` | URL of Nexpose install binary |
| `nexpose_first_name` | `Mr."` | Registered user first name |
| `nexpose_last_name` | `Smith"` | Registered user last name |
| `nexpose_company_name` | `MiB"` | Registered company name |
| `nexpose_logon_name` | `msmith"` | Username for initial logon to console |
| `nexpose_engine` | `True` | Whether this is a console or just a scan engine |
| `nexpose_init_service` | `True` | Whether to start the Nexpose service after installation |
| `nexpose_suppress_unattended_reboot` | `True` | Not really sure what this does |
| `nexpose_ca_certs` | `[see defaults/main.yml` | List of Certificates to add to the deafult Java keystore. These must be place in the `files` directory. |
| `nexpose_install_dir` | `/opt/rapid7/nexpose` | Directory where Nexpose will be installed. You'll need 80GB for a Console and 10GB for an Engine. |
| `nexpose_console_port` | `3780` | HTTPS port the Console listens on. |
| `nexpose_engine_port` | `40814` | Port the Engine uses to communicate with the Console. |

Dependencies
------------

None.

Example Playbook
----------------
Here is a playbook to setup a Nexpose Console using the standard HTTPS port. You can use `vars_prompt` to enter the initial password or put it in an [Ansible Vault](http://docs.ansible.com/ansible/playbooks_vault.html).

```yaml
- name: Configure Nexpose Console
  hosts: nexpose-consoles
  become: yes

  vars:
    nexpose_engine: False
    nexpose_console_port: 443

  vars_prompt:
    - name: nexpose_logon_password
      prompt: "Enter logon password"
      private: yes
      confirm: yes

  roles:
    - ansible-role-nexpose
```

Here is playbook to setup a Nexpose Engine:

```yaml
  - name: Configure Nexpose Engine
    hosts: nexpose-engines
    become: yes

    roles:
      - ansible-role-nexpose
```

License
-------

MIT
