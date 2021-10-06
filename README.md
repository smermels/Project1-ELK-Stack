## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](Diagrams/Network_Diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the file may be used to install only certain pieces of it, such as Filebeat.

  -[DVWA Playbook](https://github.com/smermels/Project1-ELK-Stack/blob/main/Ansible/DVWAPlaybook.yml.txt)
  
  -[ELK Stack Playbook](https://github.com/smermels/Project1-ELK-Stack/blob/main/Ansible/ELKStackPlaybook.yml.txt)
  
  -[Filebeat Playbook](https://github.com/smermels/Project1-ELK-Stack/blob/main/Ansible/filebeat-playbook.yml.txt)
  
  -[Metricbeat Playbook](https://github.com/smermels/Project1-ELK-Stack/blob/main/Ansible/metricbeat-playbook.yml.txt)
  
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

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.

The configuration details of each machine may be found below.

|         Name         | Function           | Private IP Address | Public IP Address | Operating System |
|:--------------------:|--------------------|--------------------|-------------------|------------------|
| Jump Box Provisioner | Gateway            | 10.0.0.4           | 13.72.80.50       | Ubuntu LTS 18.04 |
| Web-1                | Application Server | 10.0.0.5           | 40.114.125.52     | Ubuntu LTS 18.04 |
| Web-2                | Application Server | 10.0.0.6           | 40.114.125.52     | Ubuntu LTS 18.04 |
| ELK-Stack            | ELK Stack          | 10.1.0.4           | 23.102.108.30     | Ubuntu LTS 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner and ELK Stacks machines can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My Home IP Address

Machines within the network can only be accessed by the Jump Box Privisioner.

A summary of the access policies in place can be found in the table below.

|         Name         | Publicly Accessible | Allowed IP Address |
|:--------------------:|---------------------|--------------------|
| Jump Box Provisioner | Yes                 | My Home IP Address |
| ELK-Stack            | Yes                 | My Home IP Address |
| Web-1                | No                  | 10.0.0.4           |
| Web-2                | No                  | 10.0.0.4           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous becauseit allows a consistent configuration. In addition to consistency, with an automated setup, the ELK stack can be created and configured very quickly.

The playbook implements the following tasks:

  - Configure maximum mapped memory with sysctl module
  
  - Install docker.io and python3-pip packages with apt module
  
  - Install docker python package with pip
  
  - Enable systemd docker service
  
  - Run ELK docker container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](Diagrams/DockerPS.JPG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- Web-1: 10.0.0.5

- Web-2: 10.0.0.6

We have installed the following Beats on these machines:

- Filebeat

- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat parses and forwards system logs from the Web VMs to the ELK Stack in an easy to read format.
- Metricbeat reports system and service statistics about the Web VMs to the ELK stack VM.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ELKStackPlaybook.yml file to /etc/ansible/roles/.
- Update the /etc/ansible/hosts/ file to include the ELK stack VM IP address.
- Run the playbook, and navigate to http://23.102.108.30:5601/app/kibana to check that the installation worked as expected.
