Nexpose
=========

Setup Nexpose as scanner or console.

Also included is a module that will add CA certs to the Java keystore, allowing you to add your own CA cert as a trusted source.

Requirements
------------

- Open HTTPS port in firewall on host (or disable firewall)

Role Variables
--------------

URL of Nexpose install binary:

    nexpose_download_url: "http://download2.rapid7.com/download/NeXpose-v4/NeXposeSetup-Linux64.bin"

Registered user first name:

    nexpose_first_name: "Mr."

Registered user last name:

    nexpose_last_name: "Smith"

Registered company name:

    nexpose_company_name: "MiB"

Username for initial logon to console:

    nexpose_logon_name: "msmith"

Whether this is a console or just a scan engine:

    nexpose_engine: True

Whether to start the Nexpose service after installation:

    nexpose_init_service: True

Not really sure what this does:

    nexpose_suppress_unattended_reboot: True

List of Certificates to add to the deafult Java keystore. Thes must be place in the `files` directory.

    nexpose_ca_certs:
      - name: comodocalimited.crt
        alias: ComodoCALimited
        state: present


Dependencies
------------

None.

Example Playbook
----------------
You can use `var_prompt` to enter the initial password.

```yaml
    - name: Configure Nexpose console or scanner
      hosts: nexpose
      sudo: yes

      vars_prompt:
        - name: nexpose_logon_password
          prompt: "Enter logon password"
          private: yes
          confirm: yes

      roles:
        - nexpose
```

License
-------

MIT
