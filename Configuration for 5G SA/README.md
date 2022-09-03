## Open5Gs Installation 

I make this tutorial from these two sources:

[Katharina Kohls (kkohls.org)](https://kkohls.org/guides_open5gs.html)

[Building Open5GS from Sources | Open5GS](https://open5gs.org/open5gs/docs/guide/02-building-open5gs-from-sources/)

You need to know in this simulation, for the open5gs I still run this program using test script in this path: /home/lab/open5gs/build/tests/app/ follow guide from [Katharina Kohls (kkohls.org)](https://kkohls.org/guides_open5gs.html).

 1. Installation Open5Gs
     - Turn On the VM, open Linux Ubuntu Terminal then change to superuser by using this command:
	     ```Linux
	     sudo -i
	     [insert your password]
     - Update the VM using this command:
	     ```Linux
	     sudo apt update
     - Install and enable mongodb:
   	     ```Linux
	     sudo apt install mongodb
	     sudo systemctl start mongodb
	     sudo systemctl enable mongodb 
      [this command to make mongodb running everytime you turn on the VM]
     - Install requirements:
   	     ```Linux
   	    sudo apt install python3-pip python3-setuptools python3-wheel ninja-build build-essential flex bison git libsctp-dev libgnutls28-dev libgcrypt-dev libssl-dev libidn11-dev libmongoc-dev libbson-dev libyaml-dev libnghttp2-dev libmicrohttpd-dev libcurl4-gnutls-dev libnghttp2-dev libtins-dev meson libtalloc-dev cppcheck clang-tidy libsocket++1 python3-dev libbsd-arc4random-perl libkqueue-dev libssl-dev socket
   	    sudo update
        sudo upgrade
     - Build Open5Gs from sources
  	     ```Linux
         cd /home/[VM's name]
         git clone
         https://github.com/open5gs/open5gs
         cd open5gs
         meson build 
         --prefix=pwd/install   
         ```
         ![1](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/8.png?raw=true)               
       ```Linux
         ninja -C build
          ```
          ![1](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/9.png?raw=true)

     - Run this command for the internal ip configuration
   [make sure you already in path open5gs]
	     ```Linux
        sudo ./misc/netconf.sh
     - Run this test command:
	     ```Linux
	     ./build/tests/attach/attach
	     ```
	     ![10](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/10.png?raw=true)
	      ```Linux
       ./build/tests/registration/registration
       ```	      
       ![11](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/11.png?raw=true)[This is okay, from acetcom the one who make this repo said that this is a bug, in my case I just ignore and continue to the next step. All functions still work fine]
	     ```Linux 
	     ninja -C build test
	   ```
          ![12](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/12.png?raw=true)
	     ```Linux 
	     cd build 
	     meson test -v
         ```
         ![13](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/13.png?raw=true)
         ```Linux 
         ninja install
         ```
         
          ![14](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/14.png?raw=true)

     - Next, we will install the WebUI for user registration in HSS. Using this command:
	     ```Linux
		cd ../..
		sudo apt install curl
		curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash –
		sudo apt install nodejs
		cd open5gs/webui/
		npm ci --no-optional
		```
		![15](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/15.png?raw=true)
     - Congrats! You have finished the Open5Gs installation
 2. UERANSIM Installation
    - Make new VM for UERANSIM, do it like in VM preparation step and for VM network configuration you can start from step  **d**.
    - Build UERANSIM from sources
      ```Linux
      sudo apt install git make gcc g++ libsctp-dev lksctp-tools iproute2
      sudo apt install snap
      sudo snap install cmake --classic
      ```
      ![16](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/16.png?raw=true)    
    - Get the sources and build:
       ```Linux
      git clone https://github.com/aligungr/UERANSIM
      cd UERANSIM
      make   
      ```
      ![16](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/16.png?raw=true)
    - Congrats! You have successfully installed UERANSIM.
