## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/ckellermusic/CK_Cyber_Security/blob/master/Diagrams/Screen%20Shot%202020-07-31%20at%208.07.32%20PM.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting traffic to the network.
- Security load balacers prevent an organization from a DDoS attack. The advantage of a jump box is the first place the admin can commect before launching any other administrative tasks and use it as a origination point to connect to other servers or untrusted environments. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the applications and system logs.
- FIlebeat monitors changes to log files and forwards them to the ELK stack.
- Metricbeat records metrics from the operating system and services running on the servers.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function   | IP Address | Operating System     |
| -------- | ---------- | ---------- | -------------------- |
| Jump Box | Gateway    | 10.0.0.4   | Linux (ubuntu 18.04) |
| Web-1    | Web Server | 10.0.0.7   | Linux (ubuntu 18.04) |
| Web-2    | Web Server | 10.0.0.6   | Linux (ubuntu 18.04) |
| ELKVM    | Elk Stack  | 10.1.0.5   | Linux (ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 98.211.47.165

Machines within the network can only be accessed by _____.
- JumpBox-Provisioner 52.175.197.53, 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible | Allowed IP Addresses |
| ------------------- | ------------------- | -------------------- |
| JumpBox-Provisioner | yes                 | 98.211.47.165        |
| Web-1               | no                  | 10.0.0.4             |
| Web-2               | no                  | 10.0.0.4             |
| ELKVM               | no                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible automates and simplifies repetitive, complex, and tedious operations. It is to use one playbook to update all machines. 

The playbook implements the following tasks:
- Install docker.io

  - the Docker engine. Used for running containers

- Install python-3-pip

  - package used to install Python3 software

- Install Docker Module

  - Installs the Docker module

- Increase Virtual Memory

  - system control command to increase memory to 262144
  - sysctl -w vm.max_map_count=262144

- Use More Memory

  - sysctl commands:

    - name: vm.max_map_count

      ​    value: '262144'

      ​    sysctl_file: /etc/sysctl.conf

      ​    state: present

      ​    reload: yes

- Download and launch a docker elk container

  - Downloads the Docker container called sebp/elk:761
    - sebp: organization that made the container
    - Elk: container
    - 761: version

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/ckellermusic/CK_Cyber_Security/blob/master/Screen_shots/Screen%20Shot%202020-07-23%20at%207.33.22%20PM.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.7, Web-2: 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- FIlebeat monitors changes to log files and forwards them to the ELK stack. I expect it to see log data in JSON format.
- Metricbeat records metrics from the operating system and services running on the servers. I expect to see metric data from CPU and memory.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Ansible host file to /etc/ansible.
- Update the Host file to include private IP addresses of web servers and ELK servers
- Run the playbook, and navigate to http://104.208.217.146:5601/app/kibanato check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

- _Which URL do you navigate to in order to check that the ELK server is running?

  ​	ELK VM Pub IP: http://104.208.217.146:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._