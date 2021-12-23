## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
Cybersecurity-Project-1/Diagrams/Network-Map.png
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook files may be used to install only certain pieces of it, such as Filebeat.
Playbooks are located here: Cybersecurity-Project-1/Ansible/roles/
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
- Load balancers protect network security but restricting access to the VMs. Using a “Jump Box” allows the capability of managing the both/all Web servers from a single location. Docker is installed on all Web VMs and the Jump Box VM. An ansible container is used on the Jump Box to manage and configure the VMs. 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system statistics.
Filebeat watches for changes to logs and files.
From elasti.co: Metricbeat collects metrics from your systems and services. From CPU to memory, Redis to NGINX, and much more, Metricbeat is a lightweight way to send system and service statistics.

The configuration details of each machine may be found below.

| Name     | Function   | IP Address                               | Operating System     |
|----------|------------|------------------------------------------|----------------------|
| Jump Box | Gateway    | Public: 168.61.153.182 Private: 10.0.0.4 | Linux (ubuntu 18.04) |
| Web-1    | Web Server | Public: 40.122.77.122 Private: 10.0.0.5  | Linux (ubuntu 18.04) |
| Web-2    | Web Server | Public: 40.122.77.122 Private: 10.0.0.6  | Linux (ubuntu 18.04) |
| ELK      | ELK Server | Public: 52.159.118.113 Private: 10.1.0.4 | Linux (ubuntu 18.04) |

### Access Policies
The machines on the internal network are not exposed to the public Internet. 
Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 73.**.**.***. This is the public IP address provided by ISP. 
Machines within the network can only be accessed by Jump Box. The ELK VM is accessible from the Ansible container on the Jump Box, IP 10.0.0.4. 
A summary of the access policies in place can be found in the table below.
| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 73.**.**.***         |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| ELK      | No                  | 10.0.0.4             |

### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows the user to create multiple instances of the same machine repeatedly, and it allows the user to configure many machines simultaneously, saving time and effort.  
The playbook implements the following tasks:
Configure ELK VM
-Download and install docker.io
-Download and install python
-Install docker python module
-Increase virtual memory
-Download and launch a docker web container
-Enable docker service
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
Cybersecurity-Project-1/Images/ELK-Server.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| VM            | IP Address    |
|---------------|---------------|
| Web-1         | 10.0.0.5      |
| Web-2         | 10.0.0.6      |
These VMs sit behind the load balancer at IP below.  
| Load Balancer | 40.122.77.122 |
We have installed the following Beats on these machines:
-Filebeat 
-Metricbeat 
These Beats allow us to collect the following information from each machine: Filebeat watches for and collects changes to logs and files and metricbeat collects metrics from systems and services. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:
- Copy the Cybersecurity-Project-1/Ansible/roles/install-elk.yml file to /etc/ansible/
- Update the hosts file to include the IP addresses of the [webservers] and [ELK]. This will tell Ansible on which hosts to install ELK, Filebeat, and Metricbeat. 
See Cybersecurity-Project-1/Images/hosts-file-updates.png
- Run the playbook, and navigate to the IP address of your ELK machine to check that the installation worked as expected. This should have been assigned in Azure. 
See Cybersecurity-Project-1/Images/Azure-assigned-ELK-IP
Use ansible-playbook to run playbooks. 
