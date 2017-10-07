---
title: "clústeres de HBase aaaCreate en una red Virtual - Azure | Documentos de Microsoft"
description: "Introducción al uso de HBase en HDInsight de Azure Obtenga información acerca de cómo se agrupa toocreate HBase para HDInsight en red Virtual de Azure."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a>Creación de clústeres de HBase en HDInsight en Azure Virtual Network
Obtenga información acerca de cómo los clústeres de toocreate HDInsight HBase de Azure en un [red Virtual de Azure][1].

Con la integración de red virtual, clústeres de HBase pueden ser implementado toohello mismo virtual de red así como las aplicaciones que las aplicaciones pueden comunicarse directamente con HBase. Hola ventajas se incluyen:

* Conectividad directa de hello web aplicación toohello los nodos de clúster de HBase hello, que permite la comunicación a través de procedimientos remotos de HBase Java llamar a las API (RPC).
* Rendimiento mejorado gracias a que el tráfico ya no tiene que examinar varias puertas de enlace y equilibradores de carga.
* Hola capacidad tooprocess información confidencial de forma más segura sin exponer un extremo público.

### <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener Hola siguientes elementos:

* **Una suscripción de Azure**. Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Una estación de trabajo con Azure PowerShell**. Consulte [Install and use Azure PowerShell (Instalación y uso de Azure PowerShell)](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).

