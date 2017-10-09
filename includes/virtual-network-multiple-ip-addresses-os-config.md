## <span data-ttu-id="68f4a-101"><a name="os-config"></a>Agregar sistema operativo VM tooa que las direcciones IP</span><span class="sxs-lookup"><span data-stu-id="68f4a-101"><a name="os-config"></a>Add IP addresses tooa VM operating system</span></span>

<span data-ttu-id="68f4a-102">Conéctese y tooa VM de inicio de sesión que creó con varias direcciones IP privadas.</span><span class="sxs-lookup"><span data-stu-id="68f4a-102">Connect and login tooa VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="68f4a-103">Debe agregar manualmente todos los Hola direcciones IP privadas (incluidas las principales Hola) que ha agregado toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="68f4a-103">You must manually add all hello private IP addresses (including hello primary) that you added toohello VM.</span></span> <span data-ttu-id="68f4a-104">Hola completa siguiendo los pasos para su sistema operativo de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="68f4a-104">Complete hello following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="68f4a-105">Windows</span><span class="sxs-lookup"><span data-stu-id="68f4a-105">Windows</span></span>

1. <span data-ttu-id="68f4a-106">En un símbolo del sistema, escriba *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="68f4a-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="68f4a-107">Sólo verá hello *principal* dirección IP privada (a través de DHCP).</span><span class="sxs-lookup"><span data-stu-id="68f4a-107">You only see hello *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="68f4a-108">Tipo de *ncpa.cpl* Hola símbolo tooopen Hola **las conexiones de red** ventana.</span><span class="sxs-lookup"><span data-stu-id="68f4a-108">Type *ncpa.cpl* in hello command prompt tooopen hello **Network connections** window.</span></span>
3. <span data-ttu-id="68f4a-109">Abrir propiedades de hello para el adaptador adecuado de hello: **conexión de área Local**.</span><span class="sxs-lookup"><span data-stu-id="68f4a-109">Open hello properties for hello appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="68f4a-110">Haga doble clic en el Protocolo de Internet versión 4 (IPv4).</span><span class="sxs-lookup"><span data-stu-id="68f4a-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="68f4a-111">Seleccione **Hola de uso siguiente dirección IP** y escriba Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="68f4a-111">Select **Use hello following IP address** and enter hello following values:</span></span>

    * <span data-ttu-id="68f4a-112">**Dirección IP**: escriba hello *principal* dirección IP privada</span><span class="sxs-lookup"><span data-stu-id="68f4a-112">**IP address**: Enter hello *Primary* private IP address</span></span>
    * <span data-ttu-id="68f4a-113">**Máscara de subred**: establezca este valor en función de su subred.</span><span class="sxs-lookup"><span data-stu-id="68f4a-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="68f4a-114">Por ejemplo, si hello subred es un /24 subred, a continuación, subred Hola máscara es 255.255.255.0.</span><span class="sxs-lookup"><span data-stu-id="68f4a-114">For example, if hello subnet is a /24 subnet then hello subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="68f4a-115">**Puerta de enlace predeterminada**: Hola la primera dirección IP de subred Hola.</span><span class="sxs-lookup"><span data-stu-id="68f4a-115">**Default gateway**: hello first IP address in hello subnet.</span></span> <span data-ttu-id="68f4a-116">Si está de la subred 10.0.0.0/24, dirección IP de puerta de enlace de hello oscila entre 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="68f4a-116">If your subnet is 10.0.0.0/24, then hello gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="68f4a-117">Haga clic en **Hola de uso después de direcciones de servidor DNS** y escriba Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="68f4a-117">Click **Use hello following DNS server addresses** and enter hello following values:</span></span>
        * <span data-ttu-id="68f4a-118">**Servidor DNS preferido:** escriba 168.63.129.16 si no usa su propio servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="68f4a-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="68f4a-119">Si usa su propio servidor DNS, escriba la dirección IP de hello para el servidor.</span><span class="sxs-lookup"><span data-stu-id="68f4a-119">If you are using your own DNS server, enter hello IP address for your server.</span></span>
    * <span data-ttu-id="68f4a-120">Haga clic en hello **avanzadas** botón y agregue las direcciones IP adicionales.</span><span class="sxs-lookup"><span data-stu-id="68f4a-120">Click hello **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="68f4a-121">Agregue cada uno de hello secundarias direcciones IP privadas aparecen en el paso 8 toohello NIC con hello misma subred especificada para la dirección IP principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="68f4a-121">Add each of hello secondary private IP addresses listed in step 8 toohello NIC with hello same subnet specified for hello primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="68f4a-122">Si no siga los pasos de hello anteriores correctamente, puede perder conectividad tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="68f4a-122">If you do not follow hello steps above correctly, you may lose connectivity tooyour VM.</span></span> <span data-ttu-id="68f4a-123">Asegúrese de información de hello escrita en el paso 5 es correcta antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="68f4a-123">Ensure hello information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="68f4a-124">Haga clic en **Aceptar** tooclose valores de hello TCP/IP y, a continuación, **Aceptar** nuevo tooclose Hola configuración del adaptador.</span><span class="sxs-lookup"><span data-stu-id="68f4a-124">Click **OK** tooclose out hello TCP/IP settings and then **OK** again tooclose hello adapter settings.</span></span> <span data-ttu-id="68f4a-125">Se restablece la conexión RDP.</span><span class="sxs-lookup"><span data-stu-id="68f4a-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="68f4a-126">En un símbolo del sistema, escriba *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="68f4a-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="68f4a-127">Se muestran todas las direcciones IP que agregó y DHCP está desactivado.</span><span class="sxs-lookup"><span data-stu-id="68f4a-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="68f4a-128">Validación (Windows)</span><span class="sxs-lookup"><span data-stu-id="68f4a-128">Validation (Windows)</span></span>

