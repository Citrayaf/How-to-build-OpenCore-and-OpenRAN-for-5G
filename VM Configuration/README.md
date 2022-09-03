
# VM Preparation

  

## Virtualbox Preparation

  

First, you need to install virtualbox and download linux Ubuntu version 18.04.6 [We use version because when this doc is created some support application only support until Linux Ubuntu version 18.04.6] LTS (Bionic Beaver) go to this link: [Ubuntu 18.04.6 LTS (Bionic Beaver)](https://releases.ubuntu.com/18.04/). You can choose desktop or server, in this case I use desktop image.

  

## VM Preparation

  

![1](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/1.png?raw=true)
  
  

Click new, then a pop up will appear. You can name it as you want, because this VM will be used for core, I will name it **core**. For the machine folder you can choose where you want to save this VM files (it is recommend to use disk with memory with free space about 210Gbps for all this VM or if only for core you can prepare space about 70 Gbps). Then for OS please choose **Linux Ubuntu with 64 bit**. Next for RAM it’s recommend to set minimum 4Gb. For all next option you can just follow the default choices. Memory minimum can be set 70 Gb. Then click create. Nice!, now you have created a VM. Double click the VM to turn it on, choose Linux Ubuntu image that you have download. For the next step just follow the procedure for Ubuntu Installation.

  

If you miss the OS installation part, you can manually choose from Settings > Storage > click the red circle > click Add, to add Ubuntu 64 image > click ok > turn on the VM. After this you can start the Linux Ubuntu Installation.

  
  

![2](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/2.png?raw=true)

  
  

1. Network Setting for VMs

- a) Please make sure all VMs already turned down.

- b) Go to global setting in Virtualbox, click File > Preferences > Network and add a new NAT network > Click symbol on red circle to create it

  
  

![3](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/3.png?raw=true)


  
  

![4](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/4.png?raw=true)

  
  

- c) Go to setting by click third symbol from top, Enable IPv6, keep all other options, and assign a reasonable name and network CIDR.

  
  

![5](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/5.png?raw=true)


  
  

- d) Then move to each VM: go to Settings > Network and select NAT network that we have just created. For each VM, please make sure click refresh to avoid same MAC address and IP.

  
  

![6](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/6.png?raw=true)

  
  

![7](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/7.png?raw=true)
