fido2_luks
================

This role enables and regenerates the initramfs using rpm-ostree on a Fedora Atomic host to allow unlocking your luks volume
with a fido2 key.

Requirements
------------

Modules used:

  * [ansible.builtin.command](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/command_module.html)
  * [ansible.builtin.template](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/template_module.html)

Role Variables
--------------

These varables are set in the project's `group_vars/all` file. Make your edits there!

  * encrypted_volume_path - The device path of your encrypted volume

Dependencies
------------

None

Example Adhoc Run
-----------------

`ansible-playbook -i hosts -l this_host -K roles/fido2_luks/playbook.yml`

Example Playbook
----------------

    - hosts: all
      roles:
        - { role: fido2_luks }

License
-------

BSD

Author Information
------------------

  * Elia Farin (elia@sassysalamander.net)
