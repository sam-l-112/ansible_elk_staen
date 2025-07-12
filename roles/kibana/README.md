# kibana

* An ansible role for kibana.
* Tested with ansible version 2.15.3.

## How to import role

To import "kibana" role, use `import_role: name: kibana` as shown in the example below:

```
- name: Setup kibana
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
        name: kibana
      when: service_role is undefined or service_role in ["kibana"]
```




## Role variables


```
# Example: Disable https

syslog_global:
  cluster_group: "v1701_elk"

kibana:
  image: ../files/kibana.tar
  haproxy:
    users:
      - name: "admin"
        password: "password"
```

```
# Example: Enable https

syslog_global:
  cluster_group: "v1701_elk"

kibana:
  image: ../files/kibana.tar
  haproxy:
    # global.ssl.public
    ssl_type: "public"
    users:
      - name: "admin"
        password: "password"
```

* `vars/main.yml` SSL Example
```
global:
  ssl:
    # Public ssl location (PEM format)
    public:
      location: files/public_ssl/example.com.pem
      domain: example.com

    # Private ssl location (PEM format)
    private:
      location: files/private_ssl/infra.pem
      ca: files/private_ssl/infra.crt
      domain: infra
```
