---
title: aaaUse tooback de PowerShell de Windows Server tooAzure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodeploy y administrar copias de seguridad de Azure con PowerShell"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a>Implementar y administrar tooAzure copia de seguridad para el cliente de Windows del servidor de Windows con PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-client-automation.md)
> * [Clásico](backup-client-automation-classic.md)
>
>

Este artículo muestra cómo toouse PowerShell para configurar Azure copia de seguridad en Windows Server o un cliente de Windows y administrar copias de seguridad y recuperación.

## <a name="install-azure-powershell"></a>Azure PowerShell
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

En este artículo se centra en hello Azure Resource Manager (ARM) y Hola cmdlets de PowerShell de copia de seguridad en línea de MS que permiten toouse un almacén de servicios de recuperación de un grupo de recursos.

En octubre de 2015, se lanzó Azure PowerShell 1.0. Esta versión se realizó correctamente la versión de Hola 0.9.8 e imperiosa algunos cambios importantes, especialmente en el patrón de nomenclatura de Hola de cmdlets de Hola. 1.0 seguimiento cmdlets Hola patrón de nomenclatura {verbo}-AzureRm {nombre}; mientras que no incluyen nombres de hello 0.9.8 **Rm** (por ejemplo, New-AzureRmResourceGroup en lugar de New-AzureResourceGroup). Al usar Azure PowerShell 0.9.8, primero debe habilitar el modo de administrador de recursos de hello ejecutando hello **Switch-AzureMode AzureResourceManager** comando. Este comando no es necesario en la versión 1.0 o posteriores.

Si desea que toouse los scripts escritos para el entorno de hello 0.9.8, en Hola 1.0 o posterior entorno, debe actualizar cuidadosamente y probar scripts de hello en un entorno de preproducción antes de usarlos en producción tooavoid impacto inesperado.

