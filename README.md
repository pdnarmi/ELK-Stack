## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

**Note**: The following image link needs to be updated. Replace `diagram_filename.png` with the name of your diagram image file.  

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  elkStack/ansible/

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting attacks to the network.
If a server is offline, due to an attack or maintenance, services will still be available uninterupted. 

Using a Jump Box allows for the advantage of creating a single, secured access point to the virtual network via an SSH connection and also serves as a Secure Administrator Workstation (SAW), allowing an admin to make changes to machines on the network (Web-1 and Web-2) using an Ansible container to run various install playbooks written in YAML (Y'all Ain't Markup Language). However, it should be noted that if the Jump Box were to be compromised, no other machines are currently configured to make access or make changes to any machines on the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

Filebeat: A software that monitors log files, collects log events, and forwards them to Logstash or Elastisearch to be indexed.
Metricbeat

The configuration details of each machine may be found below.


| Name     | Function  | IP Address | Operating System |
|----------|---------- |------------|------------------|
| Jump Box | Gateway   |    10.0.0.4| Linux            |
|          |           | 20.55.8.198|                  |
| Web-1    | Server    |    10.0.0.5| Linux            |
| Web-2    | Server    |    10.0.0.6| Linux            |
| Elk-Box  | Monitoring|    10.0.0.7| Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

24.88.35.17: Public IP of my personal workstation

Machines within the network can only be accessed by the Jump-Box-Provisioner.

The Elk machine is accessible via SSH from the Jump-Box at 10.0.0.4 AND is also accessible for HTTP connections on Port 5601 from my personal workstation at 24.88.35.17

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses    |
|----------|---------------------|-------------------------|
| Jump Box | Yes                 |              |
| Web-1    | No                  | 10.0.0.4                |
| Web-2    | No                  | 10.0.0.4                |
| Elk Box  | No                  | 10.0.0.4|    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:

-Install docker.io
-Install python3-pip
-Install docker via pip
-Increase virtual memory
-Use more memory
-Download and launch docker elk container: Starts container and establishes ports used

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

**Note**: The following image link needs to be updated. Replace `docker_ps_output.png` with the name of your screenshot image file.  


![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

|Name  |Ip Address  |
|------|------------|
|Web-1 |    10.0.0.5|
|Web-2 |    10.0.0.6|

We have installed the following Beats on these machines:

-Filebeat
-Metricbeat

|Name  |Ip Address  |
|------|------------|
|Web-1 |    10.0.0.5|
|Web-2 |    10.0.0.6|
|ElkBox|    10.0.0.7|

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

-Filebeat: The Elastisearch Filebeat module can handle audit logs, deprecation logs, gc logs, server logs, and slow logs. These logs are then available via Kibana in the browser for analysis.
-Metricbeat: Collects metric data, such as OS metrics like CPU or memory, or data related to services running on a server. It can also be used to monitor other beats and the ELK stack itself

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to the Ansible directory.
- Update the host file to include the webserver and ELK IP addresses
- Run the playbook, and navigate to Kibana to check that the installation worked as expected. http://VM.I.P.Address:5601/app/kibana
