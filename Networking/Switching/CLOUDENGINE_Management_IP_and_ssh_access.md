## Objetivo técnico
Acceder en remoto a un switch instalado en cliente para posterior configuración.

## Mejores prácticas
Usar interfaz meth out of band como management.

### Pasos a seguir:

1. **Configurar usuario en el AAA del dispositivo**

    ```shell
    aaa
    local-user sshadmin password irreversible-cipher "contraseñasegura"
    local-user sshadmin service-type ssh
    local-user sshadmin level 3
    ```

2. **Habilitar servicio SSH**

    ```shell
    stelnet server enable
    ```

3. **Configurar usuario SSH**

    ```shell
    ssh user sshadmin
    ssh user sshadmin authentication-type password
    ssh user sshadmin service-type all
    ssh server-source -i MEth0/0/0
    ssh authorization-type default aaa
    ```

4. **Configurar TTY**

    ```shell
    user-interface vty 0 4
    authentication-mode aaa
    protocol inbound all
    ```

5. **Configurar IP gestión a interfaz**

    ```shell
    interface meth 0/0/0
    ip address X.X.X.X XX
    ```

6. **Añadir ruta para poder acceder desde fuera de la red OOB**

    ```shell
    ip route-static 0.0.0.0 0.0.0.0 X.X.X.X (gateway)
    ```





