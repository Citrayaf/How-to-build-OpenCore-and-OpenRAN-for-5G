# Configuration for 5G SA

## Open5GS Configuration
· Install package to check VM’s IP with this command:
```Linux
sudo apt install net-tools
ifconfig
```
![19](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/19.png?raw=true)

IP in interface enp0s3 (10.14.2.10) will be used for the next configuration

· Make a backup of the Open5Gs original configuration:
```Linux
cp /home/core5gs[VM’s name]/open5gs/build/configs/sample.yaml /home/ core5gs[VM’s name]/open5gs/build/configs/sample.yaml.backup
```

· Then, configure the IP of AMF NGAP by using this command:
```Linux
cd /home/core5gs/open5gs/build/configs
nano sample.yaml [To open, view, and edit the file]
```

![20](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/20.png?raw=true)

Change this parameter to:
```Linux
amf:
 sbi:
 - addr: 127.0.0.5
 port: 7777
 ngap:
 - addr: 10.14.2.10 [IP from interface enp0s3]
```

Then, I tried to change some other parameters in the core with this parameter:

![21](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/21.png?raw=true)

You can try to modify these parameters as you want: **PLMN ID** consists of **MCC** (country region for Indonesia) and **MNC** (Service provider’s unique code), **TAC** (Type Allocation Code), and **S-NSSAI** (Single Network Slice Selection Assistance Information) this parameter is new in 5G core consist of Slice/Service type (**SST**) and Slice Differentiator (**SD**). These three parameters are important parameters for integration between Core, HSS database, gNb, and UE (Simcard).

## UERANSIM Configuration
· Go to the config directory and create a copy of the configs:
```Linux
cd /home/ueran/UERANSIM/config
cp open5gs-gnb.yaml virtualbox_open5gs-gnb.yaml
cp open5gs-ue.yaml virtualbox_open5gs-ue.yaml
```

· Make the following changes to the files:
```Linux
nano virtualbox_open5gs-gnb.yaml
```

· First, put in the IP of this VM:

![23](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/23.png?raw=true)

```Linux
linkIp: 10.14.2.6
ngapIp: 10.14.2.6
gtpIp: 10.14.2.6
```
Use IP from interface enp0s3, you can see it from ifconfig

![22](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/22.png?raw=true)

· In the same file as before, change the IP of the AMF in the file same as the Open5Gs NGAP IP:
```Linux
amfConfigs:
 - address: 10.14.2.10
 port: 38412
```

· Start to build the gNb with our adjusted config file:
```Linux
./build/nr-gnb -c config/virtualbox_open5gs-gnb.yaml
```

· Continue with the UE configuration:
```Linux
nano config/virtualbox_open5gs-ue.yaml
```

· In this file, you need to change the gNb IP configuration in this UE’s part. So, UE can connect to gNb:

![24](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/24.png?raw=true)

```Linux
gnbSearchList:
 - 10.14.2.6
```

This IP represent the gNb’s IP, which is IP from interface enp0s3

· Finally, we need to register the UE in the core network. You can access and edit the required information from the UE configuration file, by using this command:
```Linux
nano config/virtualbox_open5gs-ue.yaml
```

![27](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/27.png?raw=true)

which should by default contain the following pieces of information:
```Linux
imsi: 510140000000001
key: 465B5CE8B199B49FAA5F0A2EE238A6BC
AMF: 8000
USIM: OPc
Operator Key: E8ED289DEBA952E4283B54E88E6183CA
```

You should configure these parameters the same as parameters in HSS, so the attach process can be successfully accepted. Run the HSS via webUI in open5gs VM using this command:
```Linux
cd /home/core5gs/open5gs/webui
npm run dev
```

![25](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/25.png?raw=true)

Open Mozilla Firefox open localhost:3000

![26](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/26.png?raw=true)

