---
title: "aaaAutomated v2 de copia de seguridad de SQL Server 2016 máquinas virtuales de Azure | Documentos de Microsoft"
description: "Explica la característica de copia de seguridad automatizada de Hola para 2016 VM de SQL Server que se ejecuta en Azure. Este artículo es específico tooVMs mediante Hola, Administrador de recursos."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a>Copia de seguridad automatizada v2 para Azure Virtual Machines con SQL Server 2016 (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

V2 de copia de seguridad automatizada configura automáticamente [tooMicrosoft de copia de seguridad administrada Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todas las bases de datos nuevas y existentes en una VM de Azure que ejecutan las ediciones de SQL Server 2016 Standard, Enterprise o Developer. Esto le permite las copias de seguridad de base de datos normal de tooconfigure que utilizan el almacenamiento de blobs de Azure duradero. V2 de copia de seguridad automatizada depende de hello [extensión del agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Requisitos previos
toouse v2 de copia de seguridad automatizada, revise Hola siguiendo los requisitos previos:

**Sistema operativo**:

- Windows Server 2012 R2
- Windows Server 2016

**Edición/versión de SQL Server**:

- SQL Server 2016 Standard
- SQL Server 2016 Enterprise
- SQL Server 2016 Developer

> [!IMPORTANT]
> Copia de seguridad automatizada v2 funciona con SQL Server 2016. Si está usando SQL Server 2014, puede usar copia de seguridad automatizada v1 tooback seguridad de las bases de datos. Para obtener más información, vea [Copia de seguridad automatizada para SQL Server 2014 en Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).

**Configuración de base de datos**:

- Las bases de datos de destino deben usar el modelo de recuperación completa de Hola. Para obtener más información sobre las repercusiones de Hola Hola completa del modelo de recuperación en copias de seguridad, consulte [Hola de copia de seguridad en el modelo de recuperación completa](https://technet.microsoft.com/library/ms190217.aspx).
- Las bases de datos del sistema no tiene toouse modelo de recuperación completa. Sin embargo, si necesita toobe de copias de seguridad del registro de modelo o MSDB, debe usar el modelo de recuperación completa.
- Las bases de datos de destino deben estar en la instancia de SQL Server predeterminada de Hola. Hola extensión de IaaS de SQL Server no admite instancias con nombre.

**Modelo de implementación de Azure**:

- Resource Manager

> [!NOTE]
> Copia de seguridad automatizada se basa en hello **extensión del agente de IaaS de SQL Server**. Las imágenes actuales de la galería de máquinas virtuales de SQL agregan esta extensión de manera predeterminada. Para más información, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Settings
Hello siguiente tabla describe las opciones de Hola que se pueden configurar para copia de seguridad automatizada v2. pasos de configuración real de Hello varían dependiendo de si utiliza Hola portal de Azure o comandos de PowerShell de Windows Azure.

### <a name="basic-settings"></a>Configuración básica

| Configuración | Intervalo (valor predeterminado) | Descripción |
| --- | --- | --- |
| **Copia de seguridad automatizada** | Habilitar/deshabilitar (deshabilitado) | Habilita o deshabilita la copia de seguridad automatizada para una VM de Azure que ejecuta SQL Server 2016 Standard o Enterprise. |
| **Período de retención** | 1-30 días (30 días) | número de Hola de copias de seguridad de tooretain días. |
| **Storage Account** | Cuenta de almacenamiento de Azure | Un toouse de la cuenta de almacenamiento de Azure para almacenar los archivos de copia de seguridad automatizada en almacenamiento de blobs. Se crea un contenedor en esta ubicación toostore todos los archivos de copia de seguridad. archivo de copia de seguridad de Hello convención de nomenclatura incluye Hola fecha, hora y GUID de la base de datos. |
| **Cifrado** |Habilitar/deshabilitar (deshabilitado) | Habilita o deshabilita el cifrado. Cuando está habilitado el cifrado, copia de seguridad de hello certificados usados toorestore Hola se encuentran en hello especificado cuenta de almacenamiento en hello mismo **automaticbackup** contenedor mediante Hola la misma convención de nomenclatura. Si cambia la contraseña de hello, se genera un nuevo certificado con esa contraseña, pero los certificados antiguos Hola permanecen toorestore copias de seguridad anteriores. |
| **Password** |Texto de contraseña | Una contraseña para claves de cifrado. Esto solo es necesario si se habilita el cifrado. En orden toorestore una copia de seguridad cifrada, debe tener contraseña correcta de Hola y el certificado relacionado que se usaron en tiempo de Hola se realizó la copia de seguridad de Hola. |

### <a name="advanced-settings"></a>Configuración avanzada

| Configuración | Intervalo (valor predeterminado) | Descripción |
| --- | --- | --- |
| **Copias de seguridad de bases de datos del sistema** | Habilitar/deshabilitar (deshabilitado) | Cuando se habilita, esta característica realizará también una copia de bases de datos de hello sistema: Master, MSDB y Model. Hello MSDB y las bases de datos de modelo, compruebe que están en modo de recuperación completa si desea toobe de copias de seguridad de registro realizada. Nunca se realizan copias de seguridad de registros para las bases de datos maestras. Tampoco se realizan copias de seguridad para TempDB. |
| **Programación de copia de seguridad** | Manual/Automatizado (Automatizado) | De forma predeterminada, programación de copia de seguridad de Hola se determinará automáticamente en función de crecimiento del registro de hello. Programación de copia de seguridad manual permite período de tiempo de hello usuario toospecify Hola para copias de seguridad. En este caso, las copias de seguridad siempre tendrá lugar en hello especifica la frecuencia y Hola durante el período de tiempo de un día determinado. |
| **Frecuencia de copia de seguridad completa** | Diariamente/semanalmente | Frecuencia de las copias de seguridad completas. En ambos casos, copias de seguridad completas se inician durante la ventana de hello siguiente hora programada. Cuando se selecciona semanalmente, las copias de seguridad pueden extenderse varios días hasta que se realizan correctamente las copias de seguridad de todas las bases de datos. |
| **Hora de inicio de copia de seguridad completa** | 00:00 – 23:00 (01:00) | Hora de inicio de un día determinado durante el cual se pueden realizar copias de seguridad completas. |
| **Período de tiempo de copia de seguridad completa** | 1-23 horas (1 hora) | Duración del período de tiempo de Hola de un día determinado durante el cual pueden realizar copias de seguridad completas. |
| **Frecuencia de copia de seguridad de registros** | 5-60 minutos (60 minutos) | Frecuencia de las copias de seguridad de registros. |

## <a name="understanding-full-backup-frequency"></a>Información de la frecuencia de copia de seguridad completa
Es importante toounderstand Hola diferencia entre copias de seguridad completas diarias y semanales. Para ello, se le guiará a través de dos escenarios de ejemplo.

### <a name="scenario-1-weekly-backups"></a>Escenario 1: Copias de seguridad semanales
Tiene una VM con SQL Server que contiene un número de bases de datos muy grandes.

El lunes, se habilita la copia de seguridad automatizada v2 con hello después de configuración:

- Programación de copia de seguridad: **Manual**
- Frecuencia de copia de seguridad completa: **Semanal**
- Hora de inicio de copia de seguridad completa: **01:00**
- Período de tiempo de copia de seguridad completa: **1 hora**

Esto significa que esa ventana de copia de seguridad de disponible siguiente de hello es el martes a la 1 A.M. durante una hora. En ese momento, la copia de seguridad empieza a realizar copias de seguridad de las bases de datos una a una. En este escenario, las bases de datos son lo suficientemente grandes como para que se completarán copias de seguridad completas de bases de datos primera par Hola. Sin embargo, después de una hora no todas las bases de datos de hello todavía ha realizado ninguna.

Cuando esto sucede, copia de seguridad automatizada comenzará la copia de seguridad de hello restantes Hola de bases de datos día siguiente, el miércoles a la 1 A.M. durante una hora. Si no todas las bases de datos se ha hecho en ese momento, lo intentará de nuevo Hola día siguiente en hello mismo tiempo. Se aplica este mismo comportamiento hasta que se realiza correctamente la copia de seguridad de todas las bases de datos.

Cuando vuelve a llegar el martes, la copia de seguridad automatizada empieza de nuevo a realizar la copia de seguridad de todas las bases de datos.

Este escenario muestra que la copia de seguridad automatizada solo funcionará en el período de tiempo especificado de Hola y cada base de datos se copiarán una vez por semana. Esto también muestra que es posible para las copias de seguridad toospan varios días en hello caso donde no es posible toocomplete todas las copias de seguridad en un solo día.

### <a name="scenario-2-daily-backups"></a>Escenario 2: Copias de seguridad diarias
Tiene una VM con SQL Server que contiene un número de bases de datos muy grandes.

El lunes, se habilita la copia de seguridad automatizada v2 con hello después de configuración:

- Programación de copia de seguridad: Manual
- Frecuencia de copia de seguridad completa: Diaria
- Hora de inicio de copia de seguridad completa: 22:00
- Período de tiempo de copia de seguridad completa: 6 horas

Esto significa que esa ventana de copia de seguridad de disponible siguiente de hello es el lunes a las 10 P.M. durante 6 horas. En ese momento, la copia de seguridad empieza a realizar copias de seguridad de las bases de datos una a una.

Posteriormente, se vuelve a realizar la copia de seguridad completa de todas las bases de datos el martes a las 22:00 horas durante seis horas.

> [!IMPORTANT]
> Al programar copias de seguridad diarias, se recomienda que programe un tooensure de ventana de tiempo de ampliación todas las bases de datos pueden se copia en este momento. Esto es especialmente importante en caso de hello donde haya una gran cantidad de datos tooback seguridad.

## <a name="configuration-in-hello-portal"></a>Configuración de hello Portal

Puede usar hello tooconfigure portal Azure copia de seguridad automatizada v2 durante el aprovisionamiento o para SQL Server 2016 las máquinas virtuales existentes.

### <a name="new-vms"></a>Nuevas máquinas virtuales

Utilice hello tooconfigure portal Azure copia de seguridad automatizada v2 cuando se crea una nueva máquina Virtual de SQL Server 2016 en el modelo de implementación del Administrador de recursos de Hola. 

Hola **configuración de SQL Server** hoja, seleccione **copia de seguridad automatizada**. Hello siguiente captura de pantalla de portal Azure muestra hello **copia de seguridad automatizada de SQL** hoja.

![Configuración de Copia de seguridad automatizada de SQL en Azure Portal](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> Copia de seguridad automatizada v2 está deshabilitada de forma predeterminada.

Para el contexto, vea el tema completo de hello en [aprovisionar una máquina virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Máquinas virtuales existentes

Para las máquinas virtuales de SQL Server existentes, seleccione su máquina virtual de SQL Server. A continuación, seleccione hello **configuración de SQL Server** sección de hello **configuración** hoja.

![Copia de seguridad automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

Hola **configuración de SQL Server** hoja, haga clic en hello **editar** botón Hola automatizada sección copia de seguridad.

![Configuración de Copia de seguridad automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

Cuando termine, haga clic en hello **Aceptar** botón en la parte inferior de Hola de hello **configuración de SQL Server** toosave hoja los cambios.

Si va a habilitar copia de seguridad automatizada para hello primera vez, Azure configura Hola agente de IaaS de SQL Server en segundo plano de Hola. Durante este tiempo, Hola portal de Azure es posible que no muestre que está configurada la copia de seguridad automatizada. Espere unos minutos para hello toobe de agente instalado, configurado. Después de ese hello Azure portal reflejará nueva configuración de Hola.

## <a name="configuration-with-powershell"></a>Configuración con PowerShell

Puede usar PowerShell tooconfigure v2 de copia de seguridad automatizada. Antes de comenzar:

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
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

Si el resultado muestra que **habilitar** se establece demasiado**False**, tendrá que tooenable la copia de seguridad automatizada. Hello buenas noticias son que habilitar y configurar la copia de seguridad automatizada en hello igual. Consulte la sección siguiente de hello esta información.

> [!NOTE] 
> Si comprobar la configuración de hello inmediatamente después de realizar un cambio, es posible que se pondrá en contacto valores de configuración anteriores Hola. Espere unos minutos y compruebe la configuración de hello nuevo toomake seguro de que se han aplicado los cambios.

### <a name="configure-automated-backup-v2"></a>Configuración de Copia de seguridad automatizada v2
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

A continuación, usar hello **New-AzureRmVMSqlServerAutoBackupConfig** tooenable de comandos y configurar las copias de seguridad de copia de seguridad automatizada v2 Hola configuración toostore en la cuenta de almacenamiento de Azure Hola. En este ejemplo, las copias de seguridad de Hola se establecen toobe conserva de 10 días. Las copias de seguridad de las bases de datos del sistema están habilitadas. Las copias de seguridad completas están programadas semanalmente con un período de tiempo que empieza a las 20:00 horas y dura dos horas. Las copias de seguridad de registros están programadas para que se realicen cada 30 minutos. Hola segundo comando **AzureRmVMSqlServerExtension conjunto**, Hola actualizaciones especificado VM de Azure con esta configuración.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

Podría tardar varios tooinstall minutos y configure Hola agente de IaaS de SQL Server. 

cifrado de tooenable, modificar Hola Hola de toopass de secuencia de comandos anterior **EnableEncryption** parámetro junto con una contraseña (cadena segura) para hello **CertificatePassword** parámetro. Hola siguiente script habilita la configuración de copia de seguridad automatizada de hello en el ejemplo anterior de Hola y agrega el cifrado.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

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
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

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
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Pasos siguientes
Copia de seguridad automatizada v2 configura Copia de seguridad administrada en máquinas virtuales de Azure. Por lo que es importante[revisar la documentación de Hola para copia de seguridad administrada](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Hola comportamiento e implicaciones.

Puede encontrar la copia de seguridad adicional y restaurar guía para SQL Server en máquinas virtuales de Azure en hello tema siguiente: [de copia de seguridad y restauración para SQL Server en máquinas virtuales Azure](virtual-machines-windows-sql-backup-recovery.md).

Para más información acerca de otras tareas de automatización disponibles, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Para más información sobre cómo ejecutar SQL Server en máquinas virtuales de Azure, consulte [Introducción a SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).

