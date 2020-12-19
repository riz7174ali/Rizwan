# Rizwan
My repository to upload my all Project Work

### Your network diagram.

Network Diagram:


 
Initiated live ELK deployment on Azure which is depicted in the above diagram. Alternatively, select portions of the playbook files used to install Filebeat, etc..
filebeat-playbook.yml
This document contains the following details with all the screenshots:
•	Description of the Topology
•	Access Policies
•	ELK Configuration
•	How to Use the Ansible Build
Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
•	Load balancers protect the servers from a denial of service attack. A load balancer distributes traffic amongst the servers. One benefit of using a jump box is that it protects your virtual machines from publix exposure.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system performance.
•	log files monitored by Filebeat

All the VM environment with JumpBox and connected VM’s.

 

VM’s their IP’s and the OS installed as per below - 

Name	Type	IP Address	OS Installed
JumpBox	Gateway	10.0.0.4	Ubuntu 18.04
Web1	VM	10.0.0.5	Ubuntu 18.04
Web2	VM	10.0.0.6	Ubuntu 18.04
DVWA	VM	10.0.0.7	Ubuntu 18.04
ELK-Server	VM	10.1.0.4	Ubuntu 18.04
			

Access Policies
None of the VM’s are exposed to the public Internet, and only the JumpBox VM can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
•	20.64.170.5
Machines within the network can only be accessed on Port 22.
•	10.1.0.4
A summary of the access policies in place can be found in the table below.
VM	External Access	Configured IP’s
JumpBox	No	20.64.170.5
DVWA	No	10.0.0.7
Elk-Stack	No	10.1.0.4

 
Evidence JumpBox accessing Web1 & Web2:

 
 

Virtual Network setup for the VM’s

 
Elk Configuration
ELK machine was auto-configured using Ansible through cmd line. 
Below tasks were implemented:
•	Change the memory on the ELK VM
•	Install docker.io
•	Install python-pip
•	Install docker python module
•	Download and launch a docker elk stack
Screenshot displaying the result of running Docker post configuring the ELK instance.
 

Deploying the Playbook
In order to use the playbook, user need to have an Ansible control node pre-configured. 
SSH into the control node and follow the steps below:
•	Copy the Filebeat-configuration.yml file to the ELK VM.
•	Update the hosts file to include webservers 10.0.0.5, 10.0.0.6, 10.0.0.7
•	Run the playbook, and navigate to Kibana to check that the installation worked as expected.
Elk Screenshots - 
 
Load balancer to manage the traffic:

 

Network Interfaces for the VM environment

 

Elk playbook

---
- name: Configure Elk VM with Docker
  hosts: elkservers
  remote_user: RedAdmin
  become: true
  tasks:
    # Use apt module
    - name: Install docker.io
      apt:
        update_cache: yes
        name: docker.io
        state: present

      # Use apt module
    - name: Install pip3
      apt:
        force_apt_get: yes
        name: python3-pip
        state: present

      # Use pip module
    - name: Install Docker python module
      pip:
        name: docker
        state: present

      # Use sysctl module
 

Pentest.yml Playbook:
---
- name: Config Web VM with Docker
  hosts: webservers
  become: true
  tasks:
  - name: docker.io
    apt:
      force_apt_get: yes
      update_cache: yes
      name: docker.io
      state: present

  - name: Install pip3
    apt:
      force_apt_get: yes
      name: python3-pip
      state: present

  - name: Install Docker python module
    pip:
      name: docker
      state: present

  - name: download and launch a docker web container
    docker_container:
      name: dvwa
      image: cyberxsecurity/dvwa

 



### description of the deployment.
### Tables specifying access policies and network addresses.
### A description of the investigation you completed using Kibana.
### Usage instructions.
