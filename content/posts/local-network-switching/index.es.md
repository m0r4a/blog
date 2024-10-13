---
title: "Conmutación de Redes Locales - Proyecto Final"
draft: false
date: 2024-05-25
description: "Es un projecto en packet tracer que utiliza los siguientes conceptos: VLANs, EtherChannel, redundancy, subnetting, SPT y PVST."
summary: Este fue mi proyecto final de la clase de conmutación de redes locales, es un documento acerca de la implementación de todos los temas vistos durante el semestre
---

## Topología

### En packet tracer

{{< figure
    src="resources/topology-PT_es.svg"
    alt="Image of the topology in packet tracer"
    nozoom=true
>}}

### En un entorno real

{{< figure
    src="resources/topology-real_es.svg"
    alt="Image of the topology in packet tracer"
    nozoom=true

>}}

## 1. Redundancia de red

En la topología propuesta, cada switch de salida de cada departamento tiene dos salidas, el switch principal (Main) y el switch de respaldo (Backup), por lo que tendríamos un STP con la raíz en el switch principal y la raíz secundaria en el switch de respaldo, de modo que si falla, simplemente podrían enviar sus paquetes a través del secundario sin ningún problema.

| Departamento     | Número de puertos LAN del switch    |
|--------------- | ----------------------------- |
| Ventas         | 12                            |
| Ingeniería 2.1 | 48                            |
| Ingeniería 2.2 | 12                            |
| Administración | 24                            |
| Marketing      | 48                            |

## 2. Configuración de cada Switch

| Switch | Configuración                                    |
|--------|--------------------------------------------------|
| 1      | - vlan 10                                        |
|        | - name ventas                                    |
|        | - (Inside each interface towards a computer)     |
|        |   - switchport mode access                       |
|        |   - switchport access vlan 10                    |
| 2.1    | - vlan 20                                        |
|        | - name ingeniería                                |
|        | - (Inside each interface towards a computer)     |
|        |   - switchport mode access                       |
|        |   - switchport access vlan 20                    |
| 2.2    | - vlan 20                                        |
|        | - name ingeniería                                |
|        | - (Inside each interface towards a computer)     |
|        |   - switchport mode access                       |
|        |   - switchport access vlan 20                    |
| 3      | - vlan 30                                        |
|        | - name administración                            |
|        | - (Inside each interface towards a computer)     |
|        |   - switchport mode access                       |
|        |   - switchport access vlan 30                    |
| 4      | - vlan 40                                        |
|        | - name marketing                                 |
|        | - (Inside each interface towards a computer)     |
|        |   - switchport mode access                       |
|        |   - switchport access vlan 40                    |

## 3. Router hacia el internet


{{< figure
    src="resources/router-internet.svg"
    alt="Image of the topology in packet tracer"
    nozoom=true
    class="mx-auto"
>}}

En este caso, tenemos los switches "Main" y "Backup", así que ellos realizarán el enrutamiento inter-VLAN, así que no necesitamos algo como un Router-On-A-Stick para hacer el enrutamiento de VLANs.

## 4. EtherChannel

Es posible agregar un EtherChannel en cualquiera de los switches, un ejemplo práctico sería en el caso de que, por ejemplo, ingeniería crezca y ahora necesite mucho más ancho de banda o algo similar. Pondré un ejemplo genérico de la configuración para crear un EtherChannel entre dos switches:

_En el switch1_
```
interface range GigabitEthernet1/0/1 - 2
  description enlace_hacia_switch2_Switch
  switchport mode trunk  
  channel-group 1 mode active
  channel-protocol lacp
```

_En el switch2_
```
interface range GigabitEthernet1/0/1 - 2
  description enlace_hacia_switch1_Switch
  switchport mode trunk  
  channel-group 1 mode active
  channel-protocol lacp
```

Una vez configurado, EtherChannel agrupará los puertos seleccionados en ambos switches en un único “canal” lógico.

Esto significa que el ancho de banda combinado de los enlaces físicos se utilizará para transportar tráfico entre el switch1 y el switch2. Si uno de los enlaces físicos falla, el tráfico se redirige automáticamente por el otro enlace sin intervención manual, manteniendo la conectividad y el rendimiento.

Implementar EtherChannel mejorará significativamente el rendimiento de la red entre estos dos departamentos críticos y ayudará a manejar eficientemente grandes volúmenes de tráfico, asegurando además mayor disponibilidad y redundancia.

## 5. Esquema de direccionamiento IP

Habrán 4 VLANs:
  - Ventas: 10 usuarios
  - Administración: 20 usuarios 
  - Marketing: 35 usuarios
  - Ingeniería: 50 usuarios


| Departamento     | Rango de IPs útiles                | Número de la VLAN |
| -------------- | ------------------------------------ | ----------------- |
| Ventas         | 192.168.10.0 - 192.168.10.30         | 10                |
| Ingeniería     | 192.168.10.128 - 192.168.10.190      | 20                |
| Administración | 192.168.10.32 - 192.168.10.62        | 30                |
| Marketing      | 192.168.10.64 - 192.168.10.126       | 40                |

## 6. Gateway y máscaras de red las PCs de cada departamento


| Departamento   |  Gateway      | Máscara           |
| -------------- | ------------- | ----------------- |
| Ventas         | 192.168.10.1  | 255.255.255.224   |
| Ingeniería     | 192.168.10.129| 255.255.255.192   |
| Administración | 192.168.10.33 | 255.255.255.224   |
| Marketing      | 192.168.10.65 | 255.255.255.192   |

## 7. Switches LAN, switch principal

La idea en esta topología es que el switch principal es el que se llama “Main”. El comando utilizado para verificar si el switch es el switch principal o no es:

```
# show spanning-tree
```

Una vez ejecutes el comando te dará un output así:

```
Switch#show spanning-tree
VLAN0001
  Spanning tree enabled protocol ieee
  Root ID    Priority    32769
             Address     0002.1770.0A10
             This bridge is the root
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     0002.1770.0A10
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20

Interface   Role Sts Cost      Prio.Nbr Type
----------- ---- --- --------- -------- ----
Fa0/2       Desg FWD 19        128.2    P2p
Fa0/5       Desg FWD 19        128.5    P2p
Fa0/1       Desg FWD 19        128.1    P2p
```

En donde se puede ver, en la tercera línea de la sección "Root ID" que "This bridge is the root", es decir, que este _puente_ es la raiz.

## 8. LAN switches, switch secundario

En este caso, como lo indica el nombre, la idea es que el router llamado “Backup” actúe como el secundario.

El comando que se utilizaría sería de la misma manera que el show spanning-tree, y en la leyenda que dice en la imagen anterior “Este puente es el root” dirá que es el secundario.

## 9. STP separado por VLAN

Dada el tamaño de la red y la separación en varios departamentos con diferentes requisitos de conectividad, sería posible implementar PVST+. Su implementación podría mejorar la eficiencia operativa al permitir diferentes rutas raíz para diferentes VLAN, además de que es probable que aumente la estabilidad general de la red al identificar problemas potenciales de STP en VLAN individuales, evitando que un problema en una VLAN afecte a toda la red.

Implementar PVST+ puede maximizar el uso de todos los enlaces disponibles y proporcionar una mejor experiencia al usuario al optimizar el tráfico de la red según las necesidades específicas de cada departamento.

## 10. Comandos recomendados para la seguridad del STP

_Dentro de cada interfaz conectada a una PC_

- **spanning-tree portfast**: esto no es por seguridad, pero se recomienda encarecidamente utilizarlo en interfaces que van hacia dispositivos finales como PCs.

- **spanning-tree bpduguard enable**: este comando garantiza que si una interfaz se coloca en modo portfast para una PC, por ejemplo, y luego se conecta un dispositivo capaz de enviar paquetes BPDU, como un switch, este paquete BPDU no rompa el spanning-tree, desactivando la interfaz para lograr esto. 
