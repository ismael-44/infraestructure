# Introducción a las VLANs (Virtual LANs)

## ¿Qué es una VLAN?

Una VLAN (Virtual LAN) es una red lógica que agrupa un conjunto de dispositivos de red, independientemente de su ubicación física, en una misma red local virtual. Las VLANs permiten segmentar una red física en múltiples redes lógicas para mejorar la administración, la seguridad y el rendimiento de la red.

## Beneficios de las VLANs

### 1. **Mejora de la Seguridad**
Al segmentar la red, las VLANs pueden aislar el tráfico de diferentes grupos de usuarios, lo que reduce el riesgo de accesos no autorizados y ataques internos.

### 2. **Reducción del Dominio de Broadcast**
Las VLANs limitan el alcance de los mensajes de broadcast, lo que reduce el tráfico innecesario y mejora el rendimiento de la red.

### 3. **Gestión Simplificada**
Las VLANs facilitan la gestión de la red al permitir agrupar dispositivos por función, departamento o ubicación, simplificando la configuración y el mantenimiento.

### 4. **Flexibilidad y Escalabilidad**
Las VLANs permiten mover dispositivos dentro de la red sin necesidad de cambiar la configuración física, lo que proporciona flexibilidad y facilita la expansión de la red.

## Tipos de VLANs

### 1. **VLANs de Datos**
Estas VLANs se utilizan para segmentar el tráfico de datos en la red. Por ejemplo, se puede crear una VLAN para cada departamento de una empresa (e.g., VLAN de Ventas, VLAN de Finanzas).

### 2. **VLANs de Voz**
Estas VLANs se utilizan para el tráfico de voz, asegurando que las llamadas telefónicas tengan la prioridad y la calidad de servicio (QoS) necesarias.

### 3. **VLANs de Gestión**
Estas VLANs se utilizan para el tráfico de administración de la red, separando el tráfico de gestión del tráfico de usuario para mejorar la seguridad y la eficiencia.

### 4. **VLANs de Seguridad**
Estas VLANs se utilizan para segmentar el tráfico de dispositivos que requieren alta seguridad, como los servidores de bases de datos o sistemas financieros.

## Funcionamiento de las VLANs

Las VLANs funcionan utilizando etiquetas de VLAN (VLAN tags) en los frames Ethernet. Estas etiquetas, según el estándar IEEE 802.1Q, se añaden al frame Ethernet para indicar a qué VLAN pertenece el tráfico. Los switches gestionan estas etiquetas y encaminan el tráfico en función de la VLAN de origen y destino.

### Etiquetas VLAN (VLAN Tags)

Cada frame Ethernet que pasa por un puerto trunk (que lleva tráfico de múltiples VLANs) tiene una etiqueta VLAN. Esta etiqueta contiene la identificación de la VLAN (VLAN ID), que permite a los switches determinar la VLAN correspondiente y dirigir el tráfico adecuadamente.

### Puertos Access y Trunk

- **Puertos Access:** Un puerto access pertenece a una única VLAN y envía/recibe tráfico no etiquetado. Es ideal para conectar dispositivos finales como computadoras y teléfonos IP.
- **Puertos Trunk:** Un puerto trunk puede transportar tráfico de múltiples VLANs y envía/recibe tráfico etiquetado con los IDs de VLAN. Se utiliza para interconectar switches y otros dispositivos de red.

## Funcionamiento de las VLANs a Nivel Bajo

El funcionamiento de las VLANs a nivel bajo implica la manipulación de los frames de Ethernet y el etiquetado de estos frames con información de VLAN. A continuación se detalla el proceso:

### 1. Etiquetado de Frames

Cuando un switch recibe un frame de Ethernet en un puerto configurado en modo trunk (enlace troncal), añade una etiqueta VLAN al principio del frame. Esta etiqueta VLAN, también conocida como VLAN tag, contiene información sobre a qué VLAN pertenece el frame.

### 2. Formato del VLAN Tag

El formato del VLAN tag sigue el estándar IEEE 802.1Q y consiste en 4 bytes añadidos al frame original de Ethernet:

- **Priority (3 bits):** Se utiliza para especificar la prioridad del tráfico (QoS) en caso de congestión en el switch.
- **C: (1 bit):** Se utiliza para indicar si el frame ha sido modificado o no. 
- **ID de VLAN (12 bits):** Es un identificador numérico de 12 bits que indica a qué VLAN pertenece el frame.

### 3. Procesamiento del Frame en el Switch

Cuando un switch recibe un frame con una etiqueta VLAN, examina el VLAN tag para determinar a qué VLAN pertenece el frame. Luego, el switch utiliza esta información para tomar decisiones sobre cómo procesar y encaminar el frame.

- **Filtrado de VLANs:** El switch filtra los frames entrantes para asegurarse de que solo se procesen los frames que pertenecen a las VLANs configuradas en el switch.
- **Forwarding del Frame:** El switch reenvía el frame a través de los puertos adecuados según la tabla de direcciones MAC y las VLANs configuradas.

### 4. Encaminamiento entre VLANs

Cuando un frame necesita ser encaminado entre VLANs, el switch utiliza el enrutamiento inter-VLAN. Esto implica enviar el frame a un dispositivo capaz de realizar el enrutamiento, como un router o un switch multilayer. El dispositivo de enrutamiento examina el VLAN tag del frame y toma decisiones sobre cómo encaminar el tráfico entre las VLANs.

### 5. Trabajo en Dispositivos Fin de Línea (End Devices)

Los dispositivos finales, como computadoras y servidores, generalmente no están conscientes de las VLANs. Solo interactúan con frames de Ethernet regulares y no están preocupados por el etiquetado de VLAN. El switch se encarga de agregar y eliminar los VLAN tags según sea necesario al transmitir el tráfico entre los dispositivos finales y la red VLAN.

En resumen, a nivel bajo, las VLANs funcionan etiquetando los frames de Ethernet con información de VLAN, permitiendo así la segmentación del tráfico en una red local (LAN) y el control más granular sobre cómo se gestiona y enruta ese tráfico dentro de la red.


