# Práctica 2: Restaurante

**Universidad San Carlos de Guatemala**  
**Facultad de Ingeniería**  
**Escuela de Ciencias y Sistemas**  
**Curso:** Redes de Computadoras 2  
**Semestre:** Segundo Semestre 2026  
**Grupo:** 25

### Integrantes

| Carné | Nombre Completo |
|---|---|
| 202201336 | Estuardo Josué Vaquiax Reyes |
| 202004762 | Angel Guillermo Arreaga Barrientos |
| 202203806 | Héctor Daniel Ortiz Osorio |

---

## Tabla de Contenidos

- [1. Descripción](#1-descripción)
- [2. Estado actual del proyecto](#2-estado-actual-del-proyecto)
- [3. Topología implementada](#3-topología-implementada)
  - [3.1 Distribución por pisos](#31-distribución-por-pisos)
  - [3.2 Servicios centrales](#32-servicios-centrales)
- [4. Cálculo del número de grupo](#4-cálculo-del-número-de-grupo)
- [5. Tabla de VLAN y redes](#5-tabla-de-vlan-y-redes)
  - [5.1 Subnetting VLSM y FLSM](#51-subnetting-vlsm-y-flsm)
- [6. Direccionamiento de los dispositivos finales](#6-direccionamiento-de-los-dispositivos-finales)
- [7. Mapa de conexiones](#7-mapa-de-conexiones)
  - [7.1 Dispositivos utilizados](#71-dispositivos-utilizados)
  - [7.2 Enlaces LACP](#72-enlaces-lacp)
  - [7.3 Conexiones cableadas](#73-conexiones-cableadas)
  - [7.4 Conexiones inalámbricas](#74-conexiones-inalámbricas)
- [8. Configuración básica de switches](#8-configuración-básica-de-switches)
- [9. Configuración de VLAN y enlaces troncales](#9-configuración-de-vlan-y-enlaces-troncales)
- [10. HSRP](#10-hsrp)
- [11. LACP y EtherChannel](#11-lacp-y-etherchannel)
- [12. Enrutamiento dinámico](#12-enrutamiento-dinámico)
- [13. DHCP](#13-dhcp)
- [14. Configuración inalámbrica](#14-configuración-inalámbrica)
- [15. DNS y servidor web](#15-dns-y-servidor-web)
- [16. Pruebas de conectividad](#16-pruebas-de-conectividad)
- [17. Evidencias](#17-evidencias)
- [18. Conclusiones](#18-conclusiones)

---

## 1. Descripción

La práctica consiste en diseñar e implementar en Cisco Packet Tracer la infraestructura de red de un restaurante. La solución debe integrar segmentación mediante VLAN, subnetting VLSM/FLSM, conectividad inalámbrica segura, DHCP, DNS, HTTP, HSRP y enlaces LACP.

El archivo de simulación utilizado es `Practica2_G25.pkt`.

## 2. Estado actual del proyecto

| Actividad | Estado |
|---|---|
| Creación de la carpeta de la práctica | Completado |
| Copia del enunciado oficial en `docs/` | Completado |
| Plantilla inicial del manual técnico | Completado |
| Diseño de la topología | Completado |
| Creación del archivo `Practica2_G25.pkt` | Completado |
| Cálculo y documentación de VLSM/FLSM | Completado |
| Reportes de cálculo descargados en `assets/evidence/` | Completado |
| Configuración de VLAN y enlaces trunk | Pendiente |
| Configuración de EIGRP | Pendiente |
| Configuración de LACP | Pendiente |
| Configuración de HSRP | Pendiente |
| Configuración de DHCP | Pendiente |
| Configuración inalámbrica | Pendiente |
| Configuración DNS y HTTP | Pendiente |
| Pruebas de conectividad y failover | Pendiente |
| Evidencias y conclusiones | Pendiente |

## 3. Topología implementada

> Pendiente: agregar la imagen de la topología en `assets/images/topologia-inicial.png`.

El inventario de dispositivos y el plan de cableado están documentados en la sección [7. Mapa de conexiones](#7-mapa-de-conexiones), manteniendo un único manual Markdown.

La topología se organiza en tres pisos y un segmento de Servicios Centrales:

- Piso 1: red cableada para administración y cocina.
- Piso 2: dos redes inalámbricas.
- Piso 3: dos redes inalámbricas.
- Servicios Centrales: servidores web y DHCP.

### 3.1 Distribución por pisos

| Área | Medio principal | Redes o servicios |
|---|---|---|
| Piso 1 | Cableado | `ADMIN`, `COCINA` |
| Piso 2 | Wi-Fi | `WLAN1`, `WLAN2` |
| Piso 3 | Wi-Fi | `WLAN1`, `WLAN2` |
| Servicios Centrales | Cableado | `WEB_SERVERS`, `DHCP_SERVERS` |

### 3.2 Servicios centrales

El segmento de Servicios Centrales alojará el servidor web con DNS/HTTP y el servidor DHCP. Se debe documentar la redundancia HSRP indicada para este segmento.

## 4. Cálculo del número de grupo

El grupo asignado es `25`. Para obtener el valor `X` solicitado en el enunciado:

```text
2 + 5 = 7
```

Por lo tanto, el valor utilizado para las VLAN y las redes es `X = 7`.

## 5. Tabla de VLAN y redes

| VLAN | Nombre | ID calculado | Red general |
|---|---|---:|---|
| Administración | `ADMIN` | 17 | `192.198.17.0/24` |
| Cocina | `COCINA` | 27 | `192.198.17.0/24` |
| Servidores web | `WEB_SERVERS` | 37 | `192.198.100.0/24` |
| Servidores DHCP | `DHCP_SERVERS` | 47 | `192.198.100.0/24` |

Las redes generales de los pisos inalámbricos son `192.198.27.0/24` para el piso 2 y `192.198.37.0/24` para el piso 3.

La red reservada por el enunciado para los enlaces de enrutamiento es `10.2.7.0/24`.

### 5.1 Subnetting VLSM y FLSM

La distribución se calculó con las calculadoras [FLSM de Arcadio](https://arcadio.gq/calculadora-subredes-flsm.html) y [VLSM de Arcadio](https://arcadio.gq/calculadora-subredes-vlsm.html). Se aplicó VLSM cuando los segmentos tienen diferentes cantidades de hosts y FLSM cuando las partes deben ser iguales.

#### VLSM: Piso 1

Para `192.198.17.0/24` se ordenaron los requerimientos de mayor a menor: 60 hosts para `COCINA` y 10 hosts para `ADMIN`.

| Segmento | VLAN | Hosts solicitados | Subred | Máscara | Hosts utilizables | Rango utilizable | Broadcast |
|---|---:|---:|---|---|---:|---|---|
| `COCINA` | 27 | 60 | `192.198.17.0/26` | `255.255.255.192` | 62 | `192.198.17.1 - 192.198.17.62` | `192.198.17.63` |
| `ADMIN` | 17 | 10 | `192.198.17.64/28` | `255.255.255.240` | 14 | `192.198.17.65 - 192.198.17.78` | `192.198.17.79` |

#### FLSM: redes inalámbricas y Servicios Centrales

Cada red general `/24` se dividió en dos subredes iguales `/25`. Cada subred proporciona 126 hosts utilizables, suficiente para los 80 hosts solicitados por WLAN y para cada VLAN de Servicios Centrales.

| Área | Segmento o SSID | Red general | Subred | Máscara | Hosts utilizables | Rango utilizable | Broadcast |
|---|---|---|---|---|---:|---|---|
| Piso 2 | `PISO2_G7_R1` / WLAN1 | `192.198.27.0/24` | `192.198.27.0/25` | `255.255.255.128` | 126 | `192.198.27.1 - 192.198.27.126` | `192.198.27.127` |
| Piso 2 | `PISO2_G7_R2` / WLAN2 | `192.198.27.0/24` | `192.198.27.128/25` | `255.255.255.128` | 126 | `192.198.27.129 - 192.198.27.254` | `192.198.27.255` |
| Piso 3 | `PISO3_G7_R1` / WLAN1 | `192.198.37.0/24` | `192.198.37.0/25` | `255.255.255.128` | 126 | `192.198.37.1 - 192.198.37.126` | `192.198.37.127` |
| Piso 3 | `PISO3_G7_R3` / WLAN2 | `192.198.37.0/24` | `192.198.37.128/25` | `255.255.255.128` | 126 | `192.198.37.129 - 192.198.37.254` | `192.198.37.255` |
| Servicios Centrales | `WEB_SERVERS` | `192.198.100.0/24` | `192.198.100.0/25` | `255.255.255.128` | 126 | `192.198.100.1 - 192.198.100.126` | `192.198.100.127` |
| Servicios Centrales | `DHCP_SERVERS` | `192.198.100.0/24` | `192.198.100.128/25` | `255.255.255.128` | 126 | `192.198.100.129 - 192.198.100.254` | `192.198.100.255` |

#### VLSM: enlaces de enrutamiento

Para `10.2.7.0/24` se reservaron cuatro subredes `/30`, una por cada enlace punto a punto entre un multilayer switch y un router. Cada una ofrece dos direcciones utilizables; los enlaces LACP permanecen en capa 2 y no consumen una subred adicional.

| Enlace | Subred | Máscara | Direcciones utilizables | Broadcast |
|---|---|---|---|---|
| `MLS1_P1_G25` - `R2_P1_G25` | `10.2.7.0/30` | `255.255.255.252` | `10.2.7.1 - 10.2.7.2` | `10.2.7.3` |
| `MLS1_P1_G25` - `R3_P1_G25` | `10.2.7.4/30` | `255.255.255.252` | `10.2.7.5 - 10.2.7.6` | `10.2.7.7` |
| `MLS0_SC_G25` - `R0_SC_G25` | `10.2.7.8/30` | `255.255.255.252` | `10.2.7.9 - 10.2.7.10` | `10.2.7.11` |
| `MLS0_SC_G25` - `R1_SC_G25` | `10.2.7.12/30` | `255.255.255.252` | `10.2.7.13 - 10.2.7.14` | `10.2.7.15` |

Los gateways virtuales HSRP y las direcciones exactas de las interfaces se definirán en la etapa de configuración, conservando estas subredes como base.

Los reportes generados por Arcadio se conservaron como evidencia en [`assets/evidence/`](./assets/evidence/).

## 6. Direccionamiento de los dispositivos finales

Pendiente: completar la tabla con dispositivo, VLAN, dirección IP, máscara, gateway y servidor DNS.

| Dispositivo | Segmento | Dirección IP | Máscara | Gateway | DNS |
|---|---|---|---|---|---|
| Pendiente | Pendiente | DHCP | Pendiente | Pendiente | Pendiente |

## 7. Mapa de conexiones

Las siguientes tablas concentran el inventario y el cableado de la topología. Los puertos corresponden a las etiquetas actuales del archivo de Packet Tracer.

### 7.1 Dispositivos utilizados

| Cantidad | Dispositivo en Packet Tracer | Nombres o etiquetas | Uso |
|---:|---|---|---|
| 4 | `3560-24PS Multilayer Switch` | `Multilayer Switch0` a `Multilayer Switch3` | Núcleo de Servicios Centrales, Piso 1, Piso 2 y Piso 3 |
| 2 | `2960-24TT` | `Switch0`, `Switch1` | Acceso de Servicios Centrales y Piso 1 |
| 4 | `Router 2901` | `Router0` a `Router3` | Pares HSRP de Servicios Centrales y Piso 1 |
| 4 | `WRT300N` | `PISO2_G7_R1`, `PISO2_G7_R2`, `PISO3_G7_R1`, `PISO3_G7_R3` | Acceso inalámbrico de los pisos 2 y 3 |
| 2 | `Server-PT` | `ServerWeb`, `ServerDHCP` | DNS/HTTP y DHCP |
| 7 | `PC-PT` | `PC0` a `PC6` | Clientes cableados o inalámbricos |
| 5 | `Laptop-PT` | `Laptop0` a `Laptop4` | Clientes inalámbricos o cableados |
| 4 | `Smartphone-PT` | `Smartphone0` a `Smartphone3` | Clientes inalámbricos |

Interfaces de referencia: los switches usan `Fa0/1` a `Fa0/24`; los uplinks disponibles son `Gi0/1` y `Gi0/2`; los routers 2901 usan `G0/0` y `G0/1`; los WRT300N usan `Internet` para el uplink y `Ethernet 1` a `Ethernet 4` para la LAN; los equipos finales cableados usan `FastEthernet0`.

### 7.2 Enlaces LACP

Cada enlace entre multilayer switches utiliza cuatro interfaces FastEthernet y se configura como un `Port-Channel` con LACP.

| Port-Channel | Equipo A | Puertos A | Equipo B | Puertos B | Propósito |
|---|---|---|---|---|---|
| `Po3` | `Multilayer Switch3` | `Fa0/21 - Fa0/24` | `Multilayer Switch1` | `Fa0/21 - Fa0/24` | Piso 3 - Piso 1 |
| `Po2` | `Multilayer Switch2` | `Fa0/21 - Fa0/24` | `Multilayer Switch1` | `Fa0/17 - Fa0/20` | Piso 2 - Piso 1 |
| `Po0` | `Multilayer Switch0` | `Fa0/21 - Fa0/24` | `Multilayer Switch1` | `Fa0/13 - Fa0/16` | Servicios Centrales - Piso 1 |

### 7.3 Conexiones cableadas

#### Piso 3

| Desde | Puerto | Hacia | Puerto | Tipo |
|---|---|---|---|---|
| `Multilayer Switch3` | `Fa0/1` | `PISO3_G7_R1` | `Internet` | Uplink |
| `Multilayer Switch3` | `Fa0/2` | `PISO3_G7_R3` | `Internet` | Uplink |
| `PISO3_G7_R3` | `Ethernet 1` | `PC6` | `FastEthernet0` | Cliente cableado |

Clientes Wi-Fi previstos de `PISO3_G7_R1`: `PC4`, `Laptop3`, `Smartphone2`. Clientes Wi-Fi previstos de `PISO3_G7_R3`: `PC5`, `Laptop4`, `Smartphone3`.

#### Piso 2

| Desde | Puerto | Hacia | Puerto | Tipo |
|---|---|---|---|---|
| `Multilayer Switch2` | `Fa0/1` | `PISO2_G7_R1` | `Internet` | Uplink |
| `Multilayer Switch2` | `Fa0/2` | `PISO2_G7_R2` | `Internet` | Uplink |
| `PISO2_G7_R2` | `Ethernet 1` | `PC2` | `FastEthernet0` | Cliente cableado |

Clientes Wi-Fi previstos de `PISO2_G7_R1`: `PC3`, `Laptop2`, `Smartphone1`. Clientes Wi-Fi previstos de `PISO2_G7_R2`: `PC0`, `Laptop0`, `Smartphone0`.

#### Piso 1

| Desde | Puerto | Hacia | Puerto | Tipo |
|---|---|---|---|---|
| `Multilayer Switch1` | `Fa0/1` | `Router2` | `G0/0` | Enlace de enrutamiento |
| `Multilayer Switch1` | `Fa0/2` | `Router3` | `G0/0` | Enlace de enrutamiento |
| `Switch1` | `Fa0/1` | `Router2` | `G0/1` | Segmento HSRP |
| `Switch1` | `Fa0/2` | `Router3` | `G0/1` | Segmento HSRP |
| `Switch1` | `Fa0/3` | `PC1` | `FastEthernet0` | Cliente cableado |
| `Switch1` | `Fa0/4` | `Laptop1` | `FastEthernet0` | Cliente cableado |

#### Servicios Centrales

| Desde | Puerto | Hacia | Puerto | Tipo |
|---|---|---|---|---|
| `Multilayer Switch0` | `Fa0/1` | `Router0` | `G0/0` | Enlace de enrutamiento |
| `Multilayer Switch0` | `Fa0/2` | `Router1` | `G0/0` | Enlace de enrutamiento |
| `Switch0` | `Fa0/1` | `Router0` | `G0/1` | Segmento HSRP |
| `Switch0` | `Fa0/2` | `Router1` | `G0/1` | Segmento HSRP |
| `Switch0` | `Fa0/3` | `ServerWeb` | `FastEthernet0` | VLAN 37: WEB_SERVERS |
| `Switch0` | `Fa0/4` | `ServerDHCP` | `FastEthernet0` | VLAN 47: DHCP_SERVERS |

### 7.4 Conexiones inalámbricas

| WRT300N | Clientes previstos | SSID |
|---|---|---|
| `PISO2_G7_R1` | `PC3`, `Laptop2`, `Smartphone1` | `PISO2_G7_R1` |
| `PISO2_G7_R2` | `PC0`, `Laptop0`, `Smartphone0` | `PISO2_G7_R2` |
| `PISO3_G7_R1` | `PC4`, `Laptop3`, `Smartphone2` | `PISO3_G7_R1` |
| `PISO3_G7_R3` | `PC5`, `Laptop4`, `Smartphone3` | `PISO3_G7_R3` |

Las conexiones inalámbricas no tienen puerto físico. La asociación queda pendiente de configuración. `PC2` y `PC6` sí permanecen cableadas a `Ethernet 1` de los WRT indicados arriba.

## 8. Configuración básica de switches

Pendiente: documentar hostnames, contraseñas, nombres de dominio, configuración de administración y comandos ejecutados desde consola.

## 9. Configuración de VLAN y enlaces troncales

Pendiente: documentar la creación de las VLAN 17, 27, 37 y 47, la asignación de puertos access y los enlaces trunk.

## 10. HSRP

HSRP debe configurarse en el Piso 1 y en Servicios Centrales para proporcionar redundancia ante la falla de un dispositivo de enrutamiento.

Pendiente: documentar grupos HSRP, prioridades, direcciones virtuales, routers activo/standby y pruebas de recuperación.

## 11. LACP y EtherChannel

Cada conexión entre edificios debe utilizar cuatro interfaces con LACP.

Pendiente: documentar interfaces físicas, número de `Port-Channel`, modo LACP y validación con comandos `show`.

## 12. Enrutamiento dinámico

El grupo 25 es impar, por lo que el protocolo indicado en el enunciado es **EIGRP**.

Pendiente: documentar el proceso, redes anunciadas, vecinos, rutas aprendidas y comandos de verificación.

## 13. DHCP

Todos los dispositivos finales deben obtener su dirección IP dinámicamente. El servidor DHCP debe tener un pool adecuado para cada VLAN cableada y los routers inalámbricos deben entregar direccionamiento a sus clientes.

Pendiente: documentar pools, exclusiones, gateways, DNS y pruebas de asignación.

## 14. Configuración inalámbrica

| Piso | SSID | Broadcast | Seguridad | Contraseña de red | Contraseña del router |
|---|---|---|---|---|---|
| 2 | `PISO2_G7_R1`, `PISO2_G7_R2` | No | WPA2 Personal | `G7_PISO2` | `Grupo7_P2` |
| 3 | `PISO3_G7_R1`, `PISO3_G7_R3` | Sí | WPA2 Personal | `G7_PISO3` | `Grupo7_P3` |

Pendiente: documentar direccionamiento, DHCP y pruebas de conexión de nuevos dispositivos.

## 15. DNS y servidor web

El dominio requerido es:

```text
www.practica2_Grupo7.com
```

La página HTTP debe mostrar los nombres de los integrantes y el número de grupo. Pendiente: agregar configuración, contenido publicado y pruebas desde los tres pisos.

## 16. Pruebas de conectividad

Pendiente: agregar evidencias de:

- Piso 2 hacia Piso 1.
- Piso 3 hacia Piso 1.
- Servicios Centrales hacia Piso 1.
- Asignación DHCP cableada e inalámbrica.
- Resolución DNS y acceso HTTP.
- Failover de HSRP.
- Funcionamiento de los Port-Channel LACP.

## 17. Evidencias

Las capturas se almacenarán en `assets/images/` y se enlazarán aquí conforme se complete la implementación.

### Reportes de subnetting

- [Reporte VLSM del Piso 1: `192.198.17.0/24`, 60 y 10 hosts](./assets/evidence/arcadio-vlsm-piso1-192.198.17.0-60y10hosts.pdf)
- [Reporte FLSM del Piso 2: `192.198.27.0/24`, 2 subredes](./assets/evidence/arcadio-flsm-piso2-192.198.27.0-2-subredes.pdf)
- [Reporte FLSM del Piso 3: `192.198.37.0/24`, 2 subredes](./assets/evidence/arcadio-flsm-piso3-192.198.37.0-2-subredes.pdf)
- [Reporte FLSM de Servicios Centrales: `192.198.100.0/24`, 2 subredes](./assets/evidence/arcadio-flsm-servicios-192.198.100.0-2-subredes.pdf)
- [Reporte VLSM de enrutamiento: `10.2.7.0/24`, 4 enlaces](./assets/evidence/arcadio-vlsm-routing-10.2.7.0-4-enlaces.pdf)

## 18. Conclusiones

Pendiente: documentar los resultados obtenidos, problemas encontrados, validaciones realizadas y recomendaciones.

## Documento de referencia

- [Enunciado oficial de la Práctica 2](./docs/0975_Practica_2_2S2026.pdf)
