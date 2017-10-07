---
title: aaaConfigure un agente de escucha ILB para grupos de disponibilidad AlwaysOn en Azure | Documentos de Microsoft
description: "Este tutorial usa recursos creados con el modelo de implementación clásica de Hola y crea una escucha del grupo de disponibilidad AlwaysOn en Azure que usa un equilibrador de carga interno."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a>Configuración de un agente de escucha ILB para grupos de disponibilidad AlwaysOn en Azure
> [!div class="op_single_selector"]
> * [Agente de escucha interno](../classic/ps-sql-int-listener.md)
> * [Agente de escucha externo](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a>Información general

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y el modelo clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo explica uso de Hola Hola clásico de modelo de implementación. Se recomienda el uso de modelo del Administrador de recursos de hello en implementaciones más nuevas.

tooconfigure un agente de escucha para un grupo de disponibilidad AlwaysOn en el modelo del Administrador de recursos de hello, consulte [configurar un equilibrador de carga para un grupo de disponibilidad AlwaysOn en Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

El grupo de disponibilidad puede contener réplicas que son solo locales, solo de Azure o abarcan ambas, locales y de Azure, para configuraciones híbridas. Réplicas de Azure pueden residir en hello misma región o en varias regiones que utilizan varias redes virtuales. Hello procedimientos de este artículo se supone que ya ha [configurado un grupo de disponibilidad](../classic/portal-sql-alwayson-availability-groups.md) pero aún no ha configurado un agente de escucha.

## <a name="guidelines-and-limitations-for-internal-listeners"></a>Instrucciones y limitaciones de los agentes de escucha internos
uso de Hola de un equilibrador de carga interno (ILB) con un agente de escucha del grupo de disponibilidad en Azure es toohello asunto siguientes instrucciones:

* agente de escucha del grupo de disponibilidad de Hola se admite en Windows Server 2008 R2, Windows Server 2012 y Windows Server 2012 R2.
* Sólo un agente de escucha del grupo de disponibilidad interna es compatible con los servicios de nube, porque el agente de escucha de hello es configurado toohello ILB, y no hay solo un ILB para cada servicio en la nube. Sin embargo, es posible toocreate varios agentes de escucha externos. Para más información, consulte [Configuración de un agente de escucha externo para grupos de disponibilidad AlwaysOn en Azure](../classic/ps-sql-ext-listener.md).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Determinar la accesibilidad de Hola de agente de escucha de Hola
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Este artículo se centra en la creación de un agente de escucha que usa un ILB. Si necesita un agente de escucha público o externo, busque la versión de Hola de este artículo que se describe la configuración de un [agente de escucha externo](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Creación de extremos de máquina virtual de carga equilibrada con Direct Server Return
Primero cree un ILB ejecutando script de Hola más adelante en esta sección.

Cree un punto de conexión de carga equilibrada para cada máquina virtual que hospeda una réplica de Azure. Si tiene réplicas en varias regiones, cada réplica para esa región debe estar en el mismo servicio en la nube de Hola Hola misma red virtual de Azure. La creación de réplicas de grupo de disponibilidad que abarcan varias regiones de Azure requiere configurar varias redes virtuales. Para obtener más información acerca de cómo configurar cross conectividad de red virtual, vea [configurar la conectividad de red de red virtual toovirtual](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. Hola portal de Azure, vaya tooeach máquina virtual que hospeda un detalles de réplica tooview Hola.

2. Haga clic en hello **extremos** pestaña para cada máquina virtual.

3. Compruebe que hello **nombre** y **puerto público** de punto de conexión de agente de escucha de Hola que desea toouse no están ya en uso. En el ejemplo de Hola en esta sección, se denomina hello *Miextremo*, y el puerto de hello es *1433*.

4. En el equipo local, descargue e instale hello más reciente [módulo de PowerShell](https://azure.microsoft.com/downloads/).

5. Inicie Azure PowerShell.  
    Se abre una nueva sesión de PowerShell, con hello Azure administrativos módulos cargados.

6. Ejecute `Get-AzurePublishSettingsFile`. Este cmdlet le dirigirá toodownload de explorador tooa un directorio local tooa del archivo de publicar la configuración. Puede que tenga que escribir las credenciales de inicio de sesión de la suscripción a Azure.

7. Ejecute hello siguiente `Import-AzurePublishSettingsFile` comando con la ruta de acceso de Hola de hello publicar el archivo de configuración que ha descargado:

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    Después de publicar Hola se importa el archivo de configuración, puede administrar su suscripción de Azure en la sesión de PowerShell de Hola.

8. En el *ILB*, asigne una dirección IP estática. Examine la configuración de red virtual actual de hello ejecutando Hola siguiente comando:

        (Get-AzureVNetConfig).XMLConfiguration
9. Hola Nota *subred* nombre de subred de Hola que contiene máquinas virtuales de Hola que hospedan réplicas de Hola. Este nombre se usa en el parámetro hello $SubnetName en script de Hola.

10. Hola Nota *VirtualNetworkSite* asigne un nombre y Hola a partir de *AddressPrefix* de subred de Hola que contiene máquinas virtuales de Hola que hospedan réplicas de Hola. Buscar una dirección IP disponible pasando ambos valores toohello `Test-AzureStaticVNetIP` comando y examinando hello *AvailableAddresses*. Por ejemplo, si hello red virtual se denomina *MyVNet* y tiene un intervalo de direcciones de subred que empieza a *172.16.0.128*, siguiente Hola comando haría una lista de direcciones disponibles:

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. Seleccione una de las direcciones disponibles de Hola y usarlo en el parámetro hello $ILBStaticIP del script de hello en el paso siguiente de Hola.

12. Copie Hola después de editor de texto de tooa de secuencia de comandos de PowerShell y configure toosuit de valores de las variables de hello su entorno. Se han proporcionado los valores predeterminados de algunos parámetros.  

    Las implementaciones existentes que usan grupos de afinidad no pueden agregar un ILB. Para más información sobre requisitos de ILB, consulte [Información general sobre el equilibrador de carga interno](../../../load-balancer/load-balancer-internal-overview.md).

    Además, si el grupo de disponibilidad abarca las regiones de Azure, debe ejecutar el script de Hola de una vez en cada centro de datos para el servicio de nube de Hola y nodos que residen en ese centro de datos.

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. Después de configurar las variables de hello, Hola copia escribirlo de hello texto editor tooyour PowerShell sesión toorun. Si el mensaje de Hola sigue mostrando  **>>** , presione ENTRAR de nuevo que la secuencia de comandos de hello toomake empieza a ejecutarse.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Comprobación de que KB2854082 está instalado si es necesario.
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Abrir los puertos de firewall de hello en los nodos de grupo de disponibilidad
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Crear Agente de escucha del grupo de disponibilidad de Hola

Crear Agente de escucha del grupo de disponibilidad de hello en dos pasos. En primer lugar, cree el recurso de clúster de punto de acceso de cliente de Hola y configure las dependencias. En segundo lugar, configure los recursos de clúster de hello en PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Crear punto de acceso de cliente de Hola y configurar las dependencias de clúster de Hola
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Configurar los recursos de clúster de hello en PowerShell
1. Para el ILB, debe usar la dirección IP de Hola de hello ILB que creó anteriormente. tooobtain esta dirección IP de direcciones en PowerShell, Hola de uso siguiente secuencia de comandos:

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. En una de las máquinas virtuales de hello, copie el script de PowerShell de hello para el editor de texto tooa de sistema operativo y, a continuación, establezca las variables de hello toohello los valores que anotó anteriormente.

    Para Windows Server 2012 o posterior, use Hola siguiente secuencia de comandos:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    Para Windows Server 2008 R2, utilice Hola siguiente secuencia de comandos:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. Una vez que las variables de hello establecidas, abra una ventana de Windows PowerShell con privilegios elevados, pegar Hola escribirlo desde el editor de texto hello en su toorun de sesión de PowerShell. Si el mensaje de Hola sigue mostrando  **>>** , presione ENTRAR nuevo toomake seguro de que el script de Hola empieza a ejecutarse.

4. Repita los pasos anteriores para cada máquina virtual de Hola.  
    Este script configura el recurso de dirección IP de hello con la dirección IP de hello del servicio de nube de Hola y configura otros parámetros, como puerto de sondeo de Hola. Cuando se conecta el recurso de dirección IP hello, puede responder toohello sondeo en el puerto de sondeo de Hola de extremo con equilibrio de carga de Hola que creó anteriormente.

## <a name="bring-hello-listener-online"></a>Ponga Hola el agente de escucha en línea
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Elementos de seguimiento
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a>Agente de escucha de grupo de disponibilidad de prueba hello (dentro Hola misma red virtual)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
