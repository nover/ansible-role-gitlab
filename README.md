# ansible-role-gitlab - gitlab CE server provisioning

An ansible role for provisioning the latest Gitlab CE version on Debian / Ubuntu servers

## Requirements

A modern Ubuntu or Debian server that you wish to install Gitlab CE onto

All server prerequsities are automatically installed by the role

## Role variables

The following variables are currently available while setting up the Gitlab CE installation.

### email settings

| Variable | Default | Type | Description |
| --- | --- | --- | --- |
| *gitlab_email_from* | `'gitlab@example.com'` | `string` | The "from" email when gitlab dispatches emails |
| *gitlab_email_display_name* | `'Gitlab example.com'` | `string` | The display name for the emails |
| *gitlab_email_enabled* | `'true'` | `string` | Boolean value (encoded as string) which determines whether email is enabled |
| *gitlab_support_email* | `'gitlab@example.com'` | `string` | The support email for your organization where users can get in contact with the administrators |


### General settings

| Variable | Default | Type | Description |
| --- | --- | --- | --- |
| *gitlab_ssh_host* | `'gitlab.example.com'` | `string` | SSH / push url for your gitlab server - useful of the web-server is running behind a WAF like CloudFlare |
| *gitlab_time_zone* | `'Europe/Copenhagen'` | `string` | Timezone that the gilab server runs in, [allowed values in gitlab documentation](https://docs.gitlab.com/ce/workflow/timezone.html) |

### Gitlab NGINX settings

| Variable | Default | Type | Description |
| --- | --- | --- | --- |
| *gitlab_nginx_external_url* | `'https://gitlab.example.com'` | `string` | The external URL of the gitlab installation |
| *gitlab_nginx_ssl_enable* | `true` | `bool` | Boolean, `false` to disable all SSL config in `gitlab.rb` |
| *gitlab_nginx_redirect_http_to_https* | `'true'` | `string` | String value boolean for whether gitlab should redirect http traffic to https |
| *gitlab_nginx_ssl_certificate* | `'/etc/letsencrypt/live/gitlab.example.com/fullchain.pem'` | `string` | Full path to ssl certificate |
| *gitlab_nginx_ssl_certificate_key* | `'/etc/letsencrypt/live/gitlab.example.com/privkey.pem'` | `string` | Full path to ssl certificate key |
| *gitlab_nginx_custom_server_config* | `'location ^~ /.well-known {\n alias /var/www/letsencrypt/.well-known;\n}\n'` | `string` | Custom value for the NGINX handler, very usefull when using `letsencrypt` for certificate provisioning. Default value is for `letsencrypt` |


### Gitlab container registry NGINX settings

| Variable | Default | Type | Description |
| --- | --- | --- | --- |
| *gitlab_registry_nginx_external_url* | `'https://registry.example.com'` | `string` | The external URL for the Docker Registry |
| *gitlab_registry_nginx_ssl_enable* | `true` | `bool` | Boolean, `false` to disable all SSL config in `gitlab.rb` for the registry |
| *gitlab_registry_nginx_redirect_http_to_https* | `'true'` | `string` | String value boolean for whether gitlab should redirect http traffic to https |
| *gitlab_registry_nginx_ssl_certificate* | `'/etc/letsencrypt/live/gitlab.example.com/fullchain.pem'` | `string` | Full path to ssl certificate for the registry |
| *gitlab_registry_nginx_ssl_certificate_key* | `'/etc/letsencrypt/live/gitlab.example.com/privkey.pem'` | `string` | Full path to ssl certificate key for the registry |
| *gitlab_registry_nginx_custom_server_config* | `'location ^~ /.well-known {\n alias /var/www/letsencrypt/.well-known;\n}\n'` | `string` | Custom value for the NGINX handler, very usefull when using `letsencrypt` for certificate provisioning. Default value is for `letsencrypt` |


### Backup settings

| Variable | Default | Type | Description |
| --- | --- | --- | --- |
| *gitlab_backup_path* | `'/var/opt/gitlab/backups'` | `string` | Path to store backups in  |
| *gitlab_backup_archive_permission* | `'0644'` | `string` | Permissions to store backup files with  |
| *gitlab_backup_keep_time* | `302400` | `int` | Number of seconds to retain backups in the backup path. Default is 3 days  |

## Dependencies

This role does not depend on any other roles.

## Example Playbook

Following is an example on how to use the role in your Playbook. Due to the amount of variables, they are included as a vars file.
```
- hosts: servers
  vars_files:
    - vars/gitlab-server.yml
  roles:
    - { role: nover.gitlab }
```

The `vars/gitlab-server.yml` should then contain your settings for the provisioning. The example given below
will configure for `domain.tld`, disable SSL and define a custom SSH url.

```
# vars/gitlab-server.yml file
##
# email customization
gitlab_email_from: 'you@domain.tld'
gitlab_email_enabled: 'true'

##
# general customization
gitlab_ssh_host: 'push.gitlab.domain.tld'

##
# Primary NGINX
gitlab_nginx_external_url: 'http://gitlab.domain.tld'
# you can also use false here.
gitlab_nginx_ssl_enable: no

##
# Registry NGINX
gitlab_registry_nginx_external_url: 'http://registry.domain.tld'
gitlab_registry_nginx_ssl_enable: no

##
# Backup customization
gitlab_backup_path: '/mnt/vol-gitlab-backup'
# save backups for 7 days
gitlab_backup_keep_time: 604800
```
## License

MIT
