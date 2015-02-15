# Simple proxy with authentication

## Configuration

Add a file `ansible_extra_vars.yml` with the following contents:

```YAML
---

# for local execution
listen_port: <port the proxy should listen on (e.g. 8080)>
basic_auth_user: <some user to be used for authentication>
basic_auth_password: <some password to use for authentication>

# for AWS execution
region: <an aws region (e.g. us-west-2)>
ec2_key_name: <an ssh key pair present in that region>
```

## Runnig locally

```bash
vagrant provision
```

## Running in AWS

```
export AWS_ACCESS_KEY=<an access key with rights to launch create security groups and launch ec2 instances>
export AWS_SECRET_KEY=<the belonging secret key>

ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook --extra-vars='@ansible_extra_vars.yml' -ilocalhost, provisioning/site.yml
```

## Updating in AWS

Set up the ec2 inventory script as described [here](http://docs.ansible.com/intro_dynamic_inventory.html#example-aws-ec2-external-inventory-script).

```
export AWS_ACCESS_KEY=<an access key with rights to launch create security groups and launch ec2 instances>
export AWS_SECRET_KEY=<the belonging secret key>

ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook --extra-vars='@ansible_extra_vars.yml' -u ubuntu -i ~/src/ansible/plugins/inventory/ec2.py provisioning/node.yml
```
