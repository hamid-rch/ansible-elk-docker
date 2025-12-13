# ansible-elk

Ansible role to deploy the ELK stack (Elasticsearch 9.2.2, Logstash 9.2.2, Kibana 9.2.2) and Elastic Agent (8.16.0) using Docker Compose on Ubuntu 24.04.

## Prerequisites

- Ubuntu 24.04
- Docker & Docker Compose installed
- Ansible 2.19.4

## RUN
```
ansible-playbook -i inventory/hosts playbooks/site.yml
```
