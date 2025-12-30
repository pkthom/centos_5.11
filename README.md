# centos_5.11

Dell OptiPlex760 に、CentOS5.11をインストールする

## OSインストール

DVD-Rに、以下の2つを焼いて準備する

<img width="1342" height="566" alt="image" src="https://github.com/user-attachments/assets/24faf6c9-2e44-441c-b00b-4bd50284db7c" />

マシンを起動してF12連打し、GRUBに入る

![IMG_0676](https://github.com/user-attachments/assets/5f424480-d7ac-49d1-8e61-dc6702bc6b02)

linux text と入力し、エンター

![IMG_0678](https://github.com/user-attachments/assets/08e7b87f-8df9-4b2f-af59-5171b287e155)

diskチェック

![IMG_0679](https://github.com/user-attachments/assets/7185fa0d-2556-442b-a9d8-9e26e6983f74)

![IMG_0680](https://github.com/user-attachments/assets/689f3137-a93b-4845-9f88-bcd27fbf0a28)


## 固定IPを付与する

/etc/sysconfig/network-scripts/ifcfg-eth0 が以下のようになっているので、
```
DEVICE=eth0
BOOTPROTO=dhcp
HWADDR=...
ONBOOT=yes
```
```
DEVICE=eth0
BOOTPROTO=none
HWADDR=...
ONBOOT=yes
IPADDR=10.20.30.41
NETMASK=255.255.255.0
GATEWAY=10.20.30.1
DNS1=1.1.1.1
DNS2=8.8.8.8
```
```
service network restart
```
✅-> eth0に10.20.30.41がついている　他PCからpingできる　ping 8.8.8.8 できる
