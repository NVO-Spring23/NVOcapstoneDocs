# Objective 1 - Mayuri
# Objective 1 - OpenStack: Overview
\1. Explain the following components of OpenStack -

a. Nova -   It is the compute component responsible for the vm creation

b. Swift -   used for object storage and horizontally scalable. It is ideal for storing unstructured data.

c. Cinder - Provides block storage in Openstack called as Cinder Volumes It manages snapshots.

d. Neutron – This creates network infrastructure for the virtual machines.

e. Glance – it is used for image management for VMs. It stores the images and template for VM

f. Keystone – It is responsible for authentication.

g. Horizon - It provides the web-based UI for services like nova, neutron, cinder etc.

2. What is the difference between Users and Roles?

Roles defines the set of privileges that the users can perform.

3. What is a hypervisor and which hypervisors are supported in OpenStack?

The hypervisor manages virtual machines. Openstack supports hypervisors like KVM, VMware sphere, QEMU etc.

4. Explain the meaning of ‘flavor’ in OpenStack.

Flavor defines the configurations of the virtual machines. We can create server with different compute, memory and storage according to our needs

\5. Create a new network of 64 IP addresses in the Network tab and enable DHCP for 32 of 
the IPs using either the GUI or the CLI.

Under Network Click on Create network and follow the steps in the below screenshot to have DHCP enabled network

<img width="206" alt="image" src="https://user-images.githubusercontent.com/98084044/217148286-dadcc021-510b-4ac0-a2e8-369764db7882.png">
<img width="154" alt="image" src="https://user-images.githubusercontent.com/98084044/217148310-e711ae97-bbee-4f63-970c-cb5109c3755d.png">
<img width="224" alt="image" src="https://user-images.githubusercontent.com/98084044/217148338-7f5ea004-d5e9-48ba-a1a2-269a7d745898.png">

\6. Create a router that connects this new network with the existing “public network” using 
either the GUI or the CLI.

Under Router click on create router and assign public external network so that internet can be reachable. Once done we need to add interface to the router in the DHCP network so that this router can act as a default gateway  for our network that we created.

<img width="153" alt="image" src="https://user-images.githubusercontent.com/98084044/217148386-80e582e1-23d7-4b87-891c-b2efd54532cd.png">
<img width="272" alt="image" src="https://user-images.githubusercontent.com/98084044/217148404-e1c71dc6-7648-4f60-be79-da5ae3317e45.png">


\7. Start two instances with the Cirros image present that connects to the new network of 
64 IPs using either the GUI or the CLI.

Click on Launch instance under Instances, add image, key-pair, security network and network  as given in below screenshots. Once the VM is created we could see it’s receiving IP from the DHCP network we created. We are enabling Floating IPs for each VM so that internet can be reached.
<img width="185" alt="image" src="https://user-images.githubusercontent.com/98084044/217148546-0a875580-741c-40f7-a4ba-9b002462b1ca.png">
<img width="224" alt="image" src="https://user-images.githubusercontent.com/98084044/217148571-6140d7b5-caba-431a-9274-33e8ce92812e.png">
<img width="251" alt="image" src="https://user-images.githubusercontent.com/98084044/217148595-57699c7a-a8b9-4634-af5a-c86083188b63.png">
<img width="276" alt="image" src="https://user-images.githubusercontent.com/98084044/217148632-2ecefa8c-0ca4-4d8e-bc38-b79028a47a82.png">
<img width="275" alt="image" src="https://user-images.githubusercontent.com/98084044/217148649-05985604-7b3f-4a1f-9f48-ad9acd17cabd.png">
<img width="174" alt="image" src="https://user-images.githubusercontent.com/98084044/217148685-2868b7c8-45f2-490c-bce7-031801ca5bd7.png">
<img width="262" alt="image" src="https://user-images.githubusercontent.com/98084044/217148718-45aaa044-f1f9-468b-8999-261a7e4e23b2.png">
<img width="274" alt="image" src="https://user-images.githubusercontent.com/98084044/217148736-5392357a-28c3-4c4f-ace0-5bef39f9b35a.png">

Objective 1 - Gayathri
Objective 2 - Nikhitha
# Objective 2 – Auto-scaling application using Python
###### documented by <em>Nikhitha Atluri</em>
1. Scenario:

You are working in a cloud firm that has a single instance of an application running on OpenStack cloud platform. The firm is planning to add a functionality to the single running instance of the application that can autoscale/replicate itself to multiple instances whenever the compute capacity (eg. CPU cycles or memory) reaches a pre-defined threshold. Since you are familiar with the Python programming and REST API, you are being assigned a following task:

