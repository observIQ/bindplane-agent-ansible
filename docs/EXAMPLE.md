## Examples

site.yml
```yaml
all:
  hosts:
    192.168.1.10
```

playbook.yml
```yaml
- name: bindplane-agent
  hosts: all
  become: yes
  roles:
    - role: bindplane_agent
      version: "1.28.0"
      endpoint: "ws://localhost:3001/v1/opamp"
      secret_key: "01H4P9QCXQNNQ1GE3BA34GR4EK"
      agent_id: "01H534EAD5WYZ02QVQKKE6VEY6"
      labels: "configuration=ansible"
```

Run with:
```bash
ansible-playbook playbook.yml -i ./site.yml
```
