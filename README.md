# Ansible role: AWS VPC

This role handles the creation of AWS VPC's

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc)
[![Version](https://img.shields.io/github/tag/Flaconi/ansible-role-aws-vpc.svg)](https://github.com/Flaconi/ansible-role-aws-vpc/tags)
[![Ansible Galaxy](https://img.shields.io/ansible/role/d/25919.svg)](https://galaxy.ansible.com/Flaconi/aws-vpc/)

## Requirements

* Ansible 2.5
* [botocore](https://pypi.org/project/botocore/)
* [boto3](https://pypi.org/project/boto3/)


## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable                 | Description                  |
|--------------------------|------------------------------|
| `aws_vpc_profile`        | Boto profile name to be used |
| `aws_vpc_default_region` | Default region to use        |


## Example definition

#### Required parameter only

```yml
aws_vpc_vpcs:
  - name: my-vpc-1
    cidr: 172.28.0.0/16
  - name: my-vpc-2
    cidr: 172.29.0.0/16
```

#### All available parameter
```yml
aws_vpc_vpcs:
  - name: my-vpc-1
    cidr: 172.28.0.0/16
    # Optional
    region: eu-central-1
    tags:
      - key: env
        val: development
      - key: department
        val: infra
  - name: my-vpc-2
    cidr: 172.29.0.0/16
    # Optional
    region: eu-central-1
    tags:
      - key: env
        val: production
      - key: department
        val: devops
```

#### Variablized tags

```yml
my_key: env
my_val: staging

aws_vpc_vpcs:
  - name: my-vpc-1
    cidr: 172.28.0.0/16
    # Optional
    region: eu-central-1
    tags:
      - key: "{{ my_key }}"
        val: "{{ my_val }}"
```


## Testing

#### Requirements

* Docker
* [yamllint](https://github.com/adrienverge/yamllint)

#### Run tests

```bash
# Lint the source files
make lint

# Run integration tests with default Ansible version
make test

# Run integration tests with custom Ansible version
make test ANSIBLE_VERSION=2.4
```
