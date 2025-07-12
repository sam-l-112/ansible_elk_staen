# elastalert2

* An ansible role for elastalert2.
* Tested with ansible version 2.15.3.

## How to import role

To import "elastalert2" role, use `import_role: name: elastalert2` as shown in the example below:

```
- name: Setup elastalert2
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
        name: elastalert2
      when: service_role is undefined or service_role in ["elastalert2"]
```

## Role variables

```
elastalert2:
  image: ../files/elastalert2.tar
  run_every_minutes: 15
  buffer_time_minutes: 60
  alert_time_limit_days: 2
  # TODO : Delete rule config file after removing rule config in var file
  rules:
    - name: logstash
      type: frequency
      index: "logstash-*"
      config: |
        num_events: 1
        timeframe:
          hours: 1
        filter:
          - query:
              query_string:
                query: '"Accepted publickey for root from"'
        alert:
          - "email"
        attach_related: true
        email:
          - "test@test.org"
```
