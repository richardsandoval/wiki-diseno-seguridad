Esta capa controla a los usuarios y el acceso de grupos de trabajo (workgroup access) o los recursos de internetwork, y a veces se le llama desktop layer. Los recursos más utilizados por los usuarios deben ser ubicados localmente, pero el tráfico de servicios remotos es manejado aquí, y entre sus funciones están la continuación de control de acceso y políticas, creación de dominios de colisión separados (segmentación), conectividad de grupos de trabajo en la capa de distribución (workgroup connectivity). En esta capa se lleva a cabo la conmutación Ethernet (Ethernet switching), DDR y ruteo estático (el dinámico es parte de la capa de distribución). Es importante considerar que no tienen que ser routers separados los que efectúan estas funciones de diferentes capas, podrían ser incluso varios dispositivos por capa o un dispositivo haciendo funciones de varias capas.

El proyecto en la capa de acceso consta de:

* La ip privada utilizada seria la **10.0.0.0** donde:
    -El segundo octeto es la localidad
    -El tercer octeto es el servicio utilizado


Subnet Name|	Needed   Size|	Allocated Size|	Address|	Mask|	Dec Mask|	Assignable Range|	Broadcast
--------- | ------------- | -------------- | ------ | ------ | --------- | ----------------- | ------------
ACCESO|	12000|	16382|	10.0.0.0|	/18|	255.255.192.0|	10.0.0.1 - 10.0.63.254 |	10.0.63.255
ADM|	2500|	4094 |	10.0.64.0 |	/20 |	255.255.240.0|	10.0.64.1 - 10.0.79.254|	10.0.79.255
SEC|	900|	1022|	10.0.80.0|	/22|	255.255.252.0|	10.0.80.1 - 10.0.83.254|	10.0.83.255
SERVIDORES|	600|	1022|	10.0.84.0|	/22|	255.255.252.0|	10.0.84.1 - 10.0.87.254|	10.0.87.255
ELECTRONICOS|	300|	510|	10.0.88.0|	/23|	255.255.254.0|	10.0.88.1 - 10.0.89.254|	10.0.89.255