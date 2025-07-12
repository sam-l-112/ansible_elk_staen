# elasticsearch

* An ansible role for elasticsearch.
* Tested with ansible version 2.15.3.

## How to import role

To import "elasticsearch" role, use `import_role: name: elasticsearch` as shown in the example below:

```
- name: Setup elasticsearch
  hosts: <host_group>
  gather_facts: no
  become: yes
  become_user: root
  tasks:
    - block:
        - setup:
        - service_facts:
        - include_vars: '{{ item }}'
          with_items:
            - vars/<var_file>
    - import_role:
        name: elasticsearch
      when: service_role is undefined or service_role in ["elasticsearch"]
```




## Role variables

```
syslog_global:
  cluster_group: "v1701_elk"

elasticsearch:
  image: ../files/elasticsearch.tar
  data_disk: vdb
  cluster_name: syslog
  containers:
    - { name: "syslog-master", role: "master,ingest", http_port: "9200", transport_port: "9300" }
    - { name: "syslog-data-1", role: "data", http_port: "9201", transport_port: "9301" }
    - { name: "syslog-data-2", role: "data", http_port: "9202", transport_port: "9302" }
```
