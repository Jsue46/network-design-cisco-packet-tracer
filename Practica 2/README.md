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

El archivo de simulación debe guardarse como `Practica2_25.pkt`.

## 2. Estado actual del proyecto

| Actividad | Estado |
|---|---|
| Creación de la carpeta de la práctica | Completado |
| Copia del enunciado oficial en `docs/` | Completado |
| Plantilla inicial del manual técnico | Completado |
| Diseño de la topología | Pendiente |
| Creación del archivo `Practica2_25.pkt` | Pendiente |
| Cálculo y documentación de VLSM/FLSM | Pendiente |
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

La topología se organizará en tres pisos y un segmento de Servicios Centrales:

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

### 5.1 Subnetting VLSM y FLSM

| Segmento | Red general | Requerimiento | Subred propuesta |
|---|---|---:|---|
| Piso 1 - `ADMIN` | `192.198.17.0/24` | 10 hosts | Pendiente de documentar `/28` |
| Piso 1 - `COCINA` | `192.198.17.0/24` | 60 hosts | Pendiente de documentar `/26` |
| Piso 2 - `WLAN1` | `192.198.27.0/24` | 80 hosts | Pendiente de documentar `/25` |
| Piso 2 - `WLAN2` | `192.198.27.0/24` | 80 hosts | Pendiente de documentar `/25` |
| Piso 3 - `WLAN1` | `192.198.37.0/24` | 80 hosts | Pendiente de documentar `/25` |
| Piso 3 - `WLAN2` | `192.198.37.0/24` | 80 hosts | Pendiente de documentar `/25` |
| `WEB_SERVERS` | `192.198.100.0/24` | Parte igual | Pendiente de documentar `/25` |
| `DHCP_SERVERS` | `192.198.100.0/24` | Parte igual | Pendiente de documentar `/25` |
| Enrutamiento | `10.2.7.0/24` | Enlaces entre equipos | Pendiente de dividir |

## 6. Direccionamiento de los dispositivos finales

Pendiente: completar la tabla con dispositivo, VLAN, dirección IP, máscara, gateway y servidor DNS.

| Dispositivo | Segmento | Dirección IP | Máscara | Gateway | DNS |
|---|---|---|---|---|---|
| Pendiente | Pendiente | DHCP | Pendiente | Pendiente | Pendiente |

## 7. Mapa de conexiones

Pendiente: documentar puertos, equipos vecinos, enlaces LACP, enlaces trunk y conexiones hacia los servidores y routers inalámbricos.

## 8. Configuración básica de switches

Pendiente: documentar hostnames, contraseñas, nombres de dominio, configuración de administración y comandos ejecutados desde consola.

## 9. Configuración de VLAN y enlaces troncales

Pendiente: documentar la creación de las VLAN 17, 27, 37 y 47, la asignación de puertos access y los enlaces trunk.

## 10. HSRP

HSRP debe configurarse en el piso 1 y en Servicios Centrales para proporcionar redundancia ante la falla de un dispositivo de enrutamiento.

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

- Piso 2 hacia piso 1.
- Piso 3 hacia piso 1.
- Servicios Centrales hacia piso 1.
- Asignación DHCP cableada e inalámbrica.
- Resolución DNS y acceso HTTP.
- Failover de HSRP.
- Funcionamiento de los Port-Channel LACP.

## 17. Evidencias

Las capturas se almacenarán en `assets/images/` y se enlazarán aquí conforme se complete la implementación.

## 18. Conclusiones

Pendiente: documentar los resultados obtenidos, problemas encontrados, validaciones realizadas y recomendaciones.

## Documento de referencia

- [Enunciado oficial de la Práctica 2](./docs/0975_Practica_2_2S2026.pdf)
