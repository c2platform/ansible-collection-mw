# Ansible Role Apache Reverse Proxy

A brief description of the role goes here.

<!-- MarkdownTOC levels="2,3" autolink="true" -->

- [Requirements](#requirements)
- [Role Variables](#role-variables)
  - [Static files](#static-files)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)

<!-- /MarkdownTOC -->

## Requirements

<!-- Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required. -->

## Role Variables

<!--  A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well. -->

### Static files

Create static files e.g. custom index.html or favicon.ico using `reverse_proxy_static_files` list var.

From `content` attribute

```yaml
reverse_proxy_static_files:
  - path: /var/www/html/index.html
    content: |
      <html>
      <header><title>This is title</title></header>
      <body>
      Hello world
      </body>
      </html>
```
or from a download

```yaml
reverse_proxy_static_files:
  - dest: /var/www/html/index.html
    url: file:///vagrant/downloads/index.html
```
Other optional attributes are `checksum`, `owner` and `group`. The last two default to `www-data`.  

## Dependencies

<!--   A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles. -->

## Example Playbook

<!--   Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too: -->

```yaml
    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }
```