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

# Objective 3 

## Part 1 (Optional) – Configuration of Separte User, Project and addition of New Image + Flavor:

1.	Go to the “Projects” page under Identity and create a new project (Note: This requires admin privileges)

![image](https://user-images.githubusercontent.com/48782286/217306168-6c5c1baf-fccd-4175-9b97-977d1feb6056.png)

2.	Create the new project by assigning it a name and a description (optional) – and click on create Project

![image](https://user-images.githubusercontent.com/48782286/217306245-4e00fc85-9dd3-4d54-94e2-aea06eee4831.png)

3.	Click on “Users” under Identity and create a new user

![image](https://user-images.githubusercontent.com/48782286/217306298-5d89dd1c-2745-43c8-914a-4f42ff6ece5d.png)

4.	Create a new user by assigning a user name, password and by selecting a project that was created in the previous step,  you can additionally set the user as an admin for that project

![image](https://user-images.githubusercontent.com/48782286/217306355-333c78de-6b52-4818-9031-3df6f412d0dc.png)

5.	Log out of the current user and log back in with the new user created.

6.	Download any image (Cirros, Ubuntu, CentOS etc) and navigate to the “images” section under compute

![image](https://user-images.githubusercontent.com/48782286/217306437-30a67e88-81df-45b7-8bc6-64a18ece785d.png)

7.	Click on create new image, and select the image that you downloaded. Additionally you can name the image, give it a description and make it a public image (accessable by other users)

![image](https://user-images.githubusercontent.com/48782286/217306474-f5ac8735-45a7-4a45-9a0c-9c8fcf97cd6c.png)

8.	Next, create a flavor by going to the “flavor” section under “compute” under “Admin” . You need admin permissions to add a new flavor. Click on create flavor.

![image](https://user-images.githubusercontent.com/48782286/217306517-39e85aaa-b502-4d71-ac19-82ace46876ee.png)

9.	Specify parameters for the new flavor, and give it a name and click on create flavor.

![image](https://user-images.githubusercontent.com/48782286/217306557-1155b65a-7bec-4801-858c-f8e3b313460f.png)

## Part 2 – Configuration of Virtual Networks A and B:

1.	To create Networks A and B, Click on “networks” under Network and click on “New Network”
 
 ![image](https://user-images.githubusercontent.com/48782286/217306732-2b813d00-920c-4350-9912-b6524bebecc2.png)

2.	Give a network name, and click on next. Under Subnet, Give any subnet name and give the network address for the subnet. In this example, Network A has an ip of 192.168.100.0/24, the gateway ip is 192.168.100.1 and click next
 
 ![image](https://user-images.githubusercontent.com/48782286/217306767-e3bdd19c-52a9-4fc4-80da-c05baa9ed4ac.png)

3.	Under subnet details, enable dhcp, create an address scope of your liking. In this example, we can set the scope to be 192.168.100.10,192.168.100.250. Additionally set any DNS name server, in this example, we’re configuring 8.8.8.8 (Google) and click on create.
  
  ![image](https://user-images.githubusercontent.com/48782286/217306792-3f5e4d61-956f-4ad0-b59d-ae38caf93aa1.png)

4.	Repeat the same process with appropriate IP addresses for network B.
 
 ![image](https://user-images.githubusercontent.com/48782286/217306817-91f48722-a062-4864-b30a-8db7287a75e4.png)

## Part 2 – Launching VMs in the VNs:

1.	Go to compute and click on instances and click on Launch Instance. In this example, we’ll be using the default cirros image that ships with openstack on the m1.nano flavor.
 ![image](https://user-images.githubusercontent.com/48782286/217306948-72da2843-3003-4857-beb3-2c4776e0d481.png)

2.	Give a name to the instance on the first page and click on next
 ![image](https://user-images.githubusercontent.com/48782286/217306971-8ad582b3-9806-4681-8280-fb7341bd6406.png)

3.	Select the cirros image by clicking on the up arrow key corresponding to the image. 
 ![image](https://user-images.githubusercontent.com/48782286/217306983-fce4eb98-2ffd-4e84-b098-e214992bec4f.png)


4.	Select the flavor by clicking on the up arrow key corresponding to the flavor desired. 
 ![image](https://user-images.githubusercontent.com/48782286/217307005-ca9baf1d-6236-467c-a7a5-c9fcaf85c812.png)

5.	Select the appropriate network for the VM , For a VM in VNA select the VNA network by click on the up arrow key, similarly by selecting VNB for a VM in the B network. After selecting the network, click on launch instance.
 ![image](https://user-images.githubusercontent.com/48782286/217307025-eeac4ba5-3ee9-430a-b652-88c694043237.png)

6.	Follow similar steps with appropriate networks for VMs in A and B networks. After creation of the VMs, proceed to the next step. 
7.	After creation of the VMs, you should be able to ping between VMs in the same network and unable to ping between VMs in different networks.


## Part 3 – Enabling internet access to the VMs:

1.	To enable internet access to the VMs, you need to assign each VM a floating IP address. However, to assign a VM a floating IP address from a subnet (public in this case), there should be a route between the two networks.
2.	To assign a VM in VNA a floating IP address from the public subnet, we need to add a router between the public network and VNA.
3.	To create a router, click on Routers under network and click on Create Router.
 
 ![image](https://user-images.githubusercontent.com/48782286/217307230-7ee8de04-eb07-461d-a797-bf3f901c0c8b.png)

4.	Give a name to the router, and assign the public network (network with internet access) as the external network.
 ![image](https://user-images.githubusercontent.com/48782286/217307248-ffaf49ec-857c-4da6-a22c-b8826ead945d.png)

5.	Open the router configuration UI, and under interfaces add an interface, which connects the router to the network that you wish to have internet access in. In this scenario, we want internet acces in both networks (A and B), so we can two interfaces to the router, one in VNA and one in VNB. (this will however allow inter network communication)
 ![image](https://user-images.githubusercontent.com/48782286/217307265-eb3c0e7f-e954-40cd-9bd9-fe0d8e30d21e.png)

Perform the process for VNB.
After adding the routers and interfaces, we can add floating IPs to our project and assign them to the VMs


## Part 3.1 – Creating and Assigning Floating IP addresses:

1.	Click on floating IPs under Network and click on allocate IPs to Project
 ![image](https://user-images.githubusercontent.com/48782286/217307370-4b349df8-5cfa-4b2d-831e-127a208fabf6.png)

2.	Select the pool with external internet access. In this scenario, it is the public pool. Click on allocate IP.
 ![image](https://user-images.githubusercontent.com/48782286/217307381-7e2d1f9e-2ac0-414b-b86e-c6c9e39e1b59.png)

3.	Click on the associate button that corresponds to the new floating IP address that you just created. After clicking on the associate button, select the VM you would like to have internet access to.
 ![image](https://user-images.githubusercontent.com/48782286/217307405-72d19273-07fe-46fc-9491-3bb8d4866c28.png)
![image](https://user-images.githubusercontent.com/48782286/217307426-a401f405-c332-451b-9097-30246d8b886e.png)

 
4.	After associating a floating ip address with the VM, you should have internet access to your VMs. Additionally if you used a common router for both networks, you should also have inter network communication. Refer to sample network topology diagram below.

![image](https://user-images.githubusercontent.com/48782286/217307441-6731dac0-82fe-4da9-88c2-75e65e8cc32a.png)

Objective 4 - Willy


# Objective 4 – Creating Security Groups and Rules
###### documented by <em>Willy Fernandez</em>

In the below steps, I will go through the process to create a security group in Horizon Openstack and add rules to permit or restrict the traffic.
 
**Step 1:** Log in to the horizon web page and select the respective project, in my case the project is Lab2. Select the Network tab on the sidebar and click Security Groups.

![Picture1](https://user-images.githubusercontent.com/124555068/217174487-ebee5afa-c501-41f3-91e0-a6c3ca28d5dc.jpg)
**Step 2:** Once we are on the security group page, we need to click the Create Security Group button (red square on the screenshot):

![Picture2](https://user-images.githubusercontent.com/124555068/217174656-86b2e7e8-5d7e-4fca-8395-3ee4d2dbb2c0.jpg)
**Step 3:** In the popup box that comes up, set and name and description (it is highly recommended to have a  meaningful name that can describe the rule, for example, VN1-SSH)

<img width="444" alt="Picture3" src="https://user-images.githubusercontent.com/124555068/217168317-92fcfa94-4658-4a7d-a0ad-fa256f8fd6bd.png">
 
**Step 4:** If the creation is successful, it will bring you back to the security group page, we can see the new group name at the top where it says Manage Security Group Rules, in my case VN-A_VM-2_no_ping, 

**Step 1:** The next step is click Add Rule (red square on the screenshot).

![Picture4](https://user-images.githubusercontent.com/124555068/217169381-f68175fe-bfc3-4c31-8ca4-0af2ed0912d9.jpg)
 
**Step 5:** This will bring up a new dialog box where we can select the parameters for your security group rule.

<img width="397" alt="Picture5" src="https://user-images.githubusercontent.com/124555068/217168397-67369b6e-4e24-40a5-b476-5ead9ef3c07c.png">
 
In my case, I created a rule to allow ICMP for egress traffic to the network 192.168.200.0/24

<img width="541" alt="Picture6" src="https://user-images.githubusercontent.com/124555068/217174913-138818db-eef8-4171-9439-6fa9f4dbbba3.png">
 
There are many options to filer:

<img width="251" alt="Picture7" src="https://user-images.githubusercontent.com/124555068/217168435-e8e49067-9195-4b07-86c1-0238b1c8db6f.png">
 
**Step 6:** Once the Security group is completed, now we need to associate the new Security Group with the Instance previously created.

Go to Compute > Instances. Click the drop-down menu in the row containing information about to which you wish to apply your rule (columns Actions). Select Edit Security Groups:

![Picture8](https://user-images.githubusercontent.com/124555068/217174942-71e905e7-d201-47cc-8431-d5cb97c98e3d.jpg)

**Step 7:** After selecting the Edit Security Groups, we can see the Security Groups associated with this instance:

<img width="363" alt="Picture8" src="https://user-images.githubusercontent.com/124555068/217168478-2fb2a790-dcd7-418c-9b20-b91596d12651.png">
 

In the left section, we can see available security groups and in the right section you can see security groups already attached to your VM. 

**Step 8:** To apply a Security Group instance, click the (+) button next to that group, and to remove it, click the (-) button next to it.

![Picture9](https://user-images.githubusercontent.com/124555068/217168505-00a7e399-7543-4a11-9bfe-d594ce82ccb6.jpg)


After assigning the Security Group, the rules are applied to the VMs immediately and we are ready to go.








