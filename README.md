Nessus Agent
============

Ansible role for installing and configuring Nessus Network Monitor on a CentOS or RedHat-based system.

As Tenable does not provide a standard repository to pull its agents from, it is best to host copies of them somewhere that each node can retrieve them.  You will pass a role variable for `nnm_download_page` that is only the base directory for the files.  In conjunction with `nnm_version` it will generate a valid URL to fetch from and removes the need to edit any defaults or tasks.

Role Variables
--------------

- `nnm_key`: Key used for linking with Nessus host. This is blank by default and should be set.

- `nnm_host`: Nessus host to link with (default: `cloud.tenable.com`).

- `nnm_port`: Nessus host port (default: `443`).

- `nnm_download_page`: The base URL directory for the downloaded Tenable Nessus Network Monitor.

    http://us-east.manta.joyent.com/daren.darrow@joyent.com/public/tenable/

- `nnm_linux_tmp`: /tmp


- `nnm_version`: 5.9.0

Example Playbook
----------------

    - hosts: all
      become: yes
      roles:
         - role: ansible-role-nessus-network-monitor
           nnm_key: xxxxxxxxx
