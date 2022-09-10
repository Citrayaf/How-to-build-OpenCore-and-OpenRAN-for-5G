
# VM Preparation

 

## Virtualbox Preparation

 

First, you need to install VirtualBox and download Linux Ubuntu version 18.04.6 [We use version because when this doc is created some support applications only support until Linux Ubuntu version 18.04.6] LTS (Bionic Beaver) go to this link: [Ubuntu 18.04.6 LTS (Bionic Beaver)](https://releases.ubuntu.com/18.04/). You can choose desktop or server, in this case, I use a desktop image.

 

## VM Preparation

 

![1](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/1.png?raw=true)
 
 

Click new, then a pop-up will appear. You can name it as you want because this VM will be used for core, I will name it **core**. For the machine folder you can choose where you want to save these VM files (it is recommended to use a disk with memory with free space of about 210Gbps for all this VM or if only for core you can prepare space of about 70 Gbps). Then for OS please choose **Linux Ubuntu with 64 bit**. Next for RAM, it’s recommended to set a minimum 4Gb. For all the next options you can just follow the default choices. The memory minimum can be set to 70 Gb. Then click create. Nice!, now you have created a VM. Double-click the VM to turn it on, and choose the Linux Ubuntu image that you have downloaded. For the next step just follow the procedure for Ubuntu Installation.

 

If you miss the OS installation part, you can manually choose from Settings > Storage > click the red circle > click Add, to add Ubuntu 64 image > click ok > turn on the VM. After this, you can start the Linux Ubuntu Installation.

 
 

![2](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/2.png?raw=true)

 
 

1. Network Setting for VMs

- a) Please make sure all VMs already turned down.

- b) Go to global setting in Virtualbox, click File > Preferences > Network and add a new NAT network > Click the symbol on the red circle to create it

 
 

![3](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/3.png?raw=true)


 
 

![4](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/4.png?raw=true)

 
 

- c) Go to setting by clicking the third symbol from the top, Enable IPv6, keep all other options, and assign a reasonable name and network CIDR.

 
 

![5](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/5.png?raw=true)


 
 

- d) Then move to each VM: go to Settings > Network and select NAT network that we have just created. For each VM, please make sure to click refresh to avoid the same MAC address and IP.

 
 

![6](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/6.png?raw=true)

 
 

![7](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/7.png?raw=true)

[Note]
To this, after you have done all the configuration

## VM Network Configuration
### VM Port Forwarding Configuration

a. Please make sure all VMs already turned down.

b. Go to global setting in Virtualbox, click File > Preferences > Network and add a new NAT network > Click the symbol on the red circle to create it

![3](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/3.png?raw=true)

![62](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/62.png?raw=true)

c. Go to setting by clicking the third symbol from the top, Click port forwarding.

![5](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/5.png?raw=true)

d. Go to setting by clicking the third symbol from the top, Click port forwarding. Add new configuration by clicking the button with the green plus icon. Then, make a configuration like this configuration below

![63](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/63.p