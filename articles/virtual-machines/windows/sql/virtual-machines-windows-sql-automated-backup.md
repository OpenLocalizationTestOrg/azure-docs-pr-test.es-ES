---
title: "aaaAutomated copia de seguridad de SQL Server 2014 máquinas virtuales de Azure | Documentos de Microsoft"
description: "Explica la característica de copia de seguridad automatizada de Hola para 2014 VM de SQL Server que se ejecuta en Azure. Este artículo es específico tooVMs mediante Hola, Administrador de recursos."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a>Copia de seguridad automatizada para SQL Server 2014 en Azure Virtual Machines (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Copia de seguridad automatizada configura automáticamente [tooMicrosoft de copia de seguridad administrada Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todas las bases de datos nuevas y existentes en una VM de Azure que ejecuta SQL Server 2014 Standard o Enterprise. Esto le permite las copias de seguridad de base de datos normal de tooconfigure que utilizan el almacenamiento de blobs de Azure duradero. Copia de seguridad automatizada depende de hello [extensión del agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Requisitos previos
toouse copia de seguridad automatizada, considere la posibilidad de hello siguiendo los requisitos previos:

**Sistema operativo**:

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

**Edición/versión de SQL Server**:

- SQL Server 2014 Standard
- SQL Server 2014 Enterprise

> [!IMPORTANT]
> Copia de seguridad automatizada funciona con SQL Server 2014. Si usas SQL Server 2016, puede usar copia de seguridad automatizada v2 tooback seguridad de las bases de datos. Para obtener más información, vea [Copia de seguridad automatizada v2 para SQL Server 2016 en Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).

**Configuración de base de datos**:

- Las bases de datos de destino deben usar el modelo de recuperación completa de Hola. Para obtener más información sobre las repercusiones de Hola Hola completa del modelo de recuperación en copias de seguridad, consulte [Hola de copia de seguridad en el modelo de recuperación completa](https://technet.microsoft.com/library/ms190217.aspx).
- Las bases de datos de destino deben estar en la instancia de SQL Server predeterminada de Hola. Hola extensión de IaaS de SQL Server no admite instancias con nombre.

**Modelo de implementación de Azure**:

- Resource Manager

**Azure PowerShell**:

- [Instalar los comandos de PowerShell de Azure más recientes de hello](/powershell/azure/overview) si tiene previsto tooconfigure copia de seguridad automatizada con PowerShell.

> [!NOTE]
> Copia de seguridad automatizada se basa en hello extensión del agente de IaaS de SQL Server. Las imágenes actuales de la galería de máquinas virtuales de SQL agregan esta extensión de manera predeterminada. Para más información, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Settings

Hello siguiente tabla describe las opciones de Hola que se pueden configurar para copia de seguridad automatizada. pasos de configuración real de Hello varían dependiendo de si utiliza Hola portal de Azure o comandos de PowerShell de Windows Azure.

| Configuración | Intervalo (valor predeterminado) | Descripción |
| --- | --- | --- |
| **Copia de seguridad automatizada** | Habilitar/deshabilitar (deshabilitado) | Habilita o deshabilita la copia de seguridad automatizada para una máquina virtual de Azure que ejecuta SQL Server 2014 Standard o Enterprise. |
| **Período de retención** | 1-30 días (30 días) | número de Hola de días tooretain una copia de seguridad. |
| **Storage Account** | Cuenta de almacenamiento de Azure | Un toouse de la cuenta de almacenamiento de Azure para almacenar los archivos de copia de seguridad automatizada en almacenamiento de blobs. Se crea un contenedor en esta ubicación toostore todos los archivos de copia de seguridad. archivo de copia de seguridad de Hello convención de nomenclatura incluye Hola fecha, hora y nombre de la máquina. |
| **Cifrado** | Habilitar/deshabilitar (deshabilitado) | Habilita o deshabilita el cifrado. Cuando está habilitado el cifrado, copia de seguridad de hello certificados usados toorestore Hola se encuentran en hello especificado cuenta de almacenamiento en hello mismo `automaticbackup` contenedor mediante Hola la misma convención de nomenclatura. Si cambia la contraseña de hello, se genera un nuevo certificado con esa contraseña, pero los certificados antiguos Hola permanecen toorestore copias de seguridad anteriores. |
| **Password** | Texto de contraseña | Una contraseña para claves de cifrado. Esto solo es necesario si se habilita el cifrado. En orden toorestore una copia de seguridad cifrada, debe tener contraseña correcta de Hola y el certificado relacionado que se usaron en tiempo de Hola se realizó la copia de seguridad de Hola. |

## <a name="configuration-in-hello-portal"></a>Configuración de hello Portal

Puede usar hello tooconfigure portal Azure copia de seguridad automatizada durante el aprovisionamiento o para SQL Server 2014 las máquinas virtuales existentes.

### <a name="new-vms"></a>Nuevas máquinas virtuales

Usar hello tooconfigure portal Azure copia de seguridad automatizada al crear una nueva máquina Virtual de SQL Server 2014 en el modelo de implementación del Administrador de recursos de Hola.

Hola **configuración de SQL Server** hoja, seleccione **copia de seguridad automatizada**. Hello siguiente captura de pantalla de portal Azure muestra hello **copia de seguridad automatizada de SQL** hoja.

![Configuración de Copia de seguridad automatizada de SQL en Azure Portal](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

Para el contexto, vea el tema completo de hello en [aprovisionar una máquina virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Máquinas virtuales existentes

Para las máquinas virtuales de SQL Server existentes, seleccione su máquina virtual de SQL Server. A continuación, seleccione hello **configuración de SQL Server** sección de hello **configuración** hoja.

![Copia de seguridad automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

Hola **configuración de SQL Server** hoja, haga clic en hello **editar** botón Hola automatizada sección copia de seguridad.

![Configuración de Copia de seguridad automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

Cuando termine, haga clic en hello **Aceptar** botón en la parte inferior de Hola de hello **configuración de SQL Server** toosave hoja los cambios.

Si va a habilitar copia de seguridad automatizada para hello primera vez, Azure configura Hola agente de IaaS de SQL Server en segundo plano de Hola. Durante este tiempo, Hola portal de Azure es posible que no muestre que está configurada la copia de seguridad automatizada. Espere unos minutos para hello toobe de agente instalado, configurado. Después de ese hello Azure portal reflejará nueva configuración de Hola.

> [!NOTE]
> También puede usar una plantilla para configurar Copia de seguridad automatizada. Para más información, consulte [la plantilla de inicio rápido de Azure para Copia de seguridad automatizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).

## <a name="configuration-with-powershell"></a>Configuración con PowerShell

Puede usar PowerShell tooconfigure copia de seguridad automatizada. Antes de comenzar:

- [Descargue e instale Hola más reciente de PowerShell de Azure](http://aka.ms/webpi-azps).
- Abra Windows PowerShell y asócielo con su cuenta. Puede hacerlo siguiendo los pasos de Hola Hola [configurar su suscripción](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sección de hello aprovisionamiento tema.

### <a name="install-hello-sql-iaas-extension"></a>Instalar Hola extensión de IaaS de SQL
Si se aprovisiona una máquina virtual de SQL Server de hello portal de Azure, ya debe instalarse Hola extensión de IaaS de SQL Server. Puede determinar si se instaló para la máquina virtual mediante una llamada a **Get AzureRmVM** comando y el examen de hello **extensiones** propiedad.

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

Si Hola extensión del agente de IaaS de SQL Server está instalado, verá que aparece como "SqlIaaSAgent" o "SQLIaaSExtension". **Estado de aprovisionamiento** para extensión de hello también debería mostrar "Correcto".

Si no está instalado o no se pudo toobe aprovisionado, puede instalarlo con el siguiente comando de Hola. En suma toohello VM nombre del grupo de recursos, también debe especificar la región de hello (**$region**) que la máquina virtual se encuentra en.

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <a id="verifysettings"></a> Verificación de la configuración actual

Si habilita la copia de seguridad automatizada durante el aprovisionamiento, puede usar PowerShell toocheck la configuración actual. Ejecute hello **Get AzureRmVMSqlServerExtension** comando y examine hello **AutoBackupSettings** propiedad:

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

Debería obtener siguiente toohello similar de salida:

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

Si el resultado muestra que **habilitar** se establece demasiado**False**, tendrá que tooenable la copia de seguridad automatizada. Hello buenas noticias son que habilitar y configurar la copia de seguridad automatizada en hello igual. Consulte la sección siguiente de hello esta información.

> [!NOTE] 
> Si comprobar la configuración de hello inmediatamente después de realizar un cambio, es posible que se pondrá en contacto valores de configuración anteriores Hola. Espere unos minutos y compruebe la configuración de hello nuevo toomake seguro de que se han aplicado los cambios.

### <a name="configure-automated-backup"></a>Configurar Copia de seguridad automatizada
Puede usar PowerShell tooenable copia de seguridad automatizada, así como toomodify su configuración y el comportamiento en cualquier momento.

En primer lugar, seleccione o cree una cuenta de almacenamiento para hello archivos de copia de seguridad. Hello secuencia de comandos siguiente selecciona una cuenta de almacenamiento o lo crea si no existe.

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> Copia de seguridad automatizada no permite almacenar las copias de seguridad en Premium Storage, pero pueden realizar copias de seguridad de discos de VM que usan Premium Storage.

A continuación, usar hello **New-AzureRmVMSqlServerAutoBackupConfig** tooenable de comandos y configurar copias de seguridad toostore configuración de copia de seguridad automatizada de Hola Hola cuenta de almacenamiento de Azure. En este ejemplo, las copias de seguridad de Hola se establecen toobe conserva de 10 días. Hola segundo comando **AzureRmVMSqlServerExtension conjunto**, Hola actualizaciones especificado VM de Azure con esta configuración.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

Podría tardar varios tooinstall minutos y configure Hola agente de IaaS de SQL Server.

> [!NOTE]
> Hay otras opciones para **AzureRmVMSqlServerAutoBackupConfig New** que aplican solo tooSQL Server 2016 y copia de seguridad automatizada v2. SQL Server 2014 no admite Hola después de configuración: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, y **LogBackupFrequencyInMinutes**. Si intentas tooconfigure esta configuración en una máquina virtual de SQL Server 2014, no hay ningún error, pero no se aplica la configuración de Hola. Si desea toouse esta configuración en una máquina virtual de SQL Server 2016, consulte [v2 de copia de seguridad automatizada SQL Server 2016 máquinas virtuales de Azure](virtual-machines-windows-sql-automated-backup-v2.md).

cifrado de tooenable, modificar Hola Hola de toopass de secuencia de comandos anterior **EnableEncryption** parámetro junto con una contraseña (cadena segura) para hello **CertificatePassword** parámetro. Hola siguiente script habilita la configuración de copia de seguridad automatizada de hello en el ejemplo anterior de Hola y agrega el cifrado.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

tooconfirm su configuración se aplica, [comprobar la configuración de copia de seguridad automatizada de hello](#verifysettings).

### <a name="disable-automated-backup"></a>Deshabilitar Copia de seguridad automatizada

toodisable copia de seguridad automatizada, ejecución Hola mismo script sin hello **-habilitar** parámetro toohello **AzureRmVMSqlServerAutoBackupConfig New** comando. Hola ausencia de hello **-habilitar** característica de parámetro señales Hola comando toodisable Hola. Al igual que con la instalación, puede tardar varios minutos toodisable copia de seguridad automatizada.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a>Script de ejemplo

Hello siguiente script proporciona un conjunto de variables que puede personalizar tooenable y configurar copia de seguridad automatizada para la máquina virtual. En su caso, tendrá que secuencia de comandos de toocustomize Hola según sus requisitos. Por ejemplo, podría tener cambios toomake si deseara copia de seguridad de toodisable Hola de bases de datos del sistema o habilitar el cifrado.

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Pasos siguientes

Copia de seguridad automatizada configura Copia de seguridad administrada en máquinas virtuales de Azure. Por lo que es importante[revisar la documentación de Hola para copia de seguridad administrada](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Hola comportamiento e implicaciones.

Puede encontrar la copia de seguridad adicional y restaurar guía para SQL Server en máquinas virtuales de Azure en hello tema siguiente: [de copia de seguridad y restauración para SQL Server en máquinas virtuales Azure](virtual-machines-windows-sql-backup-recovery.md).

Para más información acerca de otras tareas de automatización disponibles, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Para más información sobre cómo ejecutar SQL Server en máquinas virtuales de Azure, consulte [Introducción a SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).

