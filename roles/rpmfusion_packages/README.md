layered_packages
================

This role installs packages from rpmfusion after the repositories have been installed. 

The role will work better after rpm-ostree's `--apply-live` feature is available via
[this pull request](https://github.com/ansible-collections/community.general/pull/3908).

Requirements
------------

Modules used:

  * [community.general.rpm_ostree_pkg](https://docs.ansible.com/ansible/latest/collections/community/general/rpm_ostree_pkg_module.html)
  * [ansible.builtin.command](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/command_module.html)

Role Variables
--------------

These varables are set in the project's `group_vars/all` file. Make your edits there!

  * rpmfusion_package_install: Install these packages as layered packages.

Dependencies
------------

None

Example Adhoc Run
-----------------

`ansible-playbook -i hosts -l this_host -K roles/layered_packages/playbook.yml`

Example Playbook
----------------

    - hosts: all
      roles:
        - { role: rpmfusion_install }

License
-------

BSD

Author Information
------------------

  * Jim Campbell (jwcampbell@gmail.com)
