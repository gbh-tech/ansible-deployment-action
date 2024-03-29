<!-- omit in toc -->
# Ansible Deployment Action

<!-- omit in toc -->
## Content

- [Overview](#overview)
- [Usage](#usage)
  - [Example usage](#example-usage)

## Overview

This GitHub Action facilitates Ansible deployments, allowing you to run Ansible playbooks with ease. It provides options to configure playbook paths, AWS regions, run modes, and secrets for secure deployment.

## Usage

See [action.yml](action.yml).

``` yaml
- uses: actions/ansible-deployment@v0.0.3
  with:
    # Optional. Specifies the path to the playbook
    playbook_path: 'playbooks'

    # The name of the playbook
    playbook_name: ''

    # Optional. Set to true to run Ansible playbooks in --check mode
    dry_run: false

    # Optional. Set no_log to 'false' to let tasks log all output
    # WARNING! If you set no_log to 'false', sensitive credentials may be log
    # into the console. Default is 'true'
    no_log: true

    # Specifies the AWS region name for configuration
    aws_region: ''

    # A comma-separated string of tags to filter which tasks to run in the playbook
    # The order of the tags is important
    # Example: 'system,deployment,nginx,certbot'
    ansible_tags: ''

    # The ansible working directory
    workdir: 'ansible'

    # Optional. AWS service account access key
    aws_access_key_id: ''

    # Ensure the following values are treated as secrets!

    # Optional. Ansible vault password to decrypt secrets
    ansible_vault_password: ''

    # Optional. AWS service account secret access key
    aws_secret_access_key: ''
```

### Example usage

```yaml
- uses: gbh-tech/ansible-deployment@v0.0.3
  with:
    playbook_path: 'playbooks'
    playbook_name: 'stage.yaml'
    workdir: 'ansible'
    dry_run: true
    no_log: true
    aws_region: 'us-east-1'
    ansible_vault_password: ${{ secrets.ANSIBLE_VAULT_PASSWORD }}
    aws_access_key_id: ${{ vars.AWS_ACCESS_KEY_ID }}
    aws_secret_access_key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    ansible_tags: >-
      auth,
      env-vars,
      info
```
