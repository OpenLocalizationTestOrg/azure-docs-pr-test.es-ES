---
title: "tareas de administración de aaaAutomate en máquinas virtuales de SQL (Administrador de recursos) | Documentos de Microsoft"
description: "Este tema describe cómo toomanage Hola extensión del Agente SQL Server, que automatiza las tareas de administración de SQL Server específicas. Entre ellas se incluyen la copia de seguridad automatizada, la aplicación de revisiones automatizada y la integración de Azure Key Vault. Este tema utiliza el modo de implementación de Resource Manager Hola."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a>Automatizar tareas de administración de máquinas virtuales de Azure con hello extensión del Agente SQL Server (Administrador de recursos)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-server-agent-extension.md)
> * [Clásico](../classic/sql-server-agent-extension.md)
> 
> 

Hola (SQLIaaSExtension) de extensión del agente de IaaS de SQL Server se ejecuta en máquinas virtuales de Azure tooautomate las tareas de administración. Este tema proporciona información general de servicios de hello admitidos por la extensión de hello, así como las instrucciones de instalación, estado y eliminación.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

tooview Hola clásico versión de este artículo, consulte [extensión del Agente SQL Server para clásico de máquinas virtuales de SQL Server](../classic/sql-server-agent-extension.md).

## <a name="supported-services"></a>Servicios admitidos
Hola extensión del agente de IaaS de SQL Server admite Hola después de las tareas de administración:

| Característica de administración | Descripción |
| --- | --- |
| **Copia de seguridad automatizada de SQL** |Automatiza la programación de Hola de copias de seguridad para todas las bases de datos para la instancia de predeterminada Hola de SQL Server en VM de Hola. Para más información, consulte [Copia de seguridad automatizada para SQL Server en Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md). |
| **Aplicación de revisiones automatizada de SQL** |Configura una ventana de mantenimiento durante las actualizaciones que coloca tooyour VM puede tardar, por lo que puede evitar las actualizaciones durante las horas de máxima para la carga de trabajo. Para más información, consulte [Aplicación de revisión automatizada para SQL Server en Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md). |
| **Integración del Almacén de claves de Azure** |Permite tooautomatically instalar y configurar el almacén de claves de Azure en la VM de SQL Server. Para más información, consulte [Configuración de la integración de Azure Key Vault para SQL Server en Azure Virtual Machines (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md). |

Una vez instalado y en ejecución, Hola extensión del agente de IaaS de SQL Server hace que estas características de administración estén disponibles en el panel de SQL Server de Hola de Hola máquina virtual en hello Portal de Azure y a través de PowerShell de Azure para las imágenes de marketplace de SQL Server y a través de Azure PowerShell para las instalaciones manuales de extensión de Hola. 

## <a name="prerequisites"></a>Requisitos previos
Requisitos toouse Hola extensión del agente de IaaS de SQL Server en la máquina virtual:

**Sistema operativo**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Versiones de SQL Server**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [Descargar y configurar los comandos de PowerShell de Azure más recientes de Hola](/powershell/azure/overview)

## <a name="installation"></a>Instalación
Hola extensión del agente de IaaS de SQL Server se instala automáticamente al aprovisionar una de las imágenes de galería de máquinas virtuales de SQL Server de Hola. Si necesita la extensión de hello tooreinstall manualmente en una de estas máquinas virtuales de SQL Server, use Hola siguiente comando de PowerShell:

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

También es posible tooinstall Hola extensión del agente de IaaS de SQL Server en una máquina virtual de solo por el sistema operativo Windows Server. Esto solo se permite si además ha instalado manualmente SQL Server en ese equipo. A continuación, instalar la extensión de hello manualmente mediante el uso de Hola mismo **AzureVMSqlServerExtension conjunto** cmdlet de PowerShell.

> [!NOTE]
> Si instala manualmente Hola extensión del agente de IaaS de SQL Server en una VM solo por el sistema operativo de Windows Server, no puede administrar opciones de configuración de SQL Server de hello mediante Hola portal de Azure. En este escenario debe realizar todos los cambios con PowerShell.

## <a name="status"></a>Estado
Una manera de tooverify que se instala la extensión de hello es tooview el estado del agente de hello en hello Portal de Azure. Seleccione **toda la configuración de** en Hola hoja de la máquina virtual y, a continuación, haga clic en **extensiones**. Debería ver Hola **SQLIaaSExtension** las extensiones que aparece.

![Extensión del Agente de IaaS SQL Server en Azure Portal](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

También puede usar hello **AzureVMSqlServerExtension Get** cmdlet de Powershell de Azure.

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

comando anterior Hola confirma agente Hola se instala y proporciona información de estado general. También puede obtener información de estado específica acerca de la copia de seguridad automatizada y aplicación de revisiones con hello siga los comandos.

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a>Eliminación
Hola Portal de Azure, puede desinstalar extensión Hola haciendo clic en el botón de puntos suspensivos de hello en hello **extensiones** hoja de propiedades de la máquina virtual. Después, haga clic en **Eliminar**.

![Desinstalar Hola extensión del agente de IaaS de SQL Server en el Portal de Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

También puede usar hello **Remove-AzureRmVMSqlServerExtension** cmdlet de Powershell.

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a>Pasos siguientes
Empezar a usar uno de los servicios de hello compatibles con la extensión de Hola. Para obtener más información, vea los temas de hello hace referencia en hello [admite servicios](#supported-services) sección de este artículo.

Para obtener más información sobre cómo ejecutar SQL Server en Azure Virtual Machines, consulte [Información general sobre SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).

