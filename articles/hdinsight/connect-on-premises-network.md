---
title: "Conexión de HDInsight a la red local: Azure HDInsight | Microsoft Docs"
description: "Obtenga información sobre cómo crear un clúster de HDInsight en una instancia de Azure Virtual Network y conectarlo a la red local. Obtenga información sobre cómo usar un servidor DNS personalizado para configurar la resolución de nombres entre HDInsight y la red local."
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
ms.openlocfilehash: 6fc863010cc59e20e7d86ea9344489e574be75f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connect-hdinsight-to-your-on-premise-network"></a><span data-ttu-id="bedc0-104">Conexión de HDInsight a la red local</span><span class="sxs-lookup"><span data-stu-id="bedc0-104">Connect HDInsight to your on-premise network</span></span>

<span data-ttu-id="bedc0-105">Obtenga información sobre cómo conectar HDInsight a la red local mediante redes virtuales de Azure y una puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="bedc0-105">Learn how to connect HDInsight to your on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="bedc0-106">En este documento se brinda información de planeación sobre:</span><span class="sxs-lookup"><span data-stu-id="bedc0-106">This document provides planning information on:</span></span>

* <span data-ttu-id="bedc0-107">Uso de HDInsight en una instancia de Azure Virtual Network que se conecta con la red local.</span><span class="sxs-lookup"><span data-stu-id="bedc0-107">Using HDInsight in an Azure Virtual Network that connects to your on-premises network.</span></span>

* <span data-ttu-id="bedc0-108">Configuración de resolución de nombres DNS entre la red virtual y la red local.</span><span class="sxs-lookup"><span data-stu-id="bedc0-108">Configuring DNS name resolution between the virtual network and your on-premises network.</span></span>

* <span data-ttu-id="bedc0-109">Configuración de grupos de seguridad de red para restringir acceso a HDInsight a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="bedc0-109">Configuring network security groups to restrict internet access to HDInsight.</span></span>

* <span data-ttu-id="bedc0-110">Puertos que HDInsight proporciona en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-110">Ports provided by HDInsight on the virtual network.</span></span>

## <a name="create-the-virtual-network-configuration"></a><span data-ttu-id="bedc0-111">Creación de la configuración de la red virtual</span><span class="sxs-lookup"><span data-stu-id="bedc0-111">Create the Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bedc0-112">Si busca guías paso a paso sobre cómo conectar HDInsight con la red local mediante una instancia de Azure Virtual Network, consulte el documento [Conexión de HDInsight a la red local](connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="bedc0-112">If you are looking for step by step guidance on connecting HDInsight to your on-premises network using an Azure Virtual Network, see the [Connect HDInsight to your on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="bedc0-113">Use los documentos siguientes para obtener información sobre cómo crear una instancia de Azure Virtual Network conectada a la red local:</span><span class="sxs-lookup"><span data-stu-id="bedc0-113">Use the following documents to learn how to create an Azure Virtual Network that is connected to your on-premises network:</span></span>
    
