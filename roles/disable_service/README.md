layered_packages
================

This role disables the config-me.service oneshot service so it doesn't run again on boot


Requirements
------------

Modules used:

  * [ansible.builtin.systemd_service](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/systemd_service_module.html)

Role Variables
--------------

None

Dependencies
------------

None

Example Adhoc Run
-----------------

`ansible-playbook -i hosts -l this_host -K roles/disable_service/playbook.yml`

Example Playbook
----------------

    - hosts: all
      roles:
        - { role: disable_service }

License
-------

BSD

Author Information
------------------

  * Elia Farin (elia@sassysalamander.net)
