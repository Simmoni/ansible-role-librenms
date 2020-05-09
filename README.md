# ansible-role-librenms
Ansible role that installs LibreNMS on CentOS 7 hosts.

Installs php 7.3 from the remi repo and enables the epel repository.

The intention was to make this role idempotent as previous roles I found was not.

## Requirements

None

## Variables

Available variables are listed below, as well as in `defaults/main.yml.`

| Variable | Default Value | Description |
|--------- | ------------- | ----------- |
| new_install | yes | **Yes:** Do not copy config.php from templates directory. The LibreNMS WebUI will generate a config.php for you. **No**: Create config.php from variables and template file |
| system_timzone | UTC | System and php timezone |
| librenms\_config\_user | librenms | LibreNMS system user |
| librenms\_mysql\_username | librenms | DB username |
| librenms\_mysql\_password | examplepassword | DB password |

The following variables are only used when **new_install** is set to **No**:

| Variable | Default Value | Description |
|--------- | ------------- | ----------- |
| librenms\_config\_db\_host | localhost | DB Server address |
| librenms\_config\_db\_port | 3306 | DB Server port used to connect |
| librenms\_config\_db\_name | librenms | DB Name |
| librenms\_config\_db\_socket | | DB Socket | 
| librenms\_config\_snmp\_community | public | SNMP Community string |
| librenms\_config\_auth\_mechanism | mysql | Auth method used to log in to the LibreNMS webinterface |
| librenms\_config\_nets | 10.0.0.0/16 | List of networks to scan |
| librenms\_config\_discovery\_by\_ip | true | Add devices via auto-discovery by ip |
| librenms\_config\_update| 1 | Allow LibreNMS to automatically update |
| librenms\_config\_smokeping_dir | /var/lib/smokeping | Path to Smokeping installation |
| librenms\_config\_smokeping_pings | 20 | Number of pings to send |
| librenms\_config\_smokeping\_integration | true | Enable Smokeping integration |
| librenms\_config\_enable\_billing | 1 | Enable billing in LibreNMS |
| librenms\_config\_oxidized\_enabled | true | Enable oxidized integration |
| librenms\_config\_oxidized\_url | http://{{ ansible_fqdn }}:8888/oxidized | oxidized rest URL |
| librenms\_config\_oxidized\_features\_versioning | true | Enable oxidized config versioning |

## Dependencies

None

## Example Playbook

```- name: Install and configure ansible and rundeck
  hosts: servers
  become: yes
  roles:
    - ansible-role-librenms