---
title: 'copia de seguridad: usar PowerShell tooback seguridad cargas de trabajo DPM aaaAzure | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toodeploy y administrar copias de seguridad de Azure para Data Protection Manager (DPM) con PowerShell"
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a>Implementar y administrar tooAzure copia de seguridad de los servidores de Data Protection Manager (DPM) mediante PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Clásico](backup-dpm-automation-classic.md)
>
>

Este artículo muestra cómo toouse PowerShell toosetup copia de seguridad de Azure en un servidor DPM y toomanage copia de seguridad y recuperación.

## <a name="setting-up-hello-powershell-environment"></a>Configurar el entorno de PowerShell de Hola
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Antes de realizar copias de seguridad de PowerShell toomanage desde tooAzure de Data Protection Manager, necesita toohave entorno derecho con hello en PowerShell. En el inicio de Hola Hola de sesión de PowerShell, asegúrese de que ejecute hello después módulos derecho de comando tooimport hello y le permiten toocorrectly referencia Hola DPM cmdlets:

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a>Instalación y registro
toobegin:

1. [Descargue la última versión de PowerShell](https://github.com/Azure/azure-powershell/releases) (la versión mínima necesaria es: 1.0.0).
2. Habilitar los cmdlets de copia de seguridad de Azure de hello cambiando demasiado*AzureResourceManager* modo mediante el uso de hello **Switch-AzureMode** commandlet:

```
PS C:\> Switch-AzureMode AzureResourceManager
```

Hello siguiente configuración y tareas de registro pueden automatizarse con PowerShell:

* Creación de un almacén de Recovery Services
* Instalar el agente de copia de seguridad de Azure Hola
* Registrar con hello servicio de copia de seguridad de Azure
* Configuración de redes
* Configuración de cifrado

## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Servicios de recuperación
Hola pasos le guiará en el proceso de creación de un almacén de servicios de recuperación. Un almacén de Servicios de recuperación no es lo mismo que un almacén de copia de seguridad.

1. Si utilizas Azure Backup para hello primera vez, debe usar hello **AzureRMResourceProvider Register** cmdlet tooregister el proveedor de servicios de recuperación de Azure de hello con su suscripción.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hola almacén de servicios de recuperación es un recurso ARM, por lo que necesita tooplace dentro de un grupo de recursos. Puede usar un grupo de recursos existente o crear uno nuevo. Al crear un nuevo grupo de recursos, especifique el nombre de Hola y ubicación para el grupo de recursos de Hola.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Hola de uso **AzureRmRecoveryServicesVault New** cmdlet toocreate un nuevo almacén. Asegúrese de toospecify Hola misma ubicación para el almacén de Hola que utilizó para el grupo de recursos de Hola.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Especificar tipo de Hola de toouse de redundancia de almacenamiento; Puede usar [almacenamiento redundante local (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [almacenamiento con redundancia geográfica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Hello en el ejemplo siguiente se muestra hello - BackupStorageRedundancy opción testVault está establecida tooGeoRedundant.

   > [!TIP]
   > Muchos de los cmdlets de copia de seguridad de Azure requieren el objeto de almacén de servicios de recuperación de hello como entrada. Por este motivo, resulta toostore conveniente Hola el objeto de almacén de servicios de recuperación de copia de seguridad en una variable.
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a>Almacenes de Hola de vista en una suscripción
Use **AzureRmRecoveryServicesVault Get** tooview lista de Hola de todos los almacenes en la suscripción actual de Hola. Puede usar este toocheck de comando que se ha creado un nuevo almacén o toosee qué almacenes están disponibles en la suscripción de Hola.

Ejecutar comandos de hello, Get-AzureRmRecoveryServicesVault, y se muestran todos los almacenes de suscripción de Hola.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a>Instalar el agente de copia de seguridad de Azure de hello en un servidor DPM
Antes de instalar el agente de copia de seguridad de Azure de hello, necesita a instalador de hello toohave descargado y presente en hello Windows Server. Puede obtener última versión del instalador de Hola de Hola de hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o desde la página del panel del almacén de servicios de recuperación de Hola. Guardar instalador hello tooan ubicación fácilmente accesible como * C:\Downloads\*.

agente de hello tooinstall, ejecute el siguiente comando en una consola de PowerShell con privilegios elevados de Hola **en el servidor DPM Hola**:

```
PS C:\> MARSAgentInstaller.exe /q
```

Agente de Hola se instala con todas las opciones predeterminadas de Hola. instalación de Hello tarda unos minutos en segundo plano de Hola. Si no se especifica hello */nu* Hola opción **Windows Update** se abre la ventana final Hola de hello toocheck de instalación para las actualizaciones.

agente de Hello aparece en la lista de Hola de programas instalados. lista de hello toosee de programas instalados, vaya demasiado**el Panel de Control** > **programas** > **programas y características**.

![Agente instalado](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Opciones de instalación
toosee todas las opciones de hello disponibles a través de hello commandline, Hola de uso después de comando:

```
PS C:\> MARSAgentInstaller.exe /?
```

Hola las opciones disponibles incluyen:

| Opción | Detalles | Valor predeterminado |
| --- | --- | --- |
| /q |Instalación silenciosa |- |
| /p:"ubicación" |Carpeta de instalación de toohello de ruta de acceso para el agente de copia de seguridad de Azure Hola. |C:\Archivos de programa\Microsoft Azure Recovery Services Agent |
| /s:"ubicación" |Carpeta de caché de ruta de acceso toohello para el agente de copia de seguridad de Azure Hola. |C:\Archivos de programa\Microsoft Azure Recovery Services Agent\Scratch |
| /m |Participación en tooMicrosoft actualización |- |
| /nu |No busca actualizaciones una vez completada la instalación |- |
| /d |Desinstala el agente de Microsoft Azure Recovery Services. |- |
| /ph |Dirección host del proxy |- |
| /po |Número de puerto del host de proxy |- |
| /pu |Nombre de usuario del host de proxy |- |
| /pw |Contraseña de proxy |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a>Registrar tooa almacén de servicios de recuperación DPM
Una vez creado el almacén de servicios de recuperación de hello, descargar agente más reciente de Hola y las credenciales de almacén de Hola y almacenarlo en una ubicación adecuada como C:\Downloads.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

En el servidor DPM hello, ejecute hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) máquina de hello tooregister de cmdlet con el almacén de Hola.

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a>Opciones de configuración inicial
Una vez Hola servidor DPM está registrado con hello del almacén de servicios de recuperación, se inicia con la configuración de la suscripción de forma predeterminada. Estas opciones de suscripción incluyen hello área de almacenamiento provisional, cifrado y las redes. configuración de la suscripción de toochange necesita toofirst obtener un identificador de configuración (valor predeterminado) actual hello mediante hello [DPMCloudSubscriptionSetting Get](https://technet.microsoft.com/library/jj612793) cmdlet:

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

Todas las modificaciones son objeto de PowerShell local realiza toothis ```$setting``` y, a continuación, objetos hello es confirmada tooDPM y toosave de copia de seguridad de Azure mediante hello [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet. Necesita hello toouse ```–Commit``` tooensure de marca que Hola cambios se conservan. configuración de Hello no se aplican y se usará copia de seguridad de Azure a menos que se confirma.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a>Redes
Si la conectividad de Hola de hello DPM máquina toohello servicio de copia de seguridad de Azure en hello internet es a través de un servidor proxy, configuración del servidor proxy Hola debe proporcionarse para copias de seguridad correctas. Esto se realiza mediante hello ```-ProxyServer```y ```-ProxyPort```, ```-ProxyUsername``` hello y ```ProxyPassword``` parámetros con hello [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet. En este ejemplo, no hay ningún servidor proxy y por tanto se borra explícitamente cualquier información relacionada con el proxy.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

También se puede controlar el uso de ancho de banda con opciones de ```-WorkHourBandwidth``` y ```-NonWorkHourBandwidth``` para un conjunto determinado de días de la semana de Hola. En este ejemplo no se define ninguna limitación.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a>Configuración de área de almacenamiento provisional de Hola
agente de copia de seguridad de Azure Hola ejecutando en el servidor DPM Hola necesita almacenamiento temporal para los datos restaurados desde la nube de hello (área de almacenamiento provisional local). Configurar el área de ensayo de hello mediante hello [conjunto DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet hello y ```-StagingAreaPath``` parámetro.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

En el ejemplo de Hola anterior, área de almacenamiento provisional de Hola se establecerá demasiado*C:\StagingArea* en el objeto de PowerShell de hello ```$setting```. Asegúrese de que ya existe la carpeta especificada de hello, o bien se producirá un error en la confirmación final de Hola de configuración de la suscripción de Hola.

### <a name="encryption-settings"></a>Configuración de cifrado
Hola copia de seguridad de datos enviados tooAzure copia de seguridad es cifrada tooprotect Hola confidencialidad de datos de Hola. Hola frase de contraseña es datos de contraseña"hello" toodecrypt hello en tiempo de Hola de restauración. Importante tookeep esta información es segura para y proteger una vez que se establece.

En el siguiente ejemplo de Hola, primer comando de hello convierte la cadena de hello ```passphrase123456789``` tooa segura cadena y asigna Hola segura toohello variable de cadena denominada ```$Passphrase```. Hola segundo comando establece cadena segura de hello ```$Passphrase``` como contraseña de Hola para cifrar las copias de seguridad.

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Almacenar información de la frase de contraseña de hello seguro y protegido una vez que se establece. No será capaz de toorestore datos de Azure sin esta frase de contraseña.
>
>

En este punto, debería haber realizado todas las Hola requiere cambios toohello ```$setting``` objeto. Recuerde los cambios de hello toocommit.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a>Proteger datos tooAzure copia de seguridad
En esta sección, agregará un tooDPM del servidor de producción y, a continuación, proteger el almacenamiento DPM de hello datos toolocal y, a continuación, tooAzure copia de seguridad. En los ejemplos de hello, demostraremos cómo tooback seguridad de archivos y carpetas. Hello lógica puede fácilmente ser extendido toobackup cualquier origen de datos compatibles con DPM. Las copias de seguridad de DPM se rigen por un grupo de protección (PG) con cuatro partes:

1. **Miembros del grupo** es una lista de todos los objetos que se pueden proteger de hello (también conocido como *orígenes de datos* en DPM) que desea tooprotect Hola mismo grupo de protección. Por ejemplo, puede que desee tooprotect producción máquinas virtuales en un grupo de protección y las bases de datos de SQL Server en otro grupo de protección como pueden tener distintos requisitos de copia de seguridad. Antes de hacer copias de seguridad ningún origen de datos en un servidor de producción debe toomake seguro Hola agente de DPM está instalado en el servidor de Hola y administrado por DPM. Siga los pasos de Hola para [instalar Hola agente DPM](https://technet.microsoft.com/library/bb870935.aspx) y vinculándolo toohello adecuados en el servidor DPM.
2. **Método de protección de datos** especifica ubicaciones Hola destino de copia de seguridad - cinta y disco, en la nube. En nuestro ejemplo protegemos datos toohello local disco y toohello en la nube.
3. A **programar copia de seguridad** que especifica si las copias de seguridad necesitan toobe realizada y con qué frecuencia hello datos se sincronicen entre Hola servidor DPM y el servidor de producción de hello.
4. A **programación de retención** que especifica cuánto tiempo los puntos de recuperación de hello tooretain en Azure.

### <a name="creating-a-protection-group"></a>Creación de un grupo de protección
Empiece por crear un nuevo grupo de protección mediante hello [DPMProtectionGroup New](https://technet.microsoft.com/library/hh881722) cmdlet.

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

Hola anteriormente cmdlet creará un grupo de protección denominado *ProtectGroup01*. También es posible modificar un grupo de protección posterior toohello de copia de seguridad de tooadd nube de Azure. Sin embargo, toomake cambios toohello grupo de protección: nuevos o existentes - necesitamos tooget un identificador en un *modificable* objeto mediante hello [DPMModifiableProtectionGroup Get](https://technet.microsoft.com/library/hh881713) cmdlet.

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a>Agregar miembros de grupo toohello grupo de protección
Cada agente de DPM sabe lista Hola de orígenes de datos en el servidor de Hola que se instala en. tooadd un grupo de protección de toohello de origen de datos, Hola agente DPM necesidades toofirst envíe una lista del servidor DPM de hello orígenes de datos back-toohello. Uno o más orígenes de datos no están seleccionado y agregado toohello grupo de protección. pasos de PowerShell de Hello necesitan tooachieve esto son:

1. Capturar una lista de todos los servidores administrados por DPM a través de hello agente DPM.
2. Elija un servidor específico.
3. Capturar una lista de todos los orígenes de datos en el servidor de Hola.
4. Elija uno o más orígenes de datos y agregarlas toohello grupo de protección

Hola lista de servidores en qué Hola agente de DPM está instalado y se está administrando mediante Hola servidor DPM se adquirió con hello [DPMProductionServer Get](https://technet.microsoft.com/library/hh881600) cmdlet. En este ejemplo se van a filtrar y configurar solo PS con el nombre *productionserver01* para efectuar una copia de seguridad.

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

Ahora buscar de la lista de Hola de orígenes de datos ```$server``` con hello [DPMDatasource Get](https://technet.microsoft.com/library/hh881605) cmdlet. En este ejemplo se filtra para el volumen de Hola * D:\* que deseamos tooconfigure para copia de seguridad. Este origen de datos, a continuación, se agrega toohello grupo de protección mediante hello [DPMChildDatasource agregar](https://technet.microsoft.com/library/hh881732) cmdlet. Recuerde hello toouse *modificable* objeto de grupo de protección ```$MPG``` adiciones de hello toomake.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Repita este paso tantas veces como sea necesario, hasta que haya agregado todos los Hola elegido el grupo de protección de toohello de orígenes de datos. También puede comenzar con un solo origen de datos y flujo de trabajo de hello completa para crear el grupo de protección de Hola y en un momento posterior, agregar más orígenes de datos toohello grupo de protección.

### <a name="selecting-hello-data-protection-method"></a>Seleccionar método de protección de datos de hello
Una vez que se agregaron a orígenes de datos de hello toohello grupo de protección, Hola siguiente paso es método de protección de hello toospecify con hello [DPMProtectionType conjunto](https://technet.microsoft.com/library/hh881725) cmdlet. En este ejemplo, hello grupo de protección está configurado para el disco local y copia de seguridad en la nube. También necesita toospecify Hola datasource que desea toocloud tooprotect con hello [DPMChildDatasource agregar](https://technet.microsoft.com/library/hh881732.aspx) cmdlet con - marcador en línea.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a>Establecer la duración de retención de Hola
Establecer retención de Hola para puntos de copia de seguridad de hello mediante hello [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet. Pese a que podría parecer retención de hello tooset impar para definir programación de copia de seguridad de hello, con hello ```Set-DPMPolicyObjective``` cmdlet establece automáticamente una programación de copia de seguridad predeterminada que se pueden modificar. Siempre es programar copia de seguridad de tooset posible Hola por primera vez y Hola directiva de retención después.

En el siguiente ejemplo de Hola, Hola establece los parámetros de retención de Hola para copias de seguridad de disco. Esto conservarán las copias de seguridad de 10 días y sincronizar los datos cada 6 horas entre el servidor de producción de hello y el servidor DPM Hola. Hola ```SynchronizationFrequencyMinutes``` no se define con qué frecuencia se crea un punto de copia de seguridad, pero ¿cómo a menudo los datos están el servidor DPM toohello copiada.  Esto evita que las copias de seguridad se vuelvan demasiado grandes.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

Para copias de seguridad que se va tooAzure (DPM hace referencia toothem como copias de seguridad en línea) se pueden configurar intervalos de retención de Hola para [utilizando un esquema de su Abuelo-padre-hijo (GFS) de retención a largo plazo](backup-azure-backup-cloud-as-tape.md). Es decir, puede definir una directiva de retención combinada que implique directivas de retención diaria, semanal, mensual y anual. En este ejemplo, se crea una matriz que representa el esquema de retención complejos de Hola que queremos y, a continuación, configurar la duración de retención de hello mediante hello [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet.

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a>Programación de copia de seguridad de hello establecida
DPM establece una programación de copia de seguridad predeterminada automáticamente si se especifica el objetivo de protección de hello mediante hello ```Set-DPMPolicyObjective``` cmdlet. toochange las programaciones predeterminadas hello, usar hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet seguido por hello [DPMPolicySchedule conjunto](https://technet.microsoft.com/library/hh881723) cmdlet.

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

Hola por encima de ejemplo, ```$onlineSch``` es una matriz con cuatro elementos que contiene la programación de protección en línea existente de Hola de hello grupo de protección en el esquema GFS hello:

1. ```$onlineSch[0]```contiene las programaciones diarias Hola
2. ```$onlineSch[1]```contiene las programaciones semanales Hola
3. ```$onlineSch[2]```contiene la programación mensual Hola
4. ```$onlineSch[3]```contiene la programación anual Hola

Por ello, si necesita programación semanal de toomodify hello, debe toorefer toohello ```$onlineSch[1]```.

### <a name="initial-backup"></a>Copia de seguridad inicial
Cuando copia de seguridad de un origen de datos para hello primera vez, DPM necesidades crea réplica inicial que crea una copia completa de hello toobe de origen de datos protegido en el volumen de réplica DPM. Esta actividad puede programarse para una hora específica o puede desencadenar manualmente, mediante hello [conjunto DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet con el parámetro hello ```-NOW```.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a>Cambiar el tamaño de Hola de réplica de DPM y el volumen de punto de recuperación
También puede cambiar tamaño de hello del volumen de réplica de DPM y el uso del volumen de instantánea [DPMDatasourceDiskAllocation conjunto](https://technet.microsoft.com/library/hh881618.aspx) cmdlet como en el siguiente ejemplo de Hola: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manual - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)

### <a name="committing-hello-changes-toohello-protection-group"></a>Confirmar Hola cambia toohello grupo de protección
Por último, cambios de hello necesitan toobe confirmado antes de que DPM puede realizar la copia de seguridad de Hola por la configuración del nuevo grupo de protección de Hola. Esto puede lograrse mediante hello [DPMProtectionGroup conjunto](https://technet.microsoft.com/library/hh881758) cmdlet.

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a>Ver los puntos de copia de seguridad Hola
Puede usar hello [DPMRecoveryPoint Get](https://technet.microsoft.com/library/hh881746) cmdlet tooget una lista de todos los puntos de recuperación para un origen de datos. En este ejemplo, se realiza lo siguiente:

* captura todas Hola documento en el servidor DPM hello y almacenados en una matriz```$PG```
* obtener toohello correspondiente de hello orígenes de datos```$PG[0]```
* obtener todos los puntos de recuperación de Hola para un origen de datos.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Restauración de datos protegidos en Azure
Restauración de datos es una combinación de un objeto ```RecoverableItem``` y un objeto ```RecoveryOption```. En la sección anterior de hello, que obtuvimos una lista de puntos de copia de seguridad de Hola para un origen de datos.

En el ejemplo de Hola siguiente, se muestran la máquina virtual de Hyper-V toorestore de copia de seguridad de Azure puntos de copia de seguridad de combinación con hello de destino para la recuperación. Este ejemplo incluye:

* Crear una opción de recuperación utilizando hello [DPMRecoveryOption New](https://technet.microsoft.com/library/hh881592) cmdlet.
* Obteniendo Hola matriz de copia de seguridad puntos con hello ```Get-DPMRecoveryPoint``` cmdlet.
* Elegir un toorestore de punto de copia de seguridad de.

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

comandos de Hola se pueden extender con facilidad para cualquier tipo de origen de datos.

## <a name="next-steps"></a>Pasos siguientes
* Para obtener más información acerca de DPM vea tooAzure copia de seguridad [Introducción tooDPM copia de seguridad](backup-azure-dpm-introduction.md)
