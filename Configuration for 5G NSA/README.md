# Configuration for 5G NSA

## Open5Gs
1.Open5Gs VM, then change user to root.
2.Install the required libraries with this command:
```Linux
cd /home/core5g/open5gs/build/configs
nano sample.yaml
```
Go to the MME configuration section, then edit this parameter:
```Linux
s1ap:
 - addr: 10.14.2.10
gummei:
 plmn_id:
 mcc: 510
 mnc: 14
 mme_gid: 2
 mme_code: 1
 tai:
 plmn_id:
 mcc: 510
 mnc: 14
 tac: 5300
```

## srsRAN
1.Create network namespace to receive IP pool from core’s userplane:
```Linux
sudo ip netns add ue1
```

using this command, you can verify the new “ue1” netns exist:
```Linux
sudo ip netns list
```
2.Open new terminal tab, then backup enb.conf, rr.conf, and ue.conf using this command:
```Linux
cd /root/.config/srsran/
cp enb.conf enb.conf.backup
cp rr.conf rr.conf.backup
cp ue.conf ue.conf.backup
```
These configurations are the default configuration after installation for 4G simulation.

3.Download three new enb.conf, rr.conf, and ue.conf from this link for 5G NSA simulation:

enb.conf:
[https://docs.srsran.com/en/latest/_downloads/cbbeb9eed64bf03407cbb255828db3f5/enb_example.conf](https://docs.srsran.com/en/latest/_downloads/cbbeb9eed64bf03407cbb255828db3f5/enb_example.conf)

rr.conf: [https://docs.srsran.com/en/latest/_downloads/b9b7009b9fda34684668e48dbfcc4f7d/rr_example.conf](https://docs.srsran.com/en/latest/_downloads/b9b7009b9fda34684668e48dbfcc4f7d/rr_example.conf)

ue.conf: [https://docs.srsran.com/en/latest/_downloads/c4c658121d530b085c7f1e53083e1d6c/ue_example.conf](https://docs.srsran.com/en/latest/_downloads/c4c658121d530b085c7f1e53083e1d6c/ue_example.conf)

after downloading these three files, please rename them first to enb.conf, rr.conf, and ue.conf.

The differences between original configuration & the new one:
-eNodeB configuration
```Linux
device_name = zmq
device_args = fail_on_disconnect=true,tx_port0=tcp://*:2000,rx_port0=tcp://localhost:2001,tx_port1=tcp://*:2100,rx_port1=tcp://localhost:2101,id=enb,base_srate=23.04e6
```

![53](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/53.png?raw=true)

-Radio configuration (rr.conf)
```Linux
nr_cell_list =
(
 {
 rf_port = 1;
 cell_id = 0x02; //you can modify this parameter as you want (use hex format)
 tac = 0x0007; //you can modify this parameter as you want, but need to be the same with the core configuration (use hex format)
 pci = 500; //you can modify this parameter as you want
 root_seq_idx = 204;
 // TDD:
 //dl_arfcn = 634240;
 //band = 78;
 // FDD:
 dl_arfcn = 368500;
 band = 3;
 }
);
```

![54](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/54.png?raw=true)

4.Put those three configurations to “/root/.config/srsran” with this command:
```Linux
cp /home/srsran/Download/enb_example.conf /root/.config/srsran/enb.conf
cp /home/srsran/Download/rr_example.conf /root/.config/srsran/rr.conf
cp /home/srsran/Download/ue_example.conf /root/.config/srsran/ue.conf
```
5.Open and edit configuration files by using this command:
```Linux
cd /root/.config/srsran/
nano enb.conf
```

![54](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/55.png?raw=true)

Edit these parameters, as you want but must be the same with the core configuration:
```Linux
mcc = 510
mnc = 14
mme_addr = 10.14.2.10 [open5gs IP]
gtp_bind_addr = 10.14.2.7 [srsRAN IP]
```

![56](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/57.png?raw=true)

```Linux
s1c_bind_addr = 10.14.2.7
```

![56](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/56.png?raw=true)

```Linux
nano rr.conf
```

![56](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/58.png?raw=true)

4G anchor configuration, you can edit the TAC parameter. In my case, I try to use TAC 5300 in hex equals 0x14B4

![59](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/59.png?raw=true)

5G cell configuration. 5G cell’s TAC needs to be the same as the 4G anchor’s TAC.
```Linux
nano ue.conf
```

![59](https://github.com/Citrayaf/How-to-build-OpenCore-and-OpenRAN-for-5G/blob/main/Pictures/60.png?raw=true)

```Linux
mode = soft
algo = milenage
opc = E8ED289DEBA952E4283B54E88E6183CA
k = 465B5CE8B199B49FAA5F0A2EE238A6BC
imsi = 510140000000001
imei = 437081612381615
```

You need to modify these parameters the same as SIM card information in open5gs HSS.