---
title: tooKafka aaaConnect mediante redes virtuales - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodirectly conectar tooKafka en HDInsight a través de una red Virtual de Azure. Obtenga información acerca de cómo tooconnect tooKafka de clientes de desarrollo mediante una puerta de enlace VPN o de los clientes en sus instalaciones de red mediante el uso de un dispositivo de puerta de enlace VPN."
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
ms.openlocfilehash: 03542fe14b9a1d010dffa22a8f8d96b098a1576e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="6bcf9-104">Conectar tooKafka en HDInsight (versión preliminar) a través de una red Virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="6bcf9-104">Connect tooKafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="6bcf9-105">Obtenga información acerca de cómo se conectan toodirectly tooKafka en HDInsight con redes virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-105">Learn how toodirectly connect tooKafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="6bcf9-106">Este documento proporciona información sobre la conexión tooKafka con hello siguiendo configuraciones:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-106">This document provides information on connecting tooKafka using hello following configurations:</span></span>

* <span data-ttu-id="6bcf9-107">Desde recursos de una red local.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-107">From resources in an on-premises network.</span></span> <span data-ttu-id="6bcf9-108">Esta conexión se establece mediante un dispositivo de red privada virtual (software o hardware) en la red local.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="6bcf9-109">Desde un entorno de desarrollo con un cliente de software de red privada virtual.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="6bcf9-110">Arquitectura y planeación</span><span class="sxs-lookup"><span data-stu-id="6bcf9-110">Architecture and planning</span></span>

<span data-ttu-id="6bcf9-111">HDInsight no permite la conexión directa tooKafka sobre Hola internet pública.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-111">HDInsight does not allow direct connection tooKafka over hello public internet.</span></span> <span data-ttu-id="6bcf9-112">En su lugar, los clientes de Kafka (productores y consumidores) deben utilizar uno de los siguientes métodos de conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-112">Instead, Kafka clients (producers and consumers) must use one of hello following connection methods:</span></span>