<span data-ttu-id="68f4a-129">tooensure toohello tooconnect capaz de internet desde la configuración de IP secundaria a través de hello mediante que IP pública asociados, una vez haya agregado correctamente los pasos anteriormente, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="68f4a-129">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, once you have added it correctly using steps above, use hello following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="68f4a-130">Para las configuraciones IP secundarias, solo puede hacer ping toohello Internet si configuración de hello tiene una dirección IP pública asociada con él.</span><span class="sxs-lookup"><span data-stu-id="68f4a-130">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="68f4a-131">Para configuraciones de IP principales, una dirección IP pública no es necesario tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="68f4a-131">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="68f4a-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="68f4a-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="68f4a-133">Abra una ventana del terminal.</span><span class="sxs-lookup"><span data-stu-id="68f4a-133">Open a terminal window.</span></span>
2. <span data-ttu-id="68f4a-134">Asegúrese de que los usuarios de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="68f4a-134">Make sure you are hello root user.</span></span> <span data-ttu-id="68f4a-135">Si no está, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="68f4a-135">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="68f4a-136">Actualizar el archivo de configuración de Hola de interfaz de red de hello (suponiendo que 'eth0').</span><span class="sxs-lookup"><span data-stu-id="68f4a-136">Update hello configuration file of hello network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="68f4a-137">Mantener el artículo de línea existente de Hola para dhcp.</span><span class="sxs-lookup"><span data-stu-id="68f4a-137">Keep hello existing line item for dhcp.</span></span> <span data-ttu-id="68f4a-138">dirección IP principal de Hello permanece configurado que tenía anteriormente.</span><span class="sxs-lookup"><span data-stu-id="68f4a-138">hello primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="68f4a-139">Agregue una configuración para una dirección IP estática con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="68f4a-139">Add a configuration for an additional static IP address with hello following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="68f4a-140">Debería ver un archivo .cfg.</span><span class="sxs-lookup"><span data-stu-id="68f4a-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="68f4a-141">Archivo de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="68f4a-141">Open hello file.</span></span> <span data-ttu-id="68f4a-142">Debería ver Hola siguientes líneas al final de hello del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="68f4a-142">You should see hello following lines at hello end of hello file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="68f4a-143">Agregue Hola siguiendo las líneas después de las líneas de Hola que existen en este archivo:</span><span class="sxs-lookup"><span data-stu-id="68f4a-143">Add hello following lines after hello lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="68f4a-144">Guardar archivo hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="68f4a-144">Save hello file by using hello following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="68f4a-145">Restablecer la interfaz de red de hello sin Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="68f4a-145">Reset hello network interface with hello following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="68f4a-146">Ejecute ifdown y ifup en hello misma línea si usa una conexión remota.</span><span class="sxs-lookup"><span data-stu-id="68f4a-146">Run both ifdown and ifup in hello same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="68f4a-147">Compruebe la dirección IP de Hola se ha agregado toohello interfaz de red con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="68f4a-147">Verify hello IP address is added toohello network interface with hello following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="68f4a-148">Debería ver Hola IP direcciones que ha agregado como parte de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="68f4a-148">You should see hello IP address you added as part of hello list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="68f4a-149">Linux (Redhat, CentOS y otros)</span><span class="sxs-lookup"><span data-stu-id="68f4a-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="68f4a-150">Abra una ventana del terminal.</span><span class="sxs-lookup"><span data-stu-id="68f4a-150">Open a terminal window.</span></span>
2. <span data-ttu-id="68f4a-151">Asegúrese de que los usuarios de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="68f4a-151">Make sure you are hello root user.</span></span> <span data-ttu-id="68f4a-152">Si no está, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="68f4a-152">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="68f4a-153">Escriba la contraseña y siga las instrucciones que aparezcan.</span><span class="sxs-lookup"><span data-stu-id="68f4a-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="68f4a-154">Una vez haya usuario raíz de hello, desplazarse por las carpetas de las secuencias de comandos de red de toohello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="68f4a-154">Once you are hello root user, navigate toohello network scripts folder with hello following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="68f4a-155">Hola de lista relacionados con archivos ifcfg mediante el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="68f4a-155">List hello related ifcfg files using hello following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="68f4a-156">Debería ver *ifcfg eth0* como uno de los archivos de saludo.</span><span class="sxs-lookup"><span data-stu-id="68f4a-156">You should see *ifcfg-eth0* as one of hello files.</span></span>