a. Write a simple Python application that can ssh into the available “cirros” instance that was created in the above objective and extract the CPU utilization information. [As an alternative, you may use ceilometer service for retrieving this telemetry data] 

b. If the CPU utilization exceeds a threshold value, for example 20%, spin up additional instances of cirros. The creation of cirros instances should be triggered whenever the compute capacity (eg. CPU utilization) exceeds a predefined threshold. In order to collect CPU utilization data, you’ll have to monitor its usage using appropriate commands.

c. The Python application can use Nova REST API to create additional “Cirros” instances whenever the above condition occurs. 

d. The auto scaling of the instances should be handled considering following requirements:

**Max scaling size: 4** (this value denotes the maximum number of instances that should be spun)

**Increment size: 1** (this value denotes the number of instances that should be spun whenever CPU utilization exceeds threshold)

**Evaluation period: 40** (this value denotes the time period in seconds for monitoring CPU usage)

## Steps to achieve objective

**Step 1:** Create a network VN-A using the steps in the previous objective

**Step 2:** Create a VM with a cirros image and ngn flavor and allocate a floating IP address, for it to be access the internet 

<img width="612" alt="image" src="https://user-images.githubusercontent.com/38699144/217115339-d0161cd4-7f7b-46d4-9897-9f45ac8b1521.png">



**Step 3:** On your openstack server, create a python file in the devstack environment. To get the contents of the instances, we don’t need to SSH into the instances, rather, we can use the Nova REST API to poll any information. We can connect to a project in openstack by using the client module in the following way.***[Obj 2a]***

<img width="554" alt="image" src="https://user-images.githubusercontent.com/38699144/217115308-4e825cfc-5687-4d0b-a798-ca63e0d7e830.png">



**Step 4:** We need to check if the cpu/memory used is greater than 20% of the total memory. If it is, then we have to create a new instance with the required specifications. In the code snippet mentioned below, we check for CPU utilization every 40 seconds***.[Obj 2b,2c, 2d]***

<img width="540" alt="image" src="https://user-images.githubusercontent.com/38699144/217115368-2cf2de97-459f-488e-864c-580436f2f66b.png">



**Step 5:** Check the number of available volumes you can create and allocate instances accordingly. In this objective, we were asked to limit the scaling size to 4, hence a maximum of only 4 instances could be made and the program ends after that.***[Obj 2d]***


<img width="292" alt="image" src="https://user-images.githubusercontent.com/38699144/217115391-8cbe1fcf-1831-4f71-afc5-27ea908041ed.png">


<img width="667" alt="image" src="https://user-images.githubusercontent.com/38699144/217115427-d01b2283-0c10-4622-a0e1-4360ac8938e7.png">


2. You can use the [Linux stress tool](https://www.tecmint.com/linux-cpu-load-stress-test-with-stress-ng-tool/) to raise the CPU utilization of an instance above the threshold.

**Step 6:** You can install “stress” package on your instance, to increase the CPU utilization. The cirros OS doesn’t support package installation, so, I wrote a bash script with loops and ran it on the VM.

Objective 3 - Vishal

Objective 4 - Willy


# Objective 4 – Creating Security Groups and Rules
###### documented by <em>Willy Fernandez</em>

In the below steps, I will go through the process to create a security group in Horizon Openstack and add rules to permit or restrict the traffic.
 
Log in to the horizon web page and select the respective project, in my case the project is Lab2. Select the Network tab on the sidebar and click Security Groups.

 

Once we are on the security group page, we need to click the Create Security Group button (red square on the screenshot):

 

In the popup box that comes up, set and name and description (it is highly recommended to have a  meaningful name that can describe the rule, for example, VN1-SSH)



 
 
If the creation is successful, it will bring you back to the security group page, we can see the new group name at the top where it says Manage Security Group Rules, in my case VN-A_VM-2_no_ping, 

The next step is click Add Rule (red square on the screenshot).



 









 
This will bring up a new dialog box where we can select the parameters for your security group rule.



 
In my case, I created a rule to allow ICMP for egress traffic to the network 192.168.200.0/24


 

 
There are many options to filer:



 






 
Once the Security group is completed, now we need to associate the new Security Group with the Instance previously created.

Go to Compute > Instances. Click the drop-down menu in the row containing information about to which you wish to apply your rule (columns Actions). Select Edit Security Groups:

 
After selecting the Edit Security Groups, we can see the Security Groups associated with this instance:


 

In the left section, we can see available security groups and in the right section you can see security groups already attached to your VM. 

To apply a Security Group instance, click the (+) button next to that group, and to remove it, click the (-) button next to it.

  

After assigning the Security Group, the rules are applied to the VMs immediately and we are ready to go.


