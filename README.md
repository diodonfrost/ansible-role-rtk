ansible-role-rtk
=============

Ansible role to install the latest version of [rtk](https://github.com/rtk-ai/rtk),
a CLI proxy that reduces LLM token consumption on common dev commands.

Requirements
------------

This role requires:
- Ansible 2.10 or higher
- Python 3.x
- tar and gzip (Linux/macOS) or the zip format support (Windows) for extracting the rtk binary
- Internet access to download rtk from GitHub releases

Role Variables
--------------

The following variables are available:

| Variable | Description | Default |
|----------|-------------|---------|
| `rtk_version` | Version of rtk to install. Use 'latest' for the most recent version or specify a version like 'v0.43.0' | `latest` |
| `rtk_path` | Directory where the rtk binary will be installed | `{{ _rtk_default_path }}` |
| `rtk_pkg_url` | Full URL to the rtk archive to download | `{{ _rtk_default_pkg_url }}` |
| `rtk_checksum_verify` | Whether to verify the SHA256 checksum of the downloaded archive | `true` |
| `rtk_checksum_url` | Full URL to the rtk checksums file used to verify the downloaded archive | `{{ _rtk_default_checksum_url }}` |

Dependencies
------------

This role has no dependencies on other roles.

Example Playbook
----------------

Basic usage:

```yaml
- hosts: servers
  roles:
    - role: diodonfrost.rtk
```

With custom version:

```yaml
- hosts: servers
  roles:
    - role: diodonfrost.rtk
      vars:
        rtk_version: "v0.43.0"
```

With custom installation path:

```yaml
- hosts: servers
  roles:
    - role: diodonfrost.rtk
      vars:
        rtk_path: "/opt/rtk/bin"
```

Local Testing
-------------

This project uses [Molecule](http://molecule.readthedocs.io/) to aid in the
development and testing.

To develop or test you'll need to have installed the following:

* Linux (e.g. [Ubuntu](http://www.ubuntu.com/))
* [Docker](https://www.docker.com/)
* [Python](https://www.python.org/) (including python-pip)
* [Ansible](https://www.ansible.com/)
* [Molecule](http://molecule.readthedocs.io/)
* [Libvirt](https://libvirt.org/) (If you test a system other than Linux)
* [Vagrant](https://www.vagrantup.com/downloads.html) (If you test a system other than Linux)

Testing with Docker
-------------------

```shell
# Install requirements
pip install -r requirements-dev.txt

# Test ansible role with ubuntu 24.04
molecule test

# Test ansible role with ubuntu 22.04
image=ansible-ubuntu:22.04 molecule test

# Test ansible role with alpine latest
image=ansible-alpine:latest molecule test
```

Testing with Vagrant and Libvirt
--------------------------------

```shell
# Test ansible role with Linux
molecule test -s linux

# Test ansible role with Windows
molecule test -s windows
```

Supported Platforms
------------------

The role is tested and supported on the following platforms:

* EL (Enterprise Linux)
* Fedora
* Debian
* Ubuntu
* MacOSX
* Windows

License
-------

Apache Software License 2.0

Author Information
------------------

This role was created in 2026 by diodonfrost.
