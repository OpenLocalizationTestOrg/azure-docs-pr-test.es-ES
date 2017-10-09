---
title: "máquinas virtuales de Hyper-V aaaReplicate en nubes VMM con Azure Site Recovery y PowerShell (Administrador de recursos) | Documentos de Microsoft"
description: "Replicar máquinas virtuales de Hyper-V en nubes VMM con Azure Site Recovery y PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a>Replicar máquinas virtuales de Hyper-V en tooAzure de nubes VMM mediante PowerShell y el Administrador de recursos de Azure
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

Hola artículo incluye requisitos previos de escenario de Hola y muestra

* ¿Cómo tooset un almacén de servicios de recuperación
* Instalar hello Azure Site Recovery Provider Hola servidor VMM de origen
* Registrar servidor hello en el almacén de hello, agregue una cuenta de almacenamiento de Azure
* Instalar el agente de servicios de recuperación de Azure de hello en los servidores de host de Hyper-V
* Configurar la protección para nubes VMM, que serán aplicado tooall protegido las máquinas virtuales
* Habilite la protección para esas máquinas virtuales.
* Probar toomake de conmutación por error de Hola que todo funciona según lo previsto.

Si experimenta problemas al configurar este escenario, publicar sus preguntas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación del Administrador de recursos de Hola.
>
>

## <a name="before-you-start"></a>Antes de comenzar
Asegúrese de que tiene preparados estos requisitos previos:

