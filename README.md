[![CI](https://github.com/marvel-nccr/ansible-role-abinit/workflows/CI/badge.svg)](https://github.com/marvel-nccr/ansible-role-abinit/actions)
[![Ansible Role](https://img.shields.io/ansible/role/52051.svg)](https://galaxy.ansible.com/marvel-nccr/abinit)
[![Release](https://img.shields.io/github/tag/marvel-nccr/ansible-role-abinit.svg)](https://github.com/marvel-nccr/ansible-role-abinit/releases)

# Ansible Role: marvel-nccr.abinit

An Ansible role that installs [abinit](https://www.abinit.org) on Ubuntu.

## Installation

`ansible-galaxy install marvel-nccr.abinit`

## Role Variables

See `defaults/main.yml`

## Example Playbook

```yaml
- hosts: servers
  roles:
  - role: marvel-nccr.abinit
    vars:
      abinit_version: "9.2.1"
```

On some platforms (such as VirtualBox), the apt installed `libxc-dev` leads to test failures.
If this is the case, you may want to use a specifically compiled version, e.g. using the `marvel-nccr.libxc` role:

```yaml
- hosts: servers
  vars:
    libxc_version: "4.3.4"
    libxc_prefix: "/usr/local/libxc-{{ libxc_version }}"
  roles:
  - role: marvel-nccr.libxc
  - role: marvel-nccr.abinit
    vars:
      abinit_version: "9.2.1"
      abinit_libxc_path: "{{ libxc_prefix }}"
```

## Development and testing

This role uses [Molecule](https://molecule.readthedocs.io/en/latest/#) and [Docker](https://www.docker.com/) for tests.

After installing [Docker](https://www.docker.com/):

Clone the repository into a package named `marvel-nccr.abinit` (the folder must be named the same as the Ansible Galaxy name)

```bash
git clone https://github.com/marvel-nccr/ansible-role-abinit marvel-nccr.abinit
cd marvel-nccr.abinit
```

Then run:

```bash
pip install -r requirements.txt  # Installs molecule
molecule test  # runs tests
```

or use tox (see `tox.ini`):

```bash
pip install tox
tox
```

## Code style

Code style is formatted and linted with [pre-commit](https://pre-commit.com/).

```bash
pip install pre-commit
pre-commit run -all
```

## Deployment

Deployment to Ansible Galaxy is automated *via* GitHub Actions.
Simply tag a release `vX.Y.Z` to initiate the CI and release workflow.
Note, the release will only complete if the CI tests pass.

## License

MIT

## Contact

Please direct inquiries regarding Quantum Mobile and associated ansible roles to the [AiiDA mailinglist](http://www.aiida.net/mailing-list/).
