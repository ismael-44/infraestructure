## Objetivo técnico
Se pretende agrupar dos switches formando una pareja DFS entre ellos, para poder configurar un MLAG contra otros dispositivos.

## Mejores prácticas
El farbicante no incluye apartado de mejores practicas específicas para esta tecnología

### Pasos a seguir:

1. **Definir grupo DFS**

    Se define el grupo DFS en ambos switches

    ```shell
    system-view
    dfs-group 1
    commit
    ```

2. **Autenticación del grupo DFS y DAD**

    Se **autentica el grupo con contraseña** y se habilita el **dual-active detection**. El dual-active es una conexión heartbeat que permite detectar el estado de la pareja y tomar medidas de recuperación para minimizar el impacto del split entre switches. Se recomienda usar la interfaz de mgmt como línea de hearbeat.

    Switch A

    ```shell
    authentication-mode hmac-sha256 password "contraseñasegura_2024"
    dual-active detection source ip "ip switch A" vpn-instance "instancia vpn para management" peer "ip switch B"  
    commit
    ```
    Switch B
    ```shell
    authentication-mode hmac-sha256 password "contraseñasegura_2024"
    dual-active detection source ip "ip switch B" vpn-instance "instancia vpn para management" peer "ip switch A" 
    commit
    ```
    
3. **Definir LACP para peerlinks**

    Se define un **LACP** para tener **redundancia entre enlaces** para la pareja DFS. Se **deshabilita el STP** ya que LACP es una tecnología libre de bucles. También se reduce el **timeout del LACP a 1s**, consumirá mas recursos pero dara una respuesta más ágil a la falla de un enlace.

    Switch A
    
    ```shell
    system-view
    interface Eth-Trunk1
    mode lacp-static
    lacp timeout fast
    peer-link 1
    commit
    ```
    Switch B
    
    ```shell
    system-view
    interface Eth-Trunk1
    mode lacp-static
    lacp timeout fast
    peer-link 1
    commit
    ```

4. **Añadir interfaces para peerlink al LACP anterior**

    Se añadiran las **interfaces dedicadas a peerlink** al enlace agregado definido anteriormente

    Switch A
    
    ```shell
    system-view
    interface 100GE 1/0/7
    eth-trunk 1
    
    interface 100GE 1/0/8
    eth-trunk 1
    commit
    ```
    Switch B
    ```shell
    system-view
    interface 100GE 1/0/7
    eth-trunk 1
    
    interface 100GE 1/0/8
    eth-trunk 1
    commit
    ```
    Puedes comprobar el enlace agregado con:
    
     ```shell
    display interface eth-trunk 1
    ```
5. **Definir interfaces para MLAG**

    Se trata de configurar **una interfaz por switch** para que formen un **enlace agregado multichasis**. Se debe marcar la interfaz con el ID del grupo DFS creado anteriormente y definir un ID para el M-LAG. Es importante que en ambos switches el M-LAG ID y el dfs-group ID **coincidan**.
    
    Switch A
    
    ```shell
    system-view
    interface Eth-Trunk6
    mode lacp-static
    lacp timeout fast
    dfs-group 1 m-lag 1
    ```
    
    Switch B
    
    ```shell
    system-view
    interface Eth-Trunk6
    mode lacp-static
    lacp timeout fast
    dfs-group 1 m-lag 1
    commit
    ```
    
    Puedes comprobar la configuración con:
    
    ```shell
    display dfs-group 1 m-lag brief
    ```
    Lo correcto es que las interfaces que configuraste para el m-lag aparezcan como "**active/active**"
    
    En caso de que el M-LAG se configure contra un equipo final, como un servidor, es importante añadir a la interfaz el atributo "**stp edged-port enable**". Gracias a esto este puerto no participará en el cáculo del protocolo spanning tree.
