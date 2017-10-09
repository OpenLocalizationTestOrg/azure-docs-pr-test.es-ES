---
title: "tareas de administración de aaaAutomate en máquinas virtuales de SQL (clásico) | Documentos de Microsoft"
description: "Este tema describe cómo toomanage Hola extensión del Agente SQL Server, que automatiza las tareas de administración de SQL Server específicas. Entre ellas se incluyen la copia de seguridad automatizada, la aplicación de revisiones automatizada y la integración de Azure Key Vault. En este tema usa el modo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a>Automatizar tareas de administración de máquinas virtuales de Azure con hello extensión del Agente SQL Server (clásico)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [Clásico](../classic/sql-server-agent-extension.md)
> 
>
 
Hola (SQLIaaSAgent) de extensión del agente de IaaS de SQL Server se ejecuta en máquinas virtuales de Azure tooautomate las tareas de administración. Este tema proporciona información general de servicios de hello admitidos por la extensión de hello, así como las instrucciones de instalación, estado y eliminación.

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. versión de administrador de recursos de hello tooview de este artículo, consulte [extensión del Agente SQL Server para el Administrador de recursos en máquinas virtuales de SQL Server](../sql/virtual-machines-windows-sql-server-agent-extension.md).

## <a name="supported-services"></a>Servicios admitidos
Hola extensión del agente de IaaS de SQL Server admite Hola después de las tareas de administración:

| Característica de administración | Descripción |
| --- | --- |
| **Copia de seguridad automatizada de SQL** |Automatiza la programación de Hola de copias de seguridad para todas las bases de datos para la instancia de predeterminada Hola de SQL Server en VM de Hola. Para obtener más información, consulte [Copia de seguridad automatizada para SQL Server en máquinas virtuales de Azure (implementación clásica)](../classic/sql-automated-backup.md). |
| **Aplicación de revisiones automatizada de SQL** |Configura una ventana de mantenimiento durante las actualizaciones que coloca tooyour VM puede tardar, por lo que puede evitar las actualizaciones durante las horas de máxima para la carga de trabajo. Para obtener más información, consulte [Aplicación de revisiones automatizadas para SQL Server en máquinas virtuales de Azure (implementación clásica)](../classic/sql-automated-patching.md). |
| **Integración del Almacén de claves de Azure** |Permite tooautomatically instalar y configurar el almacén de claves de Azure en la VM de SQL Server. Para obtener más información, consulte [Configuración de la integración de Almacén de claves de Azure para SQL Server en máquinas virtuales de Azure (implementación clásica)](../classic/ps-sql-keyvault.md). |

## <a name="prerequisites"></a>Requisitos previos
Requisitos toouse Hola extensión del agente de IaaS de SQL Server en la máquina virtual:

### <a name="operating-system"></a>Sistema operativo:
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

### <a name="sql-server-versions"></a>Versiones de SQL Server:
* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

### <a name="azure-powershell"></a>Azure PowerShell:
[Descargar y configurar los comandos de PowerShell de Azure más recientes de hello](/powershell/azure/overview).

Inicie Windows PowerShell y conectar tooyour suscripción de Azure con hello **Add-AzureAccount** comando.

    Add-AzureAccount

Si tiene varias suscripciones, use **Select-AzureSubscription** suscripción de hello tooselect que contiene el destino de la VM clásico.

    Select-AzureSubscription -SubscriptionName <subscriptionname>

En este momento, puede obtener una lista de máquinas virtuales clásicas de Hola y sus nombres de servicio asociado con hello **Get-AzureVM** comando.

    Get-AzureVM

## <a name="installation"></a>Instalación
Para las máquinas virtuales clásicas, debe usar PowerShell tooinstall hello extensión del agente de IaaS de SQL Server y configurar sus servicios asociados. Hola de uso **AzureVMSqlServerExtension conjunto** extensión de Hola de tooinstall de cmdlet de PowerShell. Por ejemplo, hello siguiente comando instala la extensión de hello en una VM de Windows Server (clásico) y nombres que "SQLIaaSExtension".

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

Si actualiza la versión más reciente de toohello de hello extensión del agente de IaaS de SQL, debe reiniciar la máquina virtual después de actualizar la extensión de Hola.

> [!NOTE]
> Máquinas virtuales clásicas no tienen una opción tooinstall y configurar Hola extensión del agente de IaaS de SQL a través del portal de Hola.
> 
> 

## <a name="status"></a>Estado
Una manera de tooverify que se instala la extensión de hello es tooview el estado del agente de hello en hello Portal de Azure. Seleccione una máquina virtual que se muestran en la hoja de la máquina virtual de hello y, a continuación, haga clic en **extensiones**. Debería ver Hola **SQLIaaSAgent** las extensiones que aparece.

![Extensión del Agente de IaaS SQL Server en Azure Portal](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

También puede usar hello **AzureVMSqlServerExtension Get** cmdlet de Powershell de Azure.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a>Eliminación
Hola Portal de Azure, puede desinstalar extensión Hola haciendo clic en el botón de puntos suspensivos de hello en hello **extensiones** hoja de propiedades de la máquina virtual. Hacer clic en **Desinstalar**.

![Desinstalar Hola extensión del agente de IaaS de SQL Server en el Portal de Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

También puede usar hello **Remove-AzureVMSqlServerExtension** cmdlet de Powershell.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a>Pasos siguientes
Empezar a usar uno de los servicios de hello compatibles con la extensión de Hola. Para obtener más información, vea los temas de hello hace referencia en hello [admite servicios](#supported-services) sección de este artículo.

Para obtener más información sobre cómo ejecutar SQL Server en Azure Virtual Machines, consulte [Información general sobre SQL Server en Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