* [<span data-ttu-id="bedc0-114">Uso de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bedc0-114">Using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="bedc0-115">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bedc0-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="bedc0-116">Uso de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="bedc0-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="bedc0-117">Configuración de la resolución de nombres</span><span class="sxs-lookup"><span data-stu-id="bedc0-117">Configure name resolution</span></span>

<span data-ttu-id="bedc0-118">Para permitir que HDInsight y los recursos de la red combinada se comuniquen por nombre, debe realizar las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="bedc0-118">To allow HDInsight and resources in the joined network to communicate by name, you must perform the following actions:</span></span>

* <span data-ttu-id="bedc0-119">Cree un servidor DNS personalizado en la instancia de Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="bedc0-119">Create a custom DNS server in the Azure Virtual Network.</span></span>

* <span data-ttu-id="bedc0-120">Configure la red virtual para que use el servidor DNS personalizado en lugar de la resolución recursiva de Azure predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bedc0-120">Configure the virtual network to use the custom DNS server instead of the default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="bedc0-121">Configure el reenvío entre el servidor DNS personalizado y el servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="bedc0-121">Configure forwarding between the custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="bedc0-122">Esta configuración permite el siguiente comportamiento:</span><span class="sxs-lookup"><span data-stu-id="bedc0-122">This configuration enables the following behavior:</span></span>

* <span data-ttu-id="bedc0-123">Las solicitudes de nombres de dominio completos con el sufijo DNS __para la red virtual__ se reenvían al servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="bedc0-123">Requests for fully qualified domain names that have the DNS suffix __for the virtual network__ are forwarded to the custom DNS server.</span></span> <span data-ttu-id="bedc0-124">Entonces, el servidor DNS personalizado reenvía estas solicitudes a la resolución recursiva de Azure, que devuelve la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="bedc0-124">The custom DNS server then forwards these requests to the Azure Recursive Resolver, which returns the IP address.</span></span>

* <span data-ttu-id="bedc0-125">Todas las otras solicitudes se reenvían al servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="bedc0-125">All other requests are forwarded to the on-premises DNS server.</span></span> <span data-ttu-id="bedc0-126">Incluso las solicitudes de recursos de Internet, como microsoft.com, se reenvían al servidor DNS local para la resolución de nombres.</span><span class="sxs-lookup"><span data-stu-id="bedc0-126">Even requests for public internet resources such as microsoft.com are forwarded to the on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="bedc0-127">En el diagrama siguiente, las líneas verdes son solicitudes de recursos que finalizan en el sufijo DNS de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-127">In the following diagram, green lines are requests for resources that end in the DNS suffix of the virtual network.</span></span> <span data-ttu-id="bedc0-128">Las líneas azules son solicitudes de recursos en la red local o en Internet.</span><span class="sxs-lookup"><span data-stu-id="bedc0-128">Blue lines are requests for resources in the on-premises network or on the public internet.</span></span>

![Diagrama de cómo se resuelven las solicitudes DNS en la configuración que se usa en este documento](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="bedc0-130">Creación de un servidor DNS personalizado</span><span class="sxs-lookup"><span data-stu-id="bedc0-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bedc0-131">Debe crear y configurar el servidor DNS antes de instalar HDInsight en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-131">You must create and configure the DNS server before installing HDInsight into the virtual network.</span></span>

<span data-ttu-id="bedc0-132">Para crear una máquina virtual Linux que usa el software DNS [Bind](https://www.isc.org/downloads/bind/), use los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bedc0-132">To create a Linux VM that uses the [Bind](https://www.isc.org/downloads/bind/) DNS software, use the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="bedc0-133">Los pasos siguientes usan [Azure Portal](https://portal.azure.com) para crear una instancia de Azure Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="bedc0-133">The following steps use the [Azure portal](https://portal.azure.com) to create an Azure Virtual Machine.</span></span> <span data-ttu-id="bedc0-134">Para conocer otras formas de crear una máquina virtual, consulte los documentos [Creación de una máquina virtual: CLI de Azure](../virtual-machines/linux/quick-create-cli.md) y [Creación de una máquina virtual: Azure PowerShell](../virtual-machines/linux/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bedc0-134">For other ways to create a virtual machine, see the [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="bedc0-135">En [Azure Portal](https://portal.azure.com), seleccione __+__, __Proceso__ y __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-135">From the [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Creación de una máquina virtual Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="bedc0-137">Escriba la información siguiente d la sección __Aspectos básicos__:</span><span class="sxs-lookup"><span data-stu-id="bedc0-137">From the __Basics__ section, enter the following information:</span></span>

    * <span data-ttu-id="bedc0-138">__Nombre__: nombre descriptivo que identifica esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="bedc0-139">Por ejemplo, __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="bedc0-140">__Nombre de usuario__: nombre de la cuenta SSH.</span><span class="sxs-lookup"><span data-stu-id="bedc0-140">__User name__: The name of the SSH account.</span></span>
    * <span data-ttu-id="bedc0-141">__Clave pública SSH__ o __Contraseña__: método de autenticación de la cuenta SSH.</span><span class="sxs-lookup"><span data-stu-id="bedc0-141">__SSH public key__ or __Password__: The authentication method for the SSH account.</span></span> <span data-ttu-id="bedc0-142">Se recomienda usar claves públicas, porque son más seguras.</span><span class="sxs-lookup"><span data-stu-id="bedc0-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="bedc0-143">Para más información, consulte el documento [Creación y uso de claves SSH para máquinas virtuales Linux](../virtual-machines/linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="bedc0-143">For more information, see the [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="bedc0-144">__Grupo de recursos__: seleccione __Usar existente__ y, luego, seleccione el grupo de recursos que contiene la red virtual que se creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bedc0-144">__Resource group__: Select __Use existing__, and then select the resource group that contains the virtual network created earlier.</span></span>
    * <span data-ttu-id="bedc0-145">__Ubicación__: seleccione la misma ubicación que tiene la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-145">__Location__: Select the same location as the virtual network.</span></span>

    ![Configuración básica de la máquina virtual](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="bedc0-147">Deje los valores predeterminados de las otras entradas y, luego, seleccione __Aceptar__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-147">Leave other entries at the default values and then select __OK__.</span></span>

3. <span data-ttu-id="bedc0-148">En la sección __Choosing a size__ (Elegir un tamaño), seleccione el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-148">From the __Choose a size__ section, select the VM size.</span></span> <span data-ttu-id="bedc0-149">Para este tutorial, seleccione la opción más pequeña y de menor costo.</span><span class="sxs-lookup"><span data-stu-id="bedc0-149">For this tutorial, select the smallest and lowest cost option.</span></span> <span data-ttu-id="bedc0-150">Para continuar, use el botón __Seleccionar__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-150">To continue, use the __Select__ button.</span></span>

4. <span data-ttu-id="bedc0-151">Escriba la información siguiente de la sección __Configuración__:</span><span class="sxs-lookup"><span data-stu-id="bedc0-151">From the __Settings__ section, enter the following information:</span></span>

    * <span data-ttu-id="bedc0-152">__Red virtual__: seleccione la red virtual que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bedc0-152">__Virtual network__: Select the virtual network that you created earlier.</span></span>

    * <span data-ttu-id="bedc0-153">__Subred__: seleccione la subred predeterminada para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-153">__Subnet__: Select the default subnet for the virtual network.</span></span> <span data-ttu-id="bedc0-154">__No__ seleccione la subred que la puerta de enlace de VPN usa.</span><span class="sxs-lookup"><span data-stu-id="bedc0-154">Do __not__ select the subnet used by the VPN gateway.</span></span>

    * <span data-ttu-id="bedc0-155">__Cuenta de almacenamiento de diagnóstico__: seleccione una cuenta de almacenamiento existente o cree una nueva.</span><span class="sxs-lookup"><span data-stu-id="bedc0-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Configuración de la red virtual](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="bedc0-157">Deje los valores predeterminados de las otras entradas y, luego, seleccione __Aceptar__ para continuar.</span><span class="sxs-lookup"><span data-stu-id="bedc0-157">Leave the other entries at the default value, then select __OK__ to continue.</span></span>

5. <span data-ttu-id="bedc0-158">En la sección __Comprar__, seleccione el botón __Comprar__ para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-158">From the __Purchase__ section, select the __Purchase__ button to create the virtual machine.</span></span>

6. <span data-ttu-id="bedc0-159">En la máquina virtual que se crea, aparece la sección de __información general__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-159">Once the virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="bedc0-160">En la lista que aparece a la izquierda, seleccione __Propiedades__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-160">From the list on the left, select __Properties__.</span></span> <span data-ttu-id="bedc0-161">Guarde los valores de __dirección IP pública__ y __dirección IP privada__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-161">Save the __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="bedc0-162">Esta información se usará en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="bedc0-162">It will be used in the next section.</span></span>

    ![Direcciones IP pública y privada](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="bedc0-164">Instalación y configuración de Bind (software DNS)</span><span class="sxs-lookup"><span data-stu-id="bedc0-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="bedc0-165">Use SSH para conectarse a la __dirección IP pública__ de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-165">Use SSH to connect to the __public IP address__ of the virtual machine.</span></span> <span data-ttu-id="bedc0-166">En el ejemplo siguiente, se realiza una conexión a una máquina virtual en 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="bedc0-166">The following example connects to a virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="bedc0-167">Reemplace `sshuser` por la cuenta de usuario SSH que especificó cuando creó el clúster.</span><span class="sxs-lookup"><span data-stu-id="bedc0-167">Replace `sshuser` with the SSH user account you specified when creating the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bedc0-168">Existen diversas formas de obtener la utilidad `ssh`.</span><span class="sxs-lookup"><span data-stu-id="bedc0-168">There are a variety of ways to obtain the `ssh` utility.</span></span> <span data-ttu-id="bedc0-169">En Linux, Unix y macOS, se proporciona como parte del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="bedc0-169">On Linux, Unix, and macOS, it is provided as part of the operating system.</span></span> <span data-ttu-id="bedc0-170">Si usa Windows, considere una de las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="bedc0-170">If you are using Windows, consider one of the following options:</span></span>
    >
    > * [<span data-ttu-id="bedc0-171">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="bedc0-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="bedc0-172">Bash en Ubuntu en Windows 10</span><span class="sxs-lookup"><span data-stu-id="bedc0-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="bedc0-173">GIT (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="bedc0-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="bedc0-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="bedc0-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="bedc0-175">Para instalar Bind, use los comandos siguientes en la sesión de SSH:</span><span class="sxs-lookup"><span data-stu-id="bedc0-175">To install Bind, use the following commands from the SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="bedc0-176">Para configurar Bind a fin de reenviar las solicitudes de resolución de nombres al servidor DNS local, use el texto siguiente como contenido del archivo `/etc/bind/named.conf.options`:</span><span class="sxs-lookup"><span data-stu-id="bedc0-176">To configure Bind to forward name resolution requests to your on-prem DNS server, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with the IP address range of the virtual network
            10.1.0.0/16; # Replace with the IP address range of the on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with the IP address of the on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform to RFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="bedc0-177">Reemplace los valores de la sección `goodclients` por el intervalo de direcciones IP de la red virtual y la red local.</span><span class="sxs-lookup"><span data-stu-id="bedc0-177">Replace the values in the `goodclients` section with the IP address range of the virtual network and on-premises network.</span></span> <span data-ttu-id="bedc0-178">En esta sección se definen las direcciones desde las cuales el servidor DNS acepta solicitudes.</span><span class="sxs-lookup"><span data-stu-id="bedc0-178">This section defines the addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="bedc0-179">Reemplace la entrada `192.168.0.1` en la sección `forwarders` por la dirección IP del servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="bedc0-179">Replace the `192.168.0.1` entry in the `forwarders` section with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="bedc0-180">Esta entrada enruta las solicitudes DNS al servidor DNS local para la resolución.</span><span class="sxs-lookup"><span data-stu-id="bedc0-180">This entry routes DNS requests to your on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="bedc0-181">Para editar el archivo, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="bedc0-181">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="bedc0-182">Para guardar el archivo, use __Ctrl+X__, __Y__ y, luego, __Entrar__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-182">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="bedc0-183">En la sesión de SSH, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="bedc0-183">From the SSH session, use the following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="bedc0-184">Este comando devuelve un valor similar al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="bedc0-184">This command returns a value similar to the following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="bedc0-185">El texto `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` está en el __sufijo DNS__ de esta red virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-185">The `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is the __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="bedc0-186">Guarde este valor, porque se usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="bedc0-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="bedc0-187">Para configurar Bind a fin de resolver nombres DNS para recursos dentro de la red virtual, use el texto siguiente como contenido del archivo `/etc/bind/named.conf.local`:</span><span class="sxs-lookup"><span data-stu-id="bedc0-187">To configure Bind to resolve DNS names for resources within the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

        // Replace the following with the DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # The Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="bedc0-188">Debe reemplazar `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` por el sufijo DNS que recuperó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bedc0-188">You must replace the `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with the DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="bedc0-189">Para editar el archivo, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="bedc0-189">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="bedc0-190">Para guardar el archivo, use __Ctrl+X__, __Y__ y, luego, __Entrar__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-190">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="bedc0-191">Para iniciar Bind, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="bedc0-191">To start Bind, use the following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="bedc0-192">Para comprobar que Bind puede resolver los nombres de recursos en la red local, use los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bedc0-192">To verify that bind can resolve the names of resources in your on-premises network, use the following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="bedc0-193">Reemplace `dns.mynetwork.net` por el nombre de dominio completo (FQDN) de un recurso en la red local.</span><span class="sxs-lookup"><span data-stu-id="bedc0-193">Replace `dns.mynetwork.net` with the fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="bedc0-194">Reemplace `10.0.0.4` por la __dirección IP interna__ del servidor DNS personalizado en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-194">Replace `10.0.0.4` with the __internal IP address__ of your custom DNS server in the virtual network.</span></span>

    <span data-ttu-id="bedc0-195">La respuesta es similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="bedc0-195">The response appears similar to the following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-the-virtual-network-to-use-the-custom-dns-server"></a><span data-ttu-id="bedc0-196">Configuración de la red virtual para usar el servidor DNS personalizado</span><span class="sxs-lookup"><span data-stu-id="bedc0-196">Configure the virtual network to use the custom DNS server</span></span>

<span data-ttu-id="bedc0-197">Para configurar la red virtual para que use el servidor DNS personalizado en lugar de la resolución recursiva de Azure, use los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bedc0-197">To configure the virtual network to use the custom DNS server instead of the Azure recursive resolver, use the following steps:</span></span>

1. <span data-ttu-id="bedc0-198">En [Azure Portal](https://portal.azure.com), seleccione la red virtual y, luego, seleccione __Servidores DNS__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-198">In the [Azure portal](https://portal.azure.com), select the virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="bedc0-199">Seleccione __Personalizar__ y escriba la __dirección IP interna__ del servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="bedc0-199">Select __Custom__, and enter the __internal IP address__ of the custom DNS server.</span></span> <span data-ttu-id="bedc0-200">Por último, seleccione __Guardar__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-200">Finally, select __Save__.</span></span>

    ![Establecimiento del servidor DNS personalizado para la red](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-the-on-premises-dns-server"></a><span data-ttu-id="bedc0-202">Configuración del servidor DNS local</span><span class="sxs-lookup"><span data-stu-id="bedc0-202">Configure the on-premises DNS server</span></span>

<span data-ttu-id="bedc0-203">En la sección anterior, configuró el servidor DNS personalizado para reenviar las solicitudes al servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="bedc0-203">In the previous section, you configured the custom DNS server to forward requests to the on-premises DNS server.</span></span> <span data-ttu-id="bedc0-204">A continuación, debe configurar el servidor DNS local para reenviar las solicitudes al servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="bedc0-204">Next, you must configure the on-premises DNS server to forward requests to the custom DNS server.</span></span>

<span data-ttu-id="bedc0-205">Para conocer los pasos específicos sobre cómo configurar el servidor DNS, consulte la documentación correspondiente al software de servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="bedc0-205">For specific steps on how to configure your DNS server, consult the documentation for your DNS server software.</span></span> <span data-ttu-id="bedc0-206">Busque los pasos sobre cómo configurar un __reenvío condicional__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-206">Look for the steps on how to configure a __conditional forwarder__.</span></span>

<span data-ttu-id="bedc0-207">Un reenvío condicional solo reenvía solicitudes para un sufijo DNS específico.</span><span class="sxs-lookup"><span data-stu-id="bedc0-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="bedc0-208">En este caso, debe configurar un reenvío para el sufijo DNS de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-208">In this case, you must configure a forwarder for the DNS suffix of the virtual network.</span></span> <span data-ttu-id="bedc0-209">Las solicitudes para este sufijo se deben reenviar a la dirección IP del servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="bedc0-209">Requests for this suffix should be forwarded to the IP address of the custom DNS server.</span></span> 

<span data-ttu-id="bedc0-210">El texto siguiente es un ejemplo de la configuración de un reenvío condicional para el software DNS **Bind**:</span><span class="sxs-lookup"><span data-stu-id="bedc0-210">The following text is an example of a conditional forwarder configuration for the **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The custom DNS server's internal IP address
    };

<span data-ttu-id="bedc0-211">Para información sobre cómo usar DNS en **Windows Server 2016**, consulte la documentación de [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone).</span><span class="sxs-lookup"><span data-stu-id="bedc0-211">For information on using DNS on **Windows Server 2016**, see the [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="bedc0-212">Una vez que configure el servidor DNS local, puede usar `nslookup` desde la red local para comprobar que es posible resolver nombres en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-212">Once you have configured the on-premises DNS server, you can use `nslookup` from the on-premises network to verify that you can resolve names in the virtual network.</span></span> <span data-ttu-id="bedc0-213">El ejemplo siguiente</span><span class="sxs-lookup"><span data-stu-id="bedc0-213">The following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="bedc0-214">En este ejemplo se usa el servidor DNS local en 196.168.0.4 para resolver el nombre del servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="bedc0-214">This example uses the on-premises DNS server at 196.168.0.4 to resolve the name of the custom DNS server.</span></span> <span data-ttu-id="bedc0-215">Reemplace la dirección IP por la dirección IP del servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="bedc0-215">Replace the IP address with the one for the on-premises DNS server.</span></span> <span data-ttu-id="bedc0-216">Reemplace la dirección `dnsproxy` por el nombre de dominio completo del servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="bedc0-216">Replace the `dnsproxy` address with the fully qualified domain name of the custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="bedc0-217">Opcional: control del tráfico de red</span><span class="sxs-lookup"><span data-stu-id="bedc0-217">Optional: Control network traffic</span></span>

<span data-ttu-id="bedc0-218">Puede usar grupos de seguridad de red (NSG) o rutas definidas por el usuario (UDR) para controlar el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="bedc0-218">You can use network security groups (NSG) or user-defined routes (UDR) to control network traffic.</span></span> <span data-ttu-id="bedc0-219">Los NSG permiten filtrar el tráfico de entrada y de salida, además de permitir o denegar el tráfico.</span><span class="sxs-lookup"><span data-stu-id="bedc0-219">NSGs allow you to filter inbound and outbound traffic, and allow or deny the traffic.</span></span> <span data-ttu-id="bedc0-220">Las UDR permiten controlar el flujo del tráfico entre los recursos de la red virtual, Internet y la red local.</span><span class="sxs-lookup"><span data-stu-id="bedc0-220">UDRs allow you to control how traffic flows between resources in the virtual network, the internet, and the on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="bedc0-221">HDInsight requiere acceso de entrada desde direcciones IP específicas en la nube de Azure y acceso de salida sin restricciones.</span><span class="sxs-lookup"><span data-stu-id="bedc0-221">HDInsight requires inbound access from specific IP addresses in the Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="bedc0-222">Cuando use NSG o UDR para controlar el tráfico, debe realizar los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bedc0-222">When using NSGs or UDRs to control traffic, you must perform the following steps:</span></span>
>
> 1. <span data-ttu-id="bedc0-223">Encuentre las direcciones IP de la ubicación que contiene la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-223">Find the IP addresses for the location that contains your virtual network.</span></span> <span data-ttu-id="bedc0-224">Para obtener una lista de las direcciones IP requeridas por ubicación, consulte [Direcciones IP requeridas](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="bedc0-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="bedc0-225">Permitir el tráfico de entrada proveniente de las direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="bedc0-225">Allow inbound traffic from the IP addresses.</span></span>
>
>    * <span data-ttu-id="bedc0-226">__NSG__: permita el tráfico de __entrada__ en el puerto __443__ desde __Internet__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-226">__NSG__: Allow __inbound__ traffic on port __443__ from the __Internet__.</span></span>
>    * <span data-ttu-id="bedc0-227">__UDR__: establezca el tipo __Próximo salto__ de la ruta en __Internet__.</span><span class="sxs-lookup"><span data-stu-id="bedc0-227">__UDR__: Set the __Next Hop__ type of the route to __Internet__.</span></span>

<span data-ttu-id="bedc0-228">Para un ejemplo de cómo usar Azure PowerShell o la CLI de Azure para crear NSG, consulte el documento [Extensión de HDInsight con redes virtuales de Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg).</span><span class="sxs-lookup"><span data-stu-id="bedc0-228">For an example of using Azure PowerShell or the Azure CLI to create NSGs, see the [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-the-hdinsight-cluster"></a><span data-ttu-id="bedc0-229">Creación del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="bedc0-229">Create the HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="bedc0-230">Debe configurar el servidor DNS antes de instalar HDInsight en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-230">You must configure the custom DNS server before installing HDInsight in the virtual network.</span></span>

<span data-ttu-id="bedc0-231">Use los pasos que aparecen en el documento sobre cómo [crear un clúster de HDInsight mediante Azure Portal de un clúster](./hdinsight-hadoop-create-linux-clusters-portal.md) para crear un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bedc0-231">Use the steps in the [Create an HDInsight cluster using the Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document to create an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="bedc0-232">Durante la creación del clúster, debe elegir la ubicación que contiene la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bedc0-232">During cluster creation, you must choose the location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="bedc0-233">En la parte __Configuración avanzada__ de la configuración, debe seleccionar la red virtual y la subred que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bedc0-233">In the __Advanced settings__ part of configuration, you must select the virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-to-hdinsight"></a><span data-ttu-id="bedc0-234">Conexión a HDInsight</span><span class="sxs-lookup"><span data-stu-id="bedc0-234">Connecting to HDInsight</span></span>

<span data-ttu-id="bedc0-235">En la mayor parte de la documentación sobre HDInsight se supone que tiene acceso al clúster a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="bedc0-235">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="bedc0-236">Por ejemplo, que se puede conectar al clúster en https://NOMBREDECLÚSTER.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="bedc0-236">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="bedc0-237">Esta dirección usa la puerta de enlace pública, que no está disponible si usó NSG o UDR para restringir el acceso desde Internet.</span><span class="sxs-lookup"><span data-stu-id="bedc0-237">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="bedc0-238">Para conectarse directamente a HDInsight a través de la red virtual, use los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bedc0-238">To directly connect to HDInsight through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="bedc0-239">Para detectar los nombres de dominio completos internos de los nodos de clúster de HDInsight, use uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bedc0-239">To discover the internal fully qualified domain names of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

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

2. <span data-ttu-id="bedc0-240">Para determinar el puerto en que está disponible un servicio, consulte el documento [Puertos utilizados por los servicios Hadoop en HDInsight](./hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="bedc0-240">To determine the port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bedc0-241">Algunos servicios hospedados en los nodos principales solo están activos en un nodo a la vez.</span><span class="sxs-lookup"><span data-stu-id="bedc0-241">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="bedc0-242">Si intenta acceder a un servicio en un nodo principal y se produce un error, cambie al otro nodo principal.</span><span class="sxs-lookup"><span data-stu-id="bedc0-242">If you try accessing a service on one head node and it fails, switch to the other head node.</span></span>
    >
    > <span data-ttu-id="bedc0-243">Por ejemplo, Ambari solo está activo en un nodo principal a la vez.</span><span class="sxs-lookup"><span data-stu-id="bedc0-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="bedc0-244">Si intenta acceder a Ambari en un nodo principal y se devuelve un error 404, es porque se ejecuta en el otro nodo principal.</span><span class="sxs-lookup"><span data-stu-id="bedc0-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on the other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bedc0-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bedc0-245">Next steps</span></span>

* <span data-ttu-id="bedc0-246">Para más información sobre cómo usar HDInsight en una máquina virtual, consulte [Extensión de HDInsight con redes virtuales de Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="bedc0-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="bedc0-247">Para más información sobre las redes virtuales de Azure, consulte la [información general sobre Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bedc0-247">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="bedc0-248">Para más información sobre los grupos de seguridad de red, vea [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="bedc0-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="bedc0-249">Para más información sobre las rutas definidas por el usuario, vea [Rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bedc0-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
