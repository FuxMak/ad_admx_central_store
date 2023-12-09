# AD-ADMX-Central-Store

Provides a convenient package for the automatic download and deploment of an Microsft Active Directory ADMX Central Store.

## Dependencies / Requirements

Ansible collections:

- name: ansible.windows
- name: community.windows
- name: microsoft.ad

## Installation / Deployment

Issue these commands in order to install this custom role onto your Ansible control node.

### Install collections

```bash
# Required for all distros - Ansible must be installed
ansible-galaxy collection install ansible.windows
ansible-galaxy collection install community.windows
ansible-galaxy collection install microsoft.ad
```

### Install Python WinRM

```bash
# Ubuntu/Debian/etc.
sudo apt-get install gcc python-dev libkrb5-dev
pip install pywinrm

# RedHat/CentOS/etc.
sudo yum install gcc python-devel krb5-devel krb5-workstation python-devel
pip install pywinrm
```

## Role Variables

In order to work with this role some variables are *mandatory* to set, while others have default values.

### Mandatory

- ad_admx_central_store_cleanup: Removes installer and extracted files after import
- ad_admx_central_store_debug_mode: Debug mode for additional (verbose) output
- ad_admx_central_store_domain_name: Fully qualified domain name (FQDN)
- ad_admx_central_store_products: List of products, that are supported with automatic downloads

## Example Playbook

```yaml
---
- name: Create ADMX central store using latest installer files
  hosts:
    - primary_domain_controller
  gather_facts: false
  tasks:
    - name: Run ad_admx_central_store role
      ansible.builtin.include_role:
        name: ad_admx_central_store
      vars:
        ad_admx_central_store_cleanup: true
        ad_admx_central_store_debug_mode: false
        ad_admx_central_store_domain_name: test.domain.local
        ad_admx_central_store_products:
          - "Google Chrome"
```
