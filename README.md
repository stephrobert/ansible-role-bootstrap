# bootstrap

[![Ansible version](https://img.shields.io/badge/ansible-%3E%3D2.10-black.svg?style=flat-square&logo=ansible)](https://github.com/ansible/ansible)

⭐ Star us on GitHub — it motivates us a lot!

your role description

**Platforms Supported**:

None.

## ⚠️ Requirements

Ansible >= 2.1.

### Ansible role dependencies

None.

## ⚡ Installation

### Install with Ansible Galaxy

```shell
ansible-galaxy install bootstrap
```

### Install with git

If you do not want a global installation, clone it into your `roles_path`.

```bash
git clone   bootstrap
```

But I often add it as a submodule in a given `playbook_dir` repository.

```bash
git submodule add  roles/bootstrap
```

As the role is not managed by Ansible Galaxy, you do not have to specify the
github user account.

### ✏️ Example Playbook

Basic usage is:

```yaml
- hosts: all
  roles:
    - role: bootstrap
      vars:
        bootstrap_timeout: 10
        
```

## ⚙️ Role Variables

Variables are divided in three types.

The **default vars** section shows you which variables you may
override in your ansible inventory. As a matter of fact, all variables should
be defined there for explicitness, ease of documentation as well as overall
role manageability.

The **context variables** are shown in section below hint you
on how runtime context may affects role execution.

### Default variables

#### main

Bootsrap a machine for Ansible.

| Variable Name | Required | Type | Default | Elements | Description |
|---------------|----------|------|---------|----------|-------------|
| bootstrap_timeout | False | int | 10 |  |  |

### Context variables

Those variables from `vars/*.{yml,json}` are loaded dynamically during task
runtime using the `include_vars` module.

Variables loaded from `vars/main.yml`.

| Variable Name | Value |
|---------------|-------|
| bootstrap_os_family_map | Alpine:<br>- Alpine<br>Archlinux:<br>- Archlinux<br>- Antergos<br>- Manjaro<br>Debian:<br>- Debian<br>- Ubuntu<br>- Raspbian<br>- Neon<br>- KDE neon<br>- Linux Mint<br>- SteamOS<br>- Devuan<br>- Kali<br>- Cumulus Linux<br>- Pop!_OS<br>- Parrot<br>- Pardus GNU/Linux<br>Gentoo:<br>- Gentoo<br>- Funtoo<br>RedHat:<br>- RedHat<br>- Fedora<br>- CentOS<br>- Scientific<br>- SLC<br>- Ascendos<br>- CloudLinux<br>- PSBM<br>- Rocky<br>- OracleLinux<br>- OVS<br>- OEL<br>- Amazon<br>- Virtuozzo<br>- XenServer<br>- Alibaba<br>- EulerOS<br>- openEuler<br>- AlmaLinux<br>Suse:<br>- SLED<br>- openSUSE Tumbleweed<br>- openSUSE Leap<br>- SLES_SAP<br>- SUSE_LINUX<br>- SLES<br>- openSUSE<br>- SuSE<br> |
| bootstrap_install | {{ _bootstrap_install[bootstrap_distribution ~'_'~ bootstrap_distribution_major_version] \|default( _bootstrap_install[bootstrap_distribution] ) \|default( _bootstrap_install[bootstrap_os_family] ) }} |
| _bootstrap_install | Alpine:<br>  raw: LANG=C apk update ; apk add {{ bootstrap_packages }}<br>  stdout_regex: Installing<br>Archlinux:<br>  raw: LANG=C pacman -Sy --noconfirm {{ bootstrap_packages }}<br>  stdout_regex: ' installing python'<br>Debian:<br>  raw: LANG=C apt-get update && apt-get install -y {{ bootstrap_packages }}<br>  stdout_regex: ' 0 newly installed'<br>Gentoo:<br>  raw: LANG=C equery l {{ bootstrap_packages }}  \| \| (emaint -a sync ; emerge -qkv {{<br>    bootstrap_packages }} ; echo 'changed')<br>  stdout_regex: changed<br>RedHat:<br>  raw: LANG=C yum -y install {{ bootstrap_packages }}<br>  stdout_regex: Nothing<br>Suse:<br>  raw: LANG=C zypper -n install {{ bootstrap_packages }}<br>  stdout_regex: Nothing<br> |
| _bootstrap_packages | Alpine: python3 sudo<br>Amazon: python sudo<br>Archlinux: python sudo<br>CentOS_7: python sudo<br>Debian: python3 sudo gnupg python3-apt<br>Debian_8: python sudo gnupg<br>Debian_9: python sudo gnupg<br>Gentoo: python sudo gentoolkit<br>RedHat: python3 sudo<br>RedHat_7: python sudo<br>Suse: python3 python3-xml sudo<br> |
| bootstrap_packages | {{ _bootstrap_packages[bootstrap_distribution ~'_'~ bootstrap_distribution_major_version] \|default( _bootstrap_packages[bootstrap_distribution] ) \|default( _bootstrap_packages[bootstrap_os_family] ) }} |
| bootstrap_facts_packages | {{ _bootstrap_packages[ansible_distribution ~'_'~ ansible_distribution_major_version] \|default( _bootstrap_packages[ansible_distribution] ) \|default( _bootstrap_packages[ansible_os_family] ) }} |



## Author Information

your company (optional)