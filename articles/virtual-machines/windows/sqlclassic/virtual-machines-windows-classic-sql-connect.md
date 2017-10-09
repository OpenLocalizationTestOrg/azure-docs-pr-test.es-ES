---
title: "aaaConnect tooa Máquina Virtual de SQL Server en Azure (clásica) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconnect tooSQL Server ejecuta en una máquina Virtual en Azure. En este tema usa el modelo de implementación clásica de Hola. escenarios de Hello varían según la configuración de red de Hola y la ubicación de hello del cliente de Hola."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 4fff3936ad0bcfd3a56855a8436991e19b92522b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a>Conectar tooa Máquina Virtual de SQL Server en Azure (implementación clásico)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-connect.md)
> * [Clásico](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Información general
Este tema describe cómo tooconnect tooyour SQL Server instancia ejecuta en una máquina virtual de Azure. En él se describen algunos [escenarios de conectividad generales](#connection-scenarios) y se proporcionan los [pasos detallados para configurar la conectividad de SQL Server en una máquina virtual de Azure](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Si está usando máquinas virtuales de administrador de recursos, consulte [conectar tooa Máquina Virtual de SQL Server en Azure mediante el Administrador de recursos](../sql/virtual-machines-windows-sql-connect.md).

## <a name="connection-scenarios"></a>Escenarios de conexión
forma de Hello un cliente conecta tooSQL servidor se ejecuta en una máquina Virtual depende de la ubicación de Hola de cliente hello y configuración de la máquina/red de Hola. Entre los escenarios se incluyen los siguientes:

* [Conectar tooSQL Server Hola mismo servicio en la nube](#connect-to-sql-server-in-the-same-cloud-service)
* [Conectar tooSQL Server a través de hello internet](#connect-to-sql-server-over-the-internet)
* [Conectar tooSQL Server Hola misma red virtual](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> Antes de conectar con cualquiera de estos métodos, debe seguir hello [los pasos de esta conectividad de tooconfigure artículo](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a>Conectar tooSQL Server Hola mismo servicio en la nube
Varias máquinas virtuales pueden crearse en hello mismo servicio en la nube. toounderstand virtual este escenario, los equipos vea [cómo tooconnect las máquinas virtuales con un servicio de red o en la nube virtual](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service). Este escenario es cuando un cliente en una máquina virtual intenta tooconnect tooSQL servidor que se ejecuta en otra máquina virtual en hello mismo servicio en la nube.

En este escenario, se puede conectar con hello VM **nombre** (también se muestra como **nombre_equipo** o **hostname** en el portal de hello). Se trata de nombre hello proporcionada para hello VM durante la creación. Por ejemplo, si se denomina la VM de SQL **mysqlvm**, un cliente de la máquina virtual en hello podría utilizar el mismo servicio en la nube Hola después tooconnect de cadena de conexión:

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a>Conectar tooSQL Server a través de Internet de Hola
Si desea que tooconnect tooyour el motor de base de datos de SQL Server de hello Internet, debe crear un punto de conexión de máquina virtual para la comunicación TCP entrante. Este paso de configuración de Azure, dirige TCP puerto tráfico tooa el puerto TCP entrante que es un equipo virtual toohello accesible.

Hola a tooconnect a través de internet, debe usar DNS hello y nombre de VM extremo número de puerto la máquina virtual de hello (configurado más adelante en este artículo). Hola toofind nombre DNS, vaya toohello Azure portal y, a continuación, seleccione **máquinas virtuales (clásicas)**. Después, seleccione la máquina virtual. Hola **nombre DNS** se muestra en hello **Introducción** sección.

Por ejemplo, piense en una máquina virtual clásica denominada **mysqlvm** con un nombre DNS de **mysqlvm7777.cloudapp.net** y un punto de conexión de la máquina virtual de **57500**. Suponiendo que la conectividad configurada correctamente, Hola después de la cadena de conexión podría ser tooaccess usado Hola virtual machine desde cualquier lugar en Hola internet:

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

Aunque esto habilita la conectividad de clientes en internet de Hola, esto no implica que cualquier usuario puede conectarse tooyour SQL Server. Los clientes externos tengan toohello correcta nombre de usuario y contraseña. Para mayor seguridad, no use el puerto conocido Hola 1433 para punto de conexión de máquina virtual pública Hola. Y si es posible, considere la posibilidad de agregar una ACL en los clientes de su tráfico toohello solo extremo toorestrict que permite. Para obtener instrucciones sobre el uso de ACL con puntos de conexión, consulte [administrar Hola ACL en un punto de conexión](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

> [!NOTE]
> Es importante toonote que, cuando se utiliza esta técnica toocommunicate con SQL Server, todos los datos salientes de Hola centro de datos de Azure está sujeto toonormal [precios en las transferencias de datos de salida](https://azure.microsoft.com/pricing/details/data-transfers/).
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a>Conectar tooSQL Server Hola misma red virtual
[La red virtual](../../../virtual-network/virtual-networks-overview.md) permite otros escenarios. Se pueden conectar máquinas virtuales de hello misma red virtual, incluso si esas máquinas virtuales existen en servicios de nube diferente. Asimismo, con una [VPN de sitio a sitio](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), puede crear una arquitectura híbrida que conecta las máquinas virtuales con redes y máquinas locales.

Redes virtuales también permite toojoin su dominio de tooa de máquinas virtuales de Azure. Se trata de tooSQL de hello única manera toouse autenticación de Windows Server. Hello otros escenarios de conexión requieren autenticación de SQL con nombres de usuario y contraseñas.

Si va tooconfigure un entorno de dominio y la autenticación de Windows, no es necesario toouse pasos de hello en este punto de conexión público de artículo tooconfigure Hola u Hola autenticación de SQL y los inicios de sesión. En este escenario, se puede conectar la instancia de SQL Server de tooyour si se especifica el nombre de VM de SQL Server de hello en la cadena de conexión de Hola. Hola siguiente ejemplo se supone que también se ha configurado la autenticación de Windows y se ha concedido a ese usuario de hello instancia de SQL Server toohello de acceso.

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a>Pasos para configurar la conectividad de SQL Server en una máquina virtual de Azure
Hola pasos demuestran cómo tooconnect toohello instancia de SQL Server sobre Hola internet con SQL Server Management Studio (SSMS). Sin embargo, hello mismos pasos aplican toomaking la máquina virtual de SQL Server puede tener acceso para aplicaciones, con lo que se ejecutan de forma local y en Azure.

Para poder conectarse toohello instancia de SQL Server desde otra máquina virtual u Hola internet, debe completar Hola siguiente las tareas como se describe en secciones Hola siguientes:

* [Crear un extremo TCP para la máquina virtual de Hola](#create-a-tcp-endpoint-for-the-virtual-machine)
* [Abrir los puertos TCP en firewall de Windows hello](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [Configurar SQL Server toolisten en hello protocolo TCP](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [Configuración de SQL Server para autenticación de modo mixto](#configure-sql-server-for-mixed-mode-authentication)
* [Creación de inicios de sesión para la autenticación de SQL Server](#create-sql-server-authentication-logins)
* [Determinar el nombre DNS de Hola de máquina virtual de Hola](#determine-the-dns-name-of-the-virtual-machine)
* [Conectar toohello motor de base de datos desde otro equipo](#connect-to-the-database-engine-from-another-computer)

ruta de acceso de conexión de Hola se resume en hello siguiente diagrama:

![Conectando la máquina virtual de SQL Server de tooa](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a>Pasos siguientes
Si también va toouse grupos de disponibilidad AlwaysOn para alta disponibilidad y recuperación ante desastres, considere la posibilidad de implementar un agente de escucha. Los clientes de base de datos conectan toohello escucha en lugar de directamente tooone Hola instancias de SQL Server. Hola escucha rutas clientes toohello réplica principal en el grupo de disponibilidad de Hola. Para obtener más información, consulte [Configuración de un agente de escucha con ILB para grupos de disponibilidad AlwaysOn en Azure](../classic/ps-sql-int-listener.md).

Es importante tooreview todos de seguridad de hello las prácticas recomendadas para SQL Server que se ejecuta en una máquina virtual de Azure. Para obtener más información, consulte [Consideraciones de seguridad para SQL Server en Azure Virtual Machines](../sql/virtual-machines-windows-sql-security.md).

[Explorar la ruta de acceso de aprendizaje de hello](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server en máquinas virtuales de Azure. 

Para ver otros temas relacionados con toorunning SQL Server en máquinas virtuales de Azure, consulte [SQL Server en máquinas virtuales Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

