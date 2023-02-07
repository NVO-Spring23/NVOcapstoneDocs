Objective 1 - Mayuri

Objective 1 - Gayathri


a. Nova: Nova is for provisioning compute instances and supporting the creation of virtual machines, bare metal servers, and limited support of containers.
b. Swift: Swift is an object storage service for cloud storage like google drive, apple cloud, microsoft azure. It is used mainly to provide storage facilities to users that is hosted on the cloud.

c. Cinder: Cinder is a block storage service that provides volumes to Nova virtual machines, bare metal hosts, containers, and services that contain the VMs in terms of storage service.

d. Neutron: Neutron is a networking component of OpenStack and it provides network connectivity.

e. Glance: Glance is an image service of OpenStack where users can figure out what images to use for different VMs hosted on the network.

f. Keystone: Keystone is an identity service of OpenStack and it provides API client authentication, service discovery, and distributed multi-tenant authorization for authentication services like LDAP, OAuth, OpenID Connect, SAML, etc.

g. Horizon: Horizon provides the dashboard or web-based UI for OpenStack services.

What is the difference between Users and Roles?

Users are part of one or more projects. A role defines which actions users can perform in each of those projects that it is a part of.

What is a hypervisor and which hypervisors are supported in OpenStack?

Hypervisor is a software that is built for separating a system’s OS and resources from the hardware to the VMs associated with it. We can run any type of hypervisor in OpenStack with the default being KVM. Following hypervisors are supported in OpenStack:

 KVM, VMware, ESX/ESXi, XenServer, Hyper-V, Ironic, UML, LXC, QEMU 
 
Explain the meaning of ‘flavor’ in OpenStack.

Flavor is a measure of the compute, memory, and storage capacity of a VM.

Create a new network of 64 IP addresses in the Network tab and enable DHCP for 32 of the IPs using either the GUI or the CLI.
Create a router that connects this new network with the existing “public network” using either the GUI or the CLI.
Start two instances with the Cirros image present that connects to the new network of 64 IPs using either the GUI or the CLI.
Using GUI for the sake of simplicity:
Steps:
1. On the VM's GUI open the network tab under Project->Networks->Network. Add the network name, subnets and the 64 IP addresses. Provide the Gateway IP and create the instance.
2. A new router is created with the "public network" with subnet and IP address to the public network. The netowrk connections are made through Nova being the availability zone. Once done, the interfaces tab will display the routes and the fixed IPs to the network.
3. For both the VM instances, Cirros image is used while connecting to the 64 IPs network. To enusure the VMs are started and functioning, in the GUI the status of the VMs should be "running".




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
