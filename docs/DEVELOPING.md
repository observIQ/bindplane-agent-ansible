## Developing

### Testing

#### Setup

Install [Gcloud SDK](https://cloud.google.com/sdk/docs/install)

Install [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html), [Molecule](https://molecule.readthedocs.io/en/latest/installation.html), [Molecule GCE driver](https://github.com/ansible-community/molecule-gce), and dependencies.

```bash
pip install -r requirements.txt
export PATH=~/.local/bin:$PATH

ansible-galaxy collection install google.cloud
ansible-galaxy collection install community.crypto
```

Configure Project
1. `gcloud compute project-info add-metadata --metadata enable-oslogin=TRUE`
2. Enable api `IAM Service Account Credentials API`

Google Cloud Service Account
1. Create a GCP service account with the following roles:
  - Compute Admin
  - Compute OS Admin Login
  - Service Account User
2. Create and download the service accounts json key
3. Create ssh keypair for service account
  - `ssh-keygen -f ssh-key-ansible-sa`
4. Authenticate as the service account and bind the ssh keypair
  - `gcloud auth activate-service-account --key-file=<pat to service account json key`
  - `gcloud compute os-login ssh-keys add --key-file=ssh-key-ansible-sa.pub`
5. Get the service account's id to determine the ssh username
  - `gcloud iam service-accounts describe <service account's email> --format='value(uniqueId)'`
  - For example, id of `1066277234963989999` would be username: `sa_1066277234963989999`

Export the following environment variables using a `.env` file in the repo's root directory:
```
export GCP_PROJECT_ID=<project id>
export GOOGLE_APPLICATION_CREDENTIALS=<path to service account json key>
export SSH_KEY_FILE=<path to private ssh key used by gcp service account>
export OIQ_SECRET_KEY=<oiq cloud secret key>
export SSH_USER=sa_<service account's id>
export GCP_AUTH_KIND=serviceaccount
```

**NOTE**: SSH_USER is prefixed with `sa_`.

Make sure [gcloud ssh is configured](https://cloud.google.com/sdk/gcloud/reference/compute/config-ssh?hl=zh-tw)

#### Run Tests Locally

Local testing will use the service account for instance deployment and your personal 
account for ssh and executing ansible.

- molecule create
- molecule converge
- molecule idempotence
- molecule verify
- molecule destroy
