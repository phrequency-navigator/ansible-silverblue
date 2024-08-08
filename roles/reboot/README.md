layered_packages
================

This role reboots the system with a variable timeout


Requirements
------------

Modules used:

  * [ansible.builtin.reboot](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/reboot_module.html)

Role Variables
--------------

These varables are set in the project's `group_vars/all` file. Make your edits there!

  * reboot_timeout - The reboot timeout in seconds


Dependencies
------------

None

Example Adhoc Run
-----------------

`ansible-playbook -i hosts -l this_host -K roles/reboot/playbook.yml`

Example Playbook
----------------

    - hosts: all
      roles:
        - { role: reboot }

License
-------

BSD

Author Information
------------------

  * Elia Farin (elia@sassysalamander.net)
