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

  play #1 (apic): PLAYBOOK >> ENSURE APPLICATION CONFIGURATION EXISTS	TAGS: []
    tasks:
      CHECK >> Error checking and log setup	TAGS: [apic]
      TASK >> ENSURE APPLICATIONS TENANT EXISTS	TAGS: [app, bd, contract, epg, filter, tenant, vrf]
      TASK >> ENSURE TENANT VRF EXISTS	TAGS: [bd, vrf]
      TASK >> ENSURE TENANT BRIDGE DOMAINS EXISTS	TAGS: [bd]
      TASK >> ENSURE BRIDGE DOMAINS HAVE SUBNETS	TAGS: [bd]
      TASK >> ENSURE TENANT FILTERS EXIST	TAGS: [contract, filter]
      TASK >> ENSURE FILTERS HAVE ENTRIES	TAGS: [contract, filter]
      TASK >> ENSURE TENANT CONTRACTS EXIST	TAGS: [contract]
      TASK >> ENSURE CONTRACTS HAVE CONTRACT SUBJECTS	TAGS: [contract]
      TASK >> ENSURE CONTRACT SUBJECTS HAVE FILTERS	TAGS: [contract]
      TASK >> ENSURE APPLICATION EXISTS	TAGS: [app, epg]
      TASK >> ENSURE APPLICATION EPGS EXISTS	TAGS: [epg]
      TASK >> ENSURE DOMAIN IS BOUND TO EPG	TAGS: [epg]
      TASK >> ENSURE EPGS HAVE CONTRACTS	TAGS: [epg]
```

For whole playbook execution use:
```ansible-playbook aci_playbook.yml -e @aci_env_var_config.yml```

For partial playbook execution use:
```ansible-playbook aci_playbook.yml -e @aci_env_var_config.yml --tags bd```
