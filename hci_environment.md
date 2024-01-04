# Implementación de Entorno Hiperconvergente en Laboratorio

En esta sección voy a crear un entorno hiperconvergente en mi laboratorio personal 🛠️🚀

## Objetivo del Proyecto

El propósito de este proyecto es diseñar, implementar y documentar un stretched cluster virtual utilizando ESXi anidados dentro de un nodo físico. La configuración constará de 2 nodos de cómputo y 1 testigo para garantizar la redundancia y la alta disponibilidad. El objetivo es que el proyecto simule un datacenter físico lo mas real posible.

## Componentes Principales

1. **Hiperconvergencia con ESXi Anidados:**
   - Dos nodos de cómputo que ejecutan ESXi para formar un clúster hiperconvergente.
   - Un nodo de testigo necesario para la resiliencia del entorno y evitar split-brain.

2. **Virtualización y Orquestación de Red con Cumulus VX:**
   - Utilizaremos Cumulus VX para virtualizar y orquestar switches de red, simulando un entorno más realista y eficiente.

3. **Almacenamiento con TrueNAS y iSCSI:**
   - Implementaremos iSCSI para servir almacenamiento desde un TrueNAS, simulando la función de una cabina de almacenamiento.

## Pasos a Seguir

1. **Esquema y checklist de la infraestructura**
   - En primer lugar vamos a realizar un esquema de la asignación de direcciones IP que vamos a usar, asi como las VM que vamos a levantar. Hecho esto comenzaremos a realizar la configuración
   -  

1. **Configuración de ESXi Anidados:**
   - Despliegue de máquinas virtuales ESXi en el nodo principal.
   - Configuración del clúster hiperconvergente con vSAN.

2. **Virtualización de Red con Cumulus VX:**
   - Despliegue y configuración de Cumulus VX para gestionar switches de red virtuales.

3. **Implementación de iSCSI con TrueNAS:**
   - Configuración de TrueNAS para proporcionar servicios de almacenamiento a través de iSCSI.

4. **Pruebas y Optimización:**
   - Realización de pruebas de rendimiento y ajustes necesarios para optimizar el entorno.

## Contribuciones

¡Las contribuciones y sugerencias son bienvenidas! Si tienes ideas para mejorar la implementación, encuentras errores o deseas compartir tu experiencia, no dudes en abrir un issue o enviar un pull request.

Espero que este proyecto sirva como inspiración y referencia para implementar entornos hiperconvergentes en laboratorios personales. ¡A disfrutar del proceso de creación! 🌐🔧
