# Ansible Role HAProxy

Installs HAProxy on RedHat/CentOS 7 and Debian servers.

**Note**: Currently it is assumed that for RedHat based systems install HAProxy _from source_ because no-up-date haproxy packages exists for CentOS 7. This way you can install any version you like. Ubuntu does have off a supported `haproxy` package so Debian based system use package install. Of course these defaults can be changed

```yaml
haproxy_install_type:
  RedHat: source
  Debian: package
```

<!-- MarkdownTOC levels="2,3" autolink="true" -->

- [Requirements](#requirements)
- [Role Variables](#role-variables)
- [Dependencies](#dependencies)
- [Example configuration](#example-configuration)

<!-- /MarkdownTOC -->

## Requirements

<!-- Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required. -->

None.

## Role Variables

<!--  A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well. -->

Available variables are listed below, along with default values (see `defaults/main.yml`):

    haproxy_socket: /var/lib/haproxy/stats

The socket through which HAProxy can communicate (for admin purposes or statistics). To disable/remove this directive, set `haproxy_socket: ''` (an empty string).

    haproxy_chroot: /var/lib/haproxy

The jail directory where chroot() will be performed before dropping privileges. To disable/remove this directive, set `haproxy_chroot: ''` (an empty string). Only change this if you know what you're doing!

    haproxy_user: haproxy
    haproxy_group: haproxy

The user and group under which HAProxy should run. Only change this if you know what you're doing!

Use `haproxy_frontends` to configure frontends and `haproxy_backends` to configure the backends. See example below.

    haproxy_global_vars:
      - 'ssl-default-bind-ciphers ABCD+KLMJ:...'
      - 'ssl-default-bind-options no-sslv3'

A list of extra global variables to add to the global configuration section inside `haproxy.cfg`.

To create certificates you might consider using [cacerts2](https://github.com/c2platform/ansible-collection-core/tree/master/roles/cacerts2) from Ansible collection [c2platform.core](https://galaxy.ansible.com/c2platform/core). You would then use dict `haproxy_cacerts2_certificates` for example as follows:

```yaml
---
haproxy_cacerts2_certificates:
  - common_name: ok
    subject_alt_name:
    - "DNS:example.com"
    - "DNS:*.example.com"
    - "DNS:{{ ansible_hostname }}"
    - "DNS:{{ ansible_fqdn }}"
    - "IP:{{ hostvars[inventory_hostname]['ansible_host'] }}"
    ansible_group: haproxy
    deploy:
      pem:
        dir: /etc/haproxy/conf
        owner: www-data
        group: www-data
        mode: '640'
```

## Dependencies

<!--   A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles. -->

1. Ansible collection [c2platform.core](https://galaxy.ansible.com/c2platform/core) 0.1.4

## Example configuration

<!--   Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too: -->

The example config below configures the following
1. Redirect all traffic from 80 to 443.
2. SSL passthrough of all traffic on 443 to reverse proxy 1.1.1.2:443.
3. SSH passthrough of traffic on 7999 to Bitbucket SSH.

```yaml
---
haproxy_config:
  frontend:
    http: |
      bind 0.0.0.0:80 name 0.0.0.0:80
      mode http
      log global
      option http-keep-alive
      timeout client 30000
      default_backend redirect_http_https
    https: |
      bind *:443
      mode tcp
      default_backend rproxies
    bitbucket: |
      bind *:7999
      mode tcp
      default_backend bitbucket
  backend:
    redirect_http_https: |
      mode http
      timeout connect 30000
      timeout server 30000
      retries 3
      option httpchk
      redirect scheme https code 301
    rproxies: |
      mode tcp
      server proxy 1.1.1.2:443
    bitbucket: |
      mode tcp
      server proxy 1.1.1.4:7999
```