## <a name="create-hbase-cluster-into-virtual-network"></a>Creación de un clúster de HBase en red virtual
En esta sección, se crea un clúster de HBase basados en Linux con cuenta de almacenamiento de Azure dependiente de hello en una red virtual de Azure con un [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Para otros métodos de creación de clúster y descripción de la configuración de hello, consulte [HDInsight crear clústeres](hdinsight-hadoop-provision-linux-clusters.md). Para obtener más información sobre el uso de un toocreate plantilla Hadoop los clústeres de HDInsight, vea [Hadoop crear clústeres de HDInsight con plantillas del Administrador de recursos de Azure](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

> [!NOTE]
> Algunas propiedades están codificados en la plantilla de Hola. Por ejemplo:
>
> * **Ubicación**: este de EE. UU. 2
> * **Versión del clúster**: 3.5
> * **Número de nodos de trabajo en el clúster**: 2
> * **Nombre de la cuenta de almacenamiento predeterminada**: una cadena única
> * **Nombre de la red virtual**: &lt;Nombre del clúster&gt;-vnet
> * **Espacio de direcciones de red virtual**: 10.0.0.0/16
> * **Nombre de subred**: subnet1
> * **Intervalo de direcciones de subred**: 10.0.0.0/24
>
> &lt;Nombre del clúster > se reemplaza con el nombre de clúster de hello proporcionan cuando se usa la plantilla de Hola.
>
>

1. Haga clic en hello después de la plantilla de imagen tooopen Hola Hola portal de Azure. plantilla de Hola se encuentra en [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. De hello **implementación personalizada** hoja, escriba Hola propiedades siguientes:

   * **Suscripción**: seleccione un clúster de HDInsight de suscripción de Azure usada toocreate hello, Hola dependiente cuenta de almacenamiento y Hola red virtual de Azure.
   * **Grupo de recursos**: seleccione **Crear nuevo** y especifique un nuevo nombre al grupo de recursos.
   * **Ubicación**: seleccione una ubicación para el grupo de recursos de Hola.
   * **ClusterName**: escriba un nombre para toobe de clúster de Hadoop de hello creado.
   * **Nombre de inicio de sesión y la contraseña del clúster**: nombre de inicio de sesión predeterminado de hello es **administración**.
   * **SSH username y password**: nombre de usuario de hello predeterminada es **sshuser**.  Puede cambiarlo.
   * **Muestro mi conformidad toohello términos y condiciones de hello indicadas anteriormente**: (seleccione)
3. Haga clic en **Comprar**. Se tarda aproximadamente toocreate de aproximadamente 20 minutos de un clúster. Una vez creado el clúster de hello, haga clic en hoja de clúster de hello en tooopen portal Hola se.

Después de completar el tutorial de hello, conviene clúster de hello toodelete. Con HDInsight, los datos se almacenan en Almacenamiento de Azure, por lo que puede eliminar un clúster de forma segura cuando no está en uso. También se le cargará por un clúster de HDInsight aunque no esté en uso. Puesto que los cargos de Hola de clúster de hello son muchas veces más que los cargos de hello para el almacenamiento, conviene económico toodelete clústeres cuando no están en uso. Para obtener instrucciones de hello de la eliminación de un clúster, consulte [Hadoop administrar clústeres de HDInsight mediante el uso de Hola portal de Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

toobegin trabajar con el nuevo clúster de HBase, puede usar los procedimientos de Hola que se encuentran en [empezar a utilizar HBase con Hadoop en HDInsight](hdinsight-hbase-tutorial-get-started.md).

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a>Conectar el clúster de HBase toohello mediante las API de RPC de Java de HBase
1. Crear una infraestructura como servicio (IaaS) virtual máquina en Hola misma red virtual de Azure y Hola la misma subred. Para obtener instrucciones sobre cómo crear una nueva máquina virtual de IaaS consulte el tutorial sobre la [creación de una máquina virtual que ejecuta Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md). Al seguir los pasos de hello en este documento, debe utilizar Hola después de valores de configuración de red de hello:

   * **Red virtual**: &lt;Nombre del clúster&gt;-vnet
   * **Subred**: subnet1

   > [!IMPORTANT]
   > Reemplace &lt;nombre del clúster > con el nombre de Hola que utilizó al crear el clúster de HDInsight de hello en los pasos anteriores.
   >
   >

   Con estos valores, Hola máquina virtual se coloca en hello misma red virtual y subred que el clúster de HDInsight Hola. Esta configuración permite toodirectly comunicarse entre sí. Hay un toocreate forma un clúster de HDInsight con un nodo del borde vacío. nodo del borde Hola puede ser clúster de hello toomanage usado.  Para obtener más información, consulte [Uso de nodos perimetrales vacíos en HDInsight](hdinsight-apps-use-edge-node.md).

2. Al utilizar un tooHBase de tooconnect de aplicación de Java de forma remota, debe usar el nombre de dominio completo (FQDN) de Hola. toodetermine esto, debe tener el sufijo DNS específico de la conexión de Hola de clúster de HBase Hola. toodo, que puede usar uno de los siguientes métodos de hello:

   * Use un toomake de explorador Web una llamada Ambari:

     Examinar toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / hospeda? minimal_response = true. Convierte un archivo JSON con los sufijos DNS Hola.
   * Use el sitio Web de hello Ambari:

     1. Examinar demasiado https://&lt;ClusterName >. azurehdinsight.net.
     2. Haga clic en **Hosts** de menú superior Hola.
   * Utilizar llamadas a REST Curl toomake:

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     Hola devuelven datos JavaScript Object Notation (JSON), busque la entrada de "host_name" Hola. Contiene Hola FQDN para los nodos de hello en clúster de Hola. Por ejemplo:

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     parte de Hola de hello dominio nombre que comienza con el nombre del clúster de hello es sufijo DNS de Hola. Por ejemplo, mycluster.b1.cloudapp.net.
   * Uso de Azure PowerShell

     Hola de uso después de hello de tooregister de secuencia de comandos de PowerShell de Azure **ClusterDetail Get** función, que puede ser el sufijo DNS de hello tooreturn usado:

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     Después de ejecutar script de PowerShell de Azure de hello, comando siguiente de Hola de uso sufijo DNS de hello tooreturn mediante el uso de hello **ClusterDetail Get** función. Especifique el nombre del clúster de HBase de HDInsight, el nombre y la contraseña de administrador cuando use este comando.

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     Este comando devuelve el sufijo DNS de Hola. Por ejemplo, **yourclustername.b4.internal.cloudapp.net**.


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

tooverify que Hola máquina virtual puede comunicarse con hello clúster de HBase, use comandos de hello `ping headnode0.<dns suffix>` de la máquina virtual de Hola. Por ejemplo, haga ping a headnode0.mycluster.b1.cloudapp.net

toouse esta información en una aplicación Java, puede seguir los pasos de hello en [aplicaciones de Java de toobuild usar Maven que utilizar HBase con HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate una aplicación. aplicación de hello toohave conectar el servidor remoto de HBase de tooa, modifique hello **hbase-site.xml** archivo esta Hola de toouse FQDN de ejemplo para Zookeeper. Por ejemplo:

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> Para obtener más información acerca de la resolución de nombres en redes virtuales de Azure, incluida la forma toouse su propio servidor DNS, consulte [resolución de nombres (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
>
>

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, se habrá aprendido cómo toocreate un clúster de HBase. toolearn más información, vea:

* [Introducción a HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Uso de nodos perimetrales vacíos en HDInsight](hdinsight-apps-use-edge-node.md)
* [Configuración de la replicación geográfica de HBase en HDInsight](hdinsight-hbase-replication.md)
* [Consulte Creación de clústeres de Hadoop en HDInsight.](hdinsight-hadoop-provision-linux-clusters.md)
* [Introducción al uso de HBase con Hadoop en HDInsight](hdinsight-hbase-tutorial-get-started.md)
* [Análisis de opiniones de Twitter con HBase en HDInsight](hdinsight-hbase-analyze-twitter-sentiment.md)
* [Información general sobre redes virtuales][vnet-overview]

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Detalles de aprovisionamiento para el nuevo clúster de HBase Hola"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Use la acción de secuencia de comandos toocustomize un clúster de HBase"

[azure-preview-portal]: https://portal.azure.com
