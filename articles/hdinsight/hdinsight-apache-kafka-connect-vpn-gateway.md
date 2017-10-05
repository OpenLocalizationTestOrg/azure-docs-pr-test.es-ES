---
title: "Conexión a Kafka mediante redes virtuales - Azure HDInsight | Microsoft Docs"
description: "Aprenda a conectarse directamente a Kafka en HDInsight mediante una instancia de Azure Virtual Network. Aprenda cómo conectarse a Kafka desde clientes de desarrollo mediante una puerta de enlace de red privada virtual o desde clientes de la red local mediante un dispositivo de puerta de enlace de red privada virtual."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/01/2017
ms.author: larryfr
ms.openlocfilehash: 245bee7c1dbb0236afdc2506e7ab84b5573cbc85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-kafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="dd891-104">Conexión a Kafka en HDInsight (versión preliminar) mediante una instancia de Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="dd891-104">Connect to Kafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="dd891-105">Obtenga información sobre cómo conectarse directamente a Kafka en HDInsight mediante Azure Virtual Networks.</span><span class="sxs-lookup"><span data-stu-id="dd891-105">Learn how to directly connect to Kafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="dd891-106">En este documento se proporciona información sobre la conexión a Kafka mediante las siguientes configuraciones:</span><span class="sxs-lookup"><span data-stu-id="dd891-106">This document provides information on connecting to Kafka using the following configurations:</span></span>

* <span data-ttu-id="dd891-107">Desde recursos de una red local.</span><span class="sxs-lookup"><span data-stu-id="dd891-107">From resources in an on-premises network.</span></span> <span data-ttu-id="dd891-108">Esta conexión se establece mediante un dispositivo de red privada virtual (software o hardware) en la red local.</span><span class="sxs-lookup"><span data-stu-id="dd891-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="dd891-109">Desde un entorno de desarrollo con un cliente de software de red privada virtual.</span><span class="sxs-lookup"><span data-stu-id="dd891-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="dd891-110">Arquitectura y planeación</span><span class="sxs-lookup"><span data-stu-id="dd891-110">Architecture and planning</span></span>

<span data-ttu-id="dd891-111">HDInsight no permite la conexión directa a Kafka a través de la red pública de Internet.</span><span class="sxs-lookup"><span data-stu-id="dd891-111">HDInsight does not allow direct connection to Kafka over the public internet.</span></span> <span data-ttu-id="dd891-112">Los clientes de Kafka (productores y consumidores) deben usar uno de los siguientes métodos de conexión:</span><span class="sxs-lookup"><span data-stu-id="dd891-112">Instead, Kafka clients (producers and consumers) must use one of the following connection methods:</span></span>

