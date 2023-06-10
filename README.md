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

1. Switch2>enable
2. Switch2#configure terminal
3. Switch2(config)#hostname S2
4. S2(config)#vlan 10
5. S2(config-vlan)#name VLAN-10
6. S2(config-vlan)#vlan 20
7. S2(config-vlan)#name VLAN-20
8. S2(config-vlan)#vlan 99
9. S2(config-vlan)#name MANAGEMENT
10. S2(config-vlan)#exit
11. S2(config)#interface fa0/18
12. S2(config-if)#switchport mode access
13. S2(config-if)#switchport access vlan 20
14. S2(config-if)#interface fa0/1
15. S2(config-if)#switchport mode trunk
16. S2(config-if)#end
> lakukan show vlan untuk mengecek konfigurasi vlan yang telah dibuat.

### Konfigurasi S1

1 Switch1>enable
2 Switch1#configure terminal
3 Switch1(config)#hostname S1
4 S1(config)#vlan 10
5 S1(config-vlan)#name VLAN-10
6 S1(config-vlan)#vlan 20
7 S1(config-vlan)#name VLAN-20
8 S1(config-vlan)#vlan 99
9 S1(config-vlan)#name MANAGEMENT
10.S1(config-vlan)#exit
11.S1(config)#interface fa0/6
12.S1(config-if)#switchport mode access
13.S1(config-if)#switchport access vlan 10
14.S1(config-if)#interface fa0/1
15.S1(config-if)#switchport mode trunk
16.S1(config-if)#interface fa0/5
17.S1(config-if)#switchport mode trunk
17.S1(config-if)#end
> lakukan show vlan untuk mengecek konfigurasi vlan yang telah dibuat.

## Konfigurasi Router

### Pemberian IP

Router>enable
Router#configure terminal
Router(config)#interface g0/0/1.10
Router(config-subif)#encapsulation dot1q 10
Router(config-subif)#ip address 192.168.10.1 255.255.255.0
Router(config)#no shut

