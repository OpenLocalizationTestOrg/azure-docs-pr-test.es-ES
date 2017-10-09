---
title: "aaaReplicate tooAzure de máquinas virtuales de Hyper-V en el portal clásico de hello con PowerShell | Documentos de Microsoft"
description: "Automatizar la replicación de máquinas virtuales de Hyper-V en nubes VMM con Site Recovery y PowerShell en el portal clásico de Hola Hola"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a>Replicar tooAzure de máquinas virtuales de Hyper-V con PowerShell en el portal clásico de Hola
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [PowerShell: administrador de recursos](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Portal clásico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell: clásico](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a>Información general
Azure Site Recovery contribuye estrategia de recuperación (BCDR) ante desastres y continuidad del negocio de tooyour mediante la coordinación de replicación, la conmutación por error y la recuperación de máquinas virtuales en un número de escenarios de implementación. Para obtener una lista completa de la implementación de escenarios vea hello [Introducción a Azure Site Recovery](site-recovery-overview.md).

Este artículo muestra cómo las tareas comunes de toouse PowerShell tooautomate necesita tooperform al configurar máquinas de virtuales de Hyper-V de Azure Site Recovery tooreplicate en almacenamiento de tooAzure de nubes de System Center VMM.

artículo de Hello incluye los requisitos previos de escenario de Hola y muestra también cómo instalar tooset un almacén de Site Recovery, hello Azure Site Recovery Provider Hola servidor VMM de origen, Registrar servidor hello en el almacén de hello, agregar una cuenta de almacenamiento de Azure, instalar hello Azure Agente de servicios de recuperación en los servidores de host de Hyper-V, configurar la protección para nubes VMM que será aplicado tooall protegido las máquinas virtuales y, a continuación, habilitar la protección de las máquinas virtuales. Finalice prueba toomake de conmutación por error de Hola que todo funciona según lo previsto.

Si experimenta problemas al configurar este escenario, publicar sus preguntas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico.
>
>

## <a name="before-you-start"></a>Antes de comenzar
Asegúrese de que tiene preparados estos requisitos previos:

### <a name="azure-prerequisites"></a>Requisitos previos de Azure
* Necesitará una cuenta de [Microsoft Azure](https://azure.microsoft.com/) . Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Necesitará un toostore replicado de datos de la cuenta de almacenamiento de Azure. cuenta de Hello tiene habilitada la replicación geográfica. Debe quedar en Hola misma región que el almacén de Azure Site Recovery de Hola y asociarse Hola misma suscripción. [Más información sobre Almacenamiento de Azure](../storage/common/storage-introduction.md).
* Necesitará toomake seguro de que se cumplan las máquinas virtuales que desee tooprotect [requisitos previos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

### <a name="vmm-prerequisites"></a>Requisitos previos de VMM
* Necesitará un servidor VMM que se ejecute en System Center 2012 R2.
* Necesitará al menos una nube en el servidor VMM que desee tooprotect Hola. en la nube Hola debe contener:
  * Uno o más grupos de hosts de VMM
  * Uno o más servidores host de Hyper-V o clústeres en cada grupo de hosts.
  * Máquinas virtuales de uno o más en el servidor de Hyper-V de origen Hola.

### <a name="hyper-v-prerequisites"></a>Requisitos previos de Hyper-V
* Hello servidores host Hyper-V deben ejecutar al menos **Windows Server 2012** con el rol de Hyper-V o **Microsoft Hyper-V Server 2012** y ha hello las últimas actualizaciones instaladas.
* Si está ejecutando Hyper-V en un clúster, tenga en cuenta que ese agente de clúster no se crea automáticamente si tiene un clúster basado en una dirección IP estática. Necesitará a un agente de clúster hello tooconfigure manualmente. toodo esto, en el administrador del servidor > Administrador de clústeres de conmutación por error, clúster toohello de conectarse, haga clic en **configurar rol** y seleccione **agente de réplica de Hyper-V** en hello **Seleccionar rol**pantalla del Asistente para alta disponibilidad de Hola.
* Cualquier servidor de host de Hyper-V o clúster que se desea protección toomanage debe incluirse en una nube de VMM.

### <a name="network-mapping-prerequisites"></a>Requisitos previos de asignación de redes
Al proteger las máquinas virtuales en mapas de asignación de red de Azure entre redes de VM Hola servidor VMM de origen y destino siguiente de hello tooenable de redes de Azure:

* Todas las máquinas que conmutar por error en hello mismo pueden conectar tooeach otro, independientemente del plan de recuperación que se encuentran en red.
* Si una puerta de enlace de red es el programa de instalación en red de Azure de destino de hello, máquinas virtuales pueden conectarse a máquinas virtuales de tooother local.
* Si no configura la red asignación solo las máquinas virtuales que conmutan en hello mismo plan de recuperación será capaz de tooconnect tooeach otros después tooAzure de conmutación por error.

Si desea que la asignación de red toodeploy, necesitará la siguiente de hello:

* Hello las máquinas virtuales que desee tooprotect Hola servidor VMM de origen debe ser una red de VM tooa conectado. Esta red debe ser tooa vinculado red lógica que está asociado a la nube de Hola.
* Puede conectar una red Azure toowhich replicado a máquinas virtuales después de la conmutación por error. Esta red seleccionará en tiempo de Hola de conmutación por error. red de Hello debe formar parte de hello misma región que su suscripción de Azure Site Recovery.

### <a name="powershell-prerequisites"></a>Requisitos previos de PowerShell
Asegúrese de que tiene listo toogo de PowerShell de Azure. Si ya usa PowerShell, deberá tooupgrade tooversion 0.8.10 o una versión posterior. Para obtener información acerca de cómo configurar PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs). Una vez que se instala y configura PowerShell, puede ver todos los cmdlets disponibles de hello para el servicio de Hola de [aquí](/powershell/azure/overview).

toolearn acerca de las sugerencias que pueden ayudarle a usar los cmdlets de hello, como cómo normalmente se controlan los valores de parámetro, las entradas y salidas en Azure PowerShell, consulte [empezar a trabajar con Cmdlets de Azure](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Paso 1: Configurar la suscripción de Hola
En PowerShell, ejecute estos cmdlets:

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

Reemplazar elementos Hola Hola "< >" con información específica de su.

## <a name="step-2-create-a-site-recovery-vault"></a>Paso 2: Creación de un almacén de recuperación del sitio
En PowerShell, reemplazar elementos Hola Hola "< >" con información específica de su y ejecute estos comandos:

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a>Paso 3: Generación de una clave de registro de almacén
Generar una clave de registro en el almacén de Hola. Después de descargar hello Azure Site Recovery Provider e instalarlo en el servidor VMM hello, deberá usar este servidor VMM de hello tooregister clave en el almacén de Hola.

1. Obtener archivo de configuración de almacén de hello y establecer contexto de hello:

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. Establecer el contexto del almacén de hello ejecutando Hola siguientes comandos:

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Paso 4: Instalar hello Azure Site Recovery Provider
1. En la máquina VMM hello, cree un directorio ejecutando el siguiente comando de hello:

   ```

   pushd C:\ASR\

   ```
2. Extraiga los archivos de hello mediante el proveedor de hello descargado ejecutando el siguiente comando de Hola

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. Instalar a proveedor de hello mediante Hola siguientes comandos:

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   Espere Hola instalación toofinish.
4. Registrar servidor de hello en almacén de hello con hello siguiente comando:

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a>Paso 5: Creación de una cuenta de almacenamiento de Azure
Si no tiene una cuenta de almacenamiento de Azure, cree una cuenta de replicación geográfica habilitada mediante la ejecución de hello siguiente comando:

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

Tenga en cuenta que debe ser la cuenta de almacenamiento de hello en Hola misma región que el servicio de Azure Site Recovery de Hola y asociarse Hola misma suscripción.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Paso 6: Instalar Hola agente de servicios de recuperación de Azure
Desde Hola portal de Azure, instalar el agente de servicios de recuperación de Azure de hello en cada servidor de host de Hyper-V ubicado en nubes VMM Hola desea tooprotect.

Ejecute hello siguiente comando en todos los hosts VMM:

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a>Paso 7: Configuración de la protección de la nube
1. Crear una tooAzure de perfil de protección de nube mediante la ejecución de hello siguiente comando:

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. Obtener un contenedor de protección mediante la ejecución de hello siguientes comandos:

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. Iniciar asociación Hola del contenedor de protección de Hola a nube hello:

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. Cuando haya finalizado el trabajo de hello, ejecute hello siguiente comando:

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. Después de que el trabajo de hello ha finalizado el procesamiento, ejecute hello siguiente comando:

        Do
        {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

        if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
        }While($isJobLeftForProcessing)



finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).

## <a name="step-8-configure-network-mapping"></a>Paso 8: Configuración de la asignación de red
Antes de empezar la asignación de red Compruebe que máquinas virtuales en el servidor VMM de origen Hola son red de VM tooa conectado. Además, cree una o varias redes virtuales de Azure. Tenga en cuenta que varias redes de VM pueden ser asignado tooa sola red de Azure.

Tenga en cuenta que si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, entonces Hola máquina virtual será toothat conectado subred de destino después de la conmutación por error. Si no hay una subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.

Hola primer comando obtiene servidores de almacén de Azure Site Recovery de hello actual. comando Hello almacena servidores de Microsoft Azure Site Recovery de hello en la variable de matriz de hello $Servers.

    $Servers = Get-AzureSiteRecoveryServer


Hola segundo comando obtiene red de recuperación de sitio de hello para el primer servidor de hello en la matriz de hello $Servers. comando Hello almacena redes hello en la variable de hello $Networks.

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

Hola tercer comando obtiene las suscripciones de Azure mediante el cmdlet Get-AzureSubscription hello y, a continuación, almacena ese valor en la variable de hello $Subscriptions.

    $Subscriptions = Get-AzureSubscription



Hola cuarto comando obtiene redes virtuales de Azure utilizando el cmdlet Get-AzureVNetSite hello y, a continuación, ese valor en la variable de hello $AzureVmNetworks.

    $AzureVmNetworks = Get-AzureVNetSite



Hola final cmdlet crea una asignación entre la red principal de Hola y de red de máquina virtual de Azure Hola. Hola cmdlet especifica la red principal de hello como primer elemento de Hola de $Networks. Hola cmdlet especifica una red de máquina virtual como primer elemento de Hola de $AzureVmNetworks mediante su identificador. comando de Hello incluye el identificador de suscripción de Azure.

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a>Paso 9: Habilitación de la protección para las máquinas virtuales
Después de servidores, las nubes y las redes están configuradas correctamente, puede habilitar la protección de máquinas virtuales en la nube de Hola. Tenga en cuenta los siguiente hello:

Las máquinas virtuales deben cumplir [Requisitos previos de las máquinas virtuales de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

sistema operativo de tooenable protección hello y propiedades del disco de sistema operativo deben establecerse para la máquina virtual de Hola. Cuando se crea una máquina virtual en VMM mediante una plantilla de máquina virtual puede establecer la propiedad Hola. También puede establecer estas propiedades para las máquinas virtuales existentes en hello **General** y **configuración de Hardware** fichas de propiedades de la máquina virtual de Hola. Si no establece estas propiedades en VMM estará tooconfigure capaz de ellas en el portal de Azure Site Recovery Hola.

1. protección de tooenable, ejecute hello después de contenedor de protección de hello tooget de comando:

     $ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName
2. Obtener la entidad de protección de hello (VM) mediante la ejecución de hello siguiente comando:

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. Habilitar hello recuperación ante desastres para hello VM mediante la ejecución Hola siguiente comando:

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a>Prueba de la implementación
plan de la implementación, puede ejecutar una prueba de conmutación por error para una sola máquina virtual, o crear un plan de recuperación que consta de varias máquinas virtuales y ejecutar una prueba de conmutación por error para hello tootest. La conmutación por error de prueba simula su mecanismo de conmutación por error y recuperación en una red aislada. Observe lo siguiente:

* Si desea tooconnect toohello virtual machine en Azure mediante Escritorio remoto después de la conmutación por error de hello, habilite la conexión a Escritorio remoto en la máquina virtual de hello antes de ejecutar la conmutación por error de prueba de Hola.
* Después de la conmutación por error, deberá usar una máquina de virtual toohello pública del tooconnect de dirección IP en Azure mediante Escritorio remoto. Si desea toodo esto, asegúrese de que no hay ninguna directiva de dominio que impiden la conexión máquina virtual de tooa con una dirección pública.

finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).

### <a name="create-a-recovery-plan"></a>Creación de un plan de recuperación
1. Cree un archivo .xml como plantilla para el plan de recuperación con datos de Hola a continuación y, a continuación, guárdelo como "C:\RPTemplatePath.xml".
2. Cambie el nodo de RecoveryPlan Hola Id., nombre, PrimaryServerId y SecondaryServerId.
3. Cambie el nodo de hello ProtectionEntity PrimaryProtectionEntityId (vmid de VMM).
4. Puede agregar más máquinas virtuales añadiendo más nodos ProtectionEntity.

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. Rellene los datos de hello en plantilla hello:

        $TemplatePath = "C:\RPTemplatePath.xml";



1. Crear Hola RecoveryPlan:

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba
1. Obtener objetos de hello RecoveryPlan ejecutando el siguiente comando de hello:

     $RPObject = get-AzureSiteRecoveryRecoveryPlan-nombre $RPName;
2. Iniciar conmutación por error de prueba de hello ejecutando Hola siguiente comando:

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <a name=monitor></a> Supervisión de la actividad
Usar hello después de la actividad de hello toomonitor de comandos. Tenga en cuenta que tiene toowait entre los trabajos de hello toofinish de procesamiento.

    Do
    {
            $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
            Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
            if($job -eq $null -or $job.StateDescription -ne "Completed")
            {
                $isJobLeftForProcessing = $true;
            }

        if($isJobLeftForProcessing)
            {
                Start-Sleep -Seconds 60
            }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a>Pasos siguientes
[Obtenga más información](/powershell/azure/overview) sobre cmdlets de PowerShell de Azure Site Recovery. </a>.
