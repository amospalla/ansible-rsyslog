# ansible-rsyslog
* * *

## Description

Remote logging modes of operation:
- RELP: linux hosts use this mode (reliable).
- TCP: if RELP is not available (ie: RedHat 5) use TCP.
- UDP: if host can not use TCP default to UDP (only server is set up, clients must be configured manually).

The central server is set with the variable _rsyslog_server_host_.

Supported clients:
- Debian 7/8
- Ubuntu 12/14/16
- CentOS 5/6/7

Tested servers:
- Ubuntu 16

Rsyslog distribution versions (for reference):

| Distro    | Version|
|-----------|--------|
| Debian 6  | 4.6.4  |
| Debian 7  | 5.8.11 |
| Debian 8  | 8.4.2  |
| Ubuntu 10 | 4.2.0  |
| Ubuntu 12 | 5.8.6  |
| Ubuntu 14 | 7.4.4  |
| Ubuntu 16 | 8.16.0 |
| Centos 5  | 3.22.1 |
| Centos 6  | 5.8.10 |
| Centos 7  | 7.4.7  |

## Requisites
- python-netaddr

## Variables

Mandatory:
- _rsyslog_server_host_: server hostname as known by ansible.

Optional:
- _rsyslog_relp_port_: integer (default 20514).
- _rsyslog_tcp_port_: integer (default 514).
- _rsyslog_udp_port_: integer (default 514).
- _rsyslog_server_logs_path_: string (default /var/log/remote).
- _rsyslog_server_catchall_path_: string (default {{ rsyslog_server_catchall }}/catchall).
- _rsyslog_server_catchall_enable_: boolean (default False). Information received from unknown hosts is saved.
- _rsyslog_server_catchall_logs_path_: string (default {{ _rsyslog_server_logs_path_/catchall). Information received from unknown hosts is saved.
- _rsyslog_server_stop_on_own_logs_: boolean (default False). Rsyslog server stores localhost logs on the centralized log folder and stops processing them, so them won't also appear on /var/log.

## Example

---
```
- hosts: group_of_hosts_ansible_can_ping:!group_of_hosts_ansible_can_not_ping_ie_a_switch
  gather_facts: True
  tasks: []

- hosts: both_groups
  gather_facts: False
  vars:
    - rsyslog_server_host: log.casa.amospalla.es
  roles:
    - rsyslog

```
