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

チェック完了

![IMG_0681](https://github.com/user-attachments/assets/45476b80-7c23-4731-b6a1-d94622deac74)

もっとチェックしたいか聞いてくるので、そのままContinue

![IMG_0682](https://github.com/user-attachments/assets/00e9835f-3687-4f8b-bc9e-e020a4216bfc)

![IMG_0683](https://github.com/user-attachments/assets/dba7a290-016f-4c84-8d55-469cb1de54c8)

言語選択

![IMG_0684](https://github.com/user-attachments/assets/0990f731-3b24-4f8f-9bba-19d88f1be808)

text mode では日本語キーボード　だめらしい

![IMG_0685](https://github.com/user-attachments/assets/562e2aa4-6e2b-4f57-94e2-d0a6736f9fa0)

キーボード選択　

![IMG_0686](https://github.com/user-attachments/assets/fe3ca3af-98e1-4f10-97ff-c9c5b23160f4)

さっきトライしていたCentOS4が残っているがどうする？　不要なので、「Reinstall System」を選択

![IMG_0687](https://github.com/user-attachments/assets/604d6265-f8a4-4f73-9196-f664ecc22f02)

「全て」のパーティションを削除する

![IMG_0688](https://github.com/user-attachments/assets/5ceb25a0-0779-4b5e-8c85-49d9e533aadd)

念押ししてくるため、Yesをクリック

![IMG_0689](https://github.com/user-attachments/assets/abf9219f-4692-4b06-8466-d234a369b994)

確認が可能です　と言ってくる

![IMG_0690](https://github.com/user-attachments/assets/f3150235-f78e-43ed-bba7-a0a18154318e)

デフォルトのパーティション構成にしてくれているので、そのままOKをクリック

![IMG_0691](https://github.com/user-attachments/assets/6e975e12-dcb4-401a-b9db-d6427f5de7f2)

GRUBは有効（デフォルト）のままにする

![IMG_0692](https://github.com/user-attachments/assets/097374ae-04dc-46d9-9dca-4d1e11f0bf1b)

以下画像のまま

![IMG_0693](https://github.com/user-attachments/assets/ccc08b0e-c050-4d81-9f0e-27b6dae7b7cc)

![IMG_0695](https://github.com/user-attachments/assets/e0ddd44a-25cb-49fd-8942-d3c4363226ef)

![IMG_0696](https://github.com/user-attachments/assets/9b32ab53-d5fa-4a39-bc41-072d89bccd3a)

boot loaderをどっちにインストールしたいか？　/dev/sda のままでOK

![IMG_0697](https://github.com/user-attachments/assets/21c42042-0dc8-4857-a6da-c668e86eb2c5)

eth0をconfigureしますか？　あとでやるのでここでは　NO

![IMG_0705](https://github.com/user-attachments/assets/071891bd-57c3-4d55-b765-504c9d9fec8e)

DHCPで自動IP付与　を選択

![IMG_0706](https://github.com/user-attachments/assets/6a440021-8da6-45ad-b0fb-d44cfc45b7b0)


東京　を選択

![IMG_0707](https://github.com/user-attachments/assets/4c3367ff-4969-4001-9653-8e0a45f7fc74)

rootパスワードを設定

![IMG_0708](https://github.com/user-attachments/assets/b5968956-39b4-42fb-b59f-1842c7e47b0e)

インストールは、「server」を選択
![IMG_0710](https://github.com/user-attachments/assets/83112e3e-7516-49b3-be22-2016265435f8)

そのままOK

![IMG_0711](https://github.com/user-attachments/assets/632db7c5-eb5f-4489-8d2c-f2715a5c2eb4)

インストール完了

![IMG_0712](https://github.com/user-attachments/assets/523086f9-57fe-4425-aa3b-a296ae5f5239)

以下、選択する前に時間切れで次の画面に進んだ

![IMG_2FF9CF36-BF5A-4027-A77A-9DCDFB10573A](https://github.com/user-attachments/assets/1d4dd1b3-065f-4f22-9af9-8e85502d7f3b)


rootログインできた

![IMG_0715](https://github.com/user-attachments/assets/a55cec99-0955-4b58-ad03-2c4afbd809c2)

既にeth0がUPしていて、DHCPでVLAN内のIPが付いている

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
