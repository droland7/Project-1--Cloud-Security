# Project-1--Cloud-Security

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/droland7/Project-1--Cloud-Security/blob/main/Diagrams/Diagram_ELK_Stack_Network.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  -Ansible-Playbook-Yaml, Filebeat-Playbook-Yaml, Metricbeat-Playbook-Yaml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load balancers help protect the webservers from denial of services attacks by diverting and evenly distributing traffic between the servers. The advantage of the jump box is it is the sole controlled access point for the webservers. The jump box holds the applications that are used to run and manage the servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system metrics.
- Filebeat watches for changes in the files and then collects and sends the data to logstash/elasticsearch.
- Metricbeat collects the metric data from the services and the operating system and sends it to logstash/elasticsearch

The configuration details of each machine may be found below.

| Name     | Function | IP Address private/public | Operating System    |
|----------|----------|---------------------------|---------------------|
| Jump Box | Gateway  | 10.0.2.4 / 168.62.49.14   | Linux (Ubuntu 18.04)|
| WEB-1    | Server   | 10.0.0.5 / 20.121.212.218 | Linux (Ubuntu 18.04)|
| WEB-2    | Server   | 10.0.0.6 / 20.121.212.218 | Linux (Ubuntu 18.04)|
| ELK      | Server   | 10.1.0.4 / 104.43.167.199 | Linux (Ubuntu 18.04)|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My Public IP address

Machines within the network can only be accessed by the Jumpbox.
- Jumpbox 10.0.2.4 via SSH

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | My Public IP via SSH |
| Web-1    | No                  | Jumpbox 10.0.2.4     |
| Web-2    | No                  | Jumpbox 10.0.2.4     |
| ELK      | No                  | Jumpbox 10.0.2.4     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Running an Ansible playbook allows us to expedite the process of provisioning new VM's with same configuration settings and it saves time. 

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install docker module
- Increase memory
- Download and launch docker elk container and enable service on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/droland7/Project-1--Cloud-Security/blob/main/Diagrams/ELK_Docker_PS_Output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat watches for changes in the files and then collects and sends the data to logstash/elasticsearch.
- Metricbeat collects the metric data from the services and the operating system and sends it to logstash/elasticsearch

### Using the Playbook
In order to use the playbooks, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml and metricbeat-playbook.yml files to /etc/ansible/roles.
- Update the /etc/ansible/hosts file to include the IP addresses of the virtual machaines under the webservers section.
- Run  the  playbooks and go to http://104.43.167.199:5601/app/kibana to checked that the installation worked as expected.
