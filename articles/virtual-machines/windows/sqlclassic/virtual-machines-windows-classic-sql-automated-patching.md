---
title: "aaaAutomated aplicación de revisiones para las máquinas virtuales de SQL Server (clásico) | Documentos de Microsoft"
description: "Explica característica de aplicación de revisiones automatizada de Hola para SQL Server máquinas virtuales que ejecutan en Azure utilizando el modo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a>Aplicación de revisiones automatizadas para SQL Server en máquinas virtuales de Azure (implementación clásica)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [Clásico](../classic/sql-automated-patching.md)
> 
> 

Aplicación de revisión automatizada establece una ventana de mantenimiento para una máquina virtual de Azure con SQL Server. Actualizaciones automatizadas solo puede instalarse durante esta ventana de mantenimiento. Para SQL Server, esto garantiza que las actualizaciones del sistema y los reinicios asociados se producen en tiempo posible mejor hello en la base de datos de Hola. Aplicación de revisiones automatizada depende de hello [extensión del agente de IaaS de SQL Server](../classic/sql-server-agent-extension.md).

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. versión de administrador de recursos de hello tooview de este artículo, consulte [aplicación de revisiones automatizada para SQL Server en el Administrador de recursos de máquinas virtuales de Azure](../sql/virtual-machines-windows-sql-automated-patching.md).

## <a name="prerequisites"></a>Requisitos previos
toouse aplicación de revisiones automatizada, considere la posibilidad de hello siguiendo los requisitos previos:

**Sistema operativo**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Versión de SQL Server**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [Comandos de PowerShell de Azure más recientes de Hola de instalación](/powershell/azure/overview).

**Extensión IaaS de SQL Server**:

* [Instalar extensión de IaaS de SQL Server de hello](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Settings
Hello siguiente tabla describe las opciones de Hola que pueden configurarse para la aplicación de revisiones automatizada. Para las máquinas virtuales clásicas, debe usar PowerShell tooconfigure esta configuración.

| Configuración | Valores posibles | Description |
| --- | --- | --- |
| **Aplicación de revisiones automatizada** |Habilitar/deshabilitar (deshabilitado) |Habilita o deshabilita Aplicación de revisión automatizada para una máquina virtual de Azure. |
| **Programación de mantenimiento** |Cada día, el lunes, el martes, el miércoles, el jueves, el viernes, el sábado, el domingo |programación de Hola para descargar e instalar actualizaciones de Microsoft, Windows y SQL Server para la máquina virtual. |
| **Hora de inicio de mantenimiento** |0-24 |Hola inicio local tiempo tooupdate Hola la máquina virtual. |
| **Duración de la ventana de mantenimiento** |30-180 |número de Hola de minutos permitido descarga de hello toocomplete e instalación de actualizaciones. |
| **Categoría de la revisión** |Importante |categoría de Hola de toodownload actualizaciones e instalar. |

## <a name="configuration-with-powershell"></a>Configuración con PowerShell
En el siguiente ejemplo de Hola, PowerShell es usado tooconfigure aplicación de revisiones automatizada en una máquina virtual existente de SQL Server. Hola **New-AzureVMSqlServerAutoPatchingConfig** comando configura una nueva ventana de mantenimiento para las actualizaciones automáticas.

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

Siguiendo con este ejemplo, hello tabla siguiente describen efecto práctico de hello en el destino de hello VM de Azure:

| Parámetro | Efecto |
| --- | --- |
| **DayOfWeek** |Las revisiones instaladas cada jueves. |
| **MaintenanceWindowStartingHour** |Inicia las actualizaciones a las 11:00 a.m. |
| **MaintenanceWindowsDuration** |Las revisiones deben instalarse en un plazo de 120 minutos. En función del tiempo de inicio de hello, debe finalizar a la 1:00 pm. |
| **PatchCategory** |Hola solo configuración posible para este parámetro es "Importante". |

Podría tardar varios tooinstall minutos y configure Hola agente de IaaS de SQL Server.

toodisable aplicación de revisiones automatizada, ejecución Hola mismo script sin Hola - Enable parámetro toohello New-AzureVMSqlServerAutoPatchingConfig. Como con la instalación, puede tardar varios toodisable minutos aplicación de revisiones automatizada.

## <a name="next-steps"></a>Pasos siguientes
Para más información acerca de otras tareas de automatización disponibles, consulte la [extensión Agente de IaaS de SQL Server](../classic/sql-server-agent-extension.md).

Para más información sobre cómo ejecutar SQL Server en máquinas virtuales de Azure, consulte [Introducción a SQL Server en Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

