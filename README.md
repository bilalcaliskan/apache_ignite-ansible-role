# Apache Ignite Ansible Role

[![CI](https://github.com/bilalcaliskan/apache_ignite-ansible-role/workflows/CI/badge.svg?event=push)](https://github.com/bilalcaliskan/apache_ignite-ansible-role/actions?query=workflow%3ACI)

Installs and configures Apache Ignite on Redhat/Debian based hosts.

## Requirements

This role requires minimum Ansible version 2.4 and maximum Ansible version 2.9. You can install suggested version with pip:
```
$ pip install "ansible==2.9.16"
```

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: true`, or invoke the role in your playbook like:

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.apache_ignite
```

## Download
This role is also available on [Ansible Galaxy](https://galaxy.ansible.com/bilalcaliskan/apache_ignite), you can install with below command:
```shell
$ ansible-galaxy install bilalcaliskan.apache_ignite
```

## Role Variables
See the default values in [defaults/main.yml](defaults/main.yml). You can overwrite them in [vars/main.yml](vars/main.yml) if neccessary or you can set them while running playbook.

> Please note that this role will ensure that `firewalld` systemd service on your servers are started and enabled by default. If you want to stop and disable `firewalld` service, please modify below variable as false when running playbook:
> ```yaml
> firewalld_enabled: false

## Dependencies

None

## Examples
### Inventory
**Single node**
```
[ignite]
ignitenode01.example.com
```

**Multi node**
```
[ignite]
ignitenode01.example.com
ignitenode02.example.com
ignitenode03.example.com
```

### Installation

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.apache_ignite
      vars:
        install_ignite: true
        ignite_version: 2.7.5
        open_file_limit: 166384
        process_limit: 127949
        java_opts: -XX:+UseG1GC -Xms1g -Xmx1g -server -XX:MaxMetaspaceSize=256m
```

### Uninstallation

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.apache_ignite
      vars:
        install_ignite: false
```

## Development
This project requires below tools while developing:
- [Ansible 2.4 or higher](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [pre-commit](https://pre-commit.com/)
- [ansible-lint](https://ansible-lint.readthedocs.io/en/latest/installing.html#using-pip-or-pipx) - required by [pre-commit](https://pre-commit.com/)
- [Bash shell](https://www.gnu.org/software/bash/) - required by [pre-commit](https://pre-commit.com/)

## License

Apache License 2.0
