# REDES2_2S_2026_G25

**Universidad San Carlos de Guatemala**  
**Facultad de Ingeniería**  
**Escuela de Ciencias y Sistemas**  
**Curso:** Redes de Computadoras 2  
**Semestre:** Segundo Semestre 2026  
**Grupo:** 25  

---

## Información del Grupo

| Carné | Nombre Completo |
|---|---|
| 202201336 | Estuardo Josué Vaquiax Reyes |
| 202004762 | Angel Guillermo Arreaga Barrientos |
| 202203806 | Héctor Daniel Ortiz Osorio |

---

## Descripción del Repositorio

Este repositorio contiene las prácticas y proyectos correspondientes al laboratorio del curso **Redes de Computadoras 2**. En él se almacenan los archivos de simulación desarrollados en **Cisco Packet Tracer**, las guías de requerimientos, la documentación técnica y las evidencias de trabajo.

---

## Contenido del Repositorio

### [Práctica 1: Monte Alto y la conectividad](./Practica1/README.md)

* **Ubicación:** `Practica1/`
* **Archivo de simulación:** [`Practica1_G25.pkt`](./Practica1/Practica1_G25.pkt)
* **Documentación técnica:** [`Practica1/README.md`](./Practica1/README.md)
* **Documentos de referencia:** [`Practica1/docs/`](./Practica1/docs/)

#### Temas Desarrollados:

1. **Segmentación por VLAN:** Implementación de VLANs para niveles educativos (Primaria, Básicos y Bachillerato).
2. **VLAN Trunking Protocol (VTP):** Administración centralizada de VLANs mediante switches en modos Server y Client.
3. **Spanning Tree Protocol (STP / RSTP):** Comparativa entre PVST (Edificio Izquierdo) y Rapid PVST (Edificio Derecho), evaluando tiempos de convergencia ante fallas de enlace.
4. **Seguridad de Puertos (Port-Security):** Restricción de direcciones MAC y políticas de puerto (*shutdown / err-disabled*) en la VLAN de Básicos.
5. **Enrutamiento Dinámico:** Configuración e interconexión de protocolos EIGRP, RIP y OSPF con redistribución de rutas para lograr conectividad total en la red.

---

### [Práctica 2: Restaurante](<./Practica2/README.md>)

* **Ubicación:** `Practica2/`
* **Archivo de simulación:** [`Practica2_G25.pkt`](<./Practica2/Practica2_G25.pkt>)
* **Documentación técnica:** [`Practica2/README.md`](<./Practica2/README.md>)
* **Enunciado oficial:** [`0975_Practica_2_2S2026.pdf`](<./Practica2/docs/0975_Practica_2_2S2026.pdf>)
* **Evidencias de subnetting:** [`Practica2/assets/evidence/`](<./Practica2/assets/evidence/>)

#### Temas de la Práctica:

1. **Diseño de topología:** Organización de Piso 1, Piso 2, Piso 3 y Servicios Centrales.
2. **Segmentación por VLAN:** VLAN 17 `ADMIN`, VLAN 27 `COCINA`, VLAN 37 `WEB_SERVERS` y VLAN 47 `DHCP_SERVERS`.
3. **Subnetting VLSM/FLSM:** División de las redes de usuarios, servidores y enlaces de enrutamiento.
4. **Enlaces troncales:** Transporte de VLAN entre switches multilayer y switches de acceso.
5. **LACP / EtherChannel:** Agregación de enlaces entre los switches multilayer.
6. **HSRP:** Redundancia de gateway en Piso 1 y Servicios Centrales.
7. **Enrutamiento dinámico:** Configuración de EIGRP para la interconexión de la topología.
8. **DHCP:** Asignación dinámica de direcciones para las VLAN cableadas y redes inalámbricas.
9. **Redes inalámbricas:** Configuración de SSID, broadcast, WPA2, direccionamiento `/25` y asociación de clientes.
10. **Servicios de red:** Configuración de DNS y HTTP para `www.practica2_Grupo7.com`.


---

## Estructura de Directorios

```text
REDES2_2S_2026_G25/
├── README.md
├── Practica1/
│   ├── Practica1_G25.pkt
│   ├── README.md
│   ├── assets/
│   │   └── images/
│   └── docs/
└── Practica2/
    ├── Practica2_G25.pkt
    ├── README.md
    ├── assets/
    │   ├── evidence/
    │   └── images/
    └── docs/
```

---

## Convenciones del Repositorio

* Cada práctica mantiene su propio manual técnico dentro de su carpeta.
* Los archivos de Packet Tracer conservan la identificación del grupo `G25`.
* Las evidencias se almacenan dentro de la carpeta `assets/` de la práctica correspondiente.
* No se marca una configuración como completada sin verificarla en Cisco Packet Tracer.