* <span data-ttu-id="6bcf9-113">Ejecute el cliente de Hola Hola misma red virtual que Kafka en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-113">Run hello client in hello same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="6bcf9-114">Esta configuración se utiliza en hello [iniciar con Apache Kafka (versión preliminar) en HDInsight](hdinsight-apache-kafka-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-114">This configuration is used in hello [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="6bcf9-115">nodos de clúster en hello HDInsight Hello cliente se ejecuta directamente o en otra máquina virtual en Hola mismo red.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-115">hello client runs directly on hello HDInsight cluster nodes or on another virtual machine in hello same network.</span></span>

* <span data-ttu-id="6bcf9-116">Conectar una red privada, como la red local, red virtual toohello.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-116">Connect a private network, such as your on-premises network, toohello virtual network.</span></span> <span data-ttu-id="6bcf9-117">Esta configuración permite a los clientes en el trabajo de toodirectly de red local con Kafka.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-117">This configuration allows clients in your on-premises network toodirectly work with Kafka.</span></span> <span data-ttu-id="6bcf9-118">tooenable esta configuración, realizar Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-118">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="6bcf9-119">Cree una red virtual.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="6bcf9-120">Cree una puerta de enlace de red privada virtual que use una configuración de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="6bcf9-121">configuración de Hello usado en este documento conecta tooa dispositivo de puerta de enlace VPN en la red local.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-121">hello configuration used in this document connects tooa VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="6bcf9-122">Crear un servidor DNS en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-122">Create a DNS server in hello virtual network.</span></span>
    4. <span data-ttu-id="6bcf9-123">Configure el enrutamiento entre el servidor DNS de hello en cada red.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-123">Configure forwarding between hello DNS server in each network.</span></span>
    5. <span data-ttu-id="6bcf9-124">Instale a Kafka en HDInsight en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-124">Install Kafka on HDInsight into hello virtual network.</span></span>

    <span data-ttu-id="6bcf9-125">Para obtener más información, vea hello [conectarse tooKafka desde una red local](#on-premises) sección.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-125">For more information, see hello [Connect tooKafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="6bcf9-126">Conectar equipos individuales toohello red virtual con una puerta de enlace VPN y el cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-126">Connect individual machines toohello virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="6bcf9-127">tooenable esta configuración, realizar Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-127">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="6bcf9-128">Cree una red virtual.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="6bcf9-129">Cree una puerta de enlace de red privada virtual que use una configuración de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="6bcf9-130">Esta configuración proporciona un cliente VPN que se puede instalar en los clientes Windows.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="6bcf9-131">Instale a Kafka en HDInsight en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-131">Install Kafka on HDInsight into hello virtual network.</span></span>
    4. <span data-ttu-id="6bcf9-132">Configurar Kafka para anunciar direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="6bcf9-133">Esta configuración permite Hola cliente tooconnect mediante en lugar de nombres de dominio de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-133">This configuration allows hello client tooconnect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="6bcf9-134">Descargue y use el cliente VPN de hello en el sistema de desarrollo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-134">Download and use hello VPN client on hello development system.</span></span>

    <span data-ttu-id="6bcf9-135">Para obtener más información, vea hello [conectarse tooKafka con un cliente VPN](#vpnclient) sección.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-135">For more information, see hello [Connect tooKafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="6bcf9-136">Esta configuración solo se recomienda para fines de desarrollo debido Hola siguientes limitaciones:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-136">This configuration is only recommended for development purposes because of hello following limitations:</span></span>
    >
    > * <span data-ttu-id="6bcf9-137">Cada cliente debe conectarse con un cliente de software de VPN.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="6bcf9-138">Azure solo proporciona un cliente basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="6bcf9-139">cliente de Hello no pasa nombre resolución solicitudes toohello red virtual, por lo que debe usar con Kafka toocommunicate de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-139">hello client does not pass name resolution requests toohello virtual network, so you must use IP addressing toocommunicate with Kafka.</span></span> <span data-ttu-id="6bcf9-140">Comunicación de IP necesita configuración adicional en el clúster Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-140">IP communication requires additional configuration on hello Kafka cluster.</span></span>

<span data-ttu-id="6bcf9-141">Para más información sobre cómo usar HDInsight en una red virtual, vea [Extensión de las funcionalidades de HDInsight con Red virtual de Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="6bcf9-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="6bcf9-142"><a id="on-premises"></a>Conectar tooKafka desde una red local</span><span class="sxs-lookup"><span data-stu-id="6bcf9-142"><a id="on-premises"></a> Connect tooKafka from an on-premises network</span></span>

<span data-ttu-id="6bcf9-143">toocreate un clúster de Kafka que se comunica con la red local, siga los pasos de Hola Hola [red local de HDInsight conectar tooyour](./connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-143">toocreate a Kafka cluster that communicates with your on-premises network, follow hello steps in hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6bcf9-144">Al crear el clúster de HDInsight de hello, seleccione hello __Kafka__ tipo de clúster.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-144">When creating hello HDInsight cluster, select hello __Kafka__ cluster type.</span></span>

<span data-ttu-id="6bcf9-145">Estos pasos para crear Hola siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-145">These steps create hello following configuration:</span></span>

* <span data-ttu-id="6bcf9-146">Red virtual</span><span class="sxs-lookup"><span data-stu-id="6bcf9-146">Azure Virtual Network</span></span>
* <span data-ttu-id="6bcf9-147">Puerta de enlace de VPN de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="6bcf9-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="6bcf9-148">Cuenta de Azure Storage (usada por HDInsight)</span><span class="sxs-lookup"><span data-stu-id="6bcf9-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="6bcf9-149">Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="6bcf9-149">Kafka on HDInsight</span></span>

<span data-ttu-id="6bcf9-150">tooverify que un cliente de Kafka puede conectarse toohello clúster local, use los pasos de Hola Hola [ejemplo: cliente de Python](#python-client) sección.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-150">tooverify that a Kafka client can connect toohello cluster from on-premises, use hello steps in hello [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="6bcf9-151"><a id="vpnclient"></a>Conectarse tooKafka con un cliente VPN</span><span class="sxs-lookup"><span data-stu-id="6bcf9-151"><a id="vpnclient"></a> Connect tooKafka with a VPN client</span></span>

<span data-ttu-id="6bcf9-152">Siga los pasos de hello en este Hola de toocreate de la sección siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-152">Use hello steps in this section toocreate hello following configuration:</span></span>

* <span data-ttu-id="6bcf9-153">Red virtual</span><span class="sxs-lookup"><span data-stu-id="6bcf9-153">Azure Virtual Network</span></span>
* <span data-ttu-id="6bcf9-154">Puerta de enlace de VPN de punto a sitio</span><span class="sxs-lookup"><span data-stu-id="6bcf9-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="6bcf9-155">Cuenta de Azure Storage (usada por HDInsight)</span><span class="sxs-lookup"><span data-stu-id="6bcf9-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="6bcf9-156">Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="6bcf9-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="6bcf9-157">Siga los pasos de Hola Hola [trabajar con certificados autofirmados para conexiones de punto a sitio](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) documento.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-157">Follow hello steps in hello [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="6bcf9-158">Este documento crea certificados de hello necesarios para puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-158">This document creates hello certificates needed for hello gateway.</span></span>

2. <span data-ttu-id="6bcf9-159">Abra un símbolo del sistema de PowerShell y usar hello después código toolog en tooyour suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-159">Open a PowerShell prompt and use hello following code toolog in tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="6bcf9-160">Usar hello después de las variables de toocreate de código que contienen información de configuración:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-160">Use hello following code toocreate variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is hello resource group name?"
    $baseName = Read-Host "What is hello base name? It is used toocreate names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want toocreate hello resources in?"
    $rootCert = Read-Host "What is hello file path toohello root certificate? It is used toosecure hello VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter hello HTTPS user name and password for hello HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter hello SSH user name and password for hello HDInsight cluster" -UserName "sshuser"

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

4. <span data-ttu-id="6bcf9-161">Siguiente de Hola de uso de código grupo de recursos de Azure de hello toocreate y red virtual:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-161">Use hello following code toocreate hello Azure resource group and virtual network:</span></span>

    ```powershell
    # Create hello resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create hello subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get hello network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for hello gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get hello certificate info
    # Get hello full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create hello VPN gateway
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
    > <span data-ttu-id="6bcf9-162">Puede tardar varios minutos para este toocomplete de proceso.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-162">It can take several minutes for this process toocomplete.</span></span>

5. <span data-ttu-id="6bcf9-163">Usar hello después de contenedor de cuenta de almacenamiento de Azure y blob de la Hola del toocreate código:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-163">Use hello following code toocreate hello Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create hello storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get hello storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create hello default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="6bcf9-164">Usar hello después de clúster de HDInsight de código toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-164">Use hello following code toocreate hello HDInsight cluster:</span></span>

    ```powershell
    # Create hello HDInsight cluster
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
  > <span data-ttu-id="6bcf9-165">Este proceso tarda aproximadamente 20 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-165">This process takes around 20 minutes toocomplete.</span></span>

8. <span data-ttu-id="6bcf9-166">Usar hello después de la dirección URL de cmdlet tooretrieve hello para el cliente de VPN de Windows hello para la red virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-166">Use hello following cmdlet tooretrieve hello URL for hello Windows VPN client for hello virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="6bcf9-167">cliente de VPN de Windows de hello toodownload, use Hola devuelve URI en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-167">toodownload hello Windows VPN client, use hello returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="6bcf9-168">Configuración de Kafka para anunciar direcciones IP</span><span class="sxs-lookup"><span data-stu-id="6bcf9-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="6bcf9-169">De forma predeterminada, Zookeeper devuelve el nombre de dominio de Hola de hello Kafka corredores de bolsa tooclients.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-169">By default, Zookeeper returns hello domain name of hello Kafka brokers tooclients.</span></span> <span data-ttu-id="6bcf9-170">Esta configuración no funciona con hello cliente VPN de software, como la resolución de nombres no puede usar para las entidades de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-170">This configuration does not work with hello VPN software client, as it cannot use name resolution for entities in hello virtual network.</span></span> <span data-ttu-id="6bcf9-171">Para esta configuración, utilice el siguiente de hello tooconfigure de pasos de direcciones IP de tooadvertise Kafka en lugar de nombres de dominio:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-171">For this configuration, use hello following steps tooconfigure Kafka tooadvertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="6bcf9-172">Mediante un explorador web, vaya a toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-172">Using a web browser, go toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="6bcf9-173">Reemplace __CLUSTERNAME__ con el nombre de Hola de hello Kafka en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-173">Replace __CLUSTERNAME__ with hello name of hello Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="6bcf9-174">Cuando se le pida, use Hola HTTPS nombre y contraseña para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-174">When prompted, use hello HTTPS user name and password for hello cluster.</span></span> <span data-ttu-id="6bcf9-175">Hola Ambari Web UI para clúster Hola se muestra.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-175">hello Ambari Web UI for hello cluster is displayed.</span></span>

2. <span data-ttu-id="6bcf9-176">información de tooview en Kafka, seleccione __Kafka__ en lista de Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-176">tooview information on Kafka, select __Kafka__ from hello list on hello left.</span></span>

    ![Lista de servicios donde Kafka aparece resaltado](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="6bcf9-178">Seleccione tooview configuración Kafka, __configuraciones__ desde la parte superior central de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-178">tooview Kafka configuration, select __Configs__ from hello top middle.</span></span>

    ![Vínculos de configuraciones de Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="6bcf9-180">Hola toofind __kafka env__ configuración, escriba `kafka-env` en hello __filtro__ campo en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-180">toofind hello __kafka-env__ configuration, enter `kafka-env` in hello __Filter__ field on hello upper right.</span></span>

    ![Configuración de Kafka para kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="6bcf9-182">las direcciones IP de tooadvertise Kafka tooconfigure, agregue Hola después de la parte inferior de toohello de texto de hello __kafka-env: plantilla__ campo:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-182">tooconfigure Kafka tooadvertise IP addresses, add hello following text toohello bottom of hello __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="6bcf9-183">interfaz de hello tooconfigure que escucha Kafka, escriba `listeners` en hello __filtro__ campo en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-183">tooconfigure hello interface that Kafka listens on, enter `listeners` in hello __Filter__ field on hello upper right.</span></span>

7. <span data-ttu-id="6bcf9-184">tooconfigure Kafka toolisten en todas las interfaces de red, cambiar el valor de Hola Hola __los agentes de escucha__ campo demasiado`PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-184">tooconfigure Kafka toolisten on all network interfaces, change hello value in hello __listeners__ field too`PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="6bcf9-185">cambios de configuración de toosave hello, usar hello __guardar__ botón.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-185">toosave hello configuration changes, use hello __Save__ button.</span></span> <span data-ttu-id="6bcf9-186">Escriba un mensaje de texto que describe los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-186">Enter a text message describing hello changes.</span></span> <span data-ttu-id="6bcf9-187">Seleccione __Aceptar__ una vez que se guardaron los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-187">Select __OK__ once hello changes have been saved.</span></span>

    ![Botón Guardar configuración](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="6bcf9-189">errores de tooprevent al reiniciar Kafka, usar hello __acciones de servicio__ botón y seleccione __en modo de mantenimiento__.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-189">tooprevent errors when restarting Kafka, use hello __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="6bcf9-190">Seleccione Aceptar toocomplete esta operación.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-190">Select OK toocomplete this operation.</span></span>

    ![Acciones de servicio, en que Activar mantenimiento aparece resaltado](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="6bcf9-192">toorestart Kafka, usar hello __reiniciar__ botón y seleccione __reiniciar todos los afectados__.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-192">toorestart Kafka, use hello __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="6bcf9-193">Confirme el reinicio de hello y, a continuación, usar hello __Aceptar__ botón una vez completada la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-193">Confirm hello restart, and then use hello __OK__ button after hello operation has completed.</span></span>

    ![Botón Reiniciar con la opción Restart All Affected resaltada](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="6bcf9-195">modo de mantenimiento de toodisable, use hello __acciones de servicio__ botón y seleccione __activar el modo de mantenimiento__.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-195">toodisable maintenance mode, use hello __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="6bcf9-196">Seleccione **Aceptar** toocomplete esta operación.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-196">Select **OK** toocomplete this operation.</span></span>

### <a name="connect-toohello-vpn-gateway"></a><span data-ttu-id="6bcf9-197">Conectar la puerta de enlace VPN toohello</span><span class="sxs-lookup"><span data-stu-id="6bcf9-197">Connect toohello VPN gateway</span></span>

<span data-ttu-id="6bcf9-198">puerta de enlace VPN de tooconnect toohello de un __cliente de Windows__, usar hello __conectar tooAzure__ sección de hello [configurar una conexión punto a sitio](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) documento.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-198">tooconnect toohello VPN gateway from a __Windows client__, use hello __Connect tooAzure__ section of hello [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="6bcf9-199"><a id="python-client"></a> Ejemplo: cliente de Python</span><span class="sxs-lookup"><span data-stu-id="6bcf9-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="6bcf9-200">toovalidate conectividad tooKafka, usar hello siguiendo los pasos toocreate y ejecute un productor de Python y un consumidor:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-200">toovalidate connectivity tooKafka, use hello following steps toocreate and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="6bcf9-201">Uso de Hola Hola de métodos tooretrieve si sigue totalmente calificado (FQDN) del nombre de dominio y direcciones IP de los nodos de Hola Hola clúster Kafka:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-201">Use one of hello following methods tooretrieve hello fully qualified domain name (FQDN) and IP addresses of hello nodes in hello Kafka cluster:</span></span>

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

    <span data-ttu-id="6bcf9-202">Este script se da por supuesto que `$resourceGroupName` es nombre Hola Hola Azure del grupo de recursos que contiene la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-202">This script assumes that `$resourceGroupName` is hello name of hello Azure resource group that contains hello virtual network.</span></span>

    <span data-ttu-id="6bcf9-203">Guardar Hola devuelve información para su uso en los pasos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-203">Save hello returned information for use in hello next steps.</span></span>

2. <span data-ttu-id="6bcf9-204">Hola de uso después de hello tooinstall [kafka-python](http://kafka-python.readthedocs.io/) cliente:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-204">Use hello following tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="6bcf9-205">toosend datos tooKafka, Hola use después el código Python:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-205">toosend data tooKafka, use hello following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="6bcf9-206">Reemplace hello `'kafka_broker'` entradas con direcciones de hello devuelven desde el paso 1 en esta sección:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-206">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="6bcf9-207">Si usas un __cliente VPN de Software__, reemplace hello `kafka_broker` entradas con la dirección IP de Hola de los nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-207">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="6bcf9-208">Si tiene __habilitada la resolución de nombres a través de un servidor DNS personalizado__, reemplace hello `kafka_broker` entradas con hello FQDN Hola de nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-208">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6bcf9-209">Este código envía la cadena de hello `test message` toohello tema `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-209">This code sends hello string `test message` toohello topic `testtopic`.</span></span> <span data-ttu-id="6bcf9-210">configuración predeterminada de Hola de Kafka en HDInsight es tema de hello toocreate si no existe.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-210">hello default configuration of Kafka on HDInsight is toocreate hello topic if it does not exist.</span></span>

4. <span data-ttu-id="6bcf9-211">mensajes de saludo tooretrieve desde Kafka, usar hello después código Python:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-211">tooretrieve hello messages from Kafka, use hello following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace hello `ip_address` entries with hello IP address of your worker nodes
   # Again, you only need one or two, not hello full list.
   # Note: auto_offset_reset='earliest' resets hello starting offset toohello beginning
   #       of hello topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="6bcf9-212">Reemplace hello `'kafka_broker'` entradas con direcciones de hello devuelven desde el paso 1 en esta sección:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-212">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="6bcf9-213">Si usas un __cliente VPN de Software__, reemplace hello `kafka_broker` entradas con la dirección IP de Hola de los nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-213">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="6bcf9-214">Si tiene __habilitada la resolución de nombres a través de un servidor DNS personalizado__, reemplace hello `kafka_broker` entradas con hello FQDN Hola de nodos de trabajador.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-214">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bcf9-215">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6bcf9-215">Next steps</span></span>

<span data-ttu-id="6bcf9-216">Para obtener más información sobre el uso de HDInsight con una red virtual, vea hello [HDInsight de Azure de extender una red Virtual de Azure](hdinsight-extend-hadoop-virtual-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="6bcf9-216">For more information on using HDInsight with a virtual network, see hello [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="6bcf9-217">Para obtener más información sobre cómo crear una red Virtual de Azure con puerta de enlace VPN de punto a sitio, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see hello following documents:</span></span>

* [<span data-ttu-id="6bcf9-218">Configurar una conexión de punto a sitio mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6bcf9-218">Configure a Point-to-Site connection using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="6bcf9-219">Configuración de una conexión de punto a sitio mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bcf9-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="6bcf9-220">Para obtener más información sobre cómo trabajar con Kafka en HDInsight, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="6bcf9-220">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="6bcf9-221">Introducción a Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="6bcf9-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="6bcf9-222">Uso de creación de reflejos con Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="6bcf9-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
