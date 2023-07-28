# Usage

## Prerequisites

**Install Ansible**

See the [Ansible docs](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

**Clone Role and Create Base Configurations**

Clone the Ansible role to your `roles/` directory. You may want to cd into the repository
and checkout a specific branch.

```bash
mkdir -p roles/
git clone https://github.com/observIQ/bindplane-agent-ansible.git roles/bindplane_agent
```

Create your `site.yml` and configure it to point to one or more hosts that
you would like to install the BindPlane Agent on.

```yaml
all:
  hosts:
    10.99.1.10
```

Create your initial `playbook.yml` file.

```yaml
- name: bindplane-agent
  hosts: all
  become: yes
  roles:
    - role: bindplane_agent
```

Your directory stucture should look like this:

```
├── playbook.yml
├── roles
│   └── bindplane_agent/
└── site.yml
```

**Windows**

Windows targets must have `winrm` properly configured. See the
[Ansible Documentation](https://docs.ansible.com/ansible/latest/os_guide/windows_setup.html)
for proper configuration.

To get started quickly for testing purposes only, you can run the following commands
to configure winrm quickly, but in an insecure way:
```ps
winrm set winrm/config/service/auth '@{Basic="true"}'
winrm set winrm/config/service '@{AllowUnencrypted="true"}'
```

## Basic Example

This example assumes you have a BindPlane OP instance at the endpoint
`ws://10.99.1.10:3001` with the secret key `01H4P9QCXQNNQ1GE3BA34GR4EK`.

Update your `playbook.yml` file to include the required options `version`,
`endpoint`, `secret_key`.
```yaml
- name: bindplane-agent
  hosts: all
  become: yes
  roles:
    - role: bindplane_agent
      version: "1.28.0"
      endpoint: "ws://localhost:3001/v1/opamp"
      secret_key: "01H4P9QCXQNNQ1GE3BA34GR4EK"
```

Deploy with:

```bash
ansible-playbook playbook.yml -i ./site.yml
```

## Specify a Configuration

BindPlane OP server looks for the label `configuration` to determine which configuration
should be pushed to the agent. Agents can be deployed without labels, however, if you would
like Ansible to control the labels, you can set them.

Update your `playbook.yml` file to include the `labels` option with the `configuration` key.
```yaml
- name: bindplane-agent
  hosts: all
  become: yes
  roles:
    - role: bindplane_agent
      version: "1.28.0"
      endpoint: "ws://localhost:3001/v1/opamp"
      secret_key: "01H4P9QCXQNNQ1GE3BA34GR4EK"
      labels: "configuration=my-config"
```

Deploy with:

```bash
ansible-playbook playbook.yml -i ./site.yml
```

## TLS

BindPlane Agent will connect to BindPlane OP using TLS when the endpoint parameter contains
the `wss` protocol.

```yaml
- name: bindplane-agent
  hosts: all
  become: yes
  roles:
    - role: bindplane_agent
      version: "1.28.0"
      endpoint: "wss://localhost:3001/v1/opamp"
      secret_key: "01H4P9QCXQNNQ1GE3BA34GR4EK"
```

Deploy with:

```bash
ansible-playbook playbook.yml -i ./site.yml
```

If The BindPlane Agent does not already trust the BindPlane OP server certificate, you can configure
a certificate authority. It is the users responsibility to deploy the certificate file to the agent
system.

```yaml
- name: bindplane-agent
  hosts: all
  become: yes
  roles:
    - role: bindplane_agent
      version: "1.28.0"
      endpoint: "wss://localhost:3001/v1/opamp"
      secret_key: "01H4P9QCXQNNQ1GE3BA34GR4EK"
      cacrt: /opt/tls/ca.crt
```

Alternatively, you can set the `insecure_skip_verify` option to `true` to skip TLS verification.

## Mutual TLS

BindPlane Agent will connect to BindPlane OP using TLS when the endpoint parameter contains
the `wss` protocol. Mutual TLS will be used for TLS authentication when the `cert_file` and
`key_file` options are configured.

It is the users responsibility to deploy the certificate and private key files to the agent
system.

```yaml
- name: bindplane-agent
  hosts: all
  become: yes
  roles:
    - role: bindplane_agent
      version: "1.28.0"
      endpoint: "wss://localhost:3001/v1/opamp"
      secret_key: "01H4P9QCXQNNQ1GE3BA34GR4EK"
      cacrt: /opt/tls/ca.crt
      cert_file: /opt/tls/agent.crt
      key_file: /opt/tls/agent.key
```

Deploy with:

```bash
ansible-playbook playbook.yml -i ./site.yml
```