### <a name="azure-prerequisites"></a>Requisitos previos de Azure
* Necesitará una cuenta de [Microsoft Azure](https://azure.microsoft.com/) . Si no tiene una, comience con un [cuenta gratuita](https://azure.microsoft.com/free). Además, puede leer sobre hello [precios de Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Si va a probar el escenario suscripción CSP de hello replicación tooa, necesitará una suscripción de CSP. Más información acerca del programa Hola CSP en [cómo tooenroll en programa CSP hello](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).
* Necesitará un tooAzure Azure v2 (Administrador de recursos) de almacenamiento cuenta toostore datos replicados. cuenta de Hello tiene habilitada la replicación geográfica. Debe ser en Hola misma región que Hola servicio Azure Site Recovery y estar asociado con hello misma suscripción u Hola CSP. toolearn más acerca de cómo configurar el almacenamiento de Azure, vea hello [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md) como referencia.
* Necesitará toomake seguro de que las máquinas virtuales que desee tooprotect cumplen con hello [requisitos previos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

> [!NOTE]
> Actualmente, solo las operaciones de nivel de máquina virtual son posibles a través de Powershell. Pronto se incluirá compatibilidad con operaciones de nivel de plan de recuperación.  Por ahora, es tooperforming limita las conmutaciones por error solo en una granularidad 'protected VM' y no en un nivel de Plan de recuperación.
>
>

### <a name="vmm-prerequisites"></a>Requisitos previos de VMM
* Necesitará un servidor VMM que se ejecute en System Center 2012 R2.
* Cualquier servidor VMM que contengan máquinas virtuales que desee tooprotect debe estar en ejecución hello Azure Site Recovery Provider. Se instala durante la implementación de Azure Site Recovery Hola.
* Necesitará al menos una nube en el servidor VMM que desee tooprotect Hola. en la nube Hola debe contener:
  * Uno o más grupos de hosts de VMM
  * Uno o más servidores host de Hyper-V o clústeres en cada grupo de hosts
  * Máquinas virtuales de uno o más en el servidor de Hyper-V de origen Hola.
* Más información acerca de cómo configurar las nubes de VMM:
  * Obtener más información acerca de las nubes privadas de VMM en [What's New en la nube privada con System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) y en [nubes de VMM 2012 y hello](http://go.microsoft.com/fwlink/?LinkId=324956).
  * Obtenga información acerca de cómo [Hola configurar VMM tejido de nube](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)
  * Una vez configurados los elementos del tejido de nube, aprenda a crear nubes privadas en [Creación de una nube privada en VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) y [Tutorial: Creación de nubes privadas con System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).

### <a name="hyper-v-prerequisites"></a>Requisitos previos de Hyper-V
* Hello servidores host Hyper-V deben ejecutar al menos **Windows Server 2012** con el rol de Hyper-V o **Microsoft Hyper-V Server 2012** y ha hello las últimas actualizaciones instaladas.
* Si está ejecutando Hyper-V en un clúster, tenga en cuenta que ese agente de clúster no se crea automáticamente si tiene un clúster basado en una dirección IP estática. Necesitará a un agente de clúster hello tooconfigure manualmente. Para
* Para obtener instrucciones, consulte [cómo tooConfigure agente de réplica de Hyper-V](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).
* Cualquier servidor de host de Hyper-V o clúster que se desea protección toomanage debe incluirse en una nube de VMM.

### <a name="network-mapping-prerequisites"></a>Requisitos previos de asignación de redes
Al proteger máquinas virtuales en Azure, la asignación de red Hola asigna redes de máquinas virtuales de hello en el servidor VMM de origen de Hola y siguientes de Hola de tooenable de redes de Azure de destino:

* Todas las máquinas que conmutar por error en hello mismo pueden conectar tooeach otro, independientemente del plan de recuperación que se encuentran en red.
* Si una puerta de enlace de red es el programa de instalación en red de Azure de destino de hello, máquinas virtuales pueden conectarse a máquinas virtuales de tooother local.
* Si no configura la asignación de red, solo Hola máquinas virtuales que conmutan en hello mismo plan de recuperación será capaz de tooconnect tooeach otros después tooAzure de conmutación por error.

Si desea que la asignación de red toodeploy, necesitará la siguiente de hello:

* Hello las máquinas virtuales que desee tooprotect Hola servidor VMM de origen debe ser una red de VM tooa conectado. Esta red debe ser tooa vinculado red lógica que está asociado a la nube de Hola.
* Puede conectar una red Azure toowhich replicado a máquinas virtuales después de la conmutación por error. Esta red seleccionará en tiempo de Hola de conmutación por error. red de Hello debe formar parte de hello misma región que su suscripción de Azure Site Recovery.

Más información sobre asignación de redes en

* [¿Cómo tooconfigure redes lógicas en VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [¿Cómo tooconfigure VM redes y puertas de enlace en VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [¿Cómo tooconfigure y supervisar redes virtuales en Azure](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a>Requisitos previos de PowerShell
Asegúrese de que tiene listo toogo de PowerShell de Azure. Si ya usa PowerShell, deberá tooupgrade tooversion 0.8.10 o una versión posterior. Para obtener información acerca de cómo configurar PowerShell, vea hello [guía tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs). Una vez que se instala y configura PowerShell, puede ver todos los cmdlets disponibles de hello para el servicio de Hola de [aquí](/powershell/azure/overview).

toolearn acerca de las sugerencias que pueden ayudarle a usar los cmdlets de hello, como cómo normalmente se controlan los valores de parámetro, las entradas y salidas en Azure PowerShell, vea hello [guía tooget iniciado con Cmdlets de Azure](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Paso 1: Configurar la suscripción de Hola
1. De Azure powershell, inicio de sesión tooyour cuenta de Azure: mediante Hola después cmdlets

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. Obtenga una lista de las suscripciones. Esto mostrará también Hola identificadores de suscripción para cada una de las suscripciones de Hola. Anote subscriptionID Hola de suscripción de hello en el que desea que el almacén de servicios de recuperación de hello toocreate

        Get-AzureRmSubscription
3. Establecer suscripción hello en qué Hola almacén de servicios de recuperación es toobe creado por mencionar Hola Id. de suscripción

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>Paso 2: Creación de un almacén de Servicios de recuperación
1. Cree un grupo de recursos en Azure Resource Manager si todavía no lo ha hecho.

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Crear un nuevo almacén de servicios de recuperación y guardar Hola creado el objeto de almacén de ASR en una variable (se usará más adelante). También puede recuperar Hola ASR almacén post creación del objeto mediante el cmdlet Get-AzureRMRecoveryServicesVault Hola:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Paso 3: Establecer contexto de almacén de servicios de recuperación de Hola

Establecer contexto de almacén de hello ejecutando Hola comando siguiente.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Paso 4: Instalar hello Azure Site Recovery Provider
1. En la máquina VMM hello, cree un directorio ejecutando el siguiente comando de hello:

       New-Item c:\ASR -type directory
2. Extraiga los archivos de hello mediante el proveedor de hello descargado ejecutando el siguiente comando de Hola

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. Instalar a proveedor de hello mediante Hola siguientes comandos:

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   Espere Hola instalación toofinish.
4. Registrar servidor de hello en almacén de hello con hello siguiente comando:

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a>Paso 5: Creación de una cuenta de almacenamiento de Azure

Si no tiene una cuenta de almacenamiento de Azure, cree una cuenta de replicación geográfica habilitada en hello mismo geográfica como Hola almacén ejecutando el siguiente comando de hello:

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

Tenga en cuenta que debe ser la cuenta de almacenamiento de hello en Hola misma región que el servicio de Azure Site Recovery de Hola y asociarse Hola misma suscripción.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Paso 6: Instalar Hola agente de servicios de recuperación de Azure
1. Descargar agente de servicios de recuperación de Azure de hello en [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) y de instalación en cada servidor de host de Hyper-V ubicado en hello VMM nubes desea tooprotect.
2. Ejecute hello siguiente comando en todos los hosts VMM:

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a>Paso 7: Configuración de la protección de la nube
1. Crear un tooAzure de la directiva de replicación mediante la ejecución de hello siguiente comando:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. Obtener un contenedor de protección mediante la ejecución de hello siguientes comandos:

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. Obtener la Hola directiva detalles tooa variable con trabajo Hola que creó y mencionar el nombre de directiva descriptivo hello:

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Comience asociación Hola del contenedor de protección de hello con la directiva de replicación de hello:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. Cuando haya finalizado el trabajo de hello, ejecute hello siguiente comando:

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. Después de que el trabajo de hello ha finalizado el procesamiento, ejecute hello siguiente comando:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).

## <a name="step-8-configure-network-mapping"></a>Paso 8: Configuración de la asignación de red
Antes de empezar la asignación de red Compruebe que máquinas virtuales en el servidor VMM de origen Hola son red de VM tooa conectado. Además, cree una o varias redes virtuales de Azure.

Obtener más información sobre cómo toocreate a virtual red con PowerShell y el Administrador de recursos de Azure en [crear una red virtual con una conexión de VPN de sitio a sitio mediante el Administrador de recursos de Azure y PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

Tenga en cuenta que varias redes de máquina Virtual pueden ser asignado tooa sola red de Azure. Si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, entonces Hola máquina virtual será toothat conectado subred de destino después de una conmutación por error. Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.

1. Hola primer comando obtiene servidores de almacén de Azure Site Recovery de hello actual. comando Hello almacena servidores de Microsoft Azure Site Recovery de hello en la variable de matriz de hello $Servers.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Hola segundo comando obtiene red de recuperación de sitio de hello para el primer servidor de hello en la matriz de hello $Servers. comando Hello almacena redes hello en la variable de hello $Networks.

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. Hola tercer comando obtiene redes virtuales de Azure y, a continuación, ese valor en la variable de hello $AzureVmNetworks.

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. Hola final cmdlet crea una asignación entre la red principal de Hola y de red de máquina virtual de Azure Hola. Hola cmdlet especifica la red principal de hello como primer elemento de Hola de $Networks. Hola cmdlet especifica una red de máquina virtual como primer elemento de Hola de $AzureVmNetworks.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a>Paso 9: Habilitación de la protección para las máquinas virtuales
Después de redes, las nubes y servidores de hello están configuradas correctamente, puede habilitar la protección de máquinas virtuales en la nube de Hola.

 Tenga en cuenta los siguiente hello:

* Las máquinas virtuales de deben cumplir los requisitos de Azure. Compruebe estos [requisitos previos y compatibilidad](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) en la Guía de planificación de Hola.
* protección de tooenable, sistema operativo de Hola y las propiedades de disco de sistema operativo deben establecerse para la máquina virtual de Hola. Cuando se crea una máquina virtual en VMM mediante una plantilla de máquina virtual puede establecer la propiedad Hola. También puede establecer estas propiedades para las máquinas virtuales existentes en hello **General** y **configuración de Hardware** fichas de propiedades de la máquina virtual de Hola. Si no establece estas propiedades en VMM estará tooconfigure capaz de ellas en el portal de Azure Site Recovery Hola.

1. protección de tooenable, ejecute hello después de contenedor de protección de hello tooget de comando:

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. Obtener la entidad de protección de hello (VM) mediante la ejecución de hello siguiente comando:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. Habilitar hello recuperación ante desastres para hello VM mediante la ejecución Hola siguiente comando:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a>Prueba de la implementación
tootest su implementación, puede ejecutar una prueba de conmutación por error para una sola máquina virtual, o crear un plan de recuperación que consta de varias máquinas virtuales y ejecutar una conmutación por error de prueba para el plan de Hola. La conmutación por error de prueba simula el mecanismo de conmutación por error y recuperación en una red aislada. Observe lo siguiente:

* Si desea tooconnect toohello virtual machine en Azure mediante Escritorio remoto después de la conmutación por error de hello, habilite la conexión a Escritorio remoto en la máquina virtual de hello antes de ejecutar la conmutación por error de prueba de Hola.
* Después de una conmutación por error, deberá usar una máquina de virtual toohello pública del tooconnect de dirección IP en Azure mediante Escritorio remoto. Si desea toodo esto, asegúrese de que no hay ninguna directiva de dominio que impiden la conexión máquina virtual de tooa con una dirección pública.

finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).

### <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba
- Iniciar conmutación por error de prueba de hello ejecutando Hola siguiente comando:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a>Ejecución de una conmutación por error planeada
- Hola de inicio de conmutación por error planeada mediante la ejecución de hello siguiente comando:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a>Ejecución de una conmutación por error no planeada
- Iniciar Hola de conmutación por error no planeada ejecutando Hola siguiente comando:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

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
[Más información](/powershell/module/azurerm.recoveryservices.backup/#recovery) sobre los cmdlets de PowerShell de Azure Site Recovery con Azure Resource Manager.
