---
title: aaaConfigure un agente de escucha externo para grupos de disponibilidad AlwaysOn | Documentos de Microsoft
description: "Este tutorial le guía a través de los pasos necesarios para crear una siempre en disponibilidad escucha de grupo en Azure que sea accesible desde el exterior mediante Hola dirección IP Virtual pública de Hola servicio en la nube asociado."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a>Configuración de un agente de escucha externo para grupos de disponibilidad AlwaysOn en Azure
> [!div class="op_single_selector"]
> * [Agente de escucha interno](../classic/ps-sql-int-listener.md)
> * [Agente de escucha externo](../classic/ps-sql-ext-listener.md)
> 
> 

Este tema muestra cómo Hola a tooconfigure un agente de escucha para un grupo de disponibilidad AlwaysOn externamente accesible a través de internet. Esto se consigue mediante la asociación del servicio de nube de hello **IP Virtual pública (VIP)** dirección con el agente de escucha de Hola.

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

El grupo de disponibilidad puede contener réplicas que son solo locales, solo de Azure o abarcan ambas, locales y de Azure, para configuraciones híbridas. Réplicas de Azure pueden residir en hello misma región o en varias regiones mediante varias redes virtuales (redes virtuales). Hola siguiente da por sentado que ya está [configurado un grupo de disponibilidad](../classic/portal-sql-alwayson-availability-groups.md) pero no se ha configurado un agente de escucha.

## <a name="guidelines-and-limitations-for-external-listeners"></a>Instrucciones y limitaciones de los agentes de escucha externos
Tenga en cuenta las siguientes directrices acerca de agente de escucha del grupo de disponibilidad de hello en Azure cuando se va a implementar con dirección Hola de púbica de servicio de nube VIP de hello:

* agente de escucha del grupo de disponibilidad de Hola se admite en Windows Server 2008 R2, Windows Server 2012 y Windows Server 2012 R2.
* aplicación de cliente de Hello debe residir en un servicio de nube diferente Hola uno que contiene la máquina virtual del grupo de disponibilidad. Azure no admite direct server devolver con el cliente y el servidor en hello mismo servicio en la nube.
* De forma predeterminada, los pasos de hello en este artículo muestran cómo hello toouse de tooconfigure un agente de escucha en la nube de dirección IP Virtual (VIP) del servicio. Sin embargo, es posible tooreserve y crear varias direcciones de VIP para su servicio en la nube. Esto le permite toouse pasos de hello en este toocreate artículo varios agentes de escucha que se asociada a una VIP diferente. Para obtener información sobre cómo toocreate varias direcciones VIP, consulte [varias VIP por cada servicio de nube](../../../load-balancer/load-balancer-multivip.md).
* Si va a crear un agente de escucha para un entorno híbrido, red de hello local debe tener conectividad toohello Internet pública en suma toohello VPN de sitio a sitio con hello red virtual de Azure. En la subred de Azure hello, agente de escucha del grupo de disponibilidad de hello solo está disponible con dirección IP pública de hello del servicio en nube respectivos Hola.
* No se admite un agente de escucha externo en hello mismo servicio en la nube que también tiene un agente de escucha interno mediante toocreate Hola equilibrador de carga interno (ILB).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Determinar la accesibilidad de Hola de agente de escucha de Hola
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Este artículo se centra en la creación de un agente de escucha que usa **equilibrio de carga externo**. Si desea que un agente de escucha de red virtual privada tooyour, busque la versión de Hola de este artículo que proporciona los pasos necesarios para configurar un [agente de escucha con ILB](../classic/ps-sql-int-listener.md)

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Creación de extremos de máquina virtual de carga equilibrada con Direct Server Return
Equilibrio de carga externo utiliza la dirección IP Virtual Hola Hola virtual pública del servicio de nube de Hola que hospeda las máquinas virtuales. Por lo que no necesita toocreate o configure el equilibrador de carga de hello en este caso.

