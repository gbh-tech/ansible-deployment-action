# Ansible Deployment Action

This GitHub Action facilitates Ansible deployments, allowing you to run Ansible playbooks with ease. It provides options to configure playbook paths, AWS regions, run modes, and secrets for secure deployment.

## Usage

See actions.yml

``` yaml
- uses: actions/ansible-deployment@v1
  with:
    # Optional. Specifies the path to the playbook
    playbook_path: './'

    # The name of the playbook
    playbook_name: ''

    # Optional. Set to true to run Ansible playbooks in --check mode
    dry_run: true

    # Specifies the AWS region name for configuration
    aws_region: ''

    # A comma-separated string of tags to filter which tasks to run in the playbook
    # The order of the tags is important
    # Example: 'system,deployment,nginx,certbot'
    ansible_tags: ''

    # Ensure the following values are treated as secrets:

    # Ansible vault password to decrypt secrets
    ansible_vault_password: ''

    # AWS service account access key
    aws_access_key_id: ''

    # AWS service account secret access key
    aws_secret_access_key: ''
```

Example usage:

```yaml
- uses: actions/ansible-deployment@v1
  with:
    playbook_path: 'playbooks/'
    playbook_name: 'stage.yaml'
    dry_run: true
    aws_region: 'us-east-1'
    ansible_tags: 'system,deployment,nginx,certbot'
    ansible_vault_password: ${{ secrets.ANSIBLE_VAULT_PASSWORD }}
    aws_access_key_id: ${{ vars.AWS_ACCESS_KEY_ID }}
    aws_secret_access_key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```
