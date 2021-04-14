# ans-aci
This module for configuration ACI fabric via Ansible.


## Structure

### group_vars folder
This folder contains group_vars yml file

### tasks folder
This folder contains tasks per ACI object.

### inventory folder
This folder contains inventory file.
The inventory folder is set as ansible.cfg parameter.

## Usage
In order to start playbook, the following parameters must be specified:
 - file with configuration data (aci_env_var_config)

Configuration data are specified with as extra vars - ```-e``` option. This repo has an example of such file with all necessary variables mentions.

```python
ansible-playbook aci_playbook.yml --list-tasks

playbook: aci_playbook.yml

  play #1 (apic): ENSURE APPLICATION CONFIGURATION EXISTS	TAGS: []
    tasks:
      INCLUDE >> Error checking and log setup	TAGS: [apic]
      INCLUDE >> ENSURE APPLICATIONS TENANT EXISTS	TAGS: [app, bd, contract, epg, filter, tenant, vrf]
      INCLUDE >> ENSURE TENANT VRF EXISTS	TAGS: [bd, vrf]
      INCLUDE >> ENSURE TENANT BRIDGE DOMAINS EXISTS	TAGS: [bd]
      INCLUDE >> ENSURE BRIDGE DOMAINS HAVE SUBNETS	TAGS: [bd]
      INCLUDE >> ENSURE TENANT FILTERS EXIST	TAGS: [contract, filter]
      INCLUDE >> ENSURE FILTERS HAVE ENTRIES	TAGS: [contract, filter]
      INCLUDE >> ENSURE TENANT CONTRACTS EXIST	TAGS: [contract]
      INCLUDE >> ENSURE CONTRACTS HAVE CONTRACT SUBJECTS	TAGS: [contract]
      INCLUDE >> ENSURE CONTRACT SUBJECTS HAVE FILTERS	TAGS: [contract]
      INCLUDE >> ENSURE APPLICATION EXISTS	TAGS: [app, epg]
      INCLUDE >> ENSURE APPLICATION EPGS EXISTS	TAGS: [epg]
      INCLUDE >> ENSURE DOMAIN IS BOUND TO EPG	TAGS: [epg]
      INCLUDE >> ENSURE EPGS HAVE CONTRACTS	TAGS: [epg]
```

For whole playbook execution use:
```ansible-playbook aci_playbook.yml -e @aci_env_var_config.yml```

For partial playbook execution use:
```ansible-playbook aci_playbook.yml -e @aci_env_var_config.yml --tags bd```
