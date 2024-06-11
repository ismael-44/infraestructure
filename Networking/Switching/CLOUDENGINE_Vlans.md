## Objetivo técnico
Se pretende apilar switches L2 para tener un único plano de management para estos.

## Mejores prácticas
Las configuraciones recomendadas por el fabricante son:

- No se deben conectar cables hasta que se indique en los pasos posteriores.
- Máximo de 9 switches para asegurar rendimiento y no sobrecargar las CPUs de los switches.
- Para formar stack los switches deben ser del mismo tipo, serie y subserie.
- Los puertos de configuración de stack deben ser del mismo tipo, no siendo posible la configuración entre puertos 10G y 40G por ejemplo.
- Se pueden usar cables dedicados para stack o crear una agrupación lógica de puertos para usarlos con fin de montar el stack.

## Pasos a seguir:

1. **Definir parámetros de stack**

    Debemos definir 3 parámetros importantes en cada switch para la configuración del stack:
    
    - **Stack domain ID:** este ID debe ser único en la red de switches e idéntico para los switches que formarán parte de la pila.
    
       **Switch 1:**
        
        ```shell
        system-view
        stack
        stack member 1 domain ID 10
        ```
        
        **Switch 2:**
        
        ```shell
        system-view
        stack
        stack member 1 domain ID 10
        ```
    
    - **Stack ID:** todos los switches de un mismo dominio de stack deben tener un ID único, por defecto es 1.
        
        **Switch 2:**
    
        ```shell
        system-view
        stack
        stack member 1 renumber 2
        ```
        
    - **Stack priority:** El dispositivo con **mayor** número de prioridad definirá el switch maestro. Por defecto la prioridad es 100. En este ejemplo el Switch 1 será el maestro.
    
        **Switch 1:**
        
        ```shell
        system-view
        stack
        stack member 1 priority 200
        ```
        
        **Switch 2:**
        
        ```shell
        system-view
        stack
        stack member 2 priority 100
        ```
        
    Salir de system-view y guardar los cambios.

2. **Reiniciar**

    Debemos reiniciar las máquinas para que apliquen la configuración de stack.

    ```shell
    reboot
    ```

3. **Configurar puertos de stack**

    Primero bajamos las interfaces de acuerdo con lo que dice el fabricante.
    
    **Switch 1:**

    ```shell
    system-view
    interface 40GE 1/0/1
    shutdown
    quit
    interface 40GE 1/0/2
    shutdown
    quit
    ```
    
    **Switch 2:**
    
    ```shell
    system-view
    interface 40GE 2/0/1
    shutdown
    quit
    interface 40GE 2/0/2
    shutdown
    quit
    ```
        
    Debemos configurar un puerto lógico que sea una agrupación de puertos físicos, los cuales, serán usados para el stack. En este caso usaremos 2 interfaces 40G. 
    
    **Switch 1:** 
    
    ```shell
    system-view
    interface Stack-Port 1/1
    port member-group interface 40GE 1/0/1 to 40GE 1/0/2
    ```
    
    **Switch 2:**
    
    ```shell
    system-view
    interface Stack-Port 2/2
    port member-group interface 40GE 2/0/1 to 40GE 2/0/2
    ```
    
    Salir de system-view y guardar los cambios.
    
    **NOTA:** Es importante que la interfaz de stack virtual tenga un ID acorde al Stack ID de la máquina. Ejemplo: para el miembro 2 la interfaz debe ser 2/2, para el miembro 3 debe ser 3/3...

4. **Reiniciar**

    El módulo de stack arranca al inicio de las máquinas, por lo que, tras reiniciar, debe estar el stack montado.

    ```shell
    reboot
    ```
