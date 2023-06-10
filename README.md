# Router-on-a-stick-project

Inter-VLAN membuat VLAN ID yang berbeda agar bisa berkomunikasi.

## Basic Network Config

 1. Berikan IP pada PC0 dan PC1
 > PC0 = 192.168.10.10
 > PC1 = 192.168.20.10
 2. Koneksikan PC dengan Switch
 > PC0 dengan fa0/6 pada S1
 > PC1 dengan fa0/18 pada S2
 3. Sambungkan Switch Dengan Perangkat Lain
 > S1 fa0/1 ke S2 fa0/1
 > S1 fa0/5 ke gig0/0/1 Router0

## Konfigurasi VLAN

### Konfigurasi S2

Switch2>enable
Switch2#configure terminal
Switch2(config)#hostname S2
S2(config)#vlan 10
S2(config-vlan)#name VLAN-10
S2(config-vlan)#vlan 20
S2(config-vlan)#name VLAN-20
S2(config-vlan)#vlan 99
S2(config-vlan)#name MANAGEMENT
S2(config-vlan)#exit
S2(config)#interface fa0/18
S2(config-if)#switchport mode access
S2(config-if)#switchport access vlan 20
S2(config-if)#interface fa0/1
S2(config-if)#switchport mode trunk
S2(config-if)#end
> lakukan show vlan untuk mengecek konfigurasi vlan yang telah dibuat.

### Konfigurasi S1

Switch1>enable
Switch1#configure terminal
Switch1(config)#hostname S1
S1(config)#vlan 10
S1(config-vlan)#name VLAN-10
S1(config-vlan)#vlan 20
S1(config-vlan)#name VLAN-20
S1(config-vlan)#vlan 99
S1(config-vlan)#name MANAGEMENT
S1(config-vlan)#exit
S1(config)#interface fa0/6
S1(config-if)#switchport mode access
S1(config-if)#switchport access vlan 10
S1(config-if)#interface fa0/1
S1(config-if)#switchport mode trunk
S1(config-if)#interface fa0/5
S1(config-if)#switchport mode trunk
S1(config-if)#end
> lakukan show vlan untuk mengecek konfigurasi vlan yang telah dibuat.

## Konfigurasi Router

### Pemberian IP

Router>enable
Router#configure terminal
Router(config)#interface g0/0/1.10
Router(config-subif)#encapsulation dot1q 10
Router(config-subif)#ip address 192.168.10.1 255.255.255.0
Router(config)#no shut

