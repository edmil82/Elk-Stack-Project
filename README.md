# Elk-Stack-Project
Stores all project related items
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](https://github.com/edmil82/Elk-Stack-Project/blob/main/Network%20Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._
  - 1
 - <code>
 ---
 - name: Configure Elk VM with Docker
  hosts: elk
  remote_user: azadmin
   become: true
   tasks:
     # Use apt module
    - name: Install docker.io
      apt:
        update_cache: yes
         force_apt_get: yes
         name: #TODO
         state: #TODO
      # Use apt module
    - name: Install python3-pip
      apt:
        force_apt_get: yes
        name: #TODO         state: #TODO
       # Use pip module (It will default to pip3)
     - name: Install Docker module
      pip:
        name: #TODO
        state: #TODO
       # Use command module
     - name: Increase virtual memory
       command: sysctl -w vm.max_map_count=262144
  # Use sysctl module
    - name: Use more memory
       sysctl:          
      name: #TODO
        value: #TODO
        state: #TODO
        reload: #TODO
       # Use docker_container module
     - name: download and launch a docker elk container
  docker_container:
         name: elk
         image: sebp/elk:761          state: started
          restart_policy: always
         # Please list the ports that ELK runs on
         published_ports:
            -  #TODO
            -  #TODO
           -  #TODO
        # Use systemd module
      - name: Enable service docker on boot
        systemd:
          name: #TODO
          enabled: #TODO
</code>

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available_, in addition to restricting access_ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
  a) Protecting availability b) to restrict access to the rest of the network to just the jump box.
  
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _configuration____ and system _files____.
- _TODO: What does Filebeat watch for?_Send all of the log files to the ELK stack in creating synchronized logging.
- _TODO: What does Metricbeat record?_Recording the actual metrics and getting statistical analysis.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 52.150.8.108   | Linux            |
| Web-1     |          | 137.117.68.195         |    Linux              |
| Web-2     |          | 137.117.68.195            | Linux                  |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __jumpbox___ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
52.150.8.108  
137.117.68.195    
137.117.68.195 

Machines within the network can only be accessed by _jumpbox____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
jumpbox 52.150.8.108
A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.7 10.0.0.9    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
convenience, efficiency, continuity

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...install Docker
- download image
- execute Docker command
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
-   52.150.8.108  
    137.117.68.195    
    137.117.68.195 

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
-   Filebeat
-   Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
-   Filebeat sends all of the log files to the ELK stack in creating synchronized logging.
-   Metricbeat records the actual metrics which allows getting statistical analysis.
-   
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __yml___ file to _vm home directory____.
- Update the _host____ file to include ip addresses
- Run the playbook, and navigate to vm home directory_ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_ansible.yml, copy to vm home directory
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_  hosts
- _Which URL do you navigate to in order to check that the ELK server is running?
- DVWA

_As a **Bonus**, provide the specific commands the user will need
