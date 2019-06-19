Nessus Network Monitor
============

Ansible role for installing and configuring Nessus Network Monitor on a CentOS or RedHat-based system.

As Tenable does not provide a standard repository to pull its agents from, it is best to host copies of them somewhere that each node can retrieve them.  You will pass a role variable for `nnm_download_page` that is only the base directory for the files.  In conjunction with `nnm_version` it will generate a valid URL to fetch from and removes the need to edit any defaults or tasks.

For the syslog variables below, the format follows this pattern: `<syslog_server_ip>:<port>:<format>:<protocol>` where format and protocol can be a 1 or 0 depending on what is desired. For example, "192.168.1.5:514:0:1"

##### Format
- Standard: 0
- CEF: 1

##### Protocol
- UDP: 0
- TCP: 1


Role Variables
--------------

- `nnm_key`: Key used for linking with Tenable.io. This is blank by default and should be set.

- `nnm_host`: Nessus host to link with (default: `cloud.tenable.com`).

- `nnm_port`: Nessus host port (default: `443`).

- `nnm_download_page`: The base URL directory for the downloaded Tenable Nessus Network Monitor.

    http://us-east.manta.joyent.com/daren.darrow@joyent.com/public/tenable/

- `nnm_linux_tmp`: /tmp


- `nnm_version`: 5.9.0

- `nnm_monitored_interfaces`: (optional) By default it will monitor on all interfaces.  List interface names if you want to restrict what is monitored.  For example, `nnm_monitored_interfaces: eth0` or `nnm_monitored_interfaces: eth0, eth1, docker0`


- `nnm_realtime_events_syslog`: Specify the IPv4 or IPv6 address and port of a Syslog server to receive real-time events from NNM.  Syslog items can be specified to Standard or CEF formats as well as UDP or TCP protocols. Example: `192.168.1.12:4567,10.10.10.10:514,[2001:DB8::23B4]:514`.  


- `nnm_vulnerability_data_syslog`: Specify the IPv4 or IPv6 address and port of a Syslog server to receive vulnerability data from NNM. Syslog items can be specified to Standard or CEF formats as well as UDP or TCP protocols. Example: `192.168.1.12:4567,10.10.10.10:514,[2001:DB8::23B4]:514`

Example Playbook
----------------

    - hosts: all
      become: yes
      roles:
         - role: ansible-role-nessus-network-monitor
           nnm_key: xxxxxxxxx
           nnm_download_page: http://us-east.manta.joyent.com/daren.darrow@joyent.com/public/tenable/
           nnm_linux_tmp: /tmp
           nnm_version: 5.9.0
           nnm_host: cloud.tenable.com
           nnm_port: 443
           nnm_activation: Cloud
           nnm_enforce_complex_passwords: 0
