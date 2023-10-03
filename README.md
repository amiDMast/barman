# Barman Ansible Role for Postgresql

This Ansible role install [Barman](https://www.pgbarman.org/), and configure backup process with one or more Postgresql clusters.

## Requirements

This role requires root privileges, so tell ansible to use `become: true` in any [convenient way](http://docs.ansible.com/ansible/latest/become.html) for you.

## Role Variables
The list contains variable names and example values.

- **barman: {map}** Parameters for barman configuration. Structure is documented below.

### The `barman` block supports:
- **log_level: INFO**
- **servers: {map}** Parameters for specific postgresql cluster which need to backup. Structure is documented below.

### The `servers` block supports:
- **name: pgserver** 
- **host: backup**
- **user: barman**
- **password: barmanpass**
- **slot_name: barmanwal**
- **bckp_create_min: "0"**
- **bckp_create_hour: "0"**
- **bckp_create_day: "*"**
- **bckp_delete_min: "0"**
- **bckp_delete_hour: "3"**
- **bckp_delete_day: "*"**
- **minimum_redundancy: 1** default = 1. Minimum number of backups to be retained. Server.

### Configuration example:
```yml
# Log levels: DEBUG, INFO, WARNING, ERROR, CRITICAL
barman:
  log_level: INFO
  servers:
    - name: pgserver
      host: backup
      user: barman
      password: barmanpass
      slot_name: barmanwal
      bckp_create_min: "0"
      bckp_create_hour: "0"
      bckp_create_day: "*"
      bckp_delete_min: "0"
      bckp_delete_hour: "3"
      bckp_delete_day: "*"
      minimum_redundancy: 1
```

## Role tags
- **barman** Main tag.
- **barman_install** Run specific task to install barman service.
- **barman_config** Run specific task to create configuration files for barman service.
- **barman_cron** Run specific task to create cron tasks for create new backups and delete oldest backups with barman service.
- **barman_users** Run specific task to configure postgres user for fetching backups and WALs for backup node.