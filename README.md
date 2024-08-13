ansible-silverblue
==================

You can use this repository to configure a [Fedora Silverblue](https://silverblue.fedoraproject.org/)
workstation or laptop with Ansible. It will make it easier to apply the same settings to multiple
hosts, saving you from having to manually configure your computer over and over again.

### Edit by Elia

This playbook works best when run over ssh, but it can be run against the localhost as well with some modifications. 
Due to some of the changes I made, such as rebooting the machine and configuring a one-shot ansible service, it will
require multiple reboots to fully complete the configuration. One reboot to apply the rpmfusion repositories, and one 
reboot to apply the packages installed from those repositories. The playbook(s) will be complete after the second reboot, 
and your machine will be ready to use. Note that the systemd service requires network-online.target, so you will need to 
be connected to the network on boot for the service to  run. If you are not connected, it will run the next time you connect 
to the internet. It will continue to run on each boot if it fails. If it is broken, you can disable it with:

    systemctl disable config-me.service

### End Edit

Included Roles
--------------

The main parts of this project can be seen in the 'roles' directory. Each role included there
contains a README file that explains what the role is and how to use it. For starters, here is a
brief summary of each role:

  - layered_packages: Install or remove packages into / from the base rpm-ostree image.
  - flatpaks: Install desired [flatpak](https://flatpak.org/) applications.
  - fonts: Install custom fonts (this role is under the GPLv3 License).
  - gnome_settings: Set various GNOME desktop settings. The role makes these changes via
    [dconf](https://wiki.gnome.org/Projects/dconf).
  - os_updates: Configure the auto-update policy for the host.

### Added by Elia

  - fido2_luks: Regenerate the initramfs to allow fido2 support, and install a script to /var/usrlocal/bin to enroll your fido2 key
  - install_service: Install the bootstrap oneshot systemd service that runs the second playbook, playbook_post.yml, on the next
    boot, and then never again. If it fails for some reason, you can re-run it with the following command:

        systemctl start config-me.service

    If you are not installing rpmfusion packages, you can safely comment this line out in your playbook_base.yml. 

  - disable_service: Disable the one-shot service installed to bootstrap the rpmfusion packages. Included in the second playbook.
  - reboot: reboots the machine. Please note that if you are not installing rpmfusion packages, this is optional, but you REALLY 
    should reboot asap to apply your packages. rpm-ostree gets confused if you let it go too long before rebooting or running an
    apply-live

  - rpmfusion_packages: installs packages from the rpmfusion repository, namely ffmpeg and mesa-va-drivers-freeworld. The required
    overrides are set in the overrides in the group_vars/all file, there are a total of ten overrides necessary for installing these
    packages. I use ffmpeg for video and audio mangling, but you may not need them if you're using the Firefox/Google Chrome flatpak.
    I install it for my own personal use, but if you do not want ffmpeg, you can safely comment out many of those overrides.

### End Added

Variables
---------

I've consolidated the project's variables into the `group_vars/all` file. This makes it easy to
update the project's variables from a single location. You should customize the values in that
file to set what changes get applied in the various roles.

Setup
-----

Clone this repository with:

  - `git clone https://github.com/j1mc/ansible-silverblue.git`

Install needed dependencies with:

  - `cd ansible-silverblue`
  - `python3 -m venv venv`
  - `source venv/bin/activate`
  - `pip3 install -r requirements.txt`
  - `ansible-galaxy collection install -r requirements.yml`

... then make edits to the `group_vars/all` file to customize this project to make it do what you
want it to do.

Run the Playbooks
-----------------

This command will run all of the included playbooks:

`ansible-playbook -i hosts -l this_host -K -v playbook_base.yml`

### Edit by Elia

Please note that this playbook REALLY wants to be run over ssh. The layered_packages role will fail if you are not able
to reboot, which ansible won't let you reboot the control node in the middle of the playbook.

    TASK [layered_packages : Reboot if new deployement is ready.] ***********************************************************************
    task path: /var/home/char/Documents/git/ansible-silverblue/roles/layered_packages/tasks/main.yml:36
    fatal: [localhost]: FAILED! => changed=false 
      elapsed: 0
      msg: Running reboot with local connection would reboot the control node.
      rebooted: false

    PLAY RECAP **************************************************************************************************************************
    localhost     

### End Edit

If you want to run any of the roles individually, please review that role's `README` file for the
needed command.

License
-------

Unless otherwise indicated in the individual role, this project is under the BSD License.
All edits made by Elia are also under the BSD license.

Authors
------

  * Jim Campbell (jwcampbell@gmail.com)
  * Modified by Elia Farin (elia@sassysalamander.net)

ToDo:
-----

[ ] Add error handling for running the playbook locally (reboot in layered_packages and reboot cannot reboot control node)