* <span data-ttu-id="dd891-113">Ejecutar el cliente en la misma red virtual que Kafka en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd891-113">Run the client in the same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="dd891-114">Esta configuración se usa en el documento [Start with Apache Kafka (preview) on HDInsight (Introducción a Apache Kafka (versión preliminar) en HDInsight)](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dd891-114">This configuration is used in the [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="dd891-115">El cliente se ejecuta directamente en los nodos del clúster de HDInsight o en otra máquina virtual de la misma red.</span><span class="sxs-lookup"><span data-stu-id="dd891-115">The client runs directly on the HDInsight cluster nodes or on another virtual machine in the same network.</span></span>

* <span data-ttu-id="dd891-116">Conectar una red privada, como la red local, a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="dd891-116">Connect a private network, such as your on-premises network, to the virtual network.</span></span> <span data-ttu-id="dd891-117">Esta configuración permite a los clientes de la red local trabajar directamente con Kafka.</span><span class="sxs-lookup"><span data-stu-id="dd891-117">This configuration allows clients in your on-premises network to directly work with Kafka.</span></span> <span data-ttu-id="dd891-118">Para habilitar esta configuración, realice las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="dd891-118">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="dd891-119">Cree una red virtual.</span><span class="sxs-lookup"><span data-stu-id="dd891-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="dd891-120">Cree una puerta de enlace de red privada virtual que use una configuración de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="dd891-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="dd891-121">La configuración usada en este documento conecta a un dispositivo de puerta de enlace de red privada virtual en la red local.</span><span class="sxs-lookup"><span data-stu-id="dd891-121">The configuration used in this document connects to a VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="dd891-122">Cree un servidor DNS en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="dd891-122">Create a DNS server in the virtual network.</span></span>
    4. <span data-ttu-id="dd891-123">Configure el reenvío entre el servidor DNS de cada red.</span><span class="sxs-lookup"><span data-stu-id="dd891-123">Configure forwarding between the DNS server in each network.</span></span>
    5. <span data-ttu-id="dd891-124">Instale Kafka en HDInsight en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="dd891-124">Install Kafka on HDInsight into the virtual network.</span></span>

    <span data-ttu-id="dd891-125">Para más información, vea la sección [Conexión a Kafka desde una red local](#on-premises).</span><span class="sxs-lookup"><span data-stu-id="dd891-125">For more information, see the [Connect to Kafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="dd891-126">Conectar equipos individuales a la red virtual mediante una puerta de enlace de red privada virtual y un cliente de red privada virtual.</span><span class="sxs-lookup"><span data-stu-id="dd891-126">Connect individual machines to the virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="dd891-127">Para habilitar esta configuración, realice las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="dd891-127">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="dd891-128">Cree una red virtual.</span><span class="sxs-lookup"><span data-stu-id="dd891-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="dd891-129">Cree una puerta de enlace de red privada virtual que use una configuración de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="dd891-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="dd891-130">Esta configuración proporciona un cliente VPN que se puede instalar en los clientes Windows.</span><span class="sxs-lookup"><span data-stu-id="dd891-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="dd891-131">Instale Kafka en HDInsight en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="dd891-131">Install Kafka on HDInsight into the virtual network.</span></span>
    4. <span data-ttu-id="dd891-132">Configurar Kafka para anunciar direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="dd891-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="dd891-133">Esta configuración permite al cliente conectarse mediante direcciones IP en lugar de nombres de dominio.</span><span class="sxs-lookup"><span data-stu-id="dd891-133">This configuration allows the client to connect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="dd891-134">Descargue y use el cliente de VPN en el sistema de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="dd891-134">Download and use the VPN client on the development system.</span></span>

    <span data-ttu-id="dd891-135">Para más información, vea la sección [Conexión a Kafka con un cliente VPN](#vpnclient).</span><span class="sxs-lookup"><span data-stu-id="dd891-135">For more information, see the [Connect to Kafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="dd891-136">Esta configuración solo se recomienda para fines de desarrollo debido a las limitaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="dd891-136">This configuration is only recommended for development purposes because of the following limitations:</span></span>
    >
    > * <span data-ttu-id="dd891-137">Cada cliente debe conectarse con un cliente de software de VPN.</span><span class="sxs-lookup"><span data-stu-id="dd891-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="dd891-138">Azure solo proporciona un cliente basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="dd891-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="dd891-139">El cliente no pasa las solicitudes de resolución de nombres a la red virtual, por lo que debe usar direcciones IP para comunicarse con Kafka.</span><span class="sxs-lookup"><span data-stu-id="dd891-139">The client does not pass name resolution requests to the virtual network, so you must use IP addressing to communicate with Kafka.</span></span> <span data-ttu-id="dd891-140">La comunicación IP exige configuración adicional en el clúster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="dd891-140">IP communication requires additional configuration on the Kafka cluster.</span></span>

<span data-ttu-id="dd891-141">Para más información sobre cómo usar HDInsight en una red virtual, vea [Extensión de las funcionalidades de HDInsight con Red virtual de Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="dd891-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="dd891-142"><a id="on-premises"></a> Conexión a Kafka desde una red local</span><span class="sxs-lookup"><span data-stu-id="dd891-142"><a id="on-premises"></a> Connect to Kafka from an on-premises network</span></span>

<span data-ttu-id="dd891-143">Para crear un clúster de Kafka que se comunique con la red local, siga los pasos del documento [Connect HDInsight to your on-premises network (Conexión de HDInsight a la red local)](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="dd891-143">To create a Kafka cluster that communicates with your on-premises network, follow the steps in the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd891-144">Al crear el clúster de HDInsight, seleccione el tipo de clúster __Kafka__.</span><span class="sxs-lookup"><span data-stu-id="dd891-144">When creating the HDInsight cluster, select the __Kafka__ cluster type.</span></span>

<span data-ttu-id="dd891-145">Estos pasos crean la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="dd891-145">These steps create the following configuration:</span></span>

* <span data-ttu-id="dd891-146">Red virtual</span><span class="sxs-lookup"><span data-stu-id="dd891-146">Azure Virtual Network</span></span>
* <span data-ttu-id="dd891-147">Puerta de enlace de VPN de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="dd891-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="dd891-148">Cuenta de Azure Storage (usada por HDInsight)</span><span class="sxs-lookup"><span data-stu-id="dd891-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="dd891-149">Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="dd891-149">Kafka on HDInsight</span></span>

<span data-ttu-id="dd891-150">Para comprobar que un cliente de Kafka puede conectarse al clúster desde el entorno local, siga los pasos de la sección [Ejemplo: cliente de Python](#python-client).</span><span class="sxs-lookup"><span data-stu-id="dd891-150">To verify that a Kafka client can connect to the cluster from on-premises, use the steps in the [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="dd891-151"><a id="vpnclient"></a> Conexión a Kafka con un cliente VPN</span><span class="sxs-lookup"><span data-stu-id="dd891-151"><a id="vpnclient"></a> Connect to Kafka with a VPN client</span></span>

<span data-ttu-id="dd891-152">Use los pasos de esta sección para crear la configuración siguiente:</span><span class="sxs-lookup"><span data-stu-id="dd891-152">Use the steps in this section to create the following configuration:</span></span>

* <span data-ttu-id="dd891-153">Red virtual</span><span class="sxs-lookup"><span data-stu-id="dd891-153">Azure Virtual Network</span></span>
* <span data-ttu-id="dd891-154">Puerta de enlace de VPN de punto a sitio</span><span class="sxs-lookup"><span data-stu-id="dd891-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="dd891-155">Cuenta de Azure Storage (usada por HDInsight)</span><span class="sxs-lookup"><span data-stu-id="dd891-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="dd891-156">Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="dd891-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="dd891-157">Siga los pasos del documento [Working with self-signed certificates for Point-to-site connections (Funcionamiento de los certificados autofirmados para conexiones de punto a sitio)](../vpn-gateway/vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="dd891-157">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="dd891-158">Este documento crea los certificados necesarios para la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dd891-158">This document creates the certificates needed for the gateway.</span></span>

2. <span data-ttu-id="dd891-159">Abra un símbolo del sistema de PowerShell y use el código siguiente para iniciar sesión en la suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="dd891-159">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="dd891-160">Use el código siguiente para crear variables que contengan la información de configuración:</span><span class="sxs-lookup"><span data-stu-id="dd891-160">Use the following code to create variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is the resource group name?"
    $baseName = Read-Host "What is the base name? It is used to create names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want to create the resources in?"
    $rootCert = Read-Host "What is the file path to the root certificate? It is used to secure the VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter the HTTPS user name and password for the HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter the SSH user name and password for the HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. <span data-ttu-id="dd891-161">Use el código siguiente para crear la red virtual y el grupo de recursos de Azure:</span><span class="sxs-lookup"><span data-stu-id="dd891-161">Use the following code to create the Azure resource group and virtual network:</span></span>

    ```powershell
    # Create the resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create the subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get the network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for the gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get the certificate info
    # Get the full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create the VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > <span data-ttu-id="dd891-162">Este proceso puede tardar varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="dd891-162">It can take several minutes for this process to complete.</span></span>

5. <span data-ttu-id="dd891-163">Use el código siguiente para crear el contenedor de blobs y la cuenta de Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="dd891-163">Use the following code to create the Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create the storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get the storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create the default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="dd891-164">Use el código siguiente para crear el clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="dd891-164">Use the following code to create the HDInsight cluster:</span></span>

    ```powershell
    # Create the HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > <span data-ttu-id="dd891-165">Este proceso tarda unos 20 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="dd891-165">This process takes around 20 minutes to complete.</span></span>

8. <span data-ttu-id="dd891-166">Use el cmdlet siguiente para recuperar la dirección URL del cliente de VPN de Windows para la red virtual:</span><span class="sxs-lookup"><span data-stu-id="dd891-166">Use the following cmdlet to retrieve the URL for the Windows VPN client for the virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="dd891-167">Para descargar el cliente de VPN de Windows, use el identificador URI devuelto en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="dd891-167">To download the Windows VPN client, use the returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="dd891-168">Configuración de Kafka para anunciar direcciones IP</span><span class="sxs-lookup"><span data-stu-id="dd891-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="dd891-169">De manera predeterminada, Zookeeper devuelve el nombre de dominio de los agentes de Kafka a los clientes.</span><span class="sxs-lookup"><span data-stu-id="dd891-169">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span></span> <span data-ttu-id="dd891-170">Esta configuración no funciona con el cliente de software de VPN, ya que no puede usar la resolución de nombres para entidades de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="dd891-170">This configuration does not work with the VPN software client, as it cannot use name resolution for entities in the virtual network.</span></span> <span data-ttu-id="dd891-171">Para esta configuración, use los pasos siguientes para configurar Kafka con el fin de anunciar direcciones IP en lugar de nombres de dominio:</span><span class="sxs-lookup"><span data-stu-id="dd891-171">For this configuration, use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="dd891-172">En el explorador web, vaya a https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="dd891-172">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="dd891-173">Reemplace __CLUSTERNAME__ por el nombre del clúster de Kafka en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd891-173">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="dd891-174">Cuando se le solicite, use el nombre de usuario y la contraseña HTTPS para el clúster.</span><span class="sxs-lookup"><span data-stu-id="dd891-174">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="dd891-175">Aparece la interfaz de usuario web de Ambari para el clúster.</span><span class="sxs-lookup"><span data-stu-id="dd891-175">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="dd891-176">Para ver información sobre Kafka, seleccione __Kafka__ en la lista de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="dd891-176">To view information on Kafka, select __Kafka__ from the list on the left.</span></span>

    ![Lista de servicios donde Kafka aparece resaltado](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="dd891-178">Para ver la configuración de Kafka, seleccione __Configs__ (Configuraciones) en la parte superior central.</span><span class="sxs-lookup"><span data-stu-id="dd891-178">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Vínculos de configuraciones de Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="dd891-180">Para encontrar la configuración __kafka-env__, escriba `kafka-env` en el campo __Filtrar__ que se encuentra en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="dd891-180">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![Configuración de Kafka para kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="dd891-182">Para configurar Kafka y anunciar direcciones IP, agregue el texto siguiente en la parte inferior del campo __kafka-env-template__:</span><span class="sxs-lookup"><span data-stu-id="dd891-182">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="dd891-183">Para configurar la interfaz en que escucha Kafka, escriba `listeners` en el campo __Filtrar__ que se encuentra en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="dd891-183">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="dd891-184">Para configurar Kafka para que escuche en todas las interfaces de red, cambie el valor del campo __listeners__ (agentes de escucha) a `PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="dd891-184">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="dd891-185">Use el botón __Guardar__ para guardar los cambios en la configuración.</span><span class="sxs-lookup"><span data-stu-id="dd891-185">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="dd891-186">Escriba un mensaje de texto para describir los cambios.</span><span class="sxs-lookup"><span data-stu-id="dd891-186">Enter a text message describing the changes.</span></span> <span data-ttu-id="dd891-187">Seleccione __Aceptar__ una vez que se guarden los cambios.</span><span class="sxs-lookup"><span data-stu-id="dd891-187">Select __OK__ once the changes have been saved.</span></span>

    ![Botón Guardar configuración](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="dd891-189">Para evitar errores al reiniciar Kafka, use el botón __Acciones de servicio__ y seleccione __Activar el modo de mantenimiento__.</span><span class="sxs-lookup"><span data-stu-id="dd891-189">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="dd891-190">Seleccione Aceptar para completar esta operación.</span><span class="sxs-lookup"><span data-stu-id="dd891-190">Select OK to complete this operation.</span></span>

    ![Acciones de servicio, en que Activar mantenimiento aparece resaltado](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="dd891-192">Para reiniciar Kafka, use el botón __Reiniciar__ y seleccione __Restart All Affected__ (Reiniciar todos los elementos afectados).</span><span class="sxs-lookup"><span data-stu-id="dd891-192">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="dd891-193">Confirme el reinicio y use el botón __Aceptar__ una vez que se complete la operación.</span><span class="sxs-lookup"><span data-stu-id="dd891-193">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![Botón Reiniciar con la opción Restart All Affected resaltada](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="dd891-195">Para deshabilitar el modo de mantenimiento, use el botón __Acciones de servicio__ y seleccione __Desactivar el modo de mantenimiento__.</span><span class="sxs-lookup"><span data-stu-id="dd891-195">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="dd891-196">Seleccione **Aceptar** para completar esta operación.</span><span class="sxs-lookup"><span data-stu-id="dd891-196">Select **OK** to complete this operation.</span></span>

### <a name="connect-to-the-vpn-gateway"></a><span data-ttu-id="dd891-197">Conexión a la puerta de enlace de VPN</span><span class="sxs-lookup"><span data-stu-id="dd891-197">Connect to the VPN gateway</span></span>

<span data-ttu-id="dd891-198">Para conectarse a la puerta de enlace de VPN desde un __cliente Windows__, use la sección __Conexión a Azure__ del documento [Configuración de una conexión de punto a sitio](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate).</span><span class="sxs-lookup"><span data-stu-id="dd891-198">To connect to the VPN gateway from a __Windows client__, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="dd891-199"><a id="python-client"></a> Ejemplo: cliente de Python</span><span class="sxs-lookup"><span data-stu-id="dd891-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="dd891-200">Para validar la conectividad con Kafka, use los pasos siguientes para crear y ejecutar un productor y un consumidor:</span><span class="sxs-lookup"><span data-stu-id="dd891-200">To validate connectivity to Kafka, use the following steps to create and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="dd891-201">Use uno de los métodos siguientes para recuperar el nombre de dominio completo (FQDN) y las direcciones IP de los nodos del clúster de Kafka:</span><span class="sxs-lookup"><span data-stu-id="dd891-201">Use one of the following methods to retrieve the fully qualified domain name (FQDN) and IP addresses of the nodes in the Kafka cluster:</span></span>

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

    <span data-ttu-id="dd891-202">En este script se supone que `$resourceGroupName` es el nombre del grupo de recursos de Azure que contiene la red virtual.</span><span class="sxs-lookup"><span data-stu-id="dd891-202">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span></span>

    <span data-ttu-id="dd891-203">Guarde la información devuelta para su uso en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="dd891-203">Save the returned information for use in the next steps.</span></span>

2. <span data-ttu-id="dd891-204">Use el código siguiente para instalar el cliente [kafka-python](http://kafka-python.readthedocs.io/):</span><span class="sxs-lookup"><span data-stu-id="dd891-204">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="dd891-205">Para enviar datos a Kafka, use el código Python siguiente:</span><span class="sxs-lookup"><span data-stu-id="dd891-205">To send data to Kafka, use the following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  # NOTE: you don't need the full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="dd891-206">Sustituya las entradas `'kafka_broker'` por las direcciones devueltas en el paso 1 de esta sección:</span><span class="sxs-lookup"><span data-stu-id="dd891-206">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="dd891-207">Si usa un __cliente de software de VPN__, sustituya las entradas `kafka_broker` por la dirección IP de los nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dd891-207">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="dd891-208">Si tiene __habilitada la resolución de nombres a través de un servidor DNS personalizado__, sustituya las entradas `kafka_broker` por el FQDN de los nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dd891-208">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd891-209">Este código envía la cadena `test message` al tema `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="dd891-209">This code sends the string `test message` to the topic `testtopic`.</span></span> <span data-ttu-id="dd891-210">La configuración predeterminada de Kafka en HDInsight es crear el tema si no existe.</span><span class="sxs-lookup"><span data-stu-id="dd891-210">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span></span>

4. <span data-ttu-id="dd891-211">Para recuperar los mensajes de Kafka, use el código Python siguiente:</span><span class="sxs-lookup"><span data-stu-id="dd891-211">To retrieve the messages from Kafka, use the following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace the `ip_address` entries with the IP address of your worker nodes
   # Again, you only need one or two, not the full list.
   # Note: auto_offset_reset='earliest' resets the starting offset to the beginning
   #       of the topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="dd891-212">Sustituya las entradas `'kafka_broker'` por las direcciones devueltas en el paso 1 de esta sección:</span><span class="sxs-lookup"><span data-stu-id="dd891-212">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="dd891-213">Si usa un __cliente de software de VPN__, sustituya las entradas `kafka_broker` por la dirección IP de los nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dd891-213">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="dd891-214">Si tiene __habilitada la resolución de nombres a través de un servidor DNS personalizado__, sustituya las entradas `kafka_broker` por el FQDN de los nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dd891-214">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd891-215">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd891-215">Next steps</span></span>

<span data-ttu-id="dd891-216">Para más información sobre cómo usar HDInsight con una red virtual, vea el documento [Extensión de las funcionalidades de HDInsight con Red virtual de Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="dd891-216">For more information on using HDInsight with a virtual network, see the [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="dd891-217">Para más información sobre cómo crear una instancia de Azure Virtual Network con puerta de enlace de VPN de punto a sitio, consulte los documentos siguientes:</span><span class="sxs-lookup"><span data-stu-id="dd891-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span></span>

* [<span data-ttu-id="dd891-218">Configuración de una conexión de punto a sitio mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dd891-218">Configure a Point-to-Site connection using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="dd891-219">Configuración de una conexión de punto a sitio mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd891-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="dd891-220">Para más información sobre cómo trabajar con Kafka en HDInsight, consulte los documentos siguientes:</span><span class="sxs-lookup"><span data-stu-id="dd891-220">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="dd891-221">Introducción a Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="dd891-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="dd891-222">Uso de creación de reflejos con Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="dd891-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
