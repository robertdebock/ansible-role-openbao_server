# [Ansible role openbao_server](#ansible-role-openbao_server)

Configure OpenBao (server) on your system.

|GitHub|GitLab|Downloads|Version|
|------|------|---------|-------|
|[![github](https://github.com/robertdebock/ansible-role-openbao_server/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-openbao_server/actions)|[![gitlab](https://gitlab.com/robertdebock-iac/ansible-role-openbao_server/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-openbao_server)|[![downloads](https://img.shields.io/ansible/role/d/robertdebock/openbao_server)](https://galaxy.ansible.com/robertdebock/openbao_server)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-openbao_server.svg)](https://github.com/robertdebock/ansible-role-openbao_server/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/robertdebock/ansible-role-openbao_server/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true

  roles:
    - role: robertdebock.openbao_server
      openbao_server_config: |
        # Copyright (c) HashiCorp, Inc.
        # SPDX-License-Identifier: MPL-2.0

        # Full configuration options can be found at https://github.com/openbao/openbao/tree/main/website/content/docs/configuration

        ui = true

        storage "file" {
          path = "/opt/openbao/data"
        }

        # HTTP listener
        #listener "tcp" {
        #  address = "127.0.0.1:8200"
        #  tls_disable = 1
        #}

        # HTTPS listener
        listener "tcp" {
          address       = "0.0.0.0:8200"
          tls_cert_file = "/opt/openbao/tls/tls.crt"
          tls_key_file  = "/opt/openbao/tls/tls.key"
        }

        # Example AWS KMS auto unseal
        #seal "awskms" {
        #  region = "us-east-1"
        #  kms_key_id = "REPLACE-ME"
        #}
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/robertdebock/ansible-role-openbao_server/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: true
  gather_facts: false

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.openbao
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/robertdebock/ansible-role-openbao_server/blob/master/defaults/main.yml):

```yaml
---
# defaults file for openbao_server

# OpenBao server configuration.
# All OpenBao server settings are contained in this dictionary.
#
# Example configuration:
# openbao_server_config: |
#   ui            = true
#   cluster_addr  = "https://127.0.0.1:8201"
#   api_addr      = "https://127.0.0.1:8200"

#   storage "raft" {
#     path = "/path/to/raft/data"
#     node_id = "raft_node_1"
#   }

#   listener "tcp" {
#     address       = "127.0.0.1:8200"
#     tls_cert_file = "/path/to/full-chain.pem"
#     tls_key_file  = "/path/to/private-key.pem"
#   }

#   telemetry {
#     statsite_address = "127.0.0.1:8125"
#     disable_hostname = true
#   }


# A map of environment variables to set for the OpenBao server.
# openbao_server_environment:
#   SOME_VARIABLE: "some_value"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-openbao_server/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap)|
|[robertdebock.openbao](https://galaxy.ansible.com/robertdebock/openbao)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-openbao/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-openbao/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-openbao/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-openbao)|

## [Context](#context)

This role is part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/ansible-role-openbao_server/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|[Amazon](https://hub.docker.com/r/robertdebock/amazonlinux)|Candidate|
|[Debian](https://hub.docker.com/r/robertdebock/debian)|bullseye, bookworm, trixie|
|[EL](https://hub.docker.com/r/robertdebock/enterpriselinux)|9|
|[Fedora](https://hub.docker.com/r/robertdebock/fedora)|42, 40|
|[Ubuntu](https://hub.docker.com/r/robertdebock/ubuntu)|jammy, noble|

The minimum version of Ansible required is 2.12, tests have been done on:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them on [GitHub](https://github.com/robertdebock/ansible-role-openbao_server/issues).

## [License](#license)

[Apache-2.0](https://github.com/robertdebock/ansible-role-openbao_server/blob/master/LICENSE).

## [Author Information](#author-information)

[robertdebock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
