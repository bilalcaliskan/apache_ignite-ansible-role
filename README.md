## Apache Ignite Ansible Role

[![CI](https://github.com/bilalcaliskan/apache_ignite-ansible-role/workflows/CI/badge.svg?event=push)](https://github.com/bilalcaliskan/apache_ignite-ansible-role/actions?query=workflow%3ACI)

Installs and configures Apache Ignite on RedHat/CentOS servers(7 and 8).

### Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: true`, or invoke the role in your playbook like:

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.apache_ignite
```

### Role Variables
See the default values in [defaults/main.yml](defaults/main.yml). You can overwrite them in [vars/main.yml](vars/main.yml) if neccessary or you can set them while running playbook.

> Please note that this role will ensure that `firewalld` systemd service on your servers are started and enabled by default. If you want to stop and disable `firewalld` service, please modify below variable as false when running playbook:  
> ```yaml  
> firewalld_enabled: false

### Dependencies

None

### Example Inventory File
*Single node*
```
[ignite]
ignitenode01.example.com
```

*Multi node*
```
[ignite]
ignitenode01.example.com
ignitenode02.example.com
ignitenode03.example.com
```

### Example Playbook File For Installation

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
        java_opts: -XX:+UseG1GC -Xms1g -Xmx1g -servers
```

You can also override default variables inside [vars/main.yml](vars/main.yml)*:
```yaml
java_opts: -XX:+UseG1GC -Xms1g -Xmx1g -server
```

### Example Playbook File For `Ununinstallation`

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.apache_ignite
      vars:
        install_ignite: false
```

### License

MIT / BSD
