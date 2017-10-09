---
title: "copia de seguridad de máquinas virtuales de SQL Server (clásico) aaaAutomated | Documentos de Microsoft"
description: "Explica la característica de copia de seguridad automatizada de Hola para ejecutar máquinas virtuales de Azure mediante el Administrador de recursos de SQL Server. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a>Copia de seguridad automatizada para SQL Server en máquinas virtuales de Azure (implementación clásica)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [Clásico](../classic/sql-automated-backup.md)
> 
> 

Copia de seguridad automatizada configura automáticamente [tooMicrosoft de copia de seguridad administrada Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todas las bases de datos nuevas y existentes en una VM de Azure que ejecuta SQL Server 2014 Standard o Enterprise. Esto le permite las copias de seguridad de base de datos normal de tooconfigure que utilizan el almacenamiento de blobs de Azure duradero. Copia de seguridad automatizada depende de hello [extensión del agente de IaaS de SQL Server](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. versión de administrador de recursos de hello tooview de este artículo, consulte [copia de seguridad automatizada para SQL Server en el Administrador de recursos de máquinas virtuales de Azure](../sql/virtual-machines-windows-sql-automated-backup.md).

## <a name="prerequisites"></a>Requisitos previos
toouse copia de seguridad automatizada, considere la posibilidad de hello siguiendo los requisitos previos:

**Sistema operativo**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Edición/versión de SQL Server**:

* SQL Server 2014 Standard
* SQL Server 2014 Enterprise

> [!NOTE]
> SQL Server 2016 no se admite todavía para Copia de seguridad automatizada.
> 
> 

**Configuración de base de datos**:

* Las bases de datos de destino deben usar el modelo de recuperación completa de Hola.

**Azure PowerShell**:

* [Comandos de PowerShell de Azure más recientes de Hola de instalación](/powershell/azure/overview).

**Extensión IaaS de SQL Server**:

* [Instalar extensión de IaaS de SQL Server de hello](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Settings
Hello siguiente tabla describe las opciones de Hola que se pueden configurar para copia de seguridad automatizada. Para las máquinas virtuales clásicas, debe usar PowerShell tooconfigure esta configuración.

| Configuración | Intervalo (valor predeterminado) | Descripción |
| --- | --- | --- |
| **Copia de seguridad automatizada** |Habilitar/deshabilitar (deshabilitado) |Habilita o deshabilita la copia de seguridad automatizada para una máquina virtual de Azure que ejecuta SQL Server 2014 Standard o Enterprise. |
| **Período de retención** |1-30 días (30 días) |número de Hola de días tooretain una copia de seguridad. |
| **Storage Account** |Cuenta de almacenamiento de Azure (cuenta de almacenamiento Hola creada para hello especificado VM) |Un toouse de la cuenta de almacenamiento de Azure para almacenar los archivos de copia de seguridad automatizada en almacenamiento de blobs. Se crea un contenedor en esta ubicación toostore todos los archivos de copia de seguridad. archivo de copia de seguridad de Hello convención de nomenclatura incluye Hola fecha, hora y nombre de la máquina. |
| **Cifrado** |Habilitar/deshabilitar (deshabilitado) |Habilita o deshabilita el cifrado. Cuando está habilitado el cifrado, los certificados de hello copia de seguridad de hello toorestore usado se encuentran en hello especificar cuenta de almacenamiento en hello mismo automaticbackup contenedor mediante Hola misma convención de nomenclatura. Si cambia la contraseña de hello, se genera un nuevo certificado con esa contraseña, pero los certificados antiguos Hola permanecen toorestore copias de seguridad anteriores. |
| **Password** |Texto de contraseña (ninguno) |Una contraseña para claves de cifrado. Esto solo es necesario si se habilita el cifrado. En orden toorestore una copia de seguridad cifrada, debe tener contraseña correcta de Hola y el certificado relacionado que se usaron en tiempo de Hola se realizó la copia de seguridad de Hola. | **Backup system databases** (Copia de seguridad de bases de datos del sistema) | Habilitar/deshabilitar (deshabilitado) | Realiza copias de seguridad completas de Master, Model y MSDB |
| **Configure backup schedule** (Configurar programación de copia de seguridad) | Manual/Automatizado (Automatizado) | Seleccione **automatizada** tooautomatically sacar el máximo y las copias de seguridad en función de crecimiento del registro de registro. Seleccione **Manual** toospecify programación de Hola para completo y las copias de seguridad de registro. |

## <a name="configuration-with-powershell"></a>Configuración con PowerShell
En el siguiente ejemplo de PowerShell de hello, copia de seguridad automatizada está configurado para una máquina virtual existente de SQL Server 2014. Hola **AzureVMSqlServerAutoBackupConfig New** comando configura copias de seguridad toostore configuración de copia de seguridad automatizada de hello en la cuenta de almacenamiento de Azure Hola especificado por la variable de hello $storageaccount. Estas copias de seguridad se conservarán durante 10 días. Hola **AzureVMSqlServerExtension conjunto** comando hello actualizaciones especificado VM de Azure con esta configuración.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

Podría tardar varios tooinstall minutos y configure Hola agente de IaaS de SQL Server.

cifrado de tooenable, modificar Hola anterior script toopass Hola parámetro EnableEncryption junto con una contraseña (cadena segura) para el parámetro CertificatePassword de Hola. Hola siguiente script habilita la configuración de copia de seguridad automatizada de hello en el ejemplo anterior de Hola y agrega el cifrado.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

toodisable copia de seguridad automática, ejecución Hola mismo script sin hello **-habilitar** parámetro toohello **AzureVMSqlServerAutoBackupConfig nuevo**. Al igual que con la instalación, puede tardar varios minutos toodisable copia de seguridad automatizada.

> [!NOTE]
> Deshabilitar y desinstalar Hola agente de IaaS de SQL Server no quita una configuración de copia de seguridad administrada de hello configurado previamente. Debe deshabilitar la copia de seguridad automatizada antes de deshabilitar o desinstalar Hola agente de IaaS de SQL Server.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Copia de seguridad automatizada configura Copia de seguridad administrada en máquinas virtuales de Azure. Por lo que es importante[revisar la documentación de Hola para copia de seguridad administrada](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Hola comportamiento e implicaciones.

Puede encontrar la copia de seguridad adicional y restaurar guía para SQL Server en máquinas virtuales de Azure en hello tema siguiente: [de copia de seguridad y restauración para SQL Server en máquinas virtuales Azure](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Para más información acerca de otras tareas de automatización disponibles, consulte la [extensión Agente de IaaS de SQL Server](../classic/sql-server-agent-extension.md).

Para más información sobre cómo ejecutar SQL Server en máquinas virtuales de Azure, consulte [Introducción a SQL Server en Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

