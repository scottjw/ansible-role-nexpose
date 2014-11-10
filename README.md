Nexpose
=========

Setup Nexpose as scanner or console.
Also included is a module that will add CA certs to the Java keystore, allowing you to add your own CA cert as a trusted source. The keystore will be replaced by Nexpose updates, so you will need to re-add them often. This role makes that easy.

Requirements
------------

- Open HTTPS port in firewall on host (or disable firewall)

Role Variables
--------------

**nexpose_download_url**    URL of Nexpose install binary.

**nexpose_first_name**      Registered user first name.

**nexpose_last_name**       Registered user last name.

**nexpose_company_name**    Registered company name.

**nexpose_logon_name**      Username for initial logon to console.

**nexpose_console**         Whether this is a console or just a scan enginer (
Default: True)

**nexpose_init_service**    Whether to start the Nexpose service after 
installation (Default: False)

**nexpose_suppress_unattended_reboot**  Not really sure. (Default: true)

**nexpose_ca_certs**        List of Certificates to add to the deafult Java 
keystore. This is to prevent erronous untrusted CA findings.


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

      roles:
        - nexpose
```

License
-------

MIT
