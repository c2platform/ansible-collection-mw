# Ansible Role Apache 2.x

An Ansible Role that installs Apache 2.x on RHEL/CentOS, Debian/Ubuntu, SLES and Solaris.


<!-- MarkdownTOC levels="2,3,4" autolink="true" -->

- [Requirements](#requirements)
- [Role Variables](#role-variables)
  - [Certificates](#certificates)
  - [Files, directories and ACL](#files-directories-and-acl)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)

<!-- /MarkdownTOC -->

## Requirements

<!-- Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required. -->

## Role Variables

<!--  A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well. -->

### Certificates

If you want to use SSL / TLS you can use dict `apache_cacerts2_certificates` in combination with [c2platform.core.cacerts2](https://github.com/c2platform/ansible-collection-core/blob/master/roles/cacerts2).

### Files, directories and ACL

Use dicts `apache_files`, `apache_directories`, `apache_acl` to create / manage any other files, directories and ACL. See [c2platform.core.files](https://github.com/c2platform/ansible-collection-core/tree/master/roles/files) for more information For example see [Backup](#backup).

## Dependencies

<!--   A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles. -->

## Example Playbook

    - hosts: webservers
      vars_files:
        - vars/main.yml
      roles:
        - { role: geerlingguy.apache }

*Inside `vars/main.yml`*:

    apache_listen_port: 8080
    apache_vhosts:
      - {servername: "example.com", documentroot: "/var/www/vhosts/example_com"}

