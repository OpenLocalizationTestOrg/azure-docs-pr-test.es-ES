---
title: "máquinas virtuales de Hyper-V en el sitio secundario de VMM tooa con PowerShell (Administrador de recursos de Azure) aaaReplicate | Documentos de Microsoft"
description: "Describe cómo la replicación de tooorchestrate de Azure Site Recovery toodeploy, la conmutación por error y la recuperación de máquinas virtuales de Hyper-V en VMM nubes sitio VMM secundario tooa con PowerShell (Administrador de recursos)"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a>Replicar máquinas virtuales de Hyper-V en VMM nubes tooa sitio VMM secundario con PowerShell (Administrador de recursos)
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Portal clásico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell: administrador de recursos](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Bienvenido tooAzure Site Recovery. Use este artículo si desea tooreplicate máquinas virtuales de Hyper-V administrados en el sitio secundario de tooa de nubes de System Center Virtual Machine Manager (VMM) local.

Este artículo muestra cómo las tareas comunes de toouse PowerShell tooautomate necesita tooperform al configurar máquinas virtuales de Azure Site Recovery tooreplicate Hyper-V en nubes VMM de System Center VMM nubes tooSystem Center en el sitio secundario.

Hola artículo incluye requisitos previos de escenario de Hola y muestra

* ¿Cómo tooset un almacén de servicios de recuperación
* Instalar hello Azure Site Recovery Provider en el servidor VMM de origen de Hola y servidor VMM de destino de Hola
* Registrar servidores VMM de hello en el almacén de Hola
* Configurar la directiva de replicación de hello nube de VMM. configuración de replicación de Hello en la directiva de hello será aplicado tooall protegido las máquinas virtuales
* Habilitar la protección de máquinas virtuales de Hola.
* Conmutación por error de prueba Hola de máquinas virtuales individualmente o como parte de una recuperación del plan toomake seguro de que todo funciona según lo previsto.
* Realizar planeada o una conmutación por error no planeada de máquinas virtuales individualmente o como parte de una toomake del plan de recuperación que todo funciona según lo previsto.

Si experimenta problemas al configurar este escenario, publicar sus preguntas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure tiene dos [modelos de implementación](../azure-resource-manager/resource-manager-deployment-model.md) diferentes para crear y utilizar recursos: Azure Resource Manager y el clásico. Azure también tiene dos portales: Hola portal de Azure clásico que admite el modelo de implementación clásica de Hola y Hola portal de Azure con compatibilidad para dos modelos de implementación. Este artículo trata el modelo de implementación del Administrador de recursos de Hola.
>
>

## <a name="on-premises-prerequisites"></a>Requisitos previos locales
Aquí es lo que necesitará en hello principal y secundaria local sitios toodeploy este escenario:

| **Requisitos previos** | **Detalles** |
| --- | --- |
| **VMM** |Se recomienda que implementar un servidor VMM en el sitio primario de Hola y un servidor VMM en el sitio secundario de Hola.<br/><br/> También puede [llevar a cabo una replicación entre nubes en un solo servidor VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). toodo Esto necesitará al menos dos nubes configuradas en el servidor VMM Hola.<br/><br/> Servidores VMM se deben ejecutar al menos System Center 2012 SP1 con las últimas actualizaciones de Hola.<br/><br/> Cada servidor VMM debe tener uno o más nubes configuradas y todas las nubes deben tener perfil de capacidad de Hyper-V de hello establecido. <br/><br/>Las nubes deben incluir uno o más grupos de hosts de VMM.<br/><br/>Más información sobre la configuración de nubes VMM en [Hola configurar VMM en la nube tejido](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), y [Tutorial: crear nubes privadas con System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).<br/><br/> Los servidores VMM deben tener acceso a Internet. |
| **Hyper-V** |Servidores de Hyper-V deben ejecutar al menos Windows Server 2012 con el rol de Hyper-V de Hola y Hola a las últimas actualizaciones instaladas.<br/><br/> Un servidor de Hyper-V debe contener una o varias máquinas virtuales.<br/><br/>  Servidores de host de Hyper-V deben estar en grupos host en nubes VMM principales y secundarias de Hola.<br/><br/> Si está ejecutando Hyper-V en un clúster en Windows Server 2012 R2, debe instalar la [actualización 2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Si va a ejecutar Hyper-V en un clúster de Windows Server 2012, tenga en cuenta que el agente de clúster no se crea automáticamente si tiene un clúster basado en una dirección IP estática. Necesitará a un agente de clúster hello tooconfigure manualmente. [Más información](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Proveedor** |Durante la implementación de Site Recovery se instale hello Azure Site Recovery Provider en servidores VMM. Hola proveedor se comunica con Site Recovery a través de HTTPS 443 tooorchestrate replicación. Se produce la replicación de datos entre Hola principales y secundarios Hyper-V servidores a través de hello LAN o una conexión VPN.<br/><br/> Hello proveedor se ejecuta en el servidor VMM Hola necesita tener acceso a direcciones URL toothese: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.<br/><br/> Además permite la comunicación de firewall de hello VMM servidores toohello [intervalos IP del centro de datos Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) y permitir que el protocolo de hello HTTPS (443). |

### <a name="network-mapping-prerequisites"></a>Requisitos previos de asignación de redes
Mapas de asignación de red entre redes de VM de VMM en servidores VMM de hello principales y secundarias para:

* Colocar óptimamente las máquinas virtuales de réplica en los hosts de Hyper-V secundarios tras la conmutación por error.
* Conectar redes de VM de tooappropriate de las máquinas virtuales de réplica.
* Si no configura la red asignación réplica máquinas virtuales no estarán conectada tooany red después de la conmutación por error.
* Si desea que tooset de red asignar durante la recuperación del sitio aquí la implementación es qué se necesita:

  * Asegúrese de que las máquinas virtuales en el origen de hello servidor host Hyper-V están conectado tooa red de VM de VMM. Esta red debe ser tooa vinculado red lógica que está asociado a la nube de Hola.
  * Compruebe que Hola secundaria en la nube que va a utilizar para la recuperación tiene configurada una red VM correspondiente. Dicha red de máquina virtual debe ser tooa vinculado red lógica que esté asociada con la nube secundaria Hola.

Más información acerca de cómo configurar redes de VMM en hello debajo de artículos

* [¿Cómo tooconfigure redes lógicas en VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [¿Cómo tooconfigure VM redes y puertas de enlace en VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)

[Más información](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sobre cómo funciona la asignación de redes.

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
1. Cree un grupo de recursos de Azure Resource Manager si todavía no lo ha hecho.

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Crear un nuevo almacén de servicios de recuperación y guardar Hola creado el objeto de almacén de ASR en una variable (se usará más adelante). También puede recuperar Hola ASR almacén post creación del objeto mediante el cmdlet Get-AzureRMRecoveryServicesVault Hola:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Paso 3: Establecer contexto de almacén de servicios de recuperación de Hola
1. Si tiene un almacén ya creado, ejecute hello debajo de almacén de comando tooget Hola.

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. Establecer contexto de almacén de hello ejecutando Hola comando siguiente.

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

## <a name="step-5-create-and-associate-a-replication-policy"></a>Paso 5: Creación y asociación de una directiva de replicación
1. Crear una directiva de replicación de Hyper-V 2012 R2 ejecutando Hola siguiente comando:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > Hola nube de VMM puede contener hosts de Hyper-V que ejecutan versiones distintas de Windows Server (como se menciona en los requisitos previos de hello Hyper-V), pero la directiva de replicación de hello es específicos de la versión de sistema operativo. Si tiene diferentes hosts que ejecutan diferentes versiones del sistema operativo, cree directivas de replicación independientes para cada tipo de versión del sistema operativo. Por ejemplo, si tiene 5 hosts que se ejecutan en Windows Servers 2012 y 3 en Windows Server 2012 R2, cree 2 directivas de replicación: una para cada tipo de versión del sistema operativo.

1. Obtengan contenedor de protección primaria de hello (nube de VMM principal) y el contenedor de protección de recuperación (recuperación de nube de VMM) mediante la ejecución de hello siguientes comandos:

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. Recuperar la directiva de Hola que creó en el paso 1 mediante nombre descriptivo de Hola de directiva de Hola

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Comience asociación Hola del contenedor de protección de hello (nube de VMM) con la directiva de replicación de hello:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. Espere a que toocomplete de trabajo de asociación de directiva de Hola. Puede comprobar si el trabajo de Hola se ha completado utilizando el siguiente fragmento de código de PowerShell de Hola.

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   Después de que el trabajo de hello ha finalizado el procesamiento, ejecute hello siguiente comando:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).

## <a name="step-6-configure-network-mapping"></a>Paso 6: Configuración de la asignación de red
1. Hola primer comando obtiene servidores de almacén de Azure Site Recovery de hello actual. comando Hello almacena servidores de Microsoft Azure Site Recovery de hello en la variable de matriz de hello $Servers.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Hola por debajo de los comandos obtener red de recuperación de sitio de hello para el servidor VMM de origen de Hola y servidor VMM de destino de Hola.

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > servidor VMM de origen de Hello puede ser Hola primera o segunda matriz de servidores de un saludo en hello. Comprobar los nombres de Hola Hola de servidores de VMM y obtener redes Hola correctamente


1. Hola final cmdlet crea una asignación entre la red principal de Hola y red de recuperación de Hola. Hola cmdlet especifica red principal de hello como primer elemento de Hola de red de recuperación $PrimaryNetworks y hello como primer elemento de Hola de $RecoveryNetworks.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a>Paso 7: Configuración de la asignación de almacenamiento
1. Hola comando siguiente obtiene la lista de Hola de clasificaciones de almacenamiento en la variable $storageclassifications.

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. Hola por debajo de los comandos obtener la clasificación de origen de hello en $SourceClassificaion variable y la clasificación de destino en la variable $TargetClassification.

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > clasificaciones de origen y destino de Hello pueden ser cualquier elemento de matriz de Hola. Consulte toohello salida de hello debajo de índice del comando toofigure Hola de clasificaciones de origen y destino de matriz $storageclassifications.

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table


1. Hola siguiente cmdlet crea una asignación entre la clasificación de origen de Hola y clasificación de destino de Hola.

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a>Paso 8: Habilitación de la protección para las máquinas virtuales
Después de redes, las nubes y servidores de hello están configuradas correctamente, puede habilitar la protección de máquinas virtuales en la nube de Hola.

1. protección de tooenable, ejecute hello después de contenedor de protección de hello tooget de comando:

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. Obtener la entidad de protección de hello (VM) mediante la ejecución de hello siguiente comando:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. Habilitar la replicación de hello VM mediante la ejecución de hello siguiente comando:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a>Prueba de la implementación
plan de la implementación, puede ejecutar una prueba de conmutación por error para una sola máquina virtual, o crear un plan de recuperación que consta de varias máquinas virtuales y ejecutar una prueba de conmutación por error para hello tootest. La conmutación por error de prueba simula su mecanismo de conmutación por error y recuperación en una red aislada.

> [!NOTE]
> Puede crear un plan de recuperación para su aplicación en el Portal de Azure.
>
>

finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).

### <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba
1. Ejecute hello debajo toowhich de red VM de cmdlets tooget Hola desea tootest conmutación por error las máquinas virtuales se.

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. Realizar una conmutación por error de prueba de una máquina virtual haciendo Hola siguiente:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. Realizar una conmutación por error de prueba de un plan de recuperación haciendo Hola siguiente:

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a>Ejecución de una conmutación por error planeada
1. Realizar una conmutación por error planeada de una máquina virtual haciendo Hola siguiente:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. Realizar una conmutación por error planeada de un plan de recuperación haciendo Hola siguiente:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a>Ejecución de una conmutación por error no planeada
1. Realizar una conmutación por error no planeada de una máquina virtual haciendo Hola siguiente:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

2. realizar una conmutación por error no planeada de un plan de recuperación haciendo Hola siguiente:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

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
