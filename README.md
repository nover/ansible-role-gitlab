# ansible-role-gitlab - gitlab CE server provisioning

An ansible role for provisioning the latest Gitlab CE version on Debian / Ubuntu servers

## Requirements

A modern Ubuntu or Debian server that you wish to install Gitlab CE onto

All server prerequsities are automatically installed by the role

## Role variables

The following variables are currently available while setting up the Gitlab CE installation.

**TODO** 

## Dependencies

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
- hosts: servers
  vars_files:
    - vars/gitlab-server.yml
  roles:
    - { role: nover.gitlab }

```
  
The `vars/gitlab-server.yml` should then contain your settings for the provisioning, like
```
# vars/gitlab-server.yml file
# TODO # 

```
## License

MIT