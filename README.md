# ansible_aws_security_groups
Ansible role to manage aws security groups fully configured from variables

For more detailed on information on the creating EC2 Security Groups with Ansible see the offical documentation for that module: http://docs.ansible.com/ansible/ec2_group_module.html.

Role Variables
--------------
```
aws_access_key - optional if boto is used
aws_secret_key - optional if boto is used
region - mandatory
vpcid - mandatory
aws_security_groups:
  - name: - mandatory
    description: - mandatory
    in_rules: - mandatory
      - proto: - mandatory
        from_port:  - mandatory
        to_port: - mandatory
        cidr_ip: or group_id: - mandatory
    out_rules: - optional, will default to all from 0.0.0.0/0
```        
        
This role will purge all security groups not present in the variables, so to remove a security group or rule just remove it from the variables


Variables example:
--------------
```
aws_access_key: ufaggufaguafsiugademo
aws_secret_key: ha7t6agsgfasjfgasygfasugfiasufdemo
region: eu-west-1
vpcid: vpc_124567
aws_security_groups:
  - name: ssh
    description: ssh security group
    in_rules:
      - proto: tcp
        from_port: 22
        to_port: 22
        cird_ip: 10.0.0.0/24
  - name: mysql
    description: mysql connections
    in_rules:
      - proto: tcp
        from_port: 3306
        to_port: 3306
        group_id: sg_fs352t5
    out_rules:
      - proto: all
        cidr_ip: 10.0.0.0/16
        
```
