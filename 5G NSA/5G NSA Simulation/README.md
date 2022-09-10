# 5G NSA Simulation

In this guide I integrate srsRAN with Open5gs, you can also simulate 5G NSA using the core from srsRAN. If you want to try to simulate 5G NSA using all programs from srsRAN in one VM you can follow the guide in this link
https://docs.srsran.com/en/latest/getting_started.html

1.Turn on core5g VM, then change the user to root

2.Launch the open5gs with this command:
```Linux
cd /home/core5g/open5gs/build/tests/app/ && ./app
```
3.Turn on the srs VM, then change the user to root

4.Launch the eNodeB by using this command:
```Linux
cd /home/srs/srsRAN/build
./srsenb/src/srsenb --rf.device_name=zmq --rf.device_args="fail_on_disconnect=true,tx_port0=tcp://*:2000,rx_port0=tcp://localhost:2001,tx_port1=tcp://*:2100,rx_port1=tcp://localhost:2101,id=enb,base_srate=23.04e6"
```
Then, check the message in the srsRAN terminal and open5gs terminal

![45](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/45.png?raw=true)

Message from srsRAN should be like this

![45](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/46.png?raw=true)

Message from open5gs should be like this

5.Launch the UE simulation by using this command:
```Linux
sudo ./srsue/src/srsue --rf.device_name=zmq --rf.device_args="tx_port0=tcp://*:2001,rx_port0=tcp://localhost:2000,tx_port1=tcp://*:2101,rx_port1=tcp://localhost:2100,id=ue,base_srate=23.04e6" --gw.netns=ue1
```
Then, check the message in the terminal of srsRAN and open5gs

![47](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/47.png?raw=true)

Message from srsUE should be like this

![49](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/49.png?raw=true)

Message from srsRAN should be like this

![48](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/48.png?raw=true)

Message from Open5Gs should be like this

6.Try try ping with this command:
to make service flow from UE to core
```Linux
sudo ip netns exec ue1 ping 10.45.0.1
```
(It is okay if there is no reply message. You can check from the srsRAN trace. If the brate value is not zero, it means UE get the downlink packet from the core)

[Additional]

7.Check the trace from srsRAN, after srsRAN is running press “t” and then enter. You will see this trace:

![50](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/50.png?raw=true)

You can also check the trace from Wireshark.