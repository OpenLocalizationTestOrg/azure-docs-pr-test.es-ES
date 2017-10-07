---
title: "aaaReplicate máquinas virtuales de Hyper-V con PowerShell y el Administrador de recursos de Azure | Documentos de Microsoft"
description: "Automatizar la replicación de Hola de máquinas virtuales de Hyper-V tooAzure con Azure Site Recovery con PowerShell y el Administrador de recursos de Azure."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a>Replicación entre máquinas virtuales de Hyper-V local y Azure con PowerShell y Azure Resource Manager
> [!div class="op_single_selector"]
> * [Portal de Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell: administrador de recursos](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Portal clásico](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a>Información general
Azure Site Recovery contribuye estrategia de recuperación de desastres y la continuidad del negocio tooyour mediante la coordinación de replicación, la conmutación por error y la recuperación de máquinas virtuales en un número de escenarios de implementación. Para obtener una lista completa de escenarios de implementación, vea hello [Introducción a Azure Site Recovery](site-recovery-overview.md).

Azure PowerShell es un módulo que proporciona cmdlets toomanage Azure a través de Windows PowerShell. Puede trabajar con dos tipos de módulos: Hola módulo perfil de Azure o un módulo de Azure Resource Manager Hola.

Los cmdlets de PowerShell de Site Recovery que están disponibles con Azure PowerShell para Azure Resource Manager le permiten proteger y recuperar los servidores en Azure.

Este artículo se describe cómo Windows PowerShell, junto con Azure Resource Manager, toodeploy Site Recovery tooconfigure toouse y orquestar tooAzure de protección del servidor. ejemplo de Hola usado en este artículo muestra cómo tooprotect, conmutación por error y recuperar las máquinas virtuales en un tooAzure de host de Hyper-V mediante PowerShell de Azure con el Administrador de recursos de Azure.

> [!NOTE]
> Hello cmdlets de PowerShell de recuperación de sitio actualmente permiten hello tooconfigure siguientes: tooanother de sitio de un administrador de la máquina Virtual y un tooAzure de sitio de Virtual Machine Manager, un tooAzure de sitio de Hyper-V.
>
>

No es necesario toobe un toouse experto de PowerShell en este artículo, pero es necesario toounderstand conceptos básicos de hello, como módulos, cmdlets y las sesiones. Para obtener más información acerca de Windows PowerShell, consulte [Introducción a Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).

Lea más sobre el [Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).

> [!NOTE]
> Pueden configurar y administrar la protección de servidores de sus clientes partners de Microsoft que forman parte del programa de proveedor de soluciones de nube (CSP) de hello respectivos CSP las suscripciones tootheir clientes (suscripciones de los inquilinos).
>
>

## <a name="before-you-start"></a>Antes de comenzar
Asegúrese de que tiene preparados estos requisitos previos:

* Una cuenta de [Microsoft Azure](https://azure.microsoft.com/) . Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/). También puede leer sobre los precios del [Administrador de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
* Azure PowerShell 1.0. Para obtener información acerca de esta versión y cómo tooinstall, consulte [Azure PowerShell 1.0.](https://azure.microsoft.com/)
* Hola [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) y [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) módulos. Puede obtener versiones más recientes de Hola de estos módulos de hello [Galería de PowerShell](https://www.powershellgallery.com/)

Este artículo se explica cómo toouse Powershell de Azure con Azure Resource Manager tooconfigure y administrar la protección de los servidores. ejemplo de Hola usado en este artículo muestra cómo tooprotect una máquina virtual, que se ejecuta en un host de Hyper-V, tooAzure. Hola siguiendo los requisitos previos es ejemplo toothis específico. Para un conjunto más completo de requisitos para saludo diversos escenarios de recuperación de sitio, consulte la documentación de toohello pertenecen toothat escenario.

* Necesitará un host de Hyper-V que ejecute Windows Server 2012 R2 o Microsoft Hyper-V Server 2012 R2 que contenga una o varias máquinas virtuales.
* Servidores de Hyper-V conectados toohello Internet, ya sea directamente o a través de un servidor proxy.
* máquinas virtuales que desea tooprotect Hello deben cumplir las con [requisitos previos de la máquina Virtual](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="step-1-sign-in-tooyour-azure-account"></a>Paso 1: Iniciar sesión en tooyour cuenta de Azure
1. Abra una consola de PowerShell y ejecute este comando toosign en tooyour cuenta de Azure. Hola cmdlet, se abrirá una página web que le solicitará las credenciales de cuenta.

        Login-AzureRmAccount

    Como alternativa, también se incluyen en sus credenciales de cuenta como un parámetro toohello `Login-AzureRmAccount` cmdlet, mediante el uso de hello `-Credential` parámetro.

    Si es socio CSP funciona en nombre de un inquilino, especificar a cliente hello como inquilino, mediante su nombre de dominio principal de tenantID o inquilino.

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. Una cuenta puede tener varias suscripciones, por lo que deberá asociar suscripción Hola desea toouse con cuenta de hello.

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. Compruebe que la suscripción está registrada toouse Hola proveedores de Azure para los servicios de recuperación y recuperación del sitio, mediante el uso de hello siguientes comandos:

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   En la salida de hello de estos comandos, si hello **RegistrationState** se establece demasiado**registrado**, puede continuar tooStep 2. Si no es así, debe registrar proveedor de falta de hello en su suscripción.

   Hola tooregister el proveedor de Azure para la recuperación de sitio y servicios de recuperación, ejecute hello siguientes comandos:

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   Compruebe que los proveedores de Hola registran correctamente mediante Hola siga los comandos: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` y `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.

## <a name="step-2-set-up-hello-recovery-services-vault"></a>Paso 2: Configurar Hola que del almacén de servicios de recuperación
1. Crear un grupo de recursos de Azure Resource Manager en el que podrá crear almacén de Hola o usar un grupo de recursos existente. Puede crear un nuevo grupo de recursos mediante Hola siguiente comando:

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    donde variable hello $ResourceGroupName contiene el nombre de Hola Hola del grupo de recursos que desee toocreate y variable hello $Geo contiene hello Azure región en qué grupo de recursos de hello toocreate (por ejemplo, "Sur de Brasil").

    Puede obtener una lista de grupos de recursos en su suscripción mediante hello `Get-AzureRmResourceGroup` cmdlet.
2. Cree un nuevo almacén de Servicios de recuperación de Azure como sigue:

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    Puede recuperar una lista de los almacenes existentes mediante hello `Get-AzureRmRecoveryServicesVault` cmdlet.

> [!NOTE]
> Si desea que las operaciones de tooperform en almacenes de Site Recovery creados mediante el portal clásico de Hola o el módulo de administración de servicio de Azure PowerShell hello, puede recuperar una lista de estos almacenes mediante hello `Get-AzureRmSiteRecoveryVault` cmdlet. Debe crear un nuevo almacén de Servicios de recuperación para todas las operaciones nuevas. almacenes de Site Recovery de Hola que creó anteriormente se admiten, pero no tienen características más recientes de Hola.
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Paso 3: Establecer contexto de almacén de servicios de recuperación de Hola
1. Establecer el contexto del almacén de hello ejecutando Hola siguiente comando:

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a>Paso 4: Crear un sitio de Hyper-V y generar una nueva clave de registro de almacén para el sitio de Hola.
1. Cree un nuevo sitio de Hyper-V como sigue:

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    Este cmdlet inicia un sitio de recuperación del sitio trabajo toocreate hello y devuelve un objeto de trabajo de recuperación del sitio. Espere Hola trabajo toocomplete y compruebe que el trabajo de Hola se completó correctamente.

    Puede recuperar el objeto de trabajo de hello y, por tanto, comprobar estado actual de Hola de trabajo de hello, usando el cmdlet Get-AzureRmSiteRecoveryJob Hola.
2. Generar y descargar una clave de registro para el sitio de hello, como se indica a continuación:

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    Hola de copia había descargado host de Hyper-V de clave toohello. Necesita hello tooregister clave Hola Hyper-V host toohello sitio.

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a>Paso 5: Instalar el proveedor de Azure Site Recovery hello y agente de servicios de recuperación de Azure en su host de Hyper-V
1. Descargar el instalador de hello para la versión más reciente de Hola de proveedor de Hola desde [Microsoft](https://aka.ms/downloaddra).
2. Instalador de ejecución hello en el host de Hyper-V y al final de Hola de instalación de hello continuar paso de registro toohello.
3. Cuando se le solicite, proporcione Hola descarga clave de registro del sitio y completar el registro del sitio de toohello de host de Hyper-V de Hola.
4. Comprobar que hospedan Hola Hyper-V se sitio toohello registrados mediante Hola siguiente comando:

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a>Paso 6: Crear una directiva de replicación y asociarla con el contenedor de protección de Hola
1. Cree una directiva de replicación como sigue:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    Comprobación de hello devuelve tooensure de trabajo que la creación de directiva de replicación de hello tiene éxito.

   > [!IMPORTANT]
   > Hello cuenta de almacenamiento especificada debe ser en Hola la misma región de Azure como el almacén de servicios de recuperación y debe tener habilitada la replicación geográfica.
   >
   > * Si Hola especifica recuperación cuenta de almacenamiento es de tipo de almacenamiento de Azure (clásica), conmutación por error de hello protegido máquinas recuperar Hola máquina tooAzure IaaS (clásico).
   > * Si Hola especifica la cuenta de almacenamiento de recuperación es de tipo de almacenamiento de Azure (Administrador de recursos de Azure), conmutación por error de hello protegido máquinas recuperar Hola máquina tooAzure IaaS (Administrador de recursos de Azure).
   >
   >
2. Obtener Hola protección contenedor toohello sitio correspondiente, como se indica a continuación:

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. Iniciar asociación Hola del contenedor de protección de hello con la directiva de replicación de hello, como se indica a continuación:

     $Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer

   Espere a toocomplete de trabajo de asociación de Hola y asegúrese de que se ha completado correctamente.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Paso 7: Habilitación de la protección para las máquinas virtuales
1. Obtener Hola protección entidad correspondiente toohello VM desea tooprotect, como se indica a continuación:

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. Empezar a proteger máquina virtual de hello, como se indica a continuación:

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > Hello cuenta de almacenamiento especificada debe ser en Hola la misma región de Azure como el almacén de servicios de recuperación y debe tener habilitada la replicación geográfica.
   >
   > * Si Hola especifica recuperación cuenta de almacenamiento es de tipo de almacenamiento de Azure (clásica), conmutación por error de hello protegido máquinas recuperar Hola máquina tooAzure IaaS (clásico).
   > * Si Hola especifica la cuenta de almacenamiento de recuperación es de tipo de almacenamiento de Azure (Administrador de recursos de Azure), conmutación por error de hello protegido máquinas recuperar Hola máquina tooAzure IaaS (Administrador de recursos de Azure).
   >
   > Si Hola VM que se va a proteger tiene más de un disco tooit adjunto, especifique el disco del sistema operativo de hello con hello *OSDiskName* parámetro.
   >
   >
3. Espere a que tooreach de máquinas virtuales de hello un estado protegido después de la replicación inicial de Hola. Esto puede tardar bastante tiempo, dependiendo de factores como la cantidad de Hola de toobe de datos replicada y Hola tooAzure de nivel superior de ancho de banda disponible. Estado del trabajo de Hola y EstadoDescripción se actualizan como se indica a continuación, en hello VM llegar a un estado protegido.

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. Actualizar propiedades de recuperación, como Hola tamaño de rol de máquina virtual y conmutación por error de hello Azure red tooattach hello de la máquina virtual red interfaz tarjetas tooupon.

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a>Paso 8: Ejecución de una conmutación por error de prueba
1. Ejecute un trabajo de conmutación por error de prueba, como sigue:

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. Compruebe que se crea la VM en Azure de la prueba de Hola. (trabajo de conmutación por error de prueba de hello está suspendido, después de crear la máquina virtual de prueba de hello en Azure. Hola completa limpiando los artefactos de hello creado al reanudar trabajo hello, como se muestra en el paso siguiente Hola.)
3. Hola completa probar conmutación por error, como se indica a continuación:

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>Pasos siguientes
[Más información](https://msdn.microsoft.com/library/azure/mt637930.aspx) sobre los cmdlets de PowerShell de Azure Site Recovery con Azure Resource Manager.
