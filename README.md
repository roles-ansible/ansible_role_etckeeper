<!--
[![Ansible Galaxy](https://ansible.l3d.space/svg/$namespace.$role.svg)](https://galaxy.ansible.com/ui/standalone/roles/$namespace/$role/)
[![BSD-3 Clause](https://ansible.l3d.space/svg/$namespace.$role_license.svg)](LICENSE)
[![Maintainance](https://ansible.l3d.space/svg/$namespace.$role_maintainance.svg)](https://ansible.l3d.space/#$namespace.$role)
-->

 ansible_role_etckeeper
=======================
Etckeeper is a collection of tools to keep track of /etc/ in a repository (Git, Mercurial, Bazaar or Darcs are supported).

This ansible role installs ETCkeeper and can cange some of the configuration.

Variables
---------

| name | default | description |
| ---- | ------- | ----------- |
| `etckeeper__vcs` | `git` | 'List of required packages for etckeeper |
| `etckeeper__git_commit_options` | | git commit options |
| `etckeeper__hg_commit_options` | | hg commit options |
| `etckeeper__bzr_commit_options` | | bzr commit options |
| `etckeeper__darcs_commit_options` | `-a` | darcs commit options |
| `etckeeper__daily_commits_per_systemd` |  `true` | If disabled all systemd tasks will be skipped |
| `etckeeper__avoid_commit_before_install` | `false` | Enablet to avoid etckeeper committing existing changes to it's repo before installation. It will cancel the installation, so you can commit the changes by hand. |
| `etckeeper__push_remotes` | | To push each commit to a remote, put the name of the remote here. *(space seperated)* |
| `etckeeper__git_remote[]` | `[]` | A list of remotes, see example below. |
| `etckeeper__git_remote[].remote` | | name of git remote eg. 'origin' |
| `etckeeper__git_remote[].repo` | | Git URL of remote |
| `etckeeper__git_name` | `etckeeper on {{ inventory_hostname }}` | Git Name for etckeeper git repo |
| `etckeeper__git_email` | `root@{{ inventory_hostname }}` | Git E-Mail for etckeeper git repo |
| `etckeeper__gitignore` | | list for git ignore |
| `etckeeper__highlevel_package_manager` | `{{ ansible_facts['pkg_mgr'] }}` | apt, pacman, pacman-g2, yum, dnf, zypper, apk, xbps, emerge, cave, etc |
| `etckeeper_lowlevel_package_manager` | `dpkg` | dpkg, rpm, pacman, pacmatic, pacman-g2, apk, xbps, cave, qlist, etc |
| `etckeeper__requirements` | `git` | List of requirements for etckeeper |
| `etckeeper__package_name` | `etckeeper` | Name of etckeeper Package |

Example Playbook
----------------

```
- name: Run etckeeper
  hosts: example.org
  roles:
    - {role: etckeeper, tags: erckeeper}
  vars:
    etckeeper__push_remotes: 'origin'
    etckeeper__git_remote:
      - remote: 'origin'
        repo: 'https://git.example.org/foo/bar.git'
```

Requirements
-----------

Some ansible modules require community.general

LICENSE
-------

MIT License

