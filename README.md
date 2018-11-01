Linux Distribution Independent hardening  based on CIS Benchmark
================

Configure any Linux machine to be CIS Distribution Independent compliant. Level 1 and 2 findings will be corrected by default.

This role **will make changes to the system** that could break things. This is not an auditing tool but rather a remediation tool to be used after an audit has been conducted.

## IMPORTANT INSTALL STEP


Based on [Distribution Independent Linux (CIS Distribution Independent Linux Benchmark version 1.1.0)](https://www.cisecurity.org/benchmark/distribution_independent_linux/).

This repo originated from work done by [Florian Utz](https://github.com/florianutz/Ubuntu1604-CIS), which repo originated from work done by [MindPointGroup](https://github.com/MindPointGroup/RHEL7-CIS)

Requirements
------------

You should carefully read through the tasks to make sure these changes will not break your systems before running this playbook.

Role Variables
--------------
There are many role variables defined in defaults/main.yml. This list shows the most important.

**cis_dil_notauto**: Run CIS checks that we typically do NOT want to automate due to the high probability of breaking the system (Default: false)

**cis_dil_section1**: CIS - General Settings (Section 1) (Default: true)

**cis_dil_section2**: CIS - Services settings (Section 2) (Default: true)

**cis_dil_section3**: CIS - Network settings (Section 3) (Default: true)

**cis_dil_section4**: CIS - Logging and Auditing settings (Section 4) (Default: true)

**cis_dil_section5**: CIS - Access, Authentication and Authorization settings (Section 5) (Default: true)

**cis_dil_section6**: CIS - System Maintenance settings (Section 6) (Default: true)

##### Disable all selinux and apparmor functions
`cis_dil_selinux_disable: false`
`cis_dil_apparmor_disable: false`

##### Service variables:
###### These control whether a server should or should not be allowed to continue to run these services

```
cis_dil_avahi_server: false
cis_dil_cups_server: false
cis_dil_dhcp_server: false
cis_dil_ldap_server: false
cis_dil_telnet_server: false
cis_dil_nfs_server: false
cis_dil_rpc_server: false
cis_dil_ntalk_server: false
cis_dil_rsyncd_server: false
cis_dil_tftp_server: false
cis_dil_rsh_server: false
cis_dil_nis_server: false
cis_dil_snmp_server: false
cis_dil_squid_server: false
cis_dil_smb_server: false
cis_dil_dovecot_server: false
cis_dil_httpd_server: false
cis_dil_vsftpd_server: false
cis_dil_named_server: false
cis_dil_bind: false
cis_dil_vsftpd: false
cis_dil_httpd: false
cis_dil_dovecot: false
cis_dil_samba: false
cis_dil_squid: false
cis_dil_net_snmp: false
```

##### Designate server as a Mail server
`cis_dil_is_mail_server: false`


##### System network parameters (host only OR host and router)
`cis_dil_is_router: false`


##### IPv6 required
`cis_dil_ipv6_required: true`


##### AIDE
`cis_dil_config_aide: true`

###### AIDE cron settings
```
cis_dil_aide_cron:
cron_user: root
cron_file: /etc/crontab
aide_job: '/usr/sbin/aide --check'
aide_minute: 0
aide_hour: 5
aide_day: '*'
aide_month: '*'
aide_weekday: '*'
```

##### SELinux policy
`cis_dil_selinux_pol: targeted`


##### Set to 'true' if X Windows is needed in your environment
`cis_dil_xwindows_required: no`


##### Client application requirements
```
cis_dil_openldap_clients_required: false
cis_dil_telnet_required: false
cis_dil_talk_required: false
cis_dil_rsh_required: false
cis_dil_ypbind_required: false
```

##### Time Synchronization
```
cis_dil_time_synchronization: chrony
cis_dil_time_Synchronization: ntp

cis_dil_time_synchronization_servers:
- 0.pool.ntp.org
- 1.pool.ntp.org
- 2.pool.ntp.org
- 3.pool.ntp.org
```

##### 3.4.2 | PATCH | Ensure /etc/hosts.allow is configured
```
cis_dil_host_allow:
- "10.0.0.0/255.0.0.0"
- "172.16.0.0/255.240.0.0"
- "192.168.0.0/255.255.0.0"
```

```
cis_dil_firewall: firewalld
cis_dil_firewall: iptables
```


Dependencies
------------

Ansible > 2.2

Example Playbook
-------------------------

```
- name: Harden Server
hosts: servers
become: yes

roles:
  - CIS_Distribution_Independent_Linux_Benchmark
```

Tags
----
Many tags are available for precise control of what is and is not changed.

Some examples of using tags:

```
# Audit and patch the site
ansible-playbook site.yml --tags="patch"
```

License
-------

CIS Distribution Linux Independent Benchmark is licenced under the [Creative Common Attribution-NonCommerctial-ShareAlike 4.0 International Public Licence](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode)

The benchmarks are available here: [https://www.cisecurity.org/cis-benchmarks/](https://www.cisecurity.org/cis-benchmarks/)

Licence of the original repository [Florian Utz](https://github.com/florianutz/Ubuntu1604-CIS) MIT

So the "final" licence is the same: MIT

