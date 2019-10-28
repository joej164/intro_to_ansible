# Intro to Ansible for Python Developers

This repo contains code samples from my "Intro to Ansible for Python Developers" talk

* `simple_play.yml` 
  * This play doesn't do much.  Just showing how a playbook looks and can run on the Ansible Control node
  * Run with the command `ansible-playbook simple_play.yml`
  * Runs on localhost, no additional config required

* `asserting_play.yml`
  * This play shows how to assert things and make decisions or do tests
  * Run with the command `ansible-playbook asserting_play.yml`
  * Runs on localhost, no additional config required

* `install_python36_on_centos_minimal.yml`
  * This play installs python3.6 on a Centos 7 Minimal computer
  * Run with the command `ansible-playbook -i hosts -l install_python36 install_python36_on_centos_minimal.yml`
  * Requires a Centos 7 Minimal VM at the IP of `192.168.56.10` with ssh enabled and credentials as defined in the hosts file

* `compile_python38_on_centos_minimal.yml`
  * This play installs python3.8 a Centos 7 Minimal install, sets up a symlink, and cleans up
  * Run with the command `ansible-playbook -i hosts -l install_python36 compile_python38_on_centos_minimal.yml`
  * Requires a Centos 7 Minimal VM at the IP of `192.168.56.11` with ssh enabled and credentials as defined in the hosts file


* Steps to set up the Centos 7 Minimal VM
  * Virtual Box Setup
    * Download Centos7 Minimal ISO from http://isoredirect.centos.org/centos/7/isos/x86_64/
      * Specific File: http://mirror.tocici.com/centos/7.7.1908/isos/x86_64/CentOS-7-x86_64-Minimal-1908.iso
    * Install VM from CentOS 7.7 minimal ISO
      * Create a new VM
      * Attach the ISO to the new VM
    * Configure Networking
      * Create a host only network under the file menu
      * First network adapter is NAT (this allows for connecting to the internet)
      * Second network adapter is host-only (this allows to ssh into the VM)
    * Power on the VM
  * CentOS Install Configuration
    * Make sure networking is enabled from the Centos 7 installer
      * In the menus make sure you enable both network adapters
      * They are disabled by default
    * If you don't want to have to update the host file with the correct IP, statically assign the second adapter an IP in the same subnet 
    * Create `ansible` user as an admin, so it had sudoers access, note the password and add it to the host file
    * Do the install and reboot the box
  * Centos OS Configuration
    * Disable DNS lookups when using SSH to connect to the server
        * update /etc/ssh/sshd_config
          ```
          set UseDNS = no
          set GSSAPIAuthentiction = no
          ```
    * By default, Centos 7 Minimal does not have SSH enabled, enable it
        * Run the command `systemctl enable sshd`
  * Ansible Host Configuration
    * Install `sshpass` on Ansible host so Ansible can use ssh passwords to log in
      * In my case it was a Mac, so I had to `brew install sshpass`
      * For linux, look up your specific distro to find out 
    * Add the ssh fingerprint to local hosts file by doing `ssh <host ip>` and typing `yes` when prompted

* Easiest way to install Ansible (for Python Developers)
    * Doesn't work on windows, may work in WSL or WSL2.  Linux or Mac only.
    * Can also install from OS packages (apt-get or yum)
    * Install python3 ( tested with Python3.7.4 on Mac )
    * Install pip3
    * Install pipenv
    * Create a directory that you'll be working in
    * Run `pipenv install ansible`
    * Run `pipenv shell` to start your Virtual Environment
    * Run `ansible --version` to see what version of Ansible is installed

