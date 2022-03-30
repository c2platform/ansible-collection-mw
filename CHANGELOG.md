# c2platform.mw CHANGELOG

This file is used to list changes made in each version of the [c2platform.mw](https://github.com/c2platform/ansible-collection-mw) collection.

## 0.1.6 (2022-03-30)

* HAProxy using [c2platform.core.facts](https://github.com/c2platform/ansible-collection-core/tree/master/roles/facts) - configure `haproxy_facts_gather_hosts` `haproxy_facts_filter` to get `haproxy_facts_hosts`.

## 0.1.5 (2022-03-28)

* Fix apache role. Var `common_files_role_name`.

## 0.1.2 (2022-03-08)

* Reusing / integrating [c2platform.core.files](https://github.com/c2platform/ansible-collection-core/blob/master/roles/files) to provide dicts apache_files, apache_directories, apache_acl

## 0.1.0 (2022-02-14)

* initial role
