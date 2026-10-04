# API documentation: pgvillage.firewall

This document describes the variables that can be used to configure the `pgvillage.firewall` role.
All defaults are defined in [defaults/main.yml](../defaults/main.yml).

## Overview

| Variable                 | Type   | Default         |
| ------------------------ | ------ | --------------- |
| `firewall_type`          | string | `external`      |
| `firewall_package_state` | string | `present`       |
| `firewall_packages`      | list   | `[firewalld]`   |
| `firewall_ports`         | dict   | see below       |

## Variables

### `firewall_type`

Which firewall implementation this role should manage.

- `firewalld`: install, start and enable firewalld, and open the ports defined in `firewall_ports`.
- `external` (or any other value): the role does nothing and leaves firewall management to something else
  (e.g. the cloud provider).

Default:

```yaml
firewall_type: external
```

### `firewall_package_state`

State of the firewall packages, passed as `state` to `ansible.builtin.package`.
Use `present` to install, `latest` to install/upgrade, or `absent` to remove.
Only used when `firewall_type` is `firewalld`.

Default:

```yaml
firewall_package_state: present
```

### `firewall_packages`

List of packages to install when `firewall_type` is `firewalld`.

Default:

```yaml
firewall_packages:
  - firewalld
```

### `firewall_ports`

Dictionary of TCP ports to open in firewalld. The key is a descriptive name (used as the loop label in
Ansible output), the value is the TCP port number. Ports are opened permanently and immediately.
Only used when `firewall_type` is `firewalld`.

Default:

```yaml
firewall_ports:
  postgres: 5432
  stolon_proxy: 25432
  etcd_client: 2379
  etcd_server: 2380
```

## Example

```yaml
- hosts: servers
  roles:
    - role: pgvillage.firewall
      vars:
        firewall_type: firewalld
        firewall_ports:
          postgres: 5432
          pgbouncer: 6432
```
