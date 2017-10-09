---
title: red de local tooyour aaaConnect HDInsight - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una HDInsight de clúster en una red Virtual de Azure y, a continuación, conéctelo red de tooyour local. Obtenga información acerca de cómo tooconfigure resolución de nombres entre HDInsight y la red local mediante el uso de un servidor DNS personalizado."
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a><span data-ttu-id="f8aab-104">Conectar HDInsight tooyour en la red local</span><span class="sxs-lookup"><span data-stu-id="f8aab-104">Connect HDInsight tooyour on-premise network</span></span>

<span data-ttu-id="f8aab-105">Obtenga información acerca de cómo tooconnect HDInsight tooyour en local de red mediante redes virtuales de Azure y una puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="f8aab-105">Learn how tooconnect HDInsight tooyour on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="f8aab-106">En este documento se brinda información de planeación sobre:</span><span class="sxs-lookup"><span data-stu-id="f8aab-106">This document provides planning information on:</span></span>

* <span data-ttu-id="f8aab-107">Uso de HDInsight en una red Virtual de Azure que se conecta tooyour local de red.</span><span class="sxs-lookup"><span data-stu-id="f8aab-107">Using HDInsight in an Azure Virtual Network that connects tooyour on-premises network.</span></span>

* <span data-ttu-id="f8aab-108">Configuración de resolución de nombres DNS entre la red virtual de Hola y de la red local.</span><span class="sxs-lookup"><span data-stu-id="f8aab-108">Configuring DNS name resolution between hello virtual network and your on-premises network.</span></span>

* <span data-ttu-id="f8aab-109">Configuración de red seguridad grupos toorestrict internet acceso tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8aab-109">Configuring network security groups toorestrict internet access tooHDInsight.</span></span>

* <span data-ttu-id="f8aab-110">Puertos proporcionados por HDInsight en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-110">Ports provided by HDInsight on hello virtual network.</span></span>

## <a name="create-hello-virtual-network-configuration"></a><span data-ttu-id="f8aab-111">Crear configuración de red Virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="f8aab-111">Create hello Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8aab-112">Si desea obtener instrucciones paso a paso sobre cómo conectar HDInsight tooyour local de red mediante una red Virtual de Azure, vea hello [HDInsight conectar tooyour en la red local](connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="f8aab-112">If you are looking for step by step guidance on connecting HDInsight tooyour on-premises network using an Azure Virtual Network, see hello [Connect HDInsight tooyour on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="f8aab-113">Siguiente Hola de uso documenta toolearn cómo toocreate una red Virtual de Azure que está conectado tooyour local red:</span><span class="sxs-lookup"><span data-stu-id="f8aab-113">Use hello following documents toolearn how toocreate an Azure Virtual Network that is connected tooyour on-premises network:</span></span>
    
