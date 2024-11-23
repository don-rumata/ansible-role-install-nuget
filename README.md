# Ansible Role: Install Nuget

[![License][license-image]][license-url]
[![Ansible Galaxy][ansible-galaxy-image]][ansible-galaxy-url]
![Ansible Role downloads](https://img.shields.io/ansible/role/d/don-rumata/install-nuget.svg)

Install [NuGet](https://www.nuget.org/) for Linux and Windows.

## Work on

### Ansible Galaxy style

```yaml
  platforms:
    - name: Ubuntu
      versions:
        - focal
        - jammy
    - name: Debian
      version:
        - buster
        - bullseye
        - bookworm
    - name: Windows
      version:
        - 2008x64 (7 64bit)
        - 2019 (10 64bit)
```

## Requirements

min_ansible_version: 2.9

## Role Variables

```yaml
nuget_download_url: https://dist.nuget.org/win-x86-commandline/latest/nuget.exe

nuget_win_path_to_install: '{{ ansible_env.ProgramFiles }}\nuget'

nuget_linux_path_to_install: /usr/local/bin
```

## Dependencies

### If you want deploy to Windows 7

Download and install [Windows Management Framework 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)

## HowTo

### How to install role

Over `ansible-galaxy`:

`TODO`.

Over `bash+git`:

```bash
mkdir -p "$HOME/.ansible/roles"
cd "$HOME/.ansible/roles"
git clone https://github.com/don-rumata/ansible-role-install-nuget don_rumata.ansible_role_install_nuget
```

### Quick config WinRM for Windows

<https://ru.stackoverflow.com/a/949971/191416>

## Example Playbooks

### I

Install latest NuGet on Windows or Linux:

`install-nuget.yml`:

```yaml
- name: Install nuget
  hosts: all
  strategy: free
  serial:
    - "100%"
  roles:
    - don_rumata.ansible_role_install_nuget
  tasks:
```

### II

Install NuGet from intranet:

`install-nuget.yml`:

```yaml
- name: Install nuget
  hosts: all
  strategy: free
  serial:
    - "100%"
  roles:
    - role: ansible-role-install-nuget
      nuget_download_url: http://10.10.10.10/soft/nuget/nuget.exe
  tasks:
```

## License

Apache License, Version 2.0

## Author Information

[don Rumata](https://github.com/don-rumata)

## TODO

- Add repo mono project.
- Install over `ansible galaxy`.

[license-image]: https://img.shields.io/github/license/don-rumata/ansible-role-install-nuget.svg
[license-url]: https://opensource.org/licenses/Apache-2.0

[ansible-galaxy-image]: https://img.shields.io/badge/ansible_galaxy-don__rumata.ansible__role__install__nuget-blue.svg
[ansible-galaxy-url]: https://galaxy.ansible.com/don_rumata/ansible_role_install_nuget
