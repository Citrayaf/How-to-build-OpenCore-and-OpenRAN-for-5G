# 5G SA Simulation

### 1. Turn on and run open5gs

a) Turn on the core5g VM (VM where you installed open5gs).

b) Open the terminal, then change to root user by using this command:
```Linux
sudo -i
```
if already change to root user, before @ will be seen as root

![28](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/28.png?raw=true)

c) Everytime turn on the core5g VM you need to execute this script for the core internal routing. By using this command:
```Linux
cd /home/core5g[VM’s name]/open5gs
sudo ./misc/netconf.sh [after executing this command there will be no output, but it’s okay]
```
d) Then execute this command to run all open5gs program:
```Linux
cd /home/core5g/open5gs/build/tests/app/ && ./app
```

There are three programs in this path: 5gc, epc, and app. 5gc is only to turn on 5G core function, epc is only to turn on 4G core function, and app will turn on both 4G and 5G core function.

e) After all programs can be successfully run like this picture below, it means your core already working fine.

![29](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/29.png?raw=true)

[Additional] To add and see SIM card information on HSS database

a) Open new tab on terminal, then change the user to root.

b) Run this command below:
```Linux
cd /home/core5g/open5gs/webui/ && npm run dev
```

c) If already appeared this message, it means the database already running successfully.

![30](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/30.png?raw=true)

d) Then you can open Mozilla Firefox and go to link [http://localhost:3000](http://localhost:3000/) , then login using this:

![31](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/31.png?raw=true)

Username: admin
Password: 1423

e) After you successfully login, you can see the SIMcard database or add new SIMcard database.

![26](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/26.png?raw=true)

### 2. Turn on and run UERANSIM (RAN & UE)

**RAN**

a) Turn on ueran VM, then open terminal.

b) Change the user to root by using this command:
```Linux
sudo -i
```
c) Change the path, then execute this command to run the RAN program:
```Linux
cd /home/ueran/UERANSIM/
./build/nr-gnb -c config/virtualbox_open5gs-gnb.yaml
```

d) Check in the ueran’s terminal and core5g’s terminal. If this message below appears, it means gNb to core already connected. This below message from ueran’s terminal

![32](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/32.png?raw=true)

and this message below from core5g’s terminal

![33](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/33.png?raw=true)

**UE**

e) Open new terminal tab, and change the user to root.

f) Change the path, the execute this command:
```Linux
cd /home/ueran/UERANSIM/build
./nr-ue -c ../config/virtualbox_open5gs-ue.yaml
```

This command simulates one UE trying to attach to the BTS.

g) Check the message in the current ueran’s terminal. “Connection setup for PDU session[1] is successful, TUN interface …”, it means the UE has already successfully attached to the gNb and can get service from the core side.

![34](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/34.png?raw=true)

Message from ueran’s terminal for gNb

![35](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/36.png?raw=true)

Message from core5g’s terminal

h) You can try to test the UE service by trying to do ping from UE. First, you need to open new terminal tab, then execute this command:
```Linux
sudo -i
cd /home  /ueran/UERANSIM/build
./nr-binder 10.45.0.2 [UE’s IP assigned from core] ping google.com
```

![37](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/37.png?raw=true)

Check the UE’s IP from this message below

![38](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/35.png?raw=true)

[Signalling Trace]

If you want to know the signalling trace between core to gNb or gNb to UE, you just need to open new terminal tab, change the user to root, then type “wireshark” and press enter. Wireshark needs to be opened in both VMs, so you can see signalling trace from the both side.

Sigtrace Example:

i. gNb connected to Core


![39](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/38.png?raw=true)

Sigtrace from gNb’s side.

![40](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/39.png?raw=true)

Sigtrace from Core’s side.

ii. UE connected to Core


Sigtrace from gNb’s side.

![40](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/40.png?raw=true)

Sigtrace from Core’s side.

![40](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/41.png?raw=true)


For reference, the signalling flow 5G SA is like this:


![40](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/5G-SA-Flow.png?raw=true)


**Congratulations!** You have successfully set up and simulated 5G SA simulation from UE to the 5GC. If you want to explore more features beyond this document, you can open these two links:

[https://kkohls.org/guides_open5gs.html](https://kkohls.org/guides_open5gs.html)

[https://open5gs.org/open5gs/docs/](https://open5gs.org/open5gs/docs/)