* [<span data-ttu-id="f8aab-114">Uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f8aab-114">Using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="f8aab-115">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8aab-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="f8aab-116">Uso de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f8aab-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="f8aab-117">Configuración de la resolución de nombres</span><span class="sxs-lookup"><span data-stu-id="f8aab-117">Configure name resolution</span></span>

<span data-ttu-id="f8aab-118">tooallow HDInsight y recursos de hello unido red toocommunicate por su nombre, debe realizar Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="f8aab-118">tooallow HDInsight and resources in hello joined network toocommunicate by name, you must perform hello following actions:</span></span>

* <span data-ttu-id="f8aab-119">Crear un servidor DNS personalizado en hello red Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8aab-119">Create a custom DNS server in hello Azure Virtual Network.</span></span>

* <span data-ttu-id="f8aab-120">Configurar Hola red virtual toouse Hola servidor DNS personalizado en lugar de forma predeterminada Hola resolución recursiva de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8aab-120">Configure hello virtual network toouse hello custom DNS server instead of hello default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="f8aab-121">Configure el enrutamiento entre servidores DNS personalizados de Hola y el servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="f8aab-121">Configure forwarding between hello custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="f8aab-122">Esta configuración permite Hola siguiente comportamiento:</span><span class="sxs-lookup"><span data-stu-id="f8aab-122">This configuration enables hello following behavior:</span></span>

* <span data-ttu-id="f8aab-123">Las solicitudes de nombres de dominio completo que tienen el sufijo DNS de hello __para la red virtual de hello__ se reenvían toohello servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="f8aab-123">Requests for fully qualified domain names that have hello DNS suffix __for hello virtual network__ are forwarded toohello custom DNS server.</span></span> <span data-ttu-id="f8aab-124">servidor DNS personalizado de Hello, a continuación, reenvía estos toohello solicitudes resolución recursiva de Azure, que devuelve la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-124">hello custom DNS server then forwards these requests toohello Azure Recursive Resolver, which returns hello IP address.</span></span>

* <span data-ttu-id="f8aab-125">Todas las demás solicitudes se reenvían a servidor DNS local toohello.</span><span class="sxs-lookup"><span data-stu-id="f8aab-125">All other requests are forwarded toohello on-premises DNS server.</span></span> <span data-ttu-id="f8aab-126">Incluso las solicitudes para recursos de internet pública como microsoft.com se reenvían toohello servidor DNS local para la resolución de nombres.</span><span class="sxs-lookup"><span data-stu-id="f8aab-126">Even requests for public internet resources such as microsoft.com are forwarded toohello on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="f8aab-127">Hola siguiente diagrama, líneas verdes son solicitudes para recursos que terminen en el sufijo DNS de Hola de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-127">In hello following diagram, green lines are requests for resources that end in hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="f8aab-128">Líneas azules son solicitudes para recursos en la red local de Hola o en Hola internet pública.</span><span class="sxs-lookup"><span data-stu-id="f8aab-128">Blue lines are requests for resources in hello on-premises network or on hello public internet.</span></span>

![Diagrama de cómo se resuelven las solicitudes DNS en la configuración de hello usado en este documento](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="f8aab-130">Creación de un servidor DNS personalizado</span><span class="sxs-lookup"><span data-stu-id="f8aab-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8aab-131">Debe crear y configurar el servidor DNS de hello antes de instalar HDInsight en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-131">You must create and configure hello DNS server before installing HDInsight into hello virtual network.</span></span>

<span data-ttu-id="f8aab-132">una VM de Linux que usa hello toocreate [enlazar](https://www.isc.org/downloads/bind/) software DNS, Hola uso pasos:</span><span class="sxs-lookup"><span data-stu-id="f8aab-132">toocreate a Linux VM that uses hello [Bind](https://www.isc.org/downloads/bind/) DNS software, use hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="f8aab-133">pasos siguientes Hello utilizan hello [portal de Azure](https://portal.azure.com) toocreate máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8aab-133">hello following steps use hello [Azure portal](https://portal.azure.com) toocreate an Azure Virtual Machine.</span></span> <span data-ttu-id="f8aab-134">Para otro toocreate formas una máquina virtual, vea hello [crear VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) y [crear VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documentos.</span><span class="sxs-lookup"><span data-stu-id="f8aab-134">For other ways toocreate a virtual machine, see hello [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="f8aab-135">De hello [portal de Azure](https://portal.azure.com), seleccione  __+__ , __proceso__, y __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="f8aab-135">From hello [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Creación de una máquina virtual Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="f8aab-137">De hello __Fundamentos__ sección, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="f8aab-137">From hello __Basics__ section, enter hello following information:</span></span>

    * <span data-ttu-id="f8aab-138">__Nombre__: nombre descriptivo que identifica esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f8aab-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="f8aab-139">Por ejemplo, __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="f8aab-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="f8aab-140">__Nombre de usuario__: nombre de Hola de hello cuenta SSH.</span><span class="sxs-lookup"><span data-stu-id="f8aab-140">__User name__: hello name of hello SSH account.</span></span>
    * <span data-ttu-id="f8aab-141">__Clave pública SSH__ o __contraseña__: Hola método de autenticación para hello cuenta SSH.</span><span class="sxs-lookup"><span data-stu-id="f8aab-141">__SSH public key__ or __Password__: hello authentication method for hello SSH account.</span></span> <span data-ttu-id="f8aab-142">Se recomienda usar claves públicas, porque son más seguras.</span><span class="sxs-lookup"><span data-stu-id="f8aab-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="f8aab-143">Para obtener más información, vea hello [crear y usar claves SSH para máquinas virtuales Linux](../virtual-machines/linux/mac-create-ssh-keys.md) documento.</span><span class="sxs-lookup"><span data-stu-id="f8aab-143">For more information, see hello [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="f8aab-144">__Grupo de recursos__: seleccione __utilizar existente__y, a continuación, seleccione grupo de recursos de Hola que contiene Hola red virtual que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f8aab-144">__Resource group__: Select __Use existing__, and then select hello resource group that contains hello virtual network created earlier.</span></span>
    * <span data-ttu-id="f8aab-145">__Ubicación__: seleccione Hola la misma ubicación que la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-145">__Location__: Select hello same location as hello virtual network.</span></span>

    ![Configuración básica de la máquina virtual](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="f8aab-147">Deje las demás entradas en hello valores predeterminados y, a continuación, seleccione __Aceptar__.</span><span class="sxs-lookup"><span data-stu-id="f8aab-147">Leave other entries at hello default values and then select __OK__.</span></span>

3. <span data-ttu-id="f8aab-148">De hello __elegir un tamaño de__ sección, tamaño de máquina virtual de hello select.</span><span class="sxs-lookup"><span data-stu-id="f8aab-148">From hello __Choose a size__ section, select hello VM size.</span></span> <span data-ttu-id="f8aab-149">Para este tutorial, seleccione hello más pequeño y opción de costo más bajo.</span><span class="sxs-lookup"><span data-stu-id="f8aab-149">For this tutorial, select hello smallest and lowest cost option.</span></span> <span data-ttu-id="f8aab-150">toocontinue, use hello __seleccione__ botón.</span><span class="sxs-lookup"><span data-stu-id="f8aab-150">toocontinue, use hello __Select__ button.</span></span>

4. <span data-ttu-id="f8aab-151">De hello __configuración__ sección, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="f8aab-151">From hello __Settings__ section, enter hello following information:</span></span>

    * <span data-ttu-id="f8aab-152">__Red virtual__: seleccione Hola red virtual que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f8aab-152">__Virtual network__: Select hello virtual network that you created earlier.</span></span>

    * <span data-ttu-id="f8aab-153">__Subred__: seleccione subred predeterminada de hello para la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-153">__Subnet__: Select hello default subnet for hello virtual network.</span></span> <span data-ttu-id="f8aab-154">Hacer __no__ seleccione Hola subred usada por la puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-154">Do __not__ select hello subnet used by hello VPN gateway.</span></span>

    * <span data-ttu-id="f8aab-155">__Cuenta de almacenamiento de diagnóstico__: seleccione una cuenta de almacenamiento existente o cree una nueva.</span><span class="sxs-lookup"><span data-stu-id="f8aab-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Configuración de la red virtual](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="f8aab-157">Deje las demás entradas de Hola como valor predeterminado de hello, a continuación, seleccione __Aceptar__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f8aab-157">Leave hello other entries at hello default value, then select __OK__ toocontinue.</span></span>

5. <span data-ttu-id="f8aab-158">De hello __compra__ sección, seleccione hello __compra__ máquina virtual de botón toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-158">From hello __Purchase__ section, select hello __Purchase__ button toocreate hello virtual machine.</span></span>

6. <span data-ttu-id="f8aab-159">Una vez creada la máquina virtual de hello, su __Introducción__ sección se muestra.</span><span class="sxs-lookup"><span data-stu-id="f8aab-159">Once hello virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="f8aab-160">En la lista Hola Hola izquierda, seleccione __propiedades__.</span><span class="sxs-lookup"><span data-stu-id="f8aab-160">From hello list on hello left, select __Properties__.</span></span> <span data-ttu-id="f8aab-161">Guardar hello __dirección IP pública__ y __dirección IP privada__ valores.</span><span class="sxs-lookup"><span data-stu-id="f8aab-161">Save hello __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="f8aab-162">Se utilizará en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-162">It will be used in hello next section.</span></span>

    ![Direcciones IP pública y privada](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="f8aab-164">Instalación y configuración de Bind (software DNS)</span><span class="sxs-lookup"><span data-stu-id="f8aab-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="f8aab-165">Utilizar SSH tooconnect toohello __dirección IP pública__ de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-165">Use SSH tooconnect toohello __public IP address__ of hello virtual machine.</span></span> <span data-ttu-id="f8aab-166">Hola siguiente ejemplo conecta a máquina virtual de tooa en 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="f8aab-166">hello following example connects tooa virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="f8aab-167">Reemplace `sshuser` con hello cuenta de usuario SSH que especificó al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-167">Replace `sshuser` with hello SSH user account you specified when creating hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f8aab-168">Hay una variedad de Hola de formas tooobtain `ssh` utilidad.</span><span class="sxs-lookup"><span data-stu-id="f8aab-168">There are a variety of ways tooobtain hello `ssh` utility.</span></span> <span data-ttu-id="f8aab-169">En Linux, Unix y macOS, se proporciona como parte del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-169">On Linux, Unix, and macOS, it is provided as part of hello operating system.</span></span> <span data-ttu-id="f8aab-170">Si usas Windows, considere una de las siguientes opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="f8aab-170">If you are using Windows, consider one of hello following options:</span></span>
    >
    > * [<span data-ttu-id="f8aab-171">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="f8aab-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="f8aab-172">Bash en Ubuntu en Windows 10</span><span class="sxs-lookup"><span data-stu-id="f8aab-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="f8aab-173">GIT (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="f8aab-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="f8aab-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="f8aab-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="f8aab-175">tooinstall Bind, utilice Hola siga los comandos de la sesión de SSH de hello:</span><span class="sxs-lookup"><span data-stu-id="f8aab-175">tooinstall Bind, use hello following commands from hello SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="f8aab-176">tooconfigure tooforward nombre resolución solicitudes tooyour local DNS servidor Bind, usar hello después de texto como contenido de Hola de hello `/etc/bind/named.conf.options` archivo:</span><span class="sxs-lookup"><span data-stu-id="f8aab-176">tooconfigure Bind tooforward name resolution requests tooyour on-prem DNS server, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="f8aab-177">Reemplace los valores de hello en hello `goodclients` sección con el intervalo de direcciones IP de Hola de red virtual de Hola y red local.</span><span class="sxs-lookup"><span data-stu-id="f8aab-177">Replace hello values in hello `goodclients` section with hello IP address range of hello virtual network and on-premises network.</span></span> <span data-ttu-id="f8aab-178">Esta sección define las direcciones de Hola que este servidor DNS acepta solicitudes de.</span><span class="sxs-lookup"><span data-stu-id="f8aab-178">This section defines hello addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="f8aab-179">Reemplace hello `192.168.0.1` entrada Hola `forwarders` sección con la dirección IP de saludo del servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="f8aab-179">Replace hello `192.168.0.1` entry in hello `forwarders` section with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="f8aab-180">Esta tooyour de las solicitudes de entrada rutas DNS local de servidor DNS para la resolución.</span><span class="sxs-lookup"><span data-stu-id="f8aab-180">This entry routes DNS requests tooyour on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="f8aab-181">tooedit este archivo, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f8aab-181">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="f8aab-182">archivo de hello toosave, use __CTRL+x__, __Y__y, a continuación, __ENTRAR__.</span><span class="sxs-lookup"><span data-stu-id="f8aab-182">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="f8aab-183">Desde la sesión de SSH de hello, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f8aab-183">From hello SSH session, use hello following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="f8aab-184">Este comando devuelve un toohello similar valor siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="f8aab-184">This command returns a value similar toohello following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="f8aab-185">Hola `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` texto es hello __sufijo DNS__ para esta red virtual.</span><span class="sxs-lookup"><span data-stu-id="f8aab-185">hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is hello __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="f8aab-186">Guarde este valor, porque se usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="f8aab-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="f8aab-187">Enlace de nombres DNS tooconfigure tooresolve para los recursos de red virtual de hello, usar hello después de texto como contenido de Hola de hello `/etc/bind/named.conf.local` archivo:</span><span class="sxs-lookup"><span data-stu-id="f8aab-187">tooconfigure Bind tooresolve DNS names for resources within hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="f8aab-188">Debe reemplazar hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` con el sufijo DNS de hello recuperó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f8aab-188">You must replace hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with hello DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="f8aab-189">tooedit este archivo, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f8aab-189">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="f8aab-190">archivo de hello toosave, use __CTRL+x__, __Y__y, a continuación, __ENTRAR__.</span><span class="sxs-lookup"><span data-stu-id="f8aab-190">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="f8aab-191">toostart Bind, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f8aab-191">toostart Bind, use hello following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="f8aab-192">tooverify que enlazan puede resolver los nombres de Hola de recursos de la red local, Hola de uso después de comandos:</span><span class="sxs-lookup"><span data-stu-id="f8aab-192">tooverify that bind can resolve hello names of resources in your on-premises network, use hello following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="f8aab-193">Reemplace `dns.mynetwork.net` con el nombre de dominio completo (FQDN) de Hola de un recurso en la red local.</span><span class="sxs-lookup"><span data-stu-id="f8aab-193">Replace `dns.mynetwork.net` with hello fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="f8aab-194">Reemplace `10.0.0.4` con hello __dirección IP interna__ del servidor DNS personalizado en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-194">Replace `10.0.0.4` with hello __internal IP address__ of your custom DNS server in hello virtual network.</span></span>

    <span data-ttu-id="f8aab-195">respuesta de Hola aparece toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="f8aab-195">hello response appears similar toohello following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a><span data-ttu-id="f8aab-196">Configurar servidor DNS personalizado de hello red virtual toouse Hola</span><span class="sxs-lookup"><span data-stu-id="f8aab-196">Configure hello virtual network toouse hello custom DNS server</span></span>

<span data-ttu-id="f8aab-197">tooconfigure Hola red virtual toouse Hola servidor DNS personalizado en lugar de hello resolución recursiva de Azure, use Hola siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="f8aab-197">tooconfigure hello virtual network toouse hello custom DNS server instead of hello Azure recursive resolver, use hello following steps:</span></span>

1. <span data-ttu-id="f8aab-198">Hola [portal de Azure](https://portal.azure.com), seleccione la red virtual de hello y, a continuación, seleccione __servidores DNS__.</span><span class="sxs-lookup"><span data-stu-id="f8aab-198">In hello [Azure portal](https://portal.azure.com), select hello virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="f8aab-199">Seleccione __personalizado__y escriba hello __dirección IP interna__ del servidor DNS personalizado Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-199">Select __Custom__, and enter hello __internal IP address__ of hello custom DNS server.</span></span> <span data-ttu-id="f8aab-200">Por último, seleccione __Guardar__.</span><span class="sxs-lookup"><span data-stu-id="f8aab-200">Finally, select __Save__.</span></span>

    ![Servidor DNS conjunto Hola personalizado para la red de Hola](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a><span data-ttu-id="f8aab-202">Configurar servidor DNS local Hola</span><span class="sxs-lookup"><span data-stu-id="f8aab-202">Configure hello on-premises DNS server</span></span>

<span data-ttu-id="f8aab-203">En la sección anterior de hello, configuró Hola personalizado DNS server tooforward solicitudes toohello en servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="f8aab-203">In hello previous section, you configured hello custom DNS server tooforward requests toohello on-premises DNS server.</span></span> <span data-ttu-id="f8aab-204">A continuación, debe configurar hello en DNS server tooforward solicitudes toohello personalizado servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="f8aab-204">Next, you must configure hello on-premises DNS server tooforward requests toohello custom DNS server.</span></span>

<span data-ttu-id="f8aab-205">Para obtener pasos específicos sobre cómo tooconfigure el servidor DNS, consulte la documentación de hello para el software del servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="f8aab-205">For specific steps on how tooconfigure your DNS server, consult hello documentation for your DNS server software.</span></span> <span data-ttu-id="f8aab-206">Busque los pasos hello tooconfigure una __reenviador condicional__.</span><span class="sxs-lookup"><span data-stu-id="f8aab-206">Look for hello steps on how tooconfigure a __conditional forwarder__.</span></span>

<span data-ttu-id="f8aab-207">Un reenvío condicional solo reenvía solicitudes para un sufijo DNS específico.</span><span class="sxs-lookup"><span data-stu-id="f8aab-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="f8aab-208">En este caso, debe configurar un reenviador para el sufijo DNS de Hola de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-208">In this case, you must configure a forwarder for hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="f8aab-209">Se deberían reenviar las solicitudes de este sufijo toohello dirección IP del servidor DNS personalizado de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-209">Requests for this suffix should be forwarded toohello IP address of hello custom DNS server.</span></span> 

<span data-ttu-id="f8aab-210">Hello texto siguiente es un ejemplo de una configuración de reenviador condicional para hello **enlazar** software DNS:</span><span class="sxs-lookup"><span data-stu-id="f8aab-210">hello following text is an example of a conditional forwarder configuration for hello **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

<span data-ttu-id="f8aab-211">Para obtener información sobre el uso de DNS en **Windows Server 2016**, vea hello [DnsServerConditionalForwarderZone agregar](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentación...</span><span class="sxs-lookup"><span data-stu-id="f8aab-211">For information on using DNS on **Windows Server 2016**, see hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="f8aab-212">Una vez haya configurado el servidor DNS de hello en local, puede utilizar `nslookup` de tooverify de red local de Hola que pueda resolver los nombres de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-212">Once you have configured hello on-premises DNS server, you can use `nslookup` from hello on-premises network tooverify that you can resolve names in hello virtual network.</span></span> <span data-ttu-id="f8aab-213">Hola siguiente ejemplo</span><span class="sxs-lookup"><span data-stu-id="f8aab-213">hello following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="f8aab-214">Este ejemplo usa Hola servidor DNS local en 196.168.0.4 tooresolve Hola nombre de saludo personalizado servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="f8aab-214">This example uses hello on-premises DNS server at 196.168.0.4 tooresolve hello name of hello custom DNS server.</span></span> <span data-ttu-id="f8aab-215">Reemplace la dirección IP de hello con hello para el servidor DNS local Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-215">Replace hello IP address with hello one for hello on-premises DNS server.</span></span> <span data-ttu-id="f8aab-216">Reemplace hello `dnsproxy` dirección con el nombre de dominio completo de Hola de servidor DNS personalizado de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-216">Replace hello `dnsproxy` address with hello fully qualified domain name of hello custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="f8aab-217">Opcional: control del tráfico de red</span><span class="sxs-lookup"><span data-stu-id="f8aab-217">Optional: Control network traffic</span></span>

<span data-ttu-id="f8aab-218">Puede usar grupos de seguridad de red (NSG) o el tráfico de red de rutas definidas por el usuario (UDR) toocontrol.</span><span class="sxs-lookup"><span data-stu-id="f8aab-218">You can use network security groups (NSG) or user-defined routes (UDR) toocontrol network traffic.</span></span> <span data-ttu-id="f8aab-219">Los NSG permiten toofilter entrantes y salientes de tráfico y permitir o denegar el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-219">NSGs allow you toofilter inbound and outbound traffic, and allow or deny hello traffic.</span></span> <span data-ttu-id="f8aab-220">UDRs le permiten toocontrol cómo fluye el tráfico entre los recursos de red virtual de hello, Hola internet y Hola red local.</span><span class="sxs-lookup"><span data-stu-id="f8aab-220">UDRs allow you toocontrol how traffic flows between resources in hello virtual network, hello internet, and hello on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="f8aab-221">HDInsight requiere acceso de entrada desde direcciones IP específicas en la nube de Azure de Hola y sin restricciones de acceso de salida.</span><span class="sxs-lookup"><span data-stu-id="f8aab-221">HDInsight requires inbound access from specific IP addresses in hello Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="f8aab-222">Cuando se utiliza el tráfico de toocontrol NSG o UDRs, debe realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f8aab-222">When using NSGs or UDRs toocontrol traffic, you must perform hello following steps:</span></span>
>
> 1. <span data-ttu-id="f8aab-223">Encontrar Hola direcciones IP para la ubicación de Hola que contiene la red virtual.</span><span class="sxs-lookup"><span data-stu-id="f8aab-223">Find hello IP addresses for hello location that contains your virtual network.</span></span> <span data-ttu-id="f8aab-224">Para obtener una lista de las direcciones IP requeridas por ubicación, consulte [Direcciones IP requeridas](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="f8aab-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="f8aab-225">Permitir el tráfico entrante desde direcciones IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-225">Allow inbound traffic from hello IP addresses.</span></span>
>
>    * <span data-ttu-id="f8aab-226">__NSG__: permitir __entrada__ tráfico en el puerto __443__ de hello __Internet__.</span><span class="sxs-lookup"><span data-stu-id="f8aab-226">__NSG__: Allow __inbound__ traffic on port __443__ from hello __Internet__.</span></span>
>    * <span data-ttu-id="f8aab-227">__UDR__: Hola conjunto __próximo salto__ tipo de hello ruta too__Internet__.</span><span class="sxs-lookup"><span data-stu-id="f8aab-227">__UDR__: Set hello __Next Hop__ type of hello route too__Internet__.</span></span>

<span data-ttu-id="f8aab-228">Para obtener un ejemplo del uso de Azure PowerShell o CLI de Azure de hello toocreate NSG, vea hello [HDInsight ampliar con redes virtuales de Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) documento.</span><span class="sxs-lookup"><span data-stu-id="f8aab-228">For an example of using Azure PowerShell or hello Azure CLI toocreate NSGs, see hello [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-hello-hdinsight-cluster"></a><span data-ttu-id="f8aab-229">Crear el clúster de HDInsight de Hola</span><span class="sxs-lookup"><span data-stu-id="f8aab-229">Create hello HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="f8aab-230">Debe configurar el servidor DNS personalizado de hello antes de instalar HDInsight en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8aab-230">You must configure hello custom DNS server before installing HDInsight in hello virtual network.</span></span>

<span data-ttu-id="f8aab-231">Hola de uso de los pasos de hello [crear un clúster de HDInsight mediante Hola portal de Azure](./hdinsight-hadoop-create-linux-clusters-portal.md) documento toocreate un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8aab-231">Use hello steps in hello [Create an HDInsight cluster using hello Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="f8aab-232">Durante la creación del clúster, debe elegir ubicación de Hola que contiene la red virtual.</span><span class="sxs-lookup"><span data-stu-id="f8aab-232">During cluster creation, you must choose hello location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="f8aab-233">Hola __configuración avanzada__ parte de configuración, debe seleccionar la red virtual de Hola y de las subredes que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f8aab-233">In hello __Advanced settings__ part of configuration, you must select hello virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-toohdinsight"></a><span data-ttu-id="f8aab-234">Conexión tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="f8aab-234">Connecting tooHDInsight</span></span>

<span data-ttu-id="f8aab-235">Documentación mayoría en HDInsight se da por supuesto que tiene acceso toohello clúster sobre Hola internet.</span><span class="sxs-lookup"><span data-stu-id="f8aab-235">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="f8aab-236">Por ejemplo, que se puede conectar el clúster de toohello en https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="f8aab-236">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="f8aab-237">Esta dirección utiliza la puerta de enlace pública hello, que no está disponible si ha usado NSG u Hola a UDRs toorestrict acceso desde internet.</span><span class="sxs-lookup"><span data-stu-id="f8aab-237">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="f8aab-238">toodirectly conecte tooHDInsight a través de la red virtual de hello, usar hello pasos:</span><span class="sxs-lookup"><span data-stu-id="f8aab-238">toodirectly connect tooHDInsight through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="f8aab-239">nombres de dominio completo interno de hello toodiscover de nodos de clúster de HDInsight de hello, use uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="f8aab-239">toodiscover hello internal fully qualified domain names of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. <span data-ttu-id="f8aab-240">puerto de hello toodetermine que un servicio está disponible en, vea hello [puertos utilizados por los servicios de Hadoop en HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.</span><span class="sxs-lookup"><span data-stu-id="f8aab-240">toodetermine hello port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f8aab-241">Algunos servicios hospedados en nodos principales Hola sólo están activas en un nodo a la vez.</span><span class="sxs-lookup"><span data-stu-id="f8aab-241">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="f8aab-242">Si intenta obtener acceso a un servicio en un nodo principal y se produce un error, cambie toohello otro nodo principal.</span><span class="sxs-lookup"><span data-stu-id="f8aab-242">If you try accessing a service on one head node and it fails, switch toohello other head node.</span></span>
    >
    > <span data-ttu-id="f8aab-243">Por ejemplo, Ambari solo está activo en un nodo principal a la vez.</span><span class="sxs-lookup"><span data-stu-id="f8aab-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="f8aab-244">Si intenta tener acceso a Ambari en un nodo principal y devuelve un error 404, a continuación, se ejecuta en Hola otro nodo principal.</span><span class="sxs-lookup"><span data-stu-id="f8aab-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on hello other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8aab-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f8aab-245">Next steps</span></span>

* <span data-ttu-id="f8aab-246">Para más información sobre cómo usar HDInsight en una red virtual, vea [Extensión de las funcionalidades de HDInsight con Red virtual de Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="f8aab-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="f8aab-247">Para obtener más información sobre redes virtuales de Azure, vea hello [información general de la red Virtual de Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8aab-247">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="f8aab-248">Para más información sobre los grupos de seguridad de red, vea [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f8aab-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="f8aab-249">Para más información sobre las rutas definidas por el usuario, vea [Rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8aab-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
