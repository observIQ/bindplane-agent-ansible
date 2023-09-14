Ansible Role For [BindPlane Agent](https://github.com/observIQ/observiq-otel-collector)
==========================

[![Integration Tests](https://github.com/observIQ/bindplane-agent-ansible/actions/workflows/integration.yml/badge.svg)](https://github.com/observIQ/bindplane-agent-ansible/actions/workflows/integration.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

Install the role in your roles path (usually in a `roles` directory
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
| `ca_file`       | optional             | Path to x509 PEM encoded CA certificate, used to trust the BindPlane OP's certificate.                              |
| `cert_file`      | optional             | Path to x509 PEM encoded certificate file path, used for mutual TLS authentication.                                 |
| `key_file`       | optional             | Path to x509 PEM encoded private key file path, used for mutual TLS authentication.                                 |
| `insecure_skip_verify` | optional     | Whether or not to skip verification of TLS certificates. |

## Documentation

- [Usage](./docs/USAGE.md)
- [Developing](./docs/DEVELOPING.md)

## License

This library is licensed under Apache 2.0. Full license text is available in [LICENSE](LICENSE).

# Community

Ansible Role For BindPlane Agent is an open source project. If you'd like to contribute, take a look at our [contribution guidelines](/docs/CONTRIBUTING.md). We look forward to building with you.

## Code of Conduct

Ansible Role For BindPlane Agent follows the [CNCF Code of Conduct](https://github.com/cncf/foundation/blob/master/code-of-conduct.md). Please report violations of the Code of Conduct to any or all [maintainers](/docs/MAINTAINERS.md).

# Other questions?

Send us an [email](mailto:support@observiq.com), or open an issue with your question. We'd love to hear from you!
