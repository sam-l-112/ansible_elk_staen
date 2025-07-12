# logstash

* An ansible role for logstash.
* Tested with ansible version 2.15.3.

## How to import role

To import "logstash" role, use `import_role: name: logstash` as shown in the example below:

```
- name: Setup logstash
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
        name: logstash
      when: service_role is undefined or service_role in ["logstash"]
```



## Role variables

```
syslog_global:
  cluster_group: "v1701_elk"

logstash:
  image: ../files/logstash.tar
  containers:
    - name: syslog
      port: 15001
      type: syslog
      mem_gb: 1
      filter: |
    - name: beats
      port: 15002
      type: beats
      mem_gb: 1
      filter: |
  log_forwarding: |

  
```
