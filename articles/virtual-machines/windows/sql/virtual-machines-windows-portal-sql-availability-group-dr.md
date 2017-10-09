---
title: "Recuperación ante desastres de grupos de disponibilidad de servidor - máquinas virtuales de Azure - aaaSQL | Documentos de Microsoft"
description: "Este artículo explica cómo agrupar tooconfigure una disponibilidad de SQL Server en máquinas virtuales de Azure con una réplica en una región distinta."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a>Configuración de un grupo de disponibilidad AlwaysOn en máquinas virtuales de Azure en distintas regiones

Este artículo explica cómo tooconfigure una disponibilidad de SQL Server Always On grupo réplica en máquinas virtuales de Azure en una ubicación remota de Azure. Use esta recuperación ante desastres de toosupport de configuración.

En este artículo se aplica tooAzure máquinas virtuales en modo de administrador de recursos.

Hello siguiente imagen muestra una implementación común de un grupo de disponibilidad en máquinas virtuales de Azure:

   ![Grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

En esta implementación, todas las máquinas virtuales se encuentran en una única región de Azure. réplicas de grupo de disponibilidad de Hello pueden tener confirmación sincrónica con conmutación automática por error en SQL-1 y 2 de SQL. toobuild esta arquitectura, consulte [plantilla de grupo de disponibilidad o tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).

Esta arquitectura es vulnerable toodowntime si Hola región de Azure deja de estar accesible. tooovercome esta vulnerabilidad, agregar una réplica en una región distinta de Azure. Hello diagrama siguiente muestra el aspecto que tendría nueva arquitectura de hello:

   ![Recuperación ante desastres de grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

Hello diagrama anterior muestra una nueva máquina virtual denominada SQL-3. SQL-3 está en una región distinta de Azure. SQL-3 se agrega toohello clúster de conmutación por error de Windows Server. SQL-3 puede hospedar una réplica del grupo de disponibilidad. Por último, tenga en cuenta que hello región de Azure para SQL-3 tiene un nuevo equilibrador de carga de Azure.

>[!NOTE]
> Un conjunto de disponibilidad de Azure es necesario cuando más de una máquina virtual se encuentra en Hola la misma región. Si sólo hay una máquina virtual en la región de hello, conjunto de disponibilidad de hello no es necesario. Solo puede colocar una máquina virtual en un conjunto de disponibilidad en el momento de la creación. Si la máquina virtual de hello ya está en un conjunto de disponibilidad, puede agregar una máquina virtual para una réplica adicional más adelante.

En esta arquitectura, réplica de hello en región remoto hello normalmente está configurada con el modo de disponibilidad de confirmación asincrónica y el modo de conmutación por error manual.

Una vez que las réplicas del grupo de disponibilidad están en Azure Virtual Machines en diferentes regiones de Azure, cada región necesita:

* Una puerta de enlace de red virtual
* Una conexión de una puerta de enlace de red virtual

Hello diagrama siguiente muestra cómo se comunican las redes Hola entre centros de datos.

   ![Grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
>Esta arquitectura incurre en cargos por datos de salida para datos replicados entre regiones de Azure. Consulte [Detalles de precios de ancho de banda](http://azure.microsoft.com/pricing/details/bandwidth/).  

## <a name="create-remote-replica"></a>Creación de réplica remota

Hola toocreate una réplica en un centro de datos remoto, lo siguiente:

1. [Crear una red virtual en la nueva región de hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

1. [Configurar una conexión de red virtual a red virtual mediante Hola portal de Azure](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).

   >[!NOTE]
   >En algunos casos, puede tener conexión de red virtual a red virtual de toouse PowerShell toocreate Hola. Por ejemplo, si utiliza diferentes cuentas de Azure no puede configurar conexión de hello en el portal de Hola. Consulte en este caso, [configurar una red virtual a red de virtual de conexión mediante Hola portal de Azure](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

1. [Crear un controlador de dominio en la nueva región de hello](../../../active-directory/active-directory-new-forest-virtual-machine.md).

   Este controlador de dominio proporciona autenticación si el controlador de dominio de hello en el sitio primario de hello no está disponible.

1. [Crear una máquina virtual de SQL Server en la nueva región de hello](virtual-machines-windows-portal-sql-server-provision.md).

1. [Cree un equilibrador de carga de Azure en red de hello en la nueva región de hello](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

   Este equilibrador de carga debe:

   - Estar en Hola la misma red y subred como Hola nueva máquina virtual.
   - Tener una dirección IP estática para el agente de escucha del grupo de disponibilidad de Hola.
   - Incluir un grupo back-end que consta de solo máquinas virtuales de hello en Hola misma región como Hola equilibrador de carga.
   - Use una dirección IP de TCP puerto sondeo toohello específico.
   - Tener una regla específica toohello SQL Server en Hola de equilibrio de carga misma región.  

1. [Agregar toohello de característica de agrupación en clústeres de conmutación por error nuevo SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

1. [Unirse a dominio de hello nuevo SQL Server toohello](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

1. [Establecer una cuenta de dominio de hello nuevo SQL Server service cuenta toouse](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).

1. [Agregar toohello de SQL Server nuevo clúster de conmutación por error de Windows Server de hello](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).

1. Crear un recurso de dirección IP en clúster de Hola.

   Puede crear el recurso de dirección IP de hello en el Administrador de clústeres de conmutación por error. Haga clic en función de grupo de disponibilidad de hello, haga clic en **Agregar recurso**, **más recursos**y haga clic en **dirección IP**.

   ![Crear dirección IP](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   Configure esta dirección IP de la siguiente manera:

   - Usar la red de Hola desde el centro de datos remotos de Hola.
   - Asignar dirección IP de Hola Hola nuevo Azure equilibrador de carga. 

1. En Hola nuevo SQL Server en el Administrador de configuración de SQL Server, [habilitar grupos de disponibilidad AlwaysOn](http://msdn.microsoft.com/library/ff878259.aspx).

1. [Puertos de firewall abiertos en Hola nuevo SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

   números de puerto de Hello necesita tooopen dependerán del entorno. Puertos abiertos para hello Azure y punto de conexión de creación de reflejo de carga sondeo del equilibrador de mantenimiento.

1. [Agregar un grupo de disponibilidad de réplica toohello en hello nuevo SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).

   Para una réplica en una región remota de Azure, establézcala en replicación asincrónica con conmutación por error manual.  

1. Agregar recurso de dirección IP de hello como dependencia para el clúster de hello escucha cliente acceso punto (nombre de red).

   Hello captura de pantalla siguiente muestra un recurso de clúster de dirección IP configurado correctamente:

   ![Grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   >grupo de recursos de clúster de Hello incluye ambas direcciones IP. Ambas direcciones IP son las dependencias de punto de acceso de cliente de agente de escucha de Hola. Hola de uso **o** operador en la configuración de dependencia de clúster de Hola.

1. [Establecer parámetros de clúster de hello en PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).

Ejecutar script de PowerShell de hello con el nombre de red del clúster de hello, dirección IP y puerto de sondeo que configuró en el equilibrador de carga de hello en nueva región de Hola.

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a>Configuración de conexión para varias subredes

réplica de Hello en el centro de datos remoto hello forma parte del grupo de disponibilidad de Hola pero está en una subred diferente. Si esta réplica se convierte en la réplica principal de hello, pueden producirse los tiempos de espera de conexión de aplicación. Este comportamiento es Hola igual que un grupo de disponibilidad local en una implementación de varias subredes. tooallow conexiones desde aplicaciones de cliente, actualice la conexión de cliente de Hola o configurar la resolución de nombres de almacenamiento en caché en el recurso de nombre de red de clústeres de Hola.

Si es posible, actualice tooset de cadenas de conexión de cliente hello `MultiSubnetFailover=Yes`. Consulte [Conectarse a MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).

Si no se puede modificar las cadenas de conexión de hello, puede configurar la caché de resolución de nombres. Consulte [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/) (Tiempos de espera de conexión en un grupo de disponibilidad con varias subredes).

## <a name="fail-over-tooremote-region"></a>Conmutar por error tooremote región

tootest del agente de escucha conectividad toohello remoto región puede conmutar por región remota de hello réplica toohello. Aunque réplica hello es asincrónica, conmutación por error es vulnerable toopotential pérdida de datos. toofail sobre sin pérdida de datos, cambiar toosynchronous de modo de disponibilidad de Hola y establecer tooautomatic de modo de conmutación por error de Hola. Usar hello pasos:

1. En **Explorador de objetos**, conectar toohello instancia de SQL Server que hospeda la réplica principal de Hola.
1. En **Grupos de disponibilidad de AlwaysOn**, **Grupos de disponibilidad**, haga clic con el botón derecho en el grupo de disponibilidad y haga clic en **Propiedades**.
1. En hello **General** página, en **réplicas de disponibilidad**, conjunto Hola réplica secundaria en toouse de sitio de recuperación ante desastres de hello **confirmación sincrónica** modo de disponibilidad y **Automática** modo de conmutación por error.
1. Si tiene una réplica secundaria en el mismo sitio que la réplica principal para alta disponibilidad, establezca esta réplica demasiado**confirmación asincrónica** y **Manual**.
1. Haga clic en Aceptar.
1. En **Explorador de objetos**, haga clic en grupo de disponibilidad de Hola y haga clic en **Mostrar panel**.
1. En el panel de hello, compruebe que Hola se sincronice la réplica en el sitio de recuperación ante desastres de Hola.
1. En **Explorador de objetos**, haga clic en grupo de disponibilidad de Hola y haga clic en **conmutación por error...** . Estudios de administración de SQL Server se abre un asistente toofail sobre SQL Server.  
1. Haga clic en **siguiente**y seleccione Hola instancia de SQL Server en el sitio de recuperación ante desastres de Hola. Haga clic en **Siguiente** de nuevo.
1. Conectar toohello de instancia de SQL Server en el sitio de recuperación ante desastres de Hola y haga clic en **siguiente**.
1. En hello **resumen** página, compruebe la configuración de Hola y haga clic en **finalizar**.

Después de probar la conectividad, mover los datos principal de tooyour atrás de réplica principal de hello del centro y establecer modo de disponibilidad hello tootheir back-configuración de funcionamiento normal. Hello tabla siguiente muestra valores operativa normal de Hola para arquitectura de hello descrita en este documento:

| Ubicación | Instancia del servidor | Rol | Modo de disponibilidad | Modo de conmutación por error
| ----- | ----- | ----- | ----- | -----
| Centro de datos principal | SQL-1 | Principal | Sincrónico | Automático
| Centro de datos principal | SQL-2 | Secundario | Sincrónico | Automático
| Centro de datos secundario o remoto | SQL-3 | Secundario | Asincrónico | Manual


### <a name="more-information-about-planned-and-forced-manual-failover"></a>Más información acerca de la conmutación por error manual planeada y forzada

Para obtener más información, vea Hola temas siguientes:

- [Realizar una conmutación por error manual planeada de un grupo de disponibilidad (SQL Server)](http://msdn.microsoft.com/library/hh231018.aspx)
- [Realizar una conmutación por error manual forzada de un grupo de disponibilidad (SQL Server)](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a>Vínculos adicionales

* [Grupos de disponibilidad AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx)
* [Máquinas virtuales de Azure](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [Equilibradores de carga de Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [Conjuntos de disponibilidad de Azure](../manage-availability.md)
