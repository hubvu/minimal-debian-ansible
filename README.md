## Ansible Role - Minimal Debian Server

<p align="center">
  <a href="https://github.com/hubvu/minimal-debian-ansible/actions" alt="Ansible Lint">
    <img src="https://github.com/hubvu/minimal-debian-ansible/actions/workflows/ansible-lint.yml/badge.svg?branch=main">
  </a>
  <a href="https://github.com/hubvu/minimal-debian-ansible/releases" alt="GitHub Release">
    <img src="https://img.shields.io/github/v/release/hubvu/minimal-debian-ansible.svg">
  </a>
  <a href="./LICENSE.md" alt="MIT License">
    <img src="https://img.shields.io/badge/license-MIT-green.svg">
  </a>
  <a href="https://github.com/hubvu/minimal-debian-ansible/tree/main#supported-distributions" alt="Supported Distributions">
    <img src="https://img.shields.io/badge/platform-debian-lightgrey.svg">
  </a>
  <a href="https://img.shields.io/github/repo-size/hubvu/minimal-debian-ansible.svg" alt="Repository Size">
    <img src="https://img.shields.io/github/repo-size/hubvu/minimal-debian-ansible.svg">
  </a>
  <a href="https://img.shields.io/github/directory-file-count/hubvu/minimal-debian-ansible.svg" alt="Repository File Count">
    <img src="https://img.shields.io/github/directory-file-count/hubvu/minimal-debian-ansible.svg">
  </a>
</p>

- [Ansible Role - Minimal Debian Server](#ansible-role---minimal-debian-server)
  - [What is this?](#what-is-this)
  - [Resource Requirements](#resource-requirements)
  - [Dependencies](#dependencies)
  - [Supported Distributions](#supported-distributions)
  - [Quick-start & Usage](#quick-start--usage)
  - [Contributing](#contributing)
  - [Acknowledgements](#acknowledgements)
  - [License](#license)

### What is this?

* A simple Ansible role that checks and ensures that non-essential packages are removed from a new Debian server installation.
  * To review the list of packages that will be removed (if applicable), check the `main.yml` file in the [tasks](./roles/minimal_debian/tasks/) directory.

### Resource Requirements

* [Debian](https://www.debian.org/distrib/) host(s) that the playbook will be run against.

### Dependencies

* [`ansible-vault`](https://docs.ansible.com/ansible/latest/user_guide/vault.html) - [**optional**] - can be used in the [`minimal_debian.yaml`](./minimal_debian.yaml) playbook to encrypt and store sensitive data "at rest". 
  * In this use case, the `ansible_sudo_password` variable, which is used as the privilege escalation password, is stored in a vault.
  * Once the secret has been created and added to the playbook, in order for a user be able to become `sudo` to run the playbook, they will need to decrypt the vault to access the variable.
  * This can be achieved by passing one of the following flags listed below when executing the the playbook;
    * `--ask-vault-pass` 
    * `--vault-password-file`
  * Below is a demonstration of how the encrypted variable is defined in the playbook;

```yaml
---
# playbook for the minimal_debian role.
- hosts: all
  vars_files:
    - become-secret
  become: true
  roles:
    - minimal_debian
```
  * For more information on how to create encrypted variables, please review the [official `ansible` documentation](https://docs.ansible.com/ansible/latest/user_guide/vault.html#encrypting-individual-variables-with-ansible-vault).

### Supported Distributions

* Tested on;
  * `debian-10`

### Quick-start & Usage

```bash
# clone the repository
$ git clone git@github.com:hubvu/minimal-debian-ansible.git

# navigate into the directory
$ cd minimal-debian-ansible/

# run the master playbook `site.yaml` with verbosity
# for non Ansible Vault users
$ ansible-playbook site.yaml \
  --inventory-file=hosts \
  --ask-become-pass \
  --verbose

# run the master playbook `site.yaml` with verbosity
# for Ansible Vault users
$ ansible-playbook site.yaml \
  --inventory-file=hosts \
  --ask-vault-pass \
  --verbose
```

### Contributing

* Contribution guidelines for this project can be found in the [Contributing](./CONTRIBUTING.md) document.

### Acknowledgements

* [CIS - Debian Linux Benchmark](https://www.cisecurity.org/benchmark/debian_linux/).
* [Ansible Lint](https://github.com/ansible-community/ansible-lint).
* [Ansible Lint for GitHub Action](https://github.com/ansible/ansible-lint-action).

### License

* Licenced under the [MIT License](./LICENSE.md).