[Descargar la versión más reciente de PowerShell de hello](https://github.com/Azure/azure-powershell/releases) (versión mínima necesaria es: 1.0.0)

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Servicios de recuperación
Hola pasos le guiará en el proceso de creación de un almacén de servicios de recuperación. Un almacén de Servicios de recuperación no es lo mismo que un almacén de copia de seguridad.

1. Si utilizas Azure Backup para hello primera vez, debe usar hello **AzureRMResourceProvider Register** cmdlet tooregister el proveedor de servicios de recuperación de Azure de hello con su suscripción.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hola almacén de servicios de recuperación es un recurso ARM, por lo que necesita tooplace dentro de un grupo de recursos. Puede usar un grupo de recursos existente o crear uno nuevo. Al crear un nuevo grupo de recursos, especifique el nombre de Hola y ubicación para el grupo de recursos de Hola.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. Hola de uso **AzureRmRecoveryServicesVault New** nuevo almacén de cmdlet toocreate Hola. Asegúrese de toospecify Hola misma ubicación para el almacén de Hola que utilizó para el grupo de recursos de Hola.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
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

Ejecute el comando de hello, **AzureRmRecoveryServicesVault Get**, y se muestran todos los almacenes de suscripción de Hola.

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


## <a name="installing-hello-azure-backup-agent"></a>Instalar el agente de copia de seguridad de Azure Hola
Antes de instalar el agente de copia de seguridad de Azure de hello, necesita a instalador de hello toohave descargado y presente en hello Windows Server. Puede obtener última versión del instalador de Hola de Hola de hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o desde la página del panel del almacén de servicios de recuperación de Hola. Guardar instalador hello tooan ubicación fácilmente accesible como * C:\Downloads\*.

O bien, use descargador de hello tooget de PowerShell:
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

agente de hello tooinstall, ejecute el siguiente comando en una consola de PowerShell con privilegios elevados de Hola:

```
PS C:\> MARSAgentInstaller.exe /q
```

Agente de Hola se instala con todas las opciones predeterminadas de Hola. instalación de Hello tarda unos minutos en segundo plano de Hola. Si no se especifica hello */nu* opción, a continuación, hello **Windows Update** se abrirá la ventana final Hola de hello toocheck de instalación para las actualizaciones. Una vez instalado, agente de Hola se mostrará en la lista de Hola de programas instalados.

lista de hello toosee de programas instalados, vaya demasiado**el Panel de Control** > **programas** > **programas y características**.

![Agente instalado](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Opciones de instalación
toosee todas las opciones disponibles a través de Hola Hola de línea de comandos, utilice Hola siguiente comando:

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

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a>El registro de Windows Server o Windows cliente máquina tooa almacén de servicios de recuperación
Una vez creado el almacén de servicios de recuperación de hello, descargar agente más reciente de Hola y las credenciales de almacén de Hola y almacenarlo en una ubicación adecuada como C:\Downloads.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

En Windows Server de Hola o equipo cliente de Windows, ejecute hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) máquina de hello tooregister de cmdlet con el almacén de Hola.
Este y otros cmdlets para copias de seguridad, son del módulo MSONLINE de hello qué Hola instalador de agente de Mars se agrega como parte del proceso de instalación de Hola. 

instalador de agente de Hello no actualiza Hola $Env: variable PSModulePath. Esto significa que se produce un error en la carga automática del módulo. tooresolve Esto puede hacer siguiente hello:

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

O bien, puede cargar manualmente el módulo de hello en el script como se indica a continuación:

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

Una vez que carga los cmdlets de copia de seguridad en línea hello, registre las credenciales de almacén de hello:


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> No utilice el archivo de credenciales de almacén de rutas de acceso relativas toospecify Hola. Debe proporcionar una ruta de acceso absoluta como un cmdlet de entrada toohello.
>
>

## <a name="networking-settings"></a>Configuración de redes
Cuando la conectividad de Hola de hello Windows máquina toohello que Internet es a través de un servidor proxy, configuración de proxy de hello también puede proporcionarse a toohello agente. En este ejemplo, no hay ningún servidor proxy y por tanto se borra explícitamente cualquier información relacionada con el proxy.

Uso de ancho de banda también puede controlarse con opciones de Hola de ```work hour bandwidth``` y ```non-work hour bandwidth``` para un conjunto determinado de días de la semana de Hola.

Establecer detalles de servidor proxy y el ancho de banda de Hola se realiza mediante hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a>Configuración de cifrado
Hola copia de seguridad de datos enviados tooAzure copia de seguridad es cifrada tooprotect Hola confidencialidad de datos de Hola. Hola frase de contraseña es datos de contraseña"hello" toodecrypt hello en tiempo de Hola de restauración.

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> Almacenar información de la frase de contraseña de hello seguro y protegido una vez que se establece. No se pueden toorestore capaz de datos de Azure sin esta frase de contraseña.
>
>

## <a name="back-up-files-and-folders"></a>Realizar copias de seguridad de archivos y carpetas
Todas las copias de seguridad de clientes y servidores de Windows tooAzure copia de seguridad se rigen por una directiva. Directiva de Hello consta de tres partes:

1. A **programar copia de seguridad** que especifica si las copias de seguridad necesitan toobe realizada y se sincronice con el servicio de Hola.
2. A **programación de retención** que especifica cuánto tiempo los puntos de recuperación de hello tooretain en Azure.
3. Una **especificación de inclusión o exclusión de archivo** que determina los elementos de los que se debe efectuar una copia de seguridad.

En este documento, dado que se está automatizando la copia de seguridad, supondremos que no se ha configurado nada. Comenzamos creando una nueva directiva de copia de seguridad mediante hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.

```
PS C:\> $newpolicy = New-OBPolicy
```

En este Hola tiempo directiva está vacía y otros cmdlets están toodefine necesario qué elementos se pueden incluir o excluir, cuando las copias de seguridad se ejecuta y Hola donde se almacenarán las copias de seguridad.

### <a name="configuring-hello-backup-schedule"></a>Configuración de programación de copia de seguridad de Hola
Hola primero de hello 3 partes de una directiva es la programación de copia de seguridad hello, que se crea utilizando hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet. programación de copia de seguridad de Hello define cuándo las copias de seguridad necesitan toobe realizada. Al crear una programación tiene parámetros de entrada de toospecify 2:

* **Días de la semana de hello** debe ejecutar esa copia de seguridad de Hola. Puede ejecutar el trabajo de copia de seguridad de hello en sólo un día o cada día de semana de Hola o cualquier combinación de entre.
* **Horas del día de hello** cuándo se debe ejecutar copia de seguridad de Hola. Puede definir una too3 diferentes horas del día de hello cuando se activará la copia de seguridad de Hola.

Por ejemplo, podría configurar una directiva de copia de seguridad que se ejecute a las 4 p.m. cada sábado y domingo.

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

programación de copia de seguridad de Hello necesita toobe asociado a una directiva, y esto puede lograrse mediante el uso de hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a>Configuración de una directiva de retención
Directiva de retención de Hello define cuánto tiempo de recuperación se conservan los puntos creados a partir de los trabajos de copia de seguridad. Al crear una nueva directiva de retención mediante hello [OBRetentionPolicy New](https://technet.microsoft.com/library/hh770425) cmdlet, puede especificar el número de Hola de días que Hola puntos de recuperación de copia de seguridad necesita toobe conservan con copia de seguridad de Azure. ejemplo de Hola siguiente establece una directiva de retención de 7 días.

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

Hello directiva de retención debe estar asociada con la directiva principal hello mediante el cmdlet de hello [OBRetentionPolicy conjunto](https://technet.microsoft.com/library/hh770405):

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a>Incluir y excluir archivos toobe copia de seguridad
Un ```OBFileSpec``` objeto define hello toobe de archivos incluidos y excluidos de una copia de seguridad. Se trata de un conjunto de reglas que ámbito out Hola proteger archivos y carpetas en un equipo. Puede tener tantas reglas de inclusión o exclusión de archivos como se necesiten y asociarlas con una directiva. Al crear un nuevo objeto OBFileSpec, puede:

* Especificar hello toobe de archivos y carpetas incluido
* Especificar hello toobe de archivos y carpetas excluido
* Especifique recursiva copia de seguridad de datos en una carpeta (o) si deben respaldar solo Hola archivos de nivel superior en la carpeta especificada de hello hasta.

Hola este último se logra mediante la marca de - no recursivas de hello en el comando New-OBFileSpec Hola.

En el siguiente ejemplo de Hola, comenzaremos hacer una copia de volumen C: y D: y excluir los archivos binarios de sistema operativo de hello en la carpeta de Windows hello y las carpetas temporales. toodo por lo que vamos a crear dos especificaciones de archivo mediante hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet: uno para la inclusión y uno para su exclusión. Una vez que se han creado las especificaciones de archivo hello, está asociados con la directiva de hello mediante hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a>Aplicar una directiva de Hola
Ahora el objeto de directiva de hello está finalizado y tiene una programación de copia de seguridad asociada, directiva de retención y una lista de inclusión/exclusión de archivos. Ahora se puede confirmar para copia de seguridad de Azure toouse esta directiva. Antes de aplicar Hola recién creado directiva asegurarse de que no hay ninguna directiva de copia de seguridad existente asociada con el servidor de hello mediante hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet. Quitar la directiva de hello le pedirá confirmación. confirmación de hello tooskip usar hello ```-Confirm:$false``` marca con el cmdlet de Hola.

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

Objeto de directiva de hello confirmación se realiza mediante hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet. Esto también requerirá confirmación. confirmación de hello tooskip usar hello ```-Confirm:$false``` marca con el cmdlet de Hola.

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

Puede ver los detalles de Hola de directiva de copia de seguridad existente de hello mediante hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet. Puede desplazarse mediante hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet para programar copia de seguridad de Hola y Hola [OBRetentionPolicy Get](https://technet.microsoft.com/library/hh770427) cmdlet para las directivas de retención de Hola

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a>Realización de una copia de seguridad ad-hoc
Una vez que se ha establecido una directiva de copia de seguridad realizar copias de seguridad de hello según la programación de Hola. También es posible usar Hola desencadenar una copia de seguridad de ad-hoc [OBBackup inicio](https://technet.microsoft.com/library/hh770426) cmdlet:

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a>Restaurar datos de Azure Backup
En esta sección le guiará a través de los pasos de Hola para automatizar la recuperación de datos de copia de seguridad de Azure. Hacerlo implica Hola pasos:

1. Seleccione el volumen de origen de Hola
2. Elija un toorestore de punto de copia de seguridad
3. Elija un elemento toorestore
4. Proceso de restauración de Hola de desencadenador

### <a name="picking-hello-source-volume"></a>Seleccionar volumen de origen de Hola
En orden toorestore un elemento de la copia de seguridad de Azure, primero debe origen de hello tooidentify de elemento de Hola. Porque nos estamos ejecutando comandos de hello en contexto de Hola de un servidor de Windows o un cliente de Windows, ya se ha identificado máquina Hola. Hola siguiente paso para identificar el origen de hello es volumen de hello tooidentify que lo contiene. Una lista de volúmenes u orígenes haciendo copias de seguridad de este equipo se puede recuperar mediante la ejecución de hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet. Este comando devuelve una matriz de todos los orígenes de Hola de este cliente/servidor de copia de seguridad.

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-toorestore"></a>Elección de un punto de copia de seguridad de qué toorestore
Recuperar una lista de puntos de copia de seguridad mediante la ejecución de hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet con parámetros adecuados. En nuestro ejemplo, elegiremos punto de copia de seguridad más reciente de hello para el volumen de origen de hello *D:* y usar toorecover un archivo específico.

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
objeto de Hello ```$rps``` es una matriz de puntos de copia de seguridad. Hola primer elemento es el último punto de Hola y elemento n-ésima de hello es punto más antiguo de Hola. punto más reciente de toochoose hello, usaremos ```$rps[0]```.

### <a name="choosing-an-item-toorestore"></a>Elegir un elemento toorestore
tooidentify Hola exacto del archivo o carpeta toorestore, recursivamente usar hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet. Se pueden examinar esa jerarquía de carpetas de manera Hola únicamente con hello ```Get-OBRecoverableItem```.

En este ejemplo, si queremos que el archivo de hello toorestore *finances.xls* podemos hacer referencia a que cuando se utiliza el objeto de hello ```$filesFolders[1]```.

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

También puede buscar toorestore elementos mediante hello ```Get-OBRecoverableItem``` cmdlet. En nuestro ejemplo, toosearch para *finances.xls* se pudo obtener un identificador en el archivo hello, ejecute este comando:

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a>Proceso de restauración de desencadenamiento Hola
proceso de restauración de hello tootrigger, primero necesitamos opciones de recuperación de toospecify Hola. Esto puede hacerse mediante el uso de hello [OBRecoveryOption New](https://technet.microsoft.com/library/hh770417.aspx) cmdlet. En este ejemplo, supongamos que queremos archivos de hello toorestore demasiado*C:\temp*. Supongamos también que deseamos tooskip archivos que ya existen en la carpeta de destino de hello *C:\temp*. toocreate tal una opción de recuperación, utilice Hola siguiente comando:

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

Ahora desencadenar el proceso de restauración de hello mediante hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) comando hello seleccionado ```$item``` de salida de hello de hello ```Get-OBRecoverableItem``` cmdlet:

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a>La desinstalación de agente de copia de seguridad de Azure Hola
Desinstalar agente de copia de seguridad de Azure de hello puede hacerse mediante el uso de hello siguiente comando:

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

Desinstalación de archivos binarios del agente de hello de la máquina de hello tiene algunos tooconsider consecuencias:

* Quita el filtro de archivos Hola de máquina de Hola y se detiene el seguimiento de cambios.
* Se quita toda la información de directiva de máquina de hello, pero información de la directiva de hello continúa toobe almacenado en el servicio de Hola.
* Se eliminan todas las programaciones de copia de seguridad y no se realizan más copias de seguridad.

Sin embargo, Hola datos almacenados en Azure permanece y se mantiene según la configuración de directiva de retención de Hola por parte del usuario. Los puntos más antiguos vencen automáticamente.

## <a name="remote-management"></a>Administración remota
Toda la administración de hello alrededor de agente de copia de seguridad de Azure de hello, directivas y orígenes de datos puede realizarse de forma remota a través de PowerShell. máquina de Hola que se administrará de forma remota debe toobe preparado correctamente.

De forma predeterminada, Hola servicio WinRM está configurado para iniciarse manualmente. tipo de inicio de Hello debe establecerse demasiado*automática* y se debe iniciar el servicio de Hola. tooverify que Hola servicio WinRM se está ejecutando, debería Hola el valor de la propiedad Status de hello *ejecutando*.

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

PowerShell debe configurarse para la comunicación remota.

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

máquina de Hello ahora pueden administrarse de forma remota: a partir de la instalación de Hola de agente de Hola. Por ejemplo, hello siguiente secuencia de comandos copia máquina remota de hello agente toohello y lo instala.

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre Azure Backup para Windows Server o cliente de Windows, consulte

* [Introducción tooAzure copia de seguridad](backup-introduction-to-azure-backup.md)
* [Copia de seguridad de servidores Windows](backup-configure-vault.md)
