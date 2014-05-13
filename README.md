EC2 AMI
========

Creates an image from a running instance on AWS.  This role is 3 of 3 parts.  Although, the roles can be used individually they were developed to use together for the most effective ec2 provisioning.

######This ec2 role was broken off of the ansible example and tailored for organizational purposes.

```
# fetch instance data from the metadata servers in ec2
- ec2_facts:

# show all known facts for this host
- debug: var=hostvars[inventory_hostname]

# just show the instance-id
- debug:
    msg: "{{ hostvars[inventory_hostname]['ansible_ec2_instance-id'] }}"

- name: Creating {{ app_name }} AMI
  ec2_ami:
    aws_access_key: "{{ ec2_access_key }}"
    aws_secret_key: "{{ ec2_secret_key }}"
    region: "{{ region }}"
    description: "{{ ami_description }}"
    instance_id: "{{ hostvars[inventory_hostname]['ansible_ec2_instance-id'] }}"
    wait: yes
    name: "{{ ami_name }}"
    state: present
```

Requirements
-----------
boto

Role Variables
-----------
* image
* instance_type
* ec2_access_key
* ec2_secret_key
* keypair
* instance_tag
* region
* group
* app_name
* server_env

Dependencies
-----------
Note: Not dependencies but developed together.
* ec2_group
* ec2_ami

License
-----------
MIT