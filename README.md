# Apache Ignite Ansible Role

[![CI](https://github.com/bilalcaliskan/apache_ignite-ansible-role/workflows/CI/badge.svg?event=push)](https://github.com/bilalcaliskan/apache_ignite-ansible-role/actions?query=workflow%3ACI)
[![GitHub tag](https://img.shields.io/github/tag/bilalcaliskan/apache_ignite-ansible-role.svg)](https://GitHub.com/bilalcaliskan/apache_ignite-ansible-role/tags/)

Installs and configures Apache Ignite on Redhat/Debian based hosts.

## Requirements
This role has below requirements:
- [Python 3.x](https://www.python.org/downloads/)
- [Ansible](https://docs.ansible.com/) (min 2.4, suggested 2.9.16)

You can install suggested version with pip3:
```
$ pip3 install "ansible==2.9.16"
```

Note that this role requires root access, so either run it in a playbook with a global `become: true`, or invoke the role in your playbook.

## Role Variables
See the default values in [defaults/main.yml](defaults/main.yml). You can overwrite them in [vars/main.yml](vars/main.yml) if neccessary or you can set them while running playbook.

> Please note that this role can ensure that `firewalld` systemd service on your servers are started and enabled by default. If you want to start and enable `firewalld` service, please modify below variable as true while running playbook:
> ```yaml
> firewalld_enabled: true
> ```

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
This project requires below tools for development:
- [Python 3.x](https://www.python.org/downloads/)
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) - (min 2.4, suggested 2.9.16)
- [pre-commit](https://pre-commit.com/)
- [ansible-lint](https://ansible-lint.readthedocs.io/en/latest/installing.html#using-pip-or-pipx) - required by [pre-commit](https://pre-commit.com/)
- [Bash shell](https://www.gnu.org/software/bash/) - required by [pre-commit](https://pre-commit.com/)

After you install all the tools above, you can simply configure [pre-commit](https://pre-commit.com/) by typing:
```shell
$ pre-commit install
```
## License

Apache License 2.0
