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
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a>Conectar tooKafka en HDInsight (versión preliminar) a través de una red Virtual de Azure

Obtenga información acerca de cómo se conectan toodirectly tooKafka en HDInsight con redes virtuales de Azure. Este documento proporciona información sobre la conexión tooKafka con hello siguiendo configuraciones:

* Desde recursos de una red local. Esta conexión se establece mediante un dispositivo de red privada virtual (software o hardware) en la red local.
* Desde un entorno de desarrollo con un cliente de software de red privada virtual.

## <a name="architecture-and-planning"></a>Arquitectura y planeación

HDInsight no permite la conexión directa tooKafka sobre Hola internet pública. En su lugar, los clientes de Kafka (productores y consumidores) deben utilizar uno de los siguientes métodos de conexión de hello:

* Ejecute el cliente de Hola Hola misma red virtual que Kafka en HDInsight. Esta configuración se utiliza en hello [iniciar con Apache Kafka (versión preliminar) en HDInsight](hdinsight-apache-kafka-get-started.md) documento. nodos de clúster en hello HDInsight Hello cliente se ejecuta directamente o en otra máquina virtual en Hola mismo red.

* Conectar una red privada, como la red local, red virtual toohello. Esta configuración permite a los clientes en el trabajo de toodirectly de red local con Kafka. tooenable esta configuración, realizar Hola siguientes tareas:

    1. Cree una red virtual.
    2. Cree una puerta de enlace de red privada virtual que use una configuración de sitio a sitio. configuración de Hello usado en este documento conecta tooa dispositivo de puerta de enlace VPN en la red local.
    3. Crear un servidor DNS en la red virtual de Hola.
    4. Configure el enrutamiento entre el servidor DNS de hello en cada red.
    5. Instale a Kafka en HDInsight en la red virtual de Hola.

    Para obtener más información, vea hello [conectarse tooKafka desde una red local](#on-premises) sección. 

* Conectar equipos individuales toohello red virtual con una puerta de enlace VPN y el cliente VPN. tooenable esta configuración, realizar Hola siguientes tareas:

    1. Cree una red virtual.
    2. Cree una puerta de enlace de red privada virtual que use una configuración de punto a sitio. Esta configuración proporciona un cliente VPN que se puede instalar en los clientes Windows.
    3. Instale a Kafka en HDInsight en la red virtual de Hola.
    4. Configurar Kafka para anunciar direcciones IP. Esta configuración permite Hola cliente tooconnect mediante en lugar de nombres de dominio de direcciones IP.
    5. Descargue y use el cliente VPN de hello en el sistema de desarrollo de Hola.

    Para obtener más información, vea hello [conectarse tooKafka con un cliente VPN](#vpnclient) sección.

    > [!WARNING]
    > Esta configuración solo se recomienda para fines de desarrollo debido Hola siguientes limitaciones:
    >
    > * Cada cliente debe conectarse con un cliente de software de VPN. Azure solo proporciona un cliente basado en Windows.
    > * cliente de Hello no pasa nombre resolución solicitudes toohello red virtual, por lo que debe usar con Kafka toocommunicate de direcciones IP. Comunicación de IP necesita configuración adicional en el clúster Kafka Hola.

Para más información sobre cómo usar HDInsight en una red virtual, vea [Extensión de las funcionalidades de HDInsight con Red virtual de Azure](./hdinsight-extend-hadoop-virtual-network.md).

## <a id="on-premises"></a>Conectar tooKafka desde una red local

toocreate un clúster de Kafka que se comunica con la red local, siga los pasos de Hola Hola [red local de HDInsight conectar tooyour](./connect-on-premises-network.md) documento.

> [!IMPORTANT]
> Al crear el clúster de HDInsight de hello, seleccione hello __Kafka__ tipo de clúster.

Estos pasos para crear Hola siguiente configuración:

* Red virtual
* Puerta de enlace de VPN de sitio a sitio
* Cuenta de Azure Storage (usada por HDInsight)
* Kafka en HDInsight

tooverify que un cliente de Kafka puede conectarse toohello clúster local, use los pasos de Hola Hola [ejemplo: cliente de Python](#python-client) sección.

## <a id="vpnclient"></a>Conectarse tooKafka con un cliente VPN

Siga los pasos de hello en este Hola de toocreate de la sección siguiente configuración:

* Red virtual
* Puerta de enlace de VPN de punto a sitio
* Cuenta de Azure Storage (usada por HDInsight)
* Kafka en HDInsight

1. Siga los pasos de Hola Hola [trabajar con certificados autofirmados para conexiones de punto a sitio](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) documento. Este documento crea certificados de hello necesarios para puerta de enlace de Hola.

2. Abra un símbolo del sistema de PowerShell y usar hello después código toolog en tooyour suscripción de Azure:

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. Usar hello después de las variables de toocreate de código que contienen información de configuración:

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

4. Siguiente de Hola de uso de código grupo de recursos de Azure de hello toocreate y red virtual:

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
    > Puede tardar varios minutos para este toocomplete de proceso.

5. Usar hello después de contenedor de cuenta de almacenamiento de Azure y blob de la Hola del toocreate código:

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

6. Usar hello después de clúster de HDInsight de código toocreate hello:

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
  > Este proceso tarda aproximadamente 20 minutos toocomplete.

8. Usar hello después de la dirección URL de cmdlet tooretrieve hello para el cliente de VPN de Windows hello para la red virtual de hello:

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    cliente de VPN de Windows de hello toodownload, use Hola devuelve URI en el explorador web.

### <a name="configure-kafka-for-ip-advertising"></a>Configuración de Kafka para anunciar direcciones IP

De forma predeterminada, Zookeeper devuelve el nombre de dominio de Hola de hello Kafka corredores de bolsa tooclients. Esta configuración no funciona con hello cliente VPN de software, como la resolución de nombres no puede usar para las entidades de red virtual de Hola. Para esta configuración, utilice el siguiente de hello tooconfigure de pasos de direcciones IP de tooadvertise Kafka en lugar de nombres de dominio:

1. Mediante un explorador web, vaya a toohttps://CLUSTERNAME.azurehdinsight.net. Reemplace __CLUSTERNAME__ con el nombre de Hola de hello Kafka en clúster de HDInsight.

    Cuando se le pida, use Hola HTTPS nombre y contraseña para clúster Hola. Hola Ambari Web UI para clúster Hola se muestra.

2. información de tooview en Kafka, seleccione __Kafka__ en lista de Hola Hola izquierda.

    ![Lista de servicios donde Kafka aparece resaltado](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. Seleccione tooview configuración Kafka, __configuraciones__ desde la parte superior central de Hola.

    ![Vínculos de configuraciones de Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. Hola toofind __kafka env__ configuración, escriba `kafka-env` en hello __filtro__ campo en la esquina superior derecha de Hola.

    ![Configuración de Kafka para kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. las direcciones IP de tooadvertise Kafka tooconfigure, agregue Hola después de la parte inferior de toohello de texto de hello __kafka-env: plantilla__ campo:

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. interfaz de hello tooconfigure que escucha Kafka, escriba `listeners` en hello __filtro__ campo en la esquina superior derecha de Hola.

7. tooconfigure Kafka toolisten en todas las interfaces de red, cambiar el valor de Hola Hola __los agentes de escucha__ campo demasiado`PLAINTEXT://0.0.0.0:9092`.

8. cambios de configuración de toosave hello, usar hello __guardar__ botón. Escriba un mensaje de texto que describe los cambios de Hola. Seleccione __Aceptar__ una vez que se guardaron los cambios de Hola.

    ![Botón Guardar configuración](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. errores de tooprevent al reiniciar Kafka, usar hello __acciones de servicio__ botón y seleccione __en modo de mantenimiento__. Seleccione Aceptar toocomplete esta operación.

    ![Acciones de servicio, en que Activar mantenimiento aparece resaltado](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. toorestart Kafka, usar hello __reiniciar__ botón y seleccione __reiniciar todos los afectados__. Confirme el reinicio de hello y, a continuación, usar hello __Aceptar__ botón una vez completada la operación de Hola.

    ![Botón Reiniciar con la opción Restart All Affected resaltada](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. modo de mantenimiento de toodisable, use hello __acciones de servicio__ botón y seleccione __activar el modo de mantenimiento__. Seleccione **Aceptar** toocomplete esta operación.

### <a name="connect-toohello-vpn-gateway"></a>Conectar la puerta de enlace VPN toohello

puerta de enlace VPN de tooconnect toohello de un __cliente de Windows__, usar hello __conectar tooAzure__ sección de hello [configurar una conexión punto a sitio](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) documento.

## <a id="python-client"></a> Ejemplo: cliente de Python

toovalidate conectividad tooKafka, usar hello siguiendo los pasos toocreate y ejecute un productor de Python y un consumidor:

1. Uso de Hola Hola de métodos tooretrieve si sigue totalmente calificado (FQDN) del nombre de dominio y direcciones IP de los nodos de Hola Hola clúster Kafka:

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

    Este script se da por supuesto que `$resourceGroupName` es nombre Hola Hola Azure del grupo de recursos que contiene la red virtual de Hola.

    Guardar Hola devuelve información para su uso en los pasos siguientes de Hola.

2. Hola de uso después de hello tooinstall [kafka-python](http://kafka-python.readthedocs.io/) cliente:

        pip install kafka-python

3. toosend datos tooKafka, Hola use después el código Python:

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    Reemplace hello `'kafka_broker'` entradas con direcciones de hello devuelven desde el paso 1 en esta sección:

    * Si usas un __cliente VPN de Software__, reemplace hello `kafka_broker` entradas con la dirección IP de Hola de los nodos de trabajador.

    * Si tiene __habilitada la resolución de nombres a través de un servidor DNS personalizado__, reemplace hello `kafka_broker` entradas con hello FQDN Hola de nodos de trabajador.

    > [!NOTE]
    > Este código envía la cadena de hello `test message` toohello tema `testtopic`. configuración predeterminada de Hola de Kafka en HDInsight es tema de hello toocreate si no existe.

4. mensajes de saludo tooretrieve desde Kafka, usar hello después código Python:

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

    Reemplace hello `'kafka_broker'` entradas con direcciones de hello devuelven desde el paso 1 en esta sección:

    * Si usas un __cliente VPN de Software__, reemplace hello `kafka_broker` entradas con la dirección IP de Hola de los nodos de trabajador.

    * Si tiene __habilitada la resolución de nombres a través de un servidor DNS personalizado__, reemplace hello `kafka_broker` entradas con hello FQDN Hola de nodos de trabajador.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de HDInsight con una red virtual, vea hello [HDInsight de Azure de extender una red Virtual de Azure](hdinsight-extend-hadoop-virtual-network.md) documento.

Para obtener más información sobre cómo crear una red Virtual de Azure con puerta de enlace VPN de punto a sitio, vea Hola siguientes documentos:

* [Configurar una conexión de punto a sitio mediante Hola portal de Azure](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [Configuración de una conexión de punto a sitio mediante Azure PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

Para obtener más información sobre cómo trabajar con Kafka en HDInsight, vea Hola siguientes documentos:

* [Introducción a Kafka en HDInsight](hdinsight-apache-kafka-get-started.md)
* [Uso de creación de reflejos con Kafka en HDInsight](hdinsight-apache-kafka-mirroring.md)
