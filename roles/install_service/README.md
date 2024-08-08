install_service
================

This role installs and enables the config-me oneshot service for running secondary installs post reboot

The role will work better after rpm-ostree's `--apply-live` feature is available via
[this pull request](https://github.com/ansible-collections/community.general/pull/3908).

Requirements
------------

Modules used:

  * [ansible.builtin.copy](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html)
  * [ansible.builtin.template](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/template_module.html)
  * [ansible.builtin.systemd_service](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/systemd_service_module.html)

Role Variables
--------------

These varables are set in the project's `group_vars/all` file. Make your edits there!

  * base_path: The location of the ansible playbook's git repository, including the repository folder itself

Dependencies
------------

None

Example Adhoc Run
-----------------

`ansible-playbook -i hosts -l this_host -K roles/install_service/playbook.yml`

Example Playbook
----------------

    - hosts: all
      roles:
        - { role: install_service }

License
-------

BSD

Author Information
------------------

  * Elia Farin (elia@sassysalamander.net)
