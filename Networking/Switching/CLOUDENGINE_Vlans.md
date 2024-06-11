## Objetivo técnico
Se pretende segmentar la red para poder separar trafico con diferentes objetivos:

- **Seguridad:** Permiten aislar diferentes segmentos de la red, lo que minimiza los riesgos de accesos no autorizados.
- **Rendimiento:** Reducen el tráfico de broadcast, lo que mejora el rendimiento de la red.
- **Gestión Simplificada:** Facilitan la administración de grupos de dispositivos en la red.
- **Escalabilidad:** Ayudan a manejar redes grandes y complejas de manera más eficiente.

## Mejores Prácticas

1. **Planificación de la Red:** Antes de implementar VLANs, es crucial planificar la estructura de la red y definir claramente las necesidades de segmentación.
2. **Uso de Nombres Descriptivos:** Asignar nombres descriptivos a las VLANs para facilitar la gestión y el mantenimiento.
3. **Seguridad:** Utilizar VLANs para separar el tráfico sensible del resto de la red.
4. **Documentación:** Mantener una documentación detallada de la configuración de las VLANs.
5. **Monitoreo y Gestión:** Implementar herramientas de monitoreo para observar el tráfico y el rendimiento de las VLANs.
6. **Consistencia:** Asegurarse de que la configuración de VLAN sea consistente en todos los switches de la red.
   

## Pasos a seguir:

### 1. Entrar en el Modo de Configuración Global

    system-view

### 2. Crear una VLAN

Para crear una VLAN, usar el siguiente comando. Por ejemplo, para crear la VLAN 10:

    vlan 10
    commit

Se aconseja añadir descripción para facilitar identificación de la vlan

    vlan 10
    description VLAN_SERVICIOS
    commit

### 4. Asignar Puertos a la VLAN

Asignamos los puertos a la VLAN recién creada. En este ejemplo, asignaremos los puertos Ethernet 1/0/1 y 1/0/2 a la VLAN 10.

    interface Ethernet1/0/1
    port link-type access
    port default vlan 10
    commit
    
    interface Ethernet1/0/2
    port link-type access
    port default vlan 10
    commit

**NOTA**: En este caso hemos configurado los puertos en modo access, es posible configurarlos en modo trunk con el siguiente paso (Consultar la guia de Modo Access vs Modo Trunk)


### 5. Configurar una VLAN Trunk

Si necesitamos que un puerto transporte tráfico de múltiples VLANs, lo configuraremos como puerto trunk. En este ejemplo, configuramos el puerto Ethernet 1/0/3 como trunk para las VLANs 10 y 20.

```shell
interface Ethernet1/0/3
port link-type trunk
port trunk allow-pass vlan 10 20
commit
```


