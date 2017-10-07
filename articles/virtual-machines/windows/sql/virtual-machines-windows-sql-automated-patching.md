---
title: "aaaAutomated aplicación de revisiones para las máquinas virtuales de SQL Server (Administrador de recursos) | Documentos de Microsoft"
description: "Explica el característica de aplicación de revisiones automatizada de Hola para SQL Server máquinas virtuales que ejecutan en Azure mediante el Administrador de recursos."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a>Aplicación de revisión automatizada para SQL Server en máquinas virtuales de Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-automated-patching.md)
> * [Clásico](../classic/sql-automated-patching.md)
> 
> 

Aplicación de revisión automatizada establece una ventana de mantenimiento para una máquina virtual de Azure con SQL Server. Actualizaciones automatizadas solo puede instalarse durante esta ventana de mantenimiento. Para SQL Server, esta rescriction garantiza que las actualizaciones del sistema y los reinicios asociados se producen en tiempo posible mejor hello en la base de datos de Hola. Aplicación de revisiones automatizada depende de hello [extensión del agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

tooview Hola clásico versión de este artículo, consulte [aplicación de revisiones automatizada para SQL Server en máquinas virtuales de Azure clásico](../classic/sql-automated-patching.md).

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

* [Instalar los comandos de PowerShell de Azure más recientes de hello](/powershell/azure/overview) si tiene previsto tooconfigure aplicación de revisiones automatizada con PowerShell.

> [!NOTE]
> Aplicación de revisiones automatizada se basa en hello extensión del agente de IaaS de SQL Server. Las imágenes actuales de la galería de máquinas virtuales de SQL agregan esta extensión de manera predeterminada. Para más información, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).
> 
> 

## <a name="settings"></a>Settings
Hello siguiente tabla describe las opciones de Hola que pueden configurarse para la aplicación de revisiones automatizada. pasos de configuración real de Hello varían dependiendo de si utiliza Hola portal de Azure o comandos de PowerShell de Windows Azure.

| Configuración | Valores posibles | Description |
| --- | --- | --- |
| **Aplicación de revisiones automatizada** |Habilitar/deshabilitar (deshabilitado) |Habilita o deshabilita Aplicación de revisión automatizada para una máquina virtual de Azure. |
| **Programación de mantenimiento** |Cada día, el lunes, el martes, el miércoles, el jueves, el viernes, el sábado, el domingo |programación de Hola para descargar e instalar actualizaciones de Microsoft, Windows y SQL Server para la máquina virtual. |
| **Hora de inicio de mantenimiento** |0-24 |Hola inicio local tiempo tooupdate Hola la máquina virtual. |
| **Duración de la ventana de mantenimiento** |30-180 |número de Hola de minutos permitido descarga de hello toocomplete e instalación de actualizaciones. |
| **Categoría de la revisión** |Importante |categoría de Hola de toodownload actualizaciones e instalar. |

## <a name="configuration-in-hello-portal"></a>Configuración de hello Portal
Puede usar hello tooconfigure portal Azure aplicación de revisiones automatizada durante el aprovisionamiento o para las máquinas virtuales existentes.

### <a name="new-vms"></a>Nuevas máquinas virtuales
Hola de uso tooconfigure portal Azure aplicación de revisiones automatizada al crear una nueva máquina Virtual de SQL Server en el modelo de implementación del Administrador de recursos de Hola.

Hola **configuración de SQL Server** hoja, seleccione **aplicación de revisiones automatizadas**. Hello siguiente captura de pantalla de portal Azure muestra hello **SQL aplicación de revisiones automatizada** hoja.

![Aplicación de revisión automatizada de SQL en el Portal de Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

Para el contexto, vea el tema completo de hello en [aprovisionar una máquina virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Máquinas virtuales existentes
Para las máquinas virtuales de SQL Server existentes, seleccione su máquina virtual de SQL Server. A continuación, seleccione hello **configuración de SQL Server** sección de hello **configuración** hoja.

![Aplicación de revisión automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

Hola **configuración de SQL Server** hoja, haga clic en hello **editar** botón Hola automatizada sección aplicación de revisiones.

![Configuración de Aplicación de revisión automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

Cuando termine, haga clic en hello **Aceptar** botón en la parte inferior de Hola de hello **configuración de SQL Server** toosave hoja los cambios.

Si va a habilitar aplicación de revisiones automatizada para hello primera vez, Azure configura Hola agente de IaaS de SQL Server en segundo plano de Hola. Durante este tiempo, Hola portal de Azure es posible que no muestre que se ha configurado la aplicación de revisiones automatizada. Espere unos minutos para hello toobe de agente instalado, configurado. Después de ese hello Azure portal refleje nueva configuración de Hola.

> [!NOTE]
> También puede usar una plantilla para configurar Aplicación de revisión automatizada. Para más información, consulte [la plantilla de inicio rápido de Azure para Aplicación de revisión automatizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).
> 
> 

## <a name="configuration-with-powershell"></a>Configuración con PowerShell
Después de aprovisionar la VM de SQL, use PowerShell tooconfigure aplicación de revisiones automatizada.

En el siguiente ejemplo de Hola, PowerShell es usado tooconfigure aplicación de revisiones automatizada en una máquina virtual existente de SQL Server. Hola **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** comando configura una nueva ventana de mantenimiento para las actualizaciones automáticas.

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

Siguiendo con este ejemplo, hello tabla siguiente describen efecto práctico de hello en el destino de hello VM de Azure:

| Parámetro | Efecto |
| --- | --- |
| **DayOfWeek** |Las revisiones instaladas cada jueves. |
| **MaintenanceWindowStartingHour** |Inicia las actualizaciones a las 11:00 a.m. |
| **MaintenanceWindowsDuration** |Las revisiones deben instalarse en un plazo de 120 minutos. En función del tiempo de inicio de hello, debe finalizar a la 1:00 pm. |
| **PatchCategory** |Hola única configuración posible para este parámetro es **importante**. |

Podría tardar varios tooinstall minutos y configure Hola agente de IaaS de SQL Server.

toodisable aplicación de revisiones automatizada, ejecución Hola mismo script sin hello **-habilitar** parámetro toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**. Hola ausencia de hello **-habilitar** característica de parámetro señales Hola comando toodisable Hola.

## <a name="next-steps"></a>Pasos siguientes
Para más información acerca de otras tareas de automatización disponibles, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Para más información sobre cómo ejecutar SQL Server en máquinas virtuales de Azure, consulte [Introducción a SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).

