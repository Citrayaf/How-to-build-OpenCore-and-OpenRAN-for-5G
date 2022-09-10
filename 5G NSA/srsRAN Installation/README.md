# srsRAN Installation

This srsRAN installation guide is based on srsRAN installation with ZMQ Virtual Radio scenario from this link:
[https://docs.srsran.com/en/latest/app_notes/source/zeromq/source/index.html](https://docs.srsran.com/en/latest/app_notes/source/zeromq/source/index.html)
1.First you need to make a new VM (ex: VM’s name is srs) with the specification same as for core5g & ueran, then set up the VM’s network configuration same as core5g & ueran

2.Install the required libraries with this command:
```Linux
sudo apt-get install build-essential cmake libfftw3-dev libmbedtls-dev libboost-program-options-dev libconfig++-dev libsctp-dev libtool autoconf automake
```

3.Install the ZeroMQ development libraries installation can be installed with:
```Linux
cd /home/srs/
git clone https://github.com/zeromq/libzmq.git
cd libzmq
./autogen.sh
./configure
make
sudo make install
sudo ldconfig
```

4.Then you need to install czmq, by using this command:
```Linux
git clone https://github.com/zeromq/czmq.git
cd czmq
./autogen.sh
./configure
make
sudo make install
sudo ldconfig
```

5.Finally, you need to compile srsRAN (assuming you have already installed all the required dependencies). By using this command:
```Linux
git clone https://github.com/srsRAN/srsRAN.git
cd srsRAN
mkdir build
cd build
cmake ../
```
 
Put extra attention to the “cmake ../” console output. Make sure you read the following line:

```Linux
...
-- FINDING ZEROMQ.
-- Checking for module 'ZeroMQ'
-- No package 'ZeroMQ' found
-- Found libZEROMQ: /usr/local/include, /usr/local/lib/libzmq.so
...
```
![44](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/44.png?raw=true)
```Linux
make
```
![51](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/51.png?raw=true)
```Linux
sudo make install
srsran_install_configs.sh user
```
![52](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/52.png?raw=true)