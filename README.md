# cdservice
Simple Continous Delivery service based on Jenkins with authentication supported by Keycloak

Role Name
=========

This is the example of simple Continous Delivery service based on Jenkins with authentication supported by Keycloak. 

Requirements
------------

The playbooks were tested on Fedora Linux 42 stable release and Ubuntu Noble LSB release

Playbooks do not include the configuration of Keycloak, Jenkins which can be done manually from the UI.

Role Variables
--------------

- ansible.cfg				- includes collections_path, inventory, remote_user
- inventory/hosts				- includes the target remote hosts
- roles/cicdpipeline/vars/main.yml	- includes configuration of dependencies
- roles/cicdpipeline/vars/certs.yml	- includes ssl certificates deployed on proxy
- roles/cicdpipeline/vars/secrets.yml 	- includes all secrets

Dependencies
------------

Tested on the following version of software:

- ansible_version: 2.20.3
- jenkins_version: stable-2.528
- jenkins_worker_version: "latest"
- nginx_version: "1.25.5"
- openssl_version: "1.1.1w"
- pcre_version: "8.45"
- zlib_version: "1.3.2"
- ubuntu_version: "24.04"
- keycloak_version: quay.io/keycloak/keycloak:26.3.5
- maven_version: "3.9-eclipse-temurin-21"
- eclipse_temurin_version: "21-jre"
- postgres_kclk_version: quay.io/sclorg/postgresql-16-c10s

Example Playbook
----------------

Generation of self-signed certificates:

>	ansible-playbook roles/cicdpipeline/tasks/execute-CA-setup.yml -J

The certificates will be available using command:

>	ansible-vault view roles/cicdpipeline/vars/certs.yml -J

Deployment of docker services:

>	ansible-playbook roles/cicdpipeline/tasks/deploy.yml -e "target_hosts=test" -J -K

Start of the services:

>	ansible-playbook roles/cicdpipeline/tasks/services_network_up.yml -e "target_hosts=test" -J -K

Stop of the services:

>	ansible-playbook roles/cicdpipeline/tasks/services_network_down.yml -e "target_hosts=test" -J -K

License
-------

AI Disclosure & Ownership

This repository contains Ansible playbooks and Bash scripts developed with the assistance of Google Gemini.

Refinement: All code has been manually reviewed, edited, and tested in a lab environment by Mariusz Bujak to ensure functional accuracy and security.

Ownership: As the human orchestrator and tester, I claim copyright over this specific implementation and license it under the terms of the GPLv3.

Dependencies

This project utilizes Docker images hosted on Quay.io and Docker Hub. Users of these playbooks are responsible for complying with the individual licenses of the software contained within those images

Author Information
------------------

Mariusz Bujak

e-mail: hang.mbujak@gmail.com
