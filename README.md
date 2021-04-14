# ans-collect-output
This module collects various outputs and puts them into respective files.

Since most of the devices supported by BSC are Nexus, examples are based on NXOS.

## Structure

### tasks folder
This folder is unlikely to be changed. It has all necessary files for this modules to work.

### templates folder
This folder has only one Jinja template that provides a structure for the output file.

## Usage
In order to collect any outputs, the following parameters must be specified:
 - inventory file
 - file with configuration data (aci_env_var_config)

The inventory folder is set as ansible.cfg parameter.

Configuration data are specified with as extra vars - ```-e``` option. This repo has an example of such file with all necessary variables mentions.

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

For whole playbook execution use:
ansible-playbook aci_playbook.yml -e @aci_env_var_config.yml

For partial playbook execution use:
ansible-playbook aci_playbook.yml -e @aci_env_var_config.yml --tags bd