---
title: "aaaConnect tooa Máquina Virtual de SQL Server (Administrador de recursos) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconnect tooSQL Server ejecuta en una máquina Virtual en Azure. En este tema usa el modelo de implementación clásica de Hola. escenarios de Hello varían según la configuración de red de Hola y la ubicación de hello del cliente de Hola."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a>Conectar tooa Máquina Virtual de SQL Server en Azure (Administrador de recursos)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-connect.md)
> * [Clásico](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Información general

Este tema describe cómo tooconnect tooyour SQL Server instancia ejecuta en una máquina virtual de Azure. En él se describen algunos [escenarios de conectividad generales](#connection-scenarios) y se proporcionan los [pasos detallados para configurar la conectividad de SQL Server en una máquina virtual de Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Para prefiere consultar un tutorial completo sobre aprovisionamiento y conectividad, consulte [Aprovisionamiento de una máquina virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="connection-scenarios"></a>Escenarios de conexión

forma de Hello un cliente conecta tooSQL servidor se ejecuta en una máquina Virtual depende de la ubicación de Hola de cliente de Hola y la configuración de red de Hola.

Si se aprovisiona una VM de SQL Server en hello portal de Azure, tiene opción de Hola de especificación de tipo hello de **de conectividad de SQL**.

![Opción de conectividad SQL pública durante el aprovisionamiento](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

Estas son algunas de las opciones de conectividad:

| Opción | Descripción |
|---|---|
| **Pública** | Conectar tooSQL Server a través de hello internet |
| **Privada** | Conectar tooSQL Server Hola misma red virtual |
| **Local** | Conectar tooSQL Server localmente en hello misma máquina virtual | 

Hello las secciones siguientes explican hello **público** y **privada** opciones con más detalle.

## <a name="connect-toosql-server-over-hello-internet"></a>Conectar tooSQL Server a través de Internet de Hola

Si desea que tooconnect tooyour el motor de base de datos de SQL Server desde Internet hello, seleccione **público** para hello **de conectividad de SQL** tipo en el portal de Hola durante el aprovisionamiento. portal de Hola Hola automáticamente lo siguiente:

* Habilita el protocolo TCP/IP de Hola para SQL Server.
* Configura un hello tooopen de regla de firewall puerto TCP de SQL Server (predeterminado: 1433).
* Habilita la autenticación de SQL Server, que es necesaria para el acceso público.
* Configura el grupo de seguridad de red de hello en hello tráfico TCP de máquina virtual tooall en hello puerto de SQL Server.

> [!IMPORTANT]
> imágenes de máquina virtual de Hola para hello programador de SQL Server y las ediciones Express no habilitan automáticamente protocolo Hola TCP/IP. Para las ediciones Developer y Express, debe usar el Administrador de configuración de SQL Server demasiado[habilitar manualmente el protocolo TCP/IP hello](#manualtcp) después de crear Hola máquina virtual.

Cualquier cliente con acceso a internet puede conectarse a instancia de SQL Server toohello especificando la dirección IP pública de Hola de máquina virtual de Hola o cualquier etiqueta DNS que se asigna la dirección IP de toothat. Si hello puerto de SQL Server es 1433, no es necesario toospecify en la cadena de conexión de Hola. Hola después de la cadena de conexión conecta tooa VM de SQL con una etiqueta DNS de `sqlvmlabel.eastus.cloudapp.azure.com` mediante la autenticación de SQL (también puede usar la dirección IP pública hello).

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

Aunque esto habilita la conectividad de clientes en internet de Hola, esto no implica que cualquier usuario puede conectarse tooyour SQL Server. Los clientes externos tengan toohello correcta nombre de usuario y contraseña. Sin embargo, para mayor seguridad, puede evitar el puerto conocido Hola 1433. Por ejemplo, si ha configurado toolisten de SQL Server en el puerto 1500 y firewall adecuados establecido y reglas del grupo de seguridad de red, podría conectarse mediante la anexión de nombre de servidor de número de puerto de hello toohello. Hello en el ejemplo siguiente se modifica Hola anterior mediante la adición de un número de puerto personalizado, **1500**, nombre del servidor toohello:

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> Al consultar SQL Server en una máquina virtual sobre Hola internet, todos los datos de salida de hello Azure datacenter está sujeto toonormal [precios en las transferencias de datos de salida](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="connect-toosql-server-within-a-virtual-network"></a>Conectar tooSQL Server dentro de una red virtual

Cuando eliges **privada** para hello **de conectividad de SQL** tipo en el portal de hello, Azure configura la mayoría de los valores de hello idénticos demasiado**público**. Hola una diferencia es que no hay ningún tooallow de regla de grupo de seguridad de red fuera de tráfico en el puerto de SQL Server de hello (predeterminado: 1433).

> [!IMPORTANT]
> imágenes de máquina virtual de Hola para hello programador de SQL Server y las ediciones Express no habilitan automáticamente protocolo Hola TCP/IP. Para las ediciones Developer y Express, debe usar el Administrador de configuración de SQL Server demasiado[habilitar manualmente el protocolo TCP/IP hello](#manualtcp) después de crear Hola máquina virtual.

La conectividad privada se suele utilizar utiliza con [Virtual Network](../../../virtual-network/virtual-networks-overview.md), lo que permite varios escenarios. Se pueden conectar máquinas virtuales de hello existe misma red virtual, incluso si esas máquinas virtuales en distintos grupos de recursos. Asimismo, con una [VPN de sitio a sitio](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), puede crear una arquitectura híbrida que conecta las máquinas virtuales con redes y máquinas locales.

Redes virtuales también permiten toojoin su dominio de tooa de máquinas virtuales de Azure. Se trata de tooSQL de hello única manera toouse autenticación de Windows Server. Hello otros escenarios de conexión requieren autenticación de SQL con nombres de usuario y contraseñas.

Si damos por hecho que ha configurado DNS en la red virtual, se puede conectar la instancia de SQL Server de tooyour especificando el nombre del equipo de hello VM de SQL Server en la cadena de conexión de Hola. Hola siguiente ejemplo también se supone que también se ha configurado la autenticación de Windows y se ha concedido a ese usuario de hello instancia de SQL Server toohello de acceso.

```
Server=mysqlvm;Integrated Security=true
```

## <a id="change"></a> Cambio de la configuración de conectividad SQL

Puede cambiar la configuración de conectividad de hello para la máquina virtual de SQL Server en hello portal de Azure.

1. Hola portal de Azure, seleccione **máquinas virtuales**.

2. Seleccione la VM con SQL Server.

3. En **Configuración**, haga clic en **Configuración de SQL Server**.

4. Hola de cambio **el nivel de conectividad SQL** tooyour requerido configuración. También puede usar este Hola de toochange de área puerto de SQL Server o la configuración de autenticación de SQL Hola.

   ![Cambio de conectividad de SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. Espere unos minutos para hello toocomplete de actualización.

   ![Notificación de actualización de la VM con SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <a id="manualtcp"></a> Habilitación de TCP/IP para las ediciones Developer y Express

Al cambiar la configuración de conectividad de SQL Server, Azure no habilita automáticamente protocolo Hola TCP/IP para SQL Server Developer y las ediciones Express. Hola a continuación se explica cómo toomanually habilitar TCP/IP para que puedan conectarse de forma remota mediante una dirección IP.

En primer lugar, conecte toohello máquina de SQL Server con Escritorio remoto.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

A continuación, habilite el protocolo Hola TCP/IP con **Administrador de configuración de SQL Server**.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a>Conectarse con SSMS

Hello pasos siguientes muestran cómo toocreate etiqueta de un DNS opcional para la máquina virtual de Azure y, a continuación, conectan con SQL Server Management Studio (SSMS).

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Pasos siguientes

instrucciones de aprovisionamiento de toosee junto con estos pasos de conectividad, consulte [aprovisionamiento de una máquina Virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).

Para ver otros temas relacionados con toorunning SQL Server en máquinas virtuales de Azure, consulte [SQL Server en máquinas virtuales Azure](virtual-machines-windows-sql-server-iaas-overview.md).
