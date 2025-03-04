# OSPF TYPE_1
Within an Area (Intra-Area Routing) → Link-State Protocol
Between Areas (Inter-Area Routing) → Distance Vector-Like Behavior

![[Pasted image 20250303231711.png]]

Router3 will learn 4 LSA 
where area 0 will learn 3 LSA(r1,r2,r3)
where area 1 will learn 2 LSA(r3.r4)

Things to do in Router1:
```
conf t
interface s0/0
ip address 10.1.1.1 255.255.255.252
no shutdown
interface f1/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit 
conf t
router ospf 1
network 10.1.1.0 0.0.0.3 area 0
network 192.168.1.0 0.0.0.255 area 0
router-id 1.1.1.1
exit
```

First para is the header of LSA and Link state and advertising router will be same in LSA
Odd number LSA are used to see the information of prefixes.
Even number LSA are used to see the information of router.

In this case Router 3 will has 2 links one is the physical link and other is considering the neighbour as link .
This is how R3 has came up with 5 links 
Router4:
![[Pasted image 20250304110246.png]]
Router3:
![[Pasted image 20250304110352.png]]
Router2:
![[Pasted image 20250304110418.png]]
Router1:
![[Pasted image 20250304110438.png]]
### LSA_1
It will be flooded within the area not the cross area
It will be used to see the information of directly connected links(information of prefixes)

### LSA_2 (DR/BDR)

```
int f1/0
ip address 10.0.0.1 255.255.255.0
no shutdown
ip ospf priority 0
```