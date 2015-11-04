Esta capa controla a los usuarios y el acceso de grupos de trabajo (workgroup access) o los recursos de internetwork, y a veces se le llama desktop layer. Los recursos más utilizados por los usuarios deben ser ubicados localmente, pero el tráfico de servicios remotos es manejado aquí, y entre sus funciones están la continuación de control de acceso y políticas, creación de dominios de colisión separados (segmentación), conectividad de grupos de trabajo en la capa de distribución (workgroup connectivity). En esta capa se lleva a cabo la conmutación Ethernet (Ethernet switching), DDR y ruteo estático (el dinámico es parte de la capa de distribución). Es importante considerar que no tienen que ser routers separados los que efectúan estas funciones de diferentes capas, podrían ser incluso varios dispositivos por capa o un dispositivo haciendo funciones de varias capas.

El proyecto en la capa de acceso consta de:

Subnet Name|	Needed   Size|	Allocated Size|	Address|	Mask|	Dec Mask|	Assignable Range|	Broadcast
--------- | ------------- | -------------- | ------ | ------ | --------- | ----------------- | ------------
ACCESO|	12000|	16382|	10.0.0.0|	/18|	255.255.192.0|	10.0.0.1 - 10.0.63.254 |	10.0.63.255
ADM|	2500|	4094 |	10.0.64.0 |	/20 |	255.255.240.0|	10.0.64.1 - 10.0.79.254|	10.0.79.255
SEC|	900|	1022|	10.0.80.0|	/22|	255.255.252.0|	10.0.80.1 - 10.0.83.254|	10.0.83.255
SERVIDORES|	600|	1022|	10.0.84.0|	/22|	255.255.252.0|	10.0.84.1 - 10.0.87.254|	10.0.87.255
ELECTRONICOS|	300|	510|	10.0.88.0|	/23|	255.255.254.0|	10.0.88.1 - 10.0.89.254|	10.0.89.255|

## Configuration Flow

 # Switch 2960
 - Dispositivo Capa 2

Configuracion| Comentario|
-------------|-----------|
hostname L2 | Se le asigno el nombre L2 al equipo
interface FastEthernet0/3 | Se utilizo la interfaz 0/3 para conectarse a los host
switchport access vlan 64| Se le asigno la vlan 64 
switchport mode access| Se configuró como modo de acceso
interface FastEthernet0/4| Se utilizo la interfaz 0/4 para conectarse a los host
switchport access vlan 80|  Se le asigno la vlan 80
switchport mode access|  Se configuró como modo de acceso
interface GigabitEthernet0/1| Esta se conecta al L3-1  
switchport mode trunk| Se configuro como modo troncal 
interface GigabitEthernet0/2| Esta se conecta al L3-2
switchport mode trunk| Se configuro como modo troncal
 
 ## Switch 3560
 - Dispositivo capa 3

# Equipo 1
- L3-1
Configuración | Comentario |
--------------|------------|
hostname L3-1|Se le asigno el nombre L3-1 al equipo|
interface FastEthernet0/1 | |
switchport trunk encapsulation dot1q | |
switchport mode trunk ||
interface Vlan64 ||
ip address 10.0.64.2 255.255.240.0 ||
standby 64 ip 10.0.64.1 ||
standby 64 priority 150 ||
standby 64 preempt ||
interface Vlan80 ||
ip address 10.0.80.2 255.255.252.0 ||
standby 80 ip 10.0.80.1 ||

 - L3-2 
Configuración | Comentario |
--------------|------------|
vlan 64|Se crea la vlan 65|
name ADM| Se le da el nomnbre de ADM|
vlan 80| Se crea la vlan 80|
name SEC| Se le da el nombre de SEC |
interface FastEthernet0/1 | Se entra a la interfaz f0/1 |
 switchport trunk encapsulation dot1q | Se le asigna el tipo de encapsulación|
 switchport trunk allowed vlan 64,80 | Se permite que crucen las vlans' 64 y  80 por el troncal |
 switchport mode trunk | Se asigna el puerto modo troncal|
 interface Vlan64 | Se entra a la interfaz de la vlan 64|
 ip address 10.0.64.3 255.255.240.0 | Se le asigna una IP|
 standby 64 ip 10.0.64.1 | Se le asigna una ip virtual al grupo 64|
 interface Vlan80 | Se entra a la interfaz de la vlan 80|
 ip address 10.0.80.3 255.255.252.0 |  Se le asigna una IP|
 standby 80 ip 10.0.80.1 |Se le asigna una ip virtual al grupo 80|
 standby 80 priority 150 | Se le asigna una prioridad mayor para que sea el active|
 standby 80 preempt | Se configura para en caso de reconexion este vuelva a ser el active|