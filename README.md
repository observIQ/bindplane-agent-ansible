Ansible Role For [BindPlane Agent](https://github.com/observIQ/observiq-otel-collector)
==========================

[![Integration Tests](https://github.com/observIQ/bindplane-agent-ansible/actions/workflows/integration.yml/badge.svg)](https://github.com/observIQ/bindplane-agent-ansible/actions/workflows/integration.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This Ansible role installs the [BindPlane Agent](https://github.com/observIQ/observiq-otel-collector).

Install this directory in your roles path (usually in a `roles` directory
alongside your playbook) under the name `bindplane_agent`:

```bash
git clone https://github.com/observIQ/bindplane-agent-ansible.git roles/bindplane_agent 
```

Role Variables
--------------

| Name           | Default Value        | Description                                                                                                         | 
| -------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------  |
| `version`      | required             | The `version` is required to specify which version of the agent to install. Supported versions: `1.28.0` or newer.  | 
| `endpoint`     | required             | Endpoint for the BindPlane OP server's OpAMP interface.                                                             | 
| `secret_key`   | required             | The BindPlane OP secret key.                                                                                        | 
| `labels`       | optional             | Labels assigned to the agent.                                                                                       |
| `cacert`       | optional             | Path to x509 PEM encoded CA certificate, used to trust the BindPlane OP's certificate.                              |
| `tlscert`      | optional             | Path to x509 PEM encoded certificate file path, used for mutual TLS authentication.                                 |
| `tlskey`       | optional             | Path to x509 PEM encoded private key file path, used for mutual TLS authentication.                                 |
| `insecure_skip_verify` | optional     | Whether or not to skip verification of TLS certificates. |

## Documentation

- [Usage](./docs/USAGE.md)
- [Developing](./docs/DEVELOPING.md)

## License

This library is licensed under Apache 2.0. Full license text is available in [LICENSE](LICENSE).