Tienes que crear un extremo de carga equilibrada para cada máquina virtual que hospeda una réplica de Azure. Si tiene réplicas en varias regiones, cada réplica para esa región debe estar en el mismo servicio en la nube de Hola Hola misma red virtual. La creación de réplicas de grupo de disponibilidad que abarcan varias regiones de Azure, requiere configurar varias redes virtuales. Para obtener más información acerca de cómo configurar la conectividad entre redes virtuales, vea [tooVNet conectividad de red virtual configurar](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. Hola portal de Azure, navegue tooeach máquina virtual que hospede una réplica y ver los detalles de Hola.
2. Haga clic en hello **extremos** pestaña para cada una de las máquinas virtuales de Hola.
3. Compruebe que hello **nombre** y **puerto público** de punto de conexión de agente de escucha de hello desea toouse no está ya en uso. En el siguiente ejemplo de Hola, nombre de hello es "MyEndpoint" y puerto de hello es "1433".
4. En el equipo local, descargue e instale [módulo más reciente de PowerShell de hello](https://azure.microsoft.com/downloads/).
5. Inicie **Azure PowerShell**. Un PowerShell nueva sesión se abre con Hola módulos administrativos de Azure cargados.
6. Ejecuta **Get-AzurePublishSettingsFile**. Este cmdlet le dirigirá toodownload de explorador tooa un directorio local tooa del archivo de publicar la configuración. Puede que tengas que escribir las credenciales de inicio de sesión de tu suscripción a Azure.
7. Ejecute hello **importación-AzurePublishSettingsFile** comando con la ruta de acceso de Hola de hello publicar el archivo de configuración que ha descargado:
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    Una vez que publique Hola se importa el archivo de configuración, puede administrar su suscripción de Azure en la sesión de PowerShell de Hola.
    
1. Copie el siguiente script de PowerShell de hello en un editor de texto y establecer toosuit de valores de las variables de hello en su entorno (han proporcionado los valores predeterminados para algunos parámetros). Tenga en cuenta que si el grupo de disponibilidad abarca las regiones de Azure, debe ejecutar el script de Hola una vez en cada centro de datos para el servicio de nube de Hola y nodos que residen en ese centro de datos.
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. Una vez configuradas las variables de hello, Hola copia escribirlo desde el editor de texto hello en su toorun de sesión de PowerShell de Azure. Si el mensaje de Hola sigue mostrando >>, escriba ENTRAR de nuevo script de Hola seguro toomake empieza a ejecutarse.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Comprobación de que KB2854082 está instalado si es necesario.
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Abrir los puertos de firewall de hello en los nodos de grupo de disponibilidad
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Crear Agente de escucha del grupo de disponibilidad de Hola

Crear Agente de escucha del grupo de disponibilidad de hello en dos pasos. En primer lugar, cree el recurso de clúster de punto de acceso de cliente de Hola y configure las dependencias. En segundo lugar, configure los recursos de clúster de hello con PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Crear punto de acceso de cliente de Hola y configurar las dependencias de clúster de Hola
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Configurar los recursos de clúster de hello en PowerShell
1. Para el equilibrio de carga externo, debe obtener la dirección IP virtual pública del saludo del servicio de nube de Hola que contiene sus réplicas. Inicie sesión en hello portal de Azure. Navegue toohello servicio en la nube que contiene el máquina virtual del grupo de disponibilidad. Abra hello **panel** vista.
2. Tenga en cuenta dirección Hola se muestra en **dirección IP Virtual pública (VIP)**. Si la solución abarca redes virtuales, repita este paso para cada servicio en la nube que contenga una máquina virtual que hospeda una réplica.
3. En una de las máquinas virtuales de hello, copie Hola script de PowerShell siguiente en un editor de texto y establecer variables de hello toohello los valores que anotó anteriormente.
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. Una vez se han establecido las variables de hello, abra una ventana de Windows PowerShell con privilegios elevados, a continuación, copie el script de Hola Hola editor de texto y péguelo en su toorun de sesión de PowerShell de Azure. Si el mensaje de Hola sigue mostrando >>, escriba ENTRAR de nuevo script de Hola seguro toomake empieza a ejecutarse.
5. Repita este paso en cada máquina virtual. Este script configura el recurso de dirección IP de hello con la dirección IP de hello del servicio de nube de Hola y configura otros parámetros como puerto de sondeo de Hola. Cuando Hola recurso de dirección IP se pone en línea, a continuación, puede responder toohello sondeo en el puerto de sondeo de Hola desde el extremo de equilibrio de carga de hello creado anteriormente en este tutorial.

## <a name="bring-hello-listener-online"></a>Ponga Hola el agente de escucha en línea
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Elementos de seguimiento
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a>Agente de escucha de grupo de disponibilidad de prueba hello (dentro Hola misma red virtual)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a>Agente de escucha de grupo de disponibilidad de prueba hello (sobre Hola internet)
En orden tooaccess Hola agente de escucha de red virtual externa hello, debe contar con equilibrio de carga de público/externo (que se describe en este tema) en lugar de ILB, que es solo es accesible dentro de hello misma red virtual. En la cadena de conexión de hello, especificar nombre de servicio de nube de Hola. Por ejemplo, si tiene un servicio en la nube con el nombre de hello *mycloudservice*, instrucción de hello sqlcmd sería como sigue:

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

A diferencia del ejemplo anterior de hello, debe usar autenticación de SQL, porque el llamador de hello no puede usar la autenticación de windows a través de Hola internet. Para más información, consulte [Always On Availability Group in Azure VM: Client Connectivity Scenarios](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx)(Grupo de disponibilidad AlwaysOn en la máquina virtual de Azure: escenarios de conectividad de cliente). Al utilizar la autenticación de SQL, asegúrese de que crea Hola mismo inicio de sesión tanto en las réplicas. Para obtener más información acerca de cómo solucionar los inicios de sesión con grupos de disponibilidad, consulte [cómo toomap inicios de sesión o use contenidos SQL réplicas de tooother tooconnect de usuario de base de datos y asignar las bases de datos de tooavailability](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx).

Si Hola siempre en las réplicas están en subredes diferentes, los clientes deberán especificar **MultisubnetFailover = True** en la cadena de conexión de Hola. Esto da como resultado tooreplicas de intentos de conexión paralelos en subredes diferentes Hola. Tenga en cuenta que este escenario incluye una implementación de grupo de disponibilidad AlwaysOn entre regiones.

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