5. <span data-ttu-id="68f4a-157">tooadd una dirección IP, cree un archivo de configuración para él, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="68f4a-157">tooadd an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="68f4a-158">Tenga en cuenta que debe crearse un archivo para cada configuración de IP.</span><span class="sxs-lookup"><span data-stu-id="68f4a-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="68f4a-159">Abra hello *ifcfg-eth0:0* archivo con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="68f4a-159">Open hello *ifcfg-eth0:0* file with hello following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="68f4a-160">Agregue el archivo de contenido toohello, *eth0:0* en este caso, con el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="68f4a-160">Add content toohello file, *eth0:0* in this case, with hello following command.</span></span> <span data-ttu-id="68f4a-161">Información de tooupdate seguro basarse en la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="68f4a-161">Be sure tooupdate information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="68f4a-162">Guardar archivo hello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="68f4a-162">Save hello file with hello following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="68f4a-163">Reinicie los servicios de red de Hola y asegúrese de que Hola cambios son correctos mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="68f4a-163">Restart hello network services and make sure hello changes are successful by running hello following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="68f4a-164">Debería ver Hola IP direcciones que ha agregado, *eth0:0*, en lista de hello devuelta.</span><span class="sxs-lookup"><span data-stu-id="68f4a-164">You should see hello IP address you added, *eth0:0*, in hello list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="68f4a-165">Validación (Linux)</span><span class="sxs-lookup"><span data-stu-id="68f4a-165">Validation (Linux)</span></span>

<span data-ttu-id="68f4a-166">tooensure son toohello tooconnect capaz de internet desde la configuración de IP secundaria a través de la dirección IP pública de hello asociado, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="68f4a-166">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, use hello following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="68f4a-167">Para las configuraciones IP secundarias, solo puede hacer ping toohello Internet si configuración de hello tiene una dirección IP pública asociada con él.</span><span class="sxs-lookup"><span data-stu-id="68f4a-167">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="68f4a-168">Para configuraciones de IP principales, una dirección IP pública no es necesario tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="68f4a-168">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

<span data-ttu-id="68f4a-169">Para máquinas virtuales de Linux, al tratar de toovalidate conectividad saliente de una NIC secundaria, puede que necesite tooadd de rutas adecuadas.</span><span class="sxs-lookup"><span data-stu-id="68f4a-169">For Linux VMs, when trying toovalidate outbound connectivity from a secondary NIC, you may need tooadd appropriate routes.</span></span> <span data-ttu-id="68f4a-170">Hay muchas toodo formas esto.</span><span class="sxs-lookup"><span data-stu-id="68f4a-170">There are many ways toodo this.</span></span> <span data-ttu-id="68f4a-171">Consulte la documentación correspondiente a su distribución de Linux.</span><span class="sxs-lookup"><span data-stu-id="68f4a-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="68f4a-172">siguiente Hello es tooaccomplish de un método:</span><span class="sxs-lookup"><span data-stu-id="68f4a-172">hello following is one method tooaccomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="68f4a-173">Ser tooreplace seguro:</span><span class="sxs-lookup"><span data-stu-id="68f4a-173">Be sure tooreplace:</span></span>
    - <span data-ttu-id="68f4a-174">**10.0.0.5** con la dirección IP privada de hello dirección que tiene una dirección IP pública dirección tooit asociado</span><span class="sxs-lookup"><span data-stu-id="68f4a-174">**10.0.0.5** with hello private IP address that has a public IP address associated tooit</span></span>
    - <span data-ttu-id="68f4a-175">**10.0.0.1** tooyour puerta de enlace predeterminada</span><span class="sxs-lookup"><span data-stu-id="68f4a-175">**10.0.0.1** tooyour default gateway</span></span>
    - <span data-ttu-id="68f4a-176">**eth2** toohello nombre de la NIC secundaria</span><span class="sxs-lookup"><span data-stu-id="68f4a-176">**eth2** toohello name of your secondary NIC</span></span>
