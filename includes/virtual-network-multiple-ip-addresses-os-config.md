## <a name="os-config"></a>Agregar sistema operativo VM tooa que las direcciones IP

Conéctese y tooa VM de inicio de sesión que creó con varias direcciones IP privadas. Debe agregar manualmente todos los Hola direcciones IP privadas (incluidas las principales Hola) que ha agregado toohello máquina virtual. Hola completa siguiendo los pasos para su sistema operativo de máquina virtual:

### <a name="windows"></a>Windows

1. En un símbolo del sistema, escriba *ipconfig /all*.  Sólo verá hello *principal* dirección IP privada (a través de DHCP).
2. Tipo de *ncpa.cpl* Hola símbolo tooopen Hola **las conexiones de red** ventana.
3. Abrir propiedades de hello para el adaptador adecuado de hello: **conexión de área Local**.
4. Haga doble clic en el Protocolo de Internet versión 4 (IPv4).
5. Seleccione **Hola de uso siguiente dirección IP** y escriba Hola siguientes valores:

    * **Dirección IP**: escriba hello *principal* dirección IP privada
    * **Máscara de subred**: establezca este valor en función de su subred. Por ejemplo, si hello subred es un /24 subred, a continuación, subred Hola máscara es 255.255.255.0.
    * **Puerta de enlace predeterminada**: Hola la primera dirección IP de subred Hola. Si está de la subred 10.0.0.0/24, dirección IP de puerta de enlace de hello oscila entre 10.0.0.1.
    * Haga clic en **Hola de uso después de direcciones de servidor DNS** y escriba Hola siguientes valores:
        * **Servidor DNS preferido:** escriba 168.63.129.16 si no usa su propio servidor DNS.  Si usa su propio servidor DNS, escriba la dirección IP de hello para el servidor.
    * Haga clic en hello **avanzadas** botón y agregue las direcciones IP adicionales. Agregue cada uno de hello secundarias direcciones IP privadas aparecen en el paso 8 toohello NIC con hello misma subred especificada para la dirección IP principal de Hola.
        >[!WARNING] 
        >Si no siga los pasos de hello anteriores correctamente, puede perder conectividad tooyour máquina virtual. Asegúrese de información de hello escrita en el paso 5 es correcta antes de continuar.

    * Haga clic en **Aceptar** tooclose valores de hello TCP/IP y, a continuación, **Aceptar** nuevo tooclose Hola configuración del adaptador. Se restablece la conexión RDP.

6. En un símbolo del sistema, escriba *ipconfig /all*. Se muestran todas las direcciones IP que agregó y DHCP está desactivado.


### <a name="validation-windows"></a>Validación (Windows)

tooensure toohello tooconnect capaz de internet desde la configuración de IP secundaria a través de hello mediante que IP pública asociados, una vez haya agregado correctamente los pasos anteriormente, use Hola siguiente comando:

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
>Para las configuraciones IP secundarias, solo puede hacer ping toohello Internet si configuración de hello tiene una dirección IP pública asociada con él. Para configuraciones de IP principales, una dirección IP pública no es necesario tooping toohello Internet.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)

1. Abra una ventana del terminal.
2. Asegúrese de que los usuarios de raíz de Hola. Si no está, escriba Hola siguiente comando:

    ```bash
    sudo -i
    ```

3. Actualizar el archivo de configuración de Hola de interfaz de red de hello (suponiendo que 'eth0').

    * Mantener el artículo de línea existente de Hola para dhcp. dirección IP principal de Hello permanece configurado que tenía anteriormente.
    * Agregue una configuración para una dirección IP estática con hello siguientes comandos:

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    Debería ver un archivo .cfg.
4. Archivo de hello abierto. Debería ver Hola siguientes líneas al final de hello del archivo hello:

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. Agregue Hola siguiendo las líneas después de las líneas de Hola que existen en este archivo:

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. Guardar archivo hello mediante Hola siguiente comando:

    ```bash
    :wq
    ```

7. Restablecer la interfaz de red de hello sin Hola siguiente comando:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > Ejecute ifdown y ifup en hello misma línea si usa una conexión remota.
    >

8. Compruebe la dirección IP de Hola se ha agregado toohello interfaz de red con hello siguiente comando:

    ```bash
    ip addr list eth0
    ```

    Debería ver Hola IP direcciones que ha agregado como parte de la lista de Hola.

### <a name="linux-redhat-centos-and-others"></a>Linux (Redhat, CentOS y otros)

1. Abra una ventana del terminal.
2. Asegúrese de que los usuarios de raíz de Hola. Si no está, escriba Hola siguiente comando:

    ```bash
    sudo -i
    ```

3. Escriba la contraseña y siga las instrucciones que aparezcan. Una vez haya usuario raíz de hello, desplazarse por las carpetas de las secuencias de comandos de red de toohello con hello siguiente comando:

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. Hola de lista relacionados con archivos ifcfg mediante el siguiente comando de hello:

    ```bash
    ls ifcfg-*
    ```

    Debería ver *ifcfg eth0* como uno de los archivos de saludo.

5. tooadd una dirección IP, cree un archivo de configuración para él, tal y como se muestra a continuación. Tenga en cuenta que debe crearse un archivo para cada configuración de IP.

    ```bash
    touch ifcfg-eth0:0
    ```

6. Abra hello *ifcfg-eth0:0* archivo con hello siguiente comando:

    ```bash
    vi ifcfg-eth0:0
    ```

7. Agregue el archivo de contenido toohello, *eth0:0* en este caso, con el siguiente comando de Hola. Información de tooupdate seguro basarse en la dirección IP.

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. Guardar archivo hello con hello siguiente comando:

    ```bash
    :wq
    ```

9. Reinicie los servicios de red de Hola y asegúrese de que Hola cambios son correctos mediante la ejecución de hello siguientes comandos:

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    Debería ver Hola IP direcciones que ha agregado, *eth0:0*, en lista de hello devuelta.

### <a name="validation-linux"></a>Validación (Linux)

tooensure son toohello tooconnect capaz de internet desde la configuración de IP secundaria a través de la dirección IP pública de hello asociado, use Hola siguiente comando:

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
>Para las configuraciones IP secundarias, solo puede hacer ping toohello Internet si configuración de hello tiene una dirección IP pública asociada con él. Para configuraciones de IP principales, una dirección IP pública no es necesario tooping toohello Internet.

Para máquinas virtuales de Linux, al tratar de toovalidate conectividad saliente de una NIC secundaria, puede que necesite tooadd de rutas adecuadas. Hay muchas toodo formas esto. Consulte la documentación correspondiente a su distribución de Linux. siguiente Hello es tooaccomplish de un método:

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- Ser tooreplace seguro:
    - **10.0.0.5** con la dirección IP privada de hello dirección que tiene una dirección IP pública dirección tooit asociado
    - **10.0.0.1** tooyour puerta de enlace predeterminada
    - **eth2** toohello nombre de la NIC secundaria
