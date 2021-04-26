## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/SarahDLG/Sarahs-awesome-repo/blob/main/README/Images/network_diagram.jpg "network diagram")

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively,
select portions of the YAML playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _filebeat-playbook.yml_
  - _metricbeat-playbook.yml_

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable, in addition to restricting access to the network. By using a load balancer we protect the availability
of our data by distributing the workload evenly between many servers. This reduces downtime, increases speed, and maximizes performance. In addition to a load balancer we
are also utilizing a Jump Box which adds an additional layer of security as well as allowing the configuration of multiple machines on our network at once.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logfiles and the operating system.

The configuration details of each machine may be found below.


| Name                 | Function   | IP Address | Operating System |
|----------------------|------------|------------|------------------|
| Jump.Box.Provisioner | Gateway    | 10.0.0.4   | Linux            |
| Web-1                | Web Server | 10.0.0.5   | Linux            |
| Web-2                | Web Server | 10.0.0.6   | Linux            |
| ELK-Server           | ELK Server | 10.1.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump.Box.Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:"my home ip address"

Machines within the network can only be accessed by the other machines on the network via the Ansible Docker Containers.
- _Once inside the Ansible Docker Container the ELK Server can be accessed by ssh connection to it's private IP: 10.1.0.4_

A summary of the access policies in place can be found in the table below.

| Name                 | Public Accessible | Allowed IP Address(es) |
|----------------------|-------------------|------------------------|
| Jump.Box.Provisioner | Yes               | My home IP address     |
| Web-1                | No                | 10.0.0.1-254           |
| Web-2                | No                | 10.0.0.1-254           |
| ELK-Server           | No                | 10.0.0.1-254           |



### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because once the yaml playbook is written, 
it can be used multiple times to completely configure other machines in the future with one command. 

The playbook implements the following tasks:
- Install Docker
- Install Python pip3
- Install Docker Python Module
- Allow the use of more memory
- Download and launch the docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text](https://github.com/SarahDLG/Sarahs-awesome-repo/blob/main/README/Images/docker_ps.jpg "docker containers")

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _Web-1 10.0.0.5_
- _Web-2 10.0.0.6_

We have installed the following Beats on these machines:
- _Filebeat_
- _Metricbeat_

Filebeat Filebeat detects changes to the filesystem. Specifically, we use it to collect Apache logs. forwards and places log data in a central location while
Metricbeat collects metrics from the OS and services running on the server.Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH
login attempts, failed sudo escalations, and CPU/RAM statistics.   

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook files to the Ansible control node.
- Update the `/etc/ansible/hosts` file to include the private IP address of your target machine.
- Run the playbook, and navigate to `http://<your elk server IP>:5601/app/kibana#/home?_g=()` to check that the installation worked as expected.
(This may take a few minutes)
