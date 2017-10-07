---
title: aaaExtend HDInsight con la red Virtual - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse red Virtual de Azure tooconnect HDInsight tooother nube recursos o los recursos de su centro de datos"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a>Extender Azure HDInsight mediante una instancia de Azure Virtual Network

Obtenga información acerca de cómo toouse HDInsight con una [red Virtual de Azure](../virtual-network/virtual-networks-overview.md). El uso de una red Virtual de Azure permite Hola los escenarios siguientes:

* Conexión tooHDInsight directamente desde una red local.

* Conexión HDInsight toodata almacena en una red Virtual de Azure.

* Directamente Hola a Hadoop acceso a los servicios que no están disponibles públicamente en internet. Por ejemplo, las API de Kafka o hello API de Java de HBase.

> [!WARNING]
> información de Hello en este documento requiere una descripción de las redes TCP/IP. Si no está familiarizado con las redes TCP/IP, debe asociarse con alguien antes de efectuar modificaciones tooproduction redes.

## <a name="planning"></a>Planificación

siguiente Hola es preguntas de Hola que debe responder al planear tooinstall HDInsight en una red virtual:

* ¿Necesita tooinstall HDInsight en una red virtual existente? ¿O bien está creando una red nueva?

    Si usa una red virtual existente, deberá toomodify configuración de red de hello antes de poder instalar HDInsight. Para obtener más información, vea hello [agregar red virtual existente del tooan HDInsight](#existingvnet) sección.

* ¿Desea que contiene la red virtual de HDInsight tooanother red tooconnect Hola virtual o la red local?

    trabajo de tooeasily con los recursos a través de redes, que puede necesita toocreate un DNS personalizado y configurar el reenvío de DNS. Para obtener más información, vea hello [conectar varias redes](#multinet) sección.

* ¿Desea toorestrict/redirigir el tráfico entrante o saliente tooHDInsight?

    HDInsight debe tiene ilimitado comunicación con direcciones IP específicas en el centro de datos de Azure Hola. También hay varios puertos que deben permitirse a través de los firewalls para la comunicación del cliente. Para obtener más información, vea hello [controlar el tráfico de red](#networktraffic) sección.

## <a id="existingvnet"></a>Agregar la red virtual de HDInsight tooan existente

Usar pasos hello en esta sección toodiscover cómo tooadd un nuevo tooan de HDInsight existente de la red Virtual de Azure.

> [!NOTE]
> No se puede agregar un clúster de HDInsight existente a una red virtual.

1. ¿Está usando un clásico o el modelo de implementación del Administrador de recursos de red virtual de hello?

    HDInsight 3.4 y versiones posteriores requieren una red virtual de Resource Manager. Las versiones anteriores de HDInsight requieren una red virtual clásica.

    Si la red existente es una red virtual clásica, debe crear una red virtual del Administrador de recursos y, a continuación, conectarse Hola dos. [Conectar toonew de redes virtuales clásica redes virtuales](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

    Una vez admitido, HDInsight instalado en red de administrador de recursos de hello puede interactuar con los recursos de red clásicos Hola.

2. ¿Usa tunelización forzada? La tunelización forzada es una configuración de subred que fuerza la salida dispositivo tooa de tráfico de Internet para la inspección y el registro. HDInsight no es compatible con la tunelización forzada. Quite la tunelización forzada antes de instalar HDInsight en una subred, o bien cree una nueva subred para HDInsight.

3. ¿Usa grupos de seguridad de red, las rutas definidas por el usuario o el tráfico de los dispositivos de red Virtual toorestrict dentro o fuera de la red virtual de hello?

    Como un servicio administrado, HDInsight requiere un acceso sin restricciones tooseveral direcciones IP en el centro de datos de Azure Hola. comunicación tooallow con estas direcciones IP, actualice las rutas definidas por el usuario ni grupos de seguridad de red existentes.

    HDInsight hospeda varios servicios, que usan varios puertos. No bloquee el tráfico de los puertos toothese. Para obtener una lista de puertos tooallow a través de firewalls de dispositivo virtual, vea hello [seguridad](#security) sección.

    toofind la configuración de seguridad existente, Hola de uso después de los comandos de Azure PowerShell o CLI de Azure:

    * Grupos de seguridad de red

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        Para obtener más información, vea hello [solucionar problemas de grupos de seguridad de red](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) documento.

        > [!IMPORTANT]
        > Se aplican reglas de grupo de seguridad de red en orden según la prioridad de la regla. se aplica Hola primera regla que coincide con el patrón de tráfico de hello y no hay otras se aplican para que el tráfico. Reglas de orden de más permisivo tooleast permisivo. Para obtener más información, vea hello [filtrar el tráfico de red con grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md) documento.

    * Rutas definidas por el usuario

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        Para obtener más información, vea hello [solucionar problemas de rutas](../virtual-network/virtual-network-routes-troubleshoot-portal.md) documento.

4. Crear un clúster de HDInsight y seleccione Hola red Virtual de Azure durante la configuración. Siga los pasos de Hola Hola siguiendo el proceso de creación de documentos toounderstand Hola clúster:

    * [Crear HDInsight con hello portal de Azure](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [Creación de HDInsight con Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [Creación de HDInsight con la CLI de Azure 1.0](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [Creación de una instancia de HDInsight mediante el uso de una plantilla de Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > Agregar HDInsight tooa de red virtual es un paso de configuración opcional. Estar seguro de red virtual de tooselect Hola al configurar el clúster de Hola.

## <a id="multinet"></a>Conectar varias redes

mayor desafío de Hello con una configuración de la red es la resolución de nombres entre redes de Hola.

Azure proporciona resolución de nombres para los servicios de Azure instalados en una red virtual. Esta resolución de nombre integrado permite HDInsight tooconnect toohello después de recursos mediante un nombre de dominio completo (FQDN):

* Hola a cualquier recurso que está disponible en internet. Por ejemplo, microsoft.com, google.com.

* Cualquier recurso que está en Hola misma red Virtual de Azure, mediante el uso de hello __nombre DNS interno__ del recurso de Hola. Por ejemplo, cuando se utiliza la resolución de nombres predeterminado de hello, siguiente Hola es nodos de ejemplo internos DNS nombres tooHDInsight asignado trabajo:

    * wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net
    * wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net

    Estos dos nodos pueden comunicarse directamente entre sí y con otros nodos de HDInsight, mediante el uso de nombres DNS internos.

resolución de nombres predeterminado de Hello __no__ permitir HDInsight tooresolve nombres Hola de recursos en redes que están unidos a un toohello red virtual. Por ejemplo, es común toojoin toohello de red virtual de red local. Con solo Hola predeterminada resolución de nombres, HDInsight no puede acceder a recursos de red local de Hola por su nombre. Hola opuesto también es true, los recursos de la red local no pueden acceder a recursos de red virtual de Hola por su nombre.

> [!WARNING]
> Debe crear el servidor DNS personalizado de Hola y configurar hello toouse de red virtual, antes de crear Hola clúster de HDInsight.

resolución de nombres de tooenable entre la red virtual de Hola y recursos en redes combinadas, debe realizar Hola siguientes acciones:

1. Crear un servidor DNS personalizado en hello donde piensa tooinstall HDInsight de red Virtual de Azure.

2. Configurar el servidor DNS personalizado de hello red virtual toouse Hola.

3. Buscar hello que Azure asigna el sufijo DNS para la red virtual. Este valor es similar demasiado`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`. Para obtener información acerca de la búsqueda de sufijo DNS de hello, vea hello [ejemplo: DNS personalizada](#example-dns) sección.

4. Configure el enrutamiento entre los servidores DNS Hola. configuración de Hello depende de tipo hello de red remota.

    * Si la red remota hello es una red local, configure el DNS como sigue:
        
        * __DNS personalizado__ (en la red virtual de hello):

            * Reenviar solicitudes para el sufijo DNS de Hola de resolución de Azure recursiva de toohello Hola red virtual (168.63.129.16). Azure administra las solicitudes de recursos de red virtual de Hola

            * Reenviar todos los otros servidores DNS de local de toohello solicitudes. Hola local de DNS controla todas las demás solicitudes de resolución de nombre, incluso las solicitudes de recursos de internet, como Microsoft.com.

        * __DNS local__: reenvíe las solicitudes para hello red virtual DNS sufijo toohello servidor DNS personalizado. servidor DNS personalizado de Hello, a continuación, reenvía a toohello recursiva Azure resolución.

        Este solicitudes de configuración de las rutas de acceso completa nombres de dominio que contienen el sufijo DNS de Hola Hola virtual toohello personalizado DNS del servidor de red. Todas las demás solicitudes (incluso para las direcciones públicas de internet) se controlan mediante el servidor DNS de hello en local.

    * Si la red remota hello es otra red Virtual de Azure, configure DNS de la siguiente manera:

        * __DNS personalizado__ (en cada red virtual):

            * Las solicitudes para el sufijo DNS de Hola de redes virtuales Hola se reenvían toohello los servidores DNS personalizados. Hola DNS en cada red virtual es responsable de resolver recursos dentro de su red.

            * Reenviar otro de resolución de Azure recursiva toohello de solicitudes. resolución recursiva de Hello es responsable de resolver locales y recursos de internet.

        servidor DNS de Hola para cada red reenvía las solicitudes toohello otro, según el sufijo DNS. Otras solicitudes se resuelven mediante hello Azure recursiva solucionador.

    Para obtener un ejemplo de cada configuración, vea hello [ejemplo: DNS personalizada](#example-dns) sección.

Para obtener más información, vea hello [resolución de nombres para las máquinas virtuales e instancias de rol](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) documento.

## <a name="directly-connect-toohadoop-services"></a>Conectar directamente tooHadoop services

Documentación mayoría en HDInsight se da por supuesto que tiene acceso toohello clúster sobre Hola internet. Por ejemplo, que se puede conectar el clúster de toohello en https://CLUSTERNAME.azurehdinsight.net. Esta dirección utiliza la puerta de enlace pública hello, que no está disponible si ha usado NSG u Hola a UDRs toorestrict acceso desde internet.

tooconnect tooAmbari y otras páginas web a través de la red virtual de hello, utilice Hola pasos:

1. nombres de dominio completo interno hello toodiscover (FQDN) de nodos de clúster de HDInsight de hello, use uno de los siguientes métodos de hello:

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

    En lista de Hola de nodos devueltos, busque Hola FQDN de Hola nodos principales y usar Hola FQDN tooconnect tooAmbari y otros servicios web. Por ejemplo, utilice `http://<headnode-fqdn>:8080` tooaccess Ambari.

    > [!IMPORTANT]
    > Algunos servicios hospedados en nodos principales Hola sólo están activas en un nodo a la vez. Si intenta obtener acceso a un servicio en un nodo principal y devuelve un error 404, cambie toohello otro nodo principal.

2. nodo de hello toodetermine y el puerto que un servicio está disponible en, vea hello [puertos utilizados por los servicios de Hadoop en HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.

## <a id="networktraffic"></a> Control del tráfico de red

Tráfico de red en un redes virtuales de Azure puede controlarse mediante Hola siguientes métodos:

* **Grupos de seguridad de red** (NSG) le permiten red toohello de toofilter tráfico entrante y saliente. Para obtener más información, vea hello [filtrar el tráfico de red con grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md) documento.

    > [!WARNING]
    > HDInsight no admite la restricción de tráfico saliente.

* **Las rutas definidas por el usuario** (UDR) definen cómo fluye el tráfico entre los recursos de red de Hola. Para obtener más información, vea hello [rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md) documento.

* **Red aparatos virtuales** replicar la funcionalidad de Hola de dispositivos como los enrutadores y firewalls. Para obtener más información, vea hello [dispositivos de red](https://azure.microsoft.com/solutions/network-appliances) documento.

Como un servicio administrado, HDInsight requiere los servicios de administración y mantenimiento de tooAzure acceso sin restricciones en hello nube de Azure. Al usar NSG y UDR, debe asegurarse de que estos servicios pueden seguir comunicándose con HDInsight.

HDInsight expone servicios en varios puertos. Cuando se utiliza un servidor de seguridad de dispositivo virtual, debe permitir el tráfico en hello puertos utilizados para estos servicios. Para obtener más información, vea la sección de hello [puertos necesarios].

### <a id="hdinsight-ip"></a> HDInsight con grupos de seguridad de red y rutas definidas por el usuario

Si planea usar **grupos de seguridad de red** o **rutas definidas por el usuario** toocontrol el tráfico de red, lleve a cabo Hola siguientes acciones antes de instalar HDInsight:

1. Identificar Hola región de Azure que piensa toouse para HDInsight.

2. Identificar las direcciones IP Hola requeridas HDInsight. Para obtener más información, vea hello [direcciones IP requiere HDInsight](#hdinsight-ip) sección.

3. Crear o modificar grupos de seguridad de red de Hola o rutas definidas por el usuario para la subred de Hola que planea tooinstall HDInsight en.

    * __Grupos de seguridad de red__: permitir __entrada__ tráfico en el puerto __443__ desde direcciones IP de Hola.
    * __Las rutas definidas por el usuario__: crear una ruta de dirección IP tooeach y establecer hello __tipo de salto siguiente__ too__Internet__.

Para obtener más información sobre grupos de seguridad de red o rutas definidas por el usuario, vea Hola siguiente documentación:

* [Grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md)

* [Rutas definidas por el usuario](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a>Tunelización forzada

La tunelización forzada es una configuración de enrutamiento definidas por el usuario donde todo el tráfico de subred es específicas de tooa forzada de red o ubicación, por ejemplo, la red local. HDInsight __no__ es compatible con la tunelización forzada.

## <a id="hdinsight-ip"></a> Direcciones IP necesarias

> [!IMPORTANT]
> Hola mantenimiento de Azure y los servicios de administración deben ser capaz de toocommunicate con HDInsight. Si utiliza grupos de seguridad de red o rutas definidas por el usuario, permitir el tráfico de hello direcciones IP para estos tooreach de servicios HDInsight.
>
> Si no utiliza grupos de seguridad de red o el tráfico de toocontrol de rutas definidas por el usuario, puede omitir esta sección.

Si utiliza grupos de seguridad de red o rutas definidas por el usuario, debe permitir el tráfico de hello mantenimiento de Azure y servicios de administración tooreach HDInsight. Usar hello después de direcciones IP de Hola de toofind de pasos que deben permitirse:

1. Siempre debe permitir el tráfico de hello después de direcciones IP:

    | Dirección IP | Puerto permitido | Dirección |
    | ---- | ----- | ----- |
    | 168.61.49.99 | 443 | Entrada |
    | 23.99.5.239 | 443 | Entrada |
    | 168.61.48.131 | 443 | Entrada |
    | 138.91.141.162 | 443 | Entrada |

2. A continuación, si el clúster de HDInsight está en uno de hello siguiendo las regiones, debe permitir el tráfico desde direcciones IP de hello enumerados para la región de hello:

    > [!IMPORTANT]
    > Si no aparece Hola región de Azure que está usando, use únicamente cuatro direcciones IP Hola del paso 1.

    | País | Region | Direcciones IP permitidas | Puerto permitido | Dirección |
    | ---- | ---- | ---- | ---- | ----- |
    | Asia | Asia oriental | 23.102.235.122</br>52.175.38.134 | 443 | Entrada |
    | &nbsp; | Sudeste asiático | 13.76.245.160</br>13.76.136.249 | 443 | Entrada |
    | Australia | Australia Oriental | 104.210.84.115</br>13.75.152.195 | 443 | Entrada |
    | &nbsp; | Sudeste de Australia | 13.77.2.56</br>13.77.2.94 | 443 | Entrada |
    | Brasil | Sur de Brasil | 191.235.84.104</br>191.235.87.113 | 443 | Entrada |
    | Canadá | Este de Canadá | 52.229.127.96</br>52.229.123.172 | 443 | Entrada |
    | &nbsp; | Centro de Canadá | 52.228.37.66</br>52.228.45.222 | 443 | Entrada |
    | China | Norte de China | 42.159.96.170</br>139.217.2.219 | 443 | Entrada |
    | &nbsp; | Este de China | 42.159.198.178</br>42.159.234.157 | 443 | Entrada |
    | Europa | Europa del Norte | 52.164.210.96</br>13.74.153.132 | 443 | Entrada |
    | &nbsp; | Europa occidental| 52.166.243.90</br>52.174.36.244 | 443 | Entrada |
    | Alemania | Centro de Alemania | 51.4.146.68</br>51.4.146.80 | 443 | Entrada |
    | &nbsp; | Noreste de Alemania | 51.5.150.132</br>51.5.144.101 | 443 | Entrada |
    | India | India Central | 52.172.153.209</br>52.172.152.49 | 443 | Entrada |
    | Japón | Este de Japón | 13.78.125.90</br>13.78.89.60 | 443 | Entrada |
    | &nbsp; | Oeste de Japón | 40.74.125.69</br>138.91.29.150 | 443 | Entrada |
    | Corea | Corea Central | 52.231.39.142</br>52.231.36.209 | 433 | Entrada |
    | &nbsp; | Corea del Sur | 52.231.203.16</br>52.231.205.214 | 443 | Entrada
    | Reino Unido | Oeste de Reino Unido | 51.141.13.110</br>51.141.7.20 | 443 | Entrada |
    | &nbsp; | Sur del Reino Unido 2 | 51.140.47.39</br>51.140.52.16 | 443 | Entrada |
    | Estados Unidos | Central EE. UU.: | 13.67.223.215</br>40.86.83.253 | 443 | Entrada |
    | &nbsp; | Centro-Norte de EE. UU | 157.56.8.38</br>157.55.213.99 | 443 | Entrada |
    | &nbsp; | Centro occidental de EE.UU. | 52.161.23.15</br>52.161.10.167 | 443 | Entrada |
    | &nbsp; | Oeste de EE. UU. 2 | 52.175.211.210</br>52.175.222.222 | 443 | Entrada |

    Para obtener información acerca de hello IP direcciones toouse para administración pública de Azure, vea hello [inteligencia de gobierno Azure + análisis](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) documento.

3. Si usa un servidor DNS personalizado con la red virtual, también debe permitir el acceso desde __168.63.129.16__. Esta es la dirección de la resolución recursiva de Azure. Para obtener más información, vea hello [la resolución de nombres para máquinas virtuales y rol instancias](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) documento.

Para obtener más información, vea hello [controlar el tráfico de red](#networktraffic) sección.

## <a id="hdinsight-ports"></a> Puertos necesarios

Si planea usar una red **firewall del dispositivo virtual** toosecure red virtual de hello, debe permitir el tráfico saliente en hello siguientes puertos:

* 53
* 443
* 1433
* 11000-11999
* 14000-14999

Para obtener una lista de puertos para servicios específicos, vea hello [puertos utilizados por los servicios de Hadoop en HDInsight](hdinsight-hadoop-port-settings-for-services.md) documento.

Para obtener más información sobre las reglas de firewall para aparatos virtuales, vea hello [escenario de dispositivo virtual](../virtual-network/virtual-network-scenario-udr-gw-nva.md) documento.

## <a id="hdinsight-nsg"></a>Ejemplo: grupos de seguridad de red con HDInsight

ejemplos de Hello en esta sección muestra cómo el grupo de seguridad de red de toocreate reglas que permiten el toocommunicate de HDInsight con hello servicios de administración de Azure. Antes de usar los ejemplos de hello, ajustar Hola IP direcciones toomatch hello las para hello región de Azure que está utilizando. Puede encontrar esta información en hello [HDInsight con grupos de seguridad de red y las rutas definidas por el usuario](#hdinsight-ip) sección.

### <a name="azure-resource-management-template"></a>Plantilla de administración de recursos de Azure

Hello siguiente plantilla de administración de recursos crea una red virtual que restringe el tráfico entrante, pero permite el tráfico de direcciones IP de hello requerido HDInsight. Esta plantilla crea también un clúster de HDInsight en la red virtual de Hola.

* [Implementar una instancia segura de Azure Virtual Network y un clúster de Hadoop de HDInsight](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> Cambiar las direcciones IP de hello usa este Hola de toomatch ejemplo región de Azure que está utilizando. Puede encontrar esta información en hello [HDInsight con grupos de seguridad de red y las rutas definidas por el usuario](#hdinsight-ip) sección.

### <a name="azure-powershell"></a>Azure PowerShell

Usar hello después toocreate de secuencia de comandos de PowerShell una red virtual que restringe el tráfico entrante y permite el tráfico desde Hola direcciones IP para la región de Europa del Norte Hola.

> [!IMPORTANT]
> Cambiar las direcciones IP de hello usa este Hola de toomatch ejemplo región de Azure que está utilizando. Puede encontrar esta información en hello [HDInsight con grupos de seguridad de red y las rutas definidas por el usuario](#hdinsight-ip) sección.

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> En este ejemplo se muestra cómo tooadd reglas tooallow el tráfico en direcciones IP de hello necesario. No contiene una regla toorestrict acceso de otros orígenes de entrada.
>
> Hola siguiente ejemplo muestra cómo tener acceso tooenable SSH de hello Internet:
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a>CLI de Azure

Usar hello siguiendo los pasos toocreate una red virtual que restringe el tráfico entrante, pero permite el tráfico de direcciones IP de hello requerido HDInsight.

1. Hola de uso después toocreate comando un nuevo grupo de seguridad de red denominado `hdisecure`. Reemplace **RESOURCEGROUPNAME** con grupo de recursos de Hola que contiene Hola red Virtual de Azure. Reemplace **ubicación** con ubicación hello (región) se creó ese grupo hello en.

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    Una vez que se ha creado el grupo de hello, recibirá información sobre el nuevo grupo de Hola.

2. Usar hello después tooadd reglas toohello nuevo grupo de seguridad red que permiten la comunicación entrante en el puerto 443 de hello servicio de mantenimiento y administración de HDInsight de Azure. Reemplace **RESOURCEGROUPNAME** con el nombre de Hola Hola del grupo de recursos que contiene Hola red Virtual de Azure.

    > [!IMPORTANT]
    > Cambiar las direcciones IP de hello usa este Hola de toomatch ejemplo región de Azure que está utilizando. Puede encontrar esta información en hello [HDInsight con grupos de seguridad de red y las rutas definidas por el usuario](#hdinsight-ip) sección.

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. tooretrieve Hola identificador único para este grupo de seguridad de red, use Hola siguiente comando:

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    Este comando devuelve un toohello similar valor siguiente texto:

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    Utilice comillas dobles alrededor de Id. en comando hello si no obtiene resultados Hola esperado.

4. Usar hello después de la subred de tooa del grupo de seguridad de comando tooapply Hola red. Reemplace hello __GUID__ y __RESOURCEGROUPNAME__ valores con hello las devuelven desde el paso anterior de Hola. Reemplace __VNETNAME__ y __SUBNETNAME__ con nombre de red virtual de Hola y el nombre de subred que desea toocreate.

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    Una vez completado este comando, puede instalar HDInsight en hello red Virtual.

> [!IMPORTANT]
> Estos pasos solo abren toohello HDInsight mantenimiento y administración de servicio de acceso a Hola nube de Azure. Cualquier otro acceso toohello clúster de HDInsight de hello exterior red Virtual está bloqueada. tooenable acceso de red virtual externa hello, debe agregar reglas de grupo de seguridad de red adicionales.
>
> Hola siguiente ejemplo muestra cómo tener acceso tooenable SSH de hello Internet:
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <a id="example-dns"></a> Ejemplo: configuración de DNS

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a>Resolución de nombres entre una red virtual y una red local conectada

En este ejemplo realiza Hola siguientes supuestos:

* Dispone de una red Virtual de Azure que es la red local de tooan conectados mediante una puerta de enlace VPN.

* servidor DNS personalizado de Hello en red virtual de Hola ejecuta Linux o Unix como sistema operativo de Hola.

* [Enlazar](https://www.isc.org/downloads/bind/) está instalado en el servidor DNS personalizado Hola.

En servidor DNS personalizado de hello en la red virtual de hello:

1. Usar Azure PowerShell o CLI de Azure toofind Hola sufijo DNS de red virtual de hello:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. En el servidor DNS personalizado de hello para la red virtual de hello, usar hello después de texto como contenido de Hola de hello `/etc/bind/named.conf.local` archivo:

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    Reemplace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valor con el sufijo DNS de saludo de la red virtual.

    Esta configuración enruta todas las solicitudes DNS para el sufijo DNS de Hola de resolución de hello red virtual toohello recursiva de Azure.

2. En el servidor DNS personalizado de hello para la red virtual de hello, usar hello después de texto como contenido de Hola de hello `/etc/bind/named.conf.options` archivo:

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Reemplace hello `10.0.0.0/16` valor con el intervalo de direcciones IP de hello de la red virtual. Esta entrada permite direcciones de solicitudes de resolución de nombres dentro de este intervalo.

    * Agregar intervalo de direcciones IP de Hola de hello local red toohello `acl goodclients { ... }` sección.  entrada permite las solicitudes de resolución de nombres de los recursos de red local de Hola.
    
    * Reemplace el valor de hello `192.168.0.1` con la dirección IP de saludo del servidor DNS local. Esta entrada enruta todos los demás DNS solicitudes toohello en servidor DNS local.

3. configuración de hello toouse, reinicie el enlace. Por ejemplo: `sudo service bind9 restart`.

4. Agregar un servidor DNS de reenviador condicional toohello local. Configurar solicitudes de toosend de reenviador condicional de hello para el sufijo DNS de Hola de servidor DNS de paso 1 toohello personalizado.

    > [!NOTE]
    > Consulte la documentación de hello para el software DNS para obtener información específica acerca de cómo tooadd un reenviador condicional.

Después de completar estos pasos, puede conectarse tooresources en cualquier red mediante nombres de dominio completo (FQDN). Ahora puede instalar HDInsight en la red virtual de Hola.

### <a name="name-resolution-between-two-connected-virtual-networks"></a>Resolución de nombres entre dos redes virtuales conectadas

En este ejemplo realiza Hola siguientes supuestos:

* Tiene dos instancias de Azure Virtual Network que se conectan mediante una puerta de enlace de VPN o un emparejamiento.

* servidor DNS personalizado de Hello en ambas redes ejecuta Linux o Unix como sistema operativo de Hola.

* [Enlazar](https://www.isc.org/downloads/bind/) está instalado en los servidores DNS personalizados Hola.

1. Usar Azure PowerShell o CLI de Azure toofind Hola sufijo DNS de ambas redes virtuales:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Hola de uso después de texto como contenido de Hola de hello `/etc/bind/named.config.local` archivo en el servidor DNS personalizado de Hola. Realice este cambio en el servidor DNS personalizado de hello en ambas redes virtuales.

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    Reemplace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valor con el sufijo DNS de Hola de hello __otros__ red virtual. Esta entrada enruta las solicitudes para el sufijo DNS de Hola de hello red remota toohello DNS personalizado en esa red.

3. En servidores DNS personalizados de hello en ambas redes virtuales, usar hello después de texto como contenido de Hola de hello `/etc/bind/named.conf.options` archivo:

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Reemplace hello `10.0.0.0/16` y `10.1.0.0/16` valores con la dirección IP de hello intervalos de las redes virtuales de direcciones. Esta entrada permite a los recursos de cada red toomake solicitudes de los servidores DNS de Hola.

    Resolución de hello Azure recursiva administra las solicitudes que no son para los sufijos DNS Hola de redes virtuales de hello (por ejemplo, microsoft.com).

4. configuración de hello toouse, reinicie el enlace. Por ejemplo, `sudo service bind9 restart` en ambos servidores DNS.

Después de completar estos pasos, puede conectarse tooresources en red virtual de hello con nombres de dominio completo (FQDN). Ahora puede instalar HDInsight en la red virtual de Hola.

## <a name="next-steps"></a>Pasos siguientes

* Para obtener un ejemplo de extremo a extremo de la configuración de red de HDInsight tooconnect tooan locales, consulte [red local de conectar HDInsight tooan](./connect-on-premises-network.md).

* Para obtener más información sobre redes virtuales de Azure, vea hello [información general de la red Virtual de Azure](../virtual-network/virtual-networks-overview.md).

* Para más información sobre los grupos de seguridad de red, vea [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).

* Para más información sobre las rutas definidas por el usuario, vea [Rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md).