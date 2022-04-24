# Ansible Role docker

This role provides dicts that can be used to create Docker resources using [community.docker](https://docs.ansible.com/ansible/latest/collections/community/docker/index.html) Ansible collection

<!-- MarkdownTOC levels="2,3" autolink="true" -->

- [Requirements](#requirements)
- [Role Variables](#role-variables)
  - [docker_networks](#docker_networks)
  - [docker_images](#docker_images)
  - [docker_containers](#docker_containers)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)

<!-- /MarkdownTOC -->

## Requirements

<!-- Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required. -->



## Role Variables

<!--  A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well. -->

### docker_networks

```yaml
docker_networks:
  - name: network_one
    connected:
      - container_a
      - container_b
      - container_c
```

See [docker_network module](https://docs.ansible.com/ansible/latest/collections/community/docker/docker_network_module.html#ansible-collections-community-docker-docker-network-module)

### docker_images

```yaml
docker_images:
  - name: pacur/centos-7
    source: pull
    # Select platform for pulling. If not specified, will pull whatever docker prefers.
    pull:
      platform: amd64
```

See [docker_image module](https://docs.ansible.com/ansible/latest/collections/community/docker/docker_image_module.html#ansible-collections-community-docker-docker-image-module)

### docker_containers

```yaml
docker_images:
  - name: mydata
    image: busybox
    volumes:
      - /data
```

See [docker_container module](https://docs.ansible.com/ansible/latest/collections/community/docker/docker_container_module.html#ansible-collections-community-docker-docker-container-module)


## Dependencies

<!--   A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles. -->

## Example Playbook

<!--   Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too: -->

```yaml
    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }
```