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
| *gitlab_nginx_external_url* | `'https://gitlab.example.com'` | `string` | desc |
| *gitlab_nginx_ssl_enable* | `true` | `bool` | Boolean, `false` to disable all SSL config in `gitlab.rb` |
| *gitlab_nginx_redirect_http_to_https* | `'true'` | `string` | String value boolean for whether gitlab should redirect http traffic to https |
| *gitlab_nginx_ssl_certificate* | `'/etc/letsencrypt/live/gitlab.example.com/fullchain.pem'` | `string` | Full path to ssl certificate |
| *gitlab_nginx_ssl_certificate_key* | `'/etc/letsencrypt/live/gitlab.example.com/privkey.pem'` | `string` | Full path to ssl certificate key |
| *gitlab_nginx_custom_server_config* | `'location ^~ /.well-known {\n alias /var/www/letsencrypt/.well-known;\n}\n'` | `string` | Custom value for the NGINX handler, very usefull when using `letsencrypt` for certificate provisioning. Default value is for `letsencrypt` |


### Gitlab container registry NGINX settings


### Backup settings


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