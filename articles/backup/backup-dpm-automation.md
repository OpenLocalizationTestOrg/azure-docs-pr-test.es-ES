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
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="288af-103">Implementar y administrar tooAzure copia de seguridad de los servidores de Data Protection Manager (DPM) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="288af-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="288af-104">ARM</span><span class="sxs-lookup"><span data-stu-id="288af-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="288af-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="288af-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="288af-106">Este artículo muestra cómo toouse PowerShell toosetup copia de seguridad de Azure en un servidor DPM y toomanage copia de seguridad y recuperación.</span><span class="sxs-lookup"><span data-stu-id="288af-106">This article shows you how toouse PowerShell toosetup Azure Backup on a DPM server, and toomanage backup and recovery.</span></span>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="288af-107">Configurar el entorno de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="288af-107">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="288af-108">Antes de realizar copias de seguridad de PowerShell toomanage desde tooAzure de Data Protection Manager, necesita toohave entorno derecho con hello en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="288af-108">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="288af-109">En el inicio de Hola Hola de sesión de PowerShell, asegúrese de que ejecute hello después módulos derecho de comando tooimport hello y le permiten toocorrectly referencia Hola DPM cmdlets:</span><span class="sxs-lookup"><span data-stu-id="288af-109">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="288af-110">Instalación y registro</span><span class="sxs-lookup"><span data-stu-id="288af-110">Setup and Registration</span></span>
<span data-ttu-id="288af-111">toobegin:</span><span class="sxs-lookup"><span data-stu-id="288af-111">toobegin:</span></span>

1. <span data-ttu-id="288af-112">[Descargue la última versión de PowerShell](https://github.com/Azure/azure-powershell/releases) (la versión mínima necesaria es: 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="288af-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="288af-113">Habilitar los cmdlets de copia de seguridad de Azure de hello cambiando demasiado*AzureResourceManager* modo mediante el uso de hello **Switch-AzureMode** commandlet:</span><span class="sxs-lookup"><span data-stu-id="288af-113">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="288af-114">Hello siguiente configuración y tareas de registro pueden automatizarse con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="288af-114">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="288af-115">Creación de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="288af-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="288af-116">Instalar el agente de copia de seguridad de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="288af-116">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="288af-117">Registrar con hello servicio de copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="288af-117">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="288af-118">Configuración de redes</span><span class="sxs-lookup"><span data-stu-id="288af-118">Networking settings</span></span>
* <span data-ttu-id="288af-119">Configuración de cifrado</span><span class="sxs-lookup"><span data-stu-id="288af-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="288af-120">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="288af-120">Create a recovery services vault</span></span>
<span data-ttu-id="288af-121">Hola pasos le guiará en el proceso de creación de un almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="288af-121">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="288af-122">Un almacén de Servicios de recuperación no es lo mismo que un almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="288af-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="288af-123">Si utilizas Azure Backup para hello primera vez, debe usar hello **AzureRMResourceProvider Register** cmdlet tooregister el proveedor de servicios de recuperación de Azure de hello con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="288af-123">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="288af-124">Hola almacén de servicios de recuperación es un recurso ARM, por lo que necesita tooplace dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="288af-124">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="288af-125">Puede usar un grupo de recursos existente o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="288af-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="288af-126">Al crear un nuevo grupo de recursos, especifique el nombre de Hola y ubicación para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-126">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="288af-127">Hola de uso **AzureRmRecoveryServicesVault New** cmdlet toocreate un nuevo almacén.</span><span class="sxs-lookup"><span data-stu-id="288af-127">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate a new vault.</span></span> <span data-ttu-id="288af-128">Asegúrese de toospecify Hola misma ubicación para el almacén de Hola que utilizó para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-128">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="288af-129">Especificar tipo de Hola de toouse de redundancia de almacenamiento; Puede usar [almacenamiento redundante local (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [almacenamiento con redundancia geográfica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="288af-129">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="288af-130">Hello en el ejemplo siguiente se muestra hello - BackupStorageRedundancy opción testVault está establecida tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="288af-130">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="288af-131">Muchos de los cmdlets de copia de seguridad de Azure requieren el objeto de almacén de servicios de recuperación de hello como entrada.</span><span class="sxs-lookup"><span data-stu-id="288af-131">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="288af-132">Por este motivo, resulta toostore conveniente Hola el objeto de almacén de servicios de recuperación de copia de seguridad en una variable.</span><span class="sxs-lookup"><span data-stu-id="288af-132">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="288af-133">Almacenes de Hola de vista en una suscripción</span><span class="sxs-lookup"><span data-stu-id="288af-133">View hello vaults in a subscription</span></span>
<span data-ttu-id="288af-134">Use **AzureRmRecoveryServicesVault Get** tooview lista de Hola de todos los almacenes en la suscripción actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-134">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="288af-135">Puede usar este toocheck de comando que se ha creado un nuevo almacén o toosee qué almacenes están disponibles en la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-135">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="288af-136">Ejecutar comandos de hello, Get-AzureRmRecoveryServicesVault, y se muestran todos los almacenes de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-136">Run hello command, Get-AzureRmRecoveryServicesVault, and all vaults in hello subscription are listed.</span></span>

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


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="288af-137">Instalar el agente de copia de seguridad de Azure de hello en un servidor DPM</span><span class="sxs-lookup"><span data-stu-id="288af-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="288af-138">Antes de instalar el agente de copia de seguridad de Azure de hello, necesita a instalador de hello toohave descargado y presente en hello Windows Server.</span><span class="sxs-lookup"><span data-stu-id="288af-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="288af-139">Puede obtener última versión del instalador de Hola de Hola de hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o desde la página del panel del almacén de servicios de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="288af-140">Guardar instalador hello tooan ubicación fácilmente accesible como * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="288af-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="288af-141">agente de hello tooinstall, ejecute el siguiente comando en una consola de PowerShell con privilegios elevados de Hola **en el servidor DPM Hola**:</span><span class="sxs-lookup"><span data-stu-id="288af-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="288af-142">Agente de Hola se instala con todas las opciones predeterminadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="288af-143">instalación de Hello tarda unos minutos en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="288af-144">Si no se especifica hello */nu* Hola opción **Windows Update** se abre la ventana final Hola de hello toocheck de instalación para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="288af-144">If you do not specify hello */nu* option hello **Windows Update** window opens at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="288af-145">agente de Hello aparece en la lista de Hola de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="288af-145">hello agent shows up in hello list of installed programs.</span></span> <span data-ttu-id="288af-146">lista de hello toosee de programas instalados, vaya demasiado**el Panel de Control** > **programas** > **programas y características**.</span><span class="sxs-lookup"><span data-stu-id="288af-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="288af-148">Opciones de instalación</span><span class="sxs-lookup"><span data-stu-id="288af-148">Installation options</span></span>
<span data-ttu-id="288af-149">toosee todas las opciones de hello disponibles a través de hello commandline, Hola de uso después de comando:</span><span class="sxs-lookup"><span data-stu-id="288af-149">toosee all hello options available via hello commandline, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="288af-150">Hola las opciones disponibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="288af-150">hello available options include:</span></span>

| <span data-ttu-id="288af-151">Opción</span><span class="sxs-lookup"><span data-stu-id="288af-151">Option</span></span> | <span data-ttu-id="288af-152">Detalles</span><span class="sxs-lookup"><span data-stu-id="288af-152">Details</span></span> | <span data-ttu-id="288af-153">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="288af-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="288af-154">/q</span><span class="sxs-lookup"><span data-stu-id="288af-154">/q</span></span> |<span data-ttu-id="288af-155">Instalación silenciosa</span><span class="sxs-lookup"><span data-stu-id="288af-155">Quiet installation</span></span> |- |
| <span data-ttu-id="288af-156">/p:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="288af-156">/p:"location"</span></span> |<span data-ttu-id="288af-157">Carpeta de instalación de toohello de ruta de acceso para el agente de copia de seguridad de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="288af-158">C:\Archivos de programa\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="288af-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="288af-159">/s:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="288af-159">/s:"location"</span></span> |<span data-ttu-id="288af-160">Carpeta de caché de ruta de acceso toohello para el agente de copia de seguridad de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="288af-161">C:\Archivos de programa\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="288af-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="288af-162">/m</span><span class="sxs-lookup"><span data-stu-id="288af-162">/m</span></span> |<span data-ttu-id="288af-163">Participación en tooMicrosoft actualización</span><span class="sxs-lookup"><span data-stu-id="288af-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="288af-164">/nu</span><span class="sxs-lookup"><span data-stu-id="288af-164">/nu</span></span> |<span data-ttu-id="288af-165">No busca actualizaciones una vez completada la instalación</span><span class="sxs-lookup"><span data-stu-id="288af-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="288af-166">/d</span><span class="sxs-lookup"><span data-stu-id="288af-166">/d</span></span> |<span data-ttu-id="288af-167">Desinstala el agente de Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="288af-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="288af-168">/ph</span><span class="sxs-lookup"><span data-stu-id="288af-168">/ph</span></span> |<span data-ttu-id="288af-169">Dirección host del proxy</span><span class="sxs-lookup"><span data-stu-id="288af-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="288af-170">/po</span><span class="sxs-lookup"><span data-stu-id="288af-170">/po</span></span> |<span data-ttu-id="288af-171">Número de puerto del host de proxy</span><span class="sxs-lookup"><span data-stu-id="288af-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="288af-172">/pu</span><span class="sxs-lookup"><span data-stu-id="288af-172">/pu</span></span> |<span data-ttu-id="288af-173">Nombre de usuario del host de proxy</span><span class="sxs-lookup"><span data-stu-id="288af-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="288af-174">/pw</span><span class="sxs-lookup"><span data-stu-id="288af-174">/pw</span></span> |<span data-ttu-id="288af-175">Contraseña de proxy</span><span class="sxs-lookup"><span data-stu-id="288af-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a><span data-ttu-id="288af-176">Registrar tooa almacén de servicios de recuperación DPM</span><span class="sxs-lookup"><span data-stu-id="288af-176">Registering DPM tooa Recovery Services Vault</span></span>
<span data-ttu-id="288af-177">Una vez creado el almacén de servicios de recuperación de hello, descargar agente más reciente de Hola y las credenciales de almacén de Hola y almacenarlo en una ubicación adecuada como C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="288af-177">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="288af-178">En el servidor DPM hello, ejecute hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) máquina de hello tooregister de cmdlet con el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-178">On hello DPM server, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="288af-179">Opciones de configuración inicial</span><span class="sxs-lookup"><span data-stu-id="288af-179">Initial configuration settings</span></span>
<span data-ttu-id="288af-180">Una vez Hola servidor DPM está registrado con hello del almacén de servicios de recuperación, se inicia con la configuración de la suscripción de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="288af-180">Once hello DPM Server is registered with hello Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="288af-181">Estas opciones de suscripción incluyen hello área de almacenamiento provisional, cifrado y las redes.</span><span class="sxs-lookup"><span data-stu-id="288af-181">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="288af-182">configuración de la suscripción de toochange necesita toofirst obtener un identificador de configuración (valor predeterminado) actual hello mediante hello [DPMCloudSubscriptionSetting Get](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="288af-182">toochange subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="288af-183">Todas las modificaciones son objeto de PowerShell local realiza toothis ```$setting``` y, a continuación, objetos hello es confirmada tooDPM y toosave de copia de seguridad de Azure mediante hello [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-183">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="288af-184">Necesita hello toouse ```–Commit``` tooensure de marca que Hola cambios se conservan.</span><span class="sxs-lookup"><span data-stu-id="288af-184">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="288af-185">configuración de Hello no se aplican y se usará copia de seguridad de Azure a menos que se confirma.</span><span class="sxs-lookup"><span data-stu-id="288af-185">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="288af-186">Redes</span><span class="sxs-lookup"><span data-stu-id="288af-186">Networking</span></span>
<span data-ttu-id="288af-187">Si la conectividad de Hola de hello DPM máquina toohello servicio de copia de seguridad de Azure en hello internet es a través de un servidor proxy, configuración del servidor proxy Hola debe proporcionarse para copias de seguridad correctas.</span><span class="sxs-lookup"><span data-stu-id="288af-187">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="288af-188">Esto se realiza mediante hello ```-ProxyServer```y ```-ProxyPort```, ```-ProxyUsername``` hello y ```ProxyPassword``` parámetros con hello [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-188">This is done by using hello ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="288af-189">En este ejemplo, no hay ningún servidor proxy y por tanto se borra explícitamente cualquier información relacionada con el proxy.</span><span class="sxs-lookup"><span data-stu-id="288af-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="288af-190">También se puede controlar el uso de ancho de banda con opciones de ```-WorkHourBandwidth``` y ```-NonWorkHourBandwidth``` para un conjunto determinado de días de la semana de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="288af-191">En este ejemplo no se define ninguna limitación.</span><span class="sxs-lookup"><span data-stu-id="288af-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a><span data-ttu-id="288af-192">Configuración de área de almacenamiento provisional de Hola</span><span class="sxs-lookup"><span data-stu-id="288af-192">Configuring hello staging Area</span></span>
<span data-ttu-id="288af-193">agente de copia de seguridad de Azure Hola ejecutando en el servidor DPM Hola necesita almacenamiento temporal para los datos restaurados desde la nube de hello (área de almacenamiento provisional local).</span><span class="sxs-lookup"><span data-stu-id="288af-193">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="288af-194">Configurar el área de ensayo de hello mediante hello [conjunto DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet hello y ```-StagingAreaPath``` parámetro.</span><span class="sxs-lookup"><span data-stu-id="288af-194">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="288af-195">En el ejemplo de Hola anterior, área de almacenamiento provisional de Hola se establecerá demasiado*C:\StagingArea* en el objeto de PowerShell de hello ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="288af-195">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="288af-196">Asegúrese de que ya existe la carpeta especificada de hello, o bien se producirá un error en la confirmación final de Hola de configuración de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-196">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="288af-197">Configuración de cifrado</span><span class="sxs-lookup"><span data-stu-id="288af-197">Encryption settings</span></span>
<span data-ttu-id="288af-198">Hola copia de seguridad de datos enviados tooAzure copia de seguridad es cifrada tooprotect Hola confidencialidad de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-198">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="288af-199">Hola frase de contraseña es datos de contraseña"hello" toodecrypt hello en tiempo de Hola de restauración.</span><span class="sxs-lookup"><span data-stu-id="288af-199">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="288af-200">Importante tookeep esta información es segura para y proteger una vez que se establece.</span><span class="sxs-lookup"><span data-stu-id="288af-200">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="288af-201">En el siguiente ejemplo de Hola, primer comando de hello convierte la cadena de hello ```passphrase123456789``` tooa segura cadena y asigna Hola segura toohello variable de cadena denominada ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="288af-201">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="288af-202">Hola segundo comando establece cadena segura de hello ```$Passphrase``` como contraseña de Hola para cifrar las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="288af-202">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="288af-203">Almacenar información de la frase de contraseña de hello seguro y protegido una vez que se establece.</span><span class="sxs-lookup"><span data-stu-id="288af-203">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="288af-204">No será capaz de toorestore datos de Azure sin esta frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="288af-204">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="288af-205">En este punto, debería haber realizado todas las Hola requiere cambios toohello ```$setting``` objeto.</span><span class="sxs-lookup"><span data-stu-id="288af-205">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="288af-206">Recuerde los cambios de hello toocommit.</span><span class="sxs-lookup"><span data-stu-id="288af-206">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="288af-207">Proteger datos tooAzure copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="288af-207">Protect data tooAzure Backup</span></span>
<span data-ttu-id="288af-208">En esta sección, agregará un tooDPM del servidor de producción y, a continuación, proteger el almacenamiento DPM de hello datos toolocal y, a continuación, tooAzure copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="288af-208">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="288af-209">En los ejemplos de hello, demostraremos cómo tooback seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="288af-209">In hello examples, we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="288af-210">Hello lógica puede fácilmente ser extendido toobackup cualquier origen de datos compatibles con DPM.</span><span class="sxs-lookup"><span data-stu-id="288af-210">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="288af-211">Las copias de seguridad de DPM se rigen por un grupo de protección (PG) con cuatro partes:</span><span class="sxs-lookup"><span data-stu-id="288af-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="288af-212">**Miembros del grupo** es una lista de todos los objetos que se pueden proteger de hello (también conocido como *orígenes de datos* en DPM) que desea tooprotect Hola mismo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="288af-212">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="288af-213">Por ejemplo, puede que desee tooprotect producción máquinas virtuales en un grupo de protección y las bases de datos de SQL Server en otro grupo de protección como pueden tener distintos requisitos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="288af-213">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="288af-214">Antes de hacer copias de seguridad ningún origen de datos en un servidor de producción debe toomake seguro Hola agente de DPM está instalado en el servidor de Hola y administrado por DPM.</span><span class="sxs-lookup"><span data-stu-id="288af-214">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="288af-215">Siga los pasos de Hola para [instalar Hola agente DPM](https://technet.microsoft.com/library/bb870935.aspx) y vinculándolo toohello adecuados en el servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="288af-215">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="288af-216">**Método de protección de datos** especifica ubicaciones Hola destino de copia de seguridad - cinta y disco, en la nube.</span><span class="sxs-lookup"><span data-stu-id="288af-216">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="288af-217">En nuestro ejemplo protegemos datos toohello local disco y toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="288af-217">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="288af-218">A **programar copia de seguridad** que especifica si las copias de seguridad necesitan toobe realizada y con qué frecuencia hello datos se sincronicen entre Hola servidor DPM y el servidor de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="288af-218">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="288af-219">A **programación de retención** que especifica cuánto tiempo los puntos de recuperación de hello tooretain en Azure.</span><span class="sxs-lookup"><span data-stu-id="288af-219">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="288af-220">Creación de un grupo de protección</span><span class="sxs-lookup"><span data-stu-id="288af-220">Creating a protection group</span></span>
<span data-ttu-id="288af-221">Empiece por crear un nuevo grupo de protección mediante hello [DPMProtectionGroup New](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-221">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="288af-222">Hola anteriormente cmdlet creará un grupo de protección denominado *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="288af-222">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="288af-223">También es posible modificar un grupo de protección posterior toohello de copia de seguridad de tooadd nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="288af-223">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="288af-224">Sin embargo, toomake cambios toohello grupo de protección: nuevos o existentes - necesitamos tooget un identificador en un *modificable* objeto mediante hello [DPMModifiableProtectionGroup Get](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-224">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="288af-225">Agregar miembros de grupo toohello grupo de protección</span><span class="sxs-lookup"><span data-stu-id="288af-225">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="288af-226">Cada agente de DPM sabe lista Hola de orígenes de datos en el servidor de Hola que se instala en.</span><span class="sxs-lookup"><span data-stu-id="288af-226">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="288af-227">tooadd un grupo de protección de toohello de origen de datos, Hola agente DPM necesidades toofirst envíe una lista del servidor DPM de hello orígenes de datos back-toohello.</span><span class="sxs-lookup"><span data-stu-id="288af-227">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="288af-228">Uno o más orígenes de datos no están seleccionado y agregado toohello grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="288af-228">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="288af-229">pasos de PowerShell de Hello necesitan tooachieve esto son:</span><span class="sxs-lookup"><span data-stu-id="288af-229">hello PowerShell steps needed tooachieve this are:</span></span>

1. <span data-ttu-id="288af-230">Capturar una lista de todos los servidores administrados por DPM a través de hello agente DPM.</span><span class="sxs-lookup"><span data-stu-id="288af-230">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="288af-231">Elija un servidor específico.</span><span class="sxs-lookup"><span data-stu-id="288af-231">Choose a specific server.</span></span>
3. <span data-ttu-id="288af-232">Capturar una lista de todos los orígenes de datos en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-232">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="288af-233">Elija uno o más orígenes de datos y agregarlas toohello grupo de protección</span><span class="sxs-lookup"><span data-stu-id="288af-233">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="288af-234">Hola lista de servidores en qué Hola agente de DPM está instalado y se está administrando mediante Hola servidor DPM se adquirió con hello [DPMProductionServer Get](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-234">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="288af-235">En este ejemplo se van a filtrar y configurar solo PS con el nombre *productionserver01* para efectuar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="288af-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="288af-236">Ahora buscar de la lista de Hola de orígenes de datos ```$server``` con hello [DPMDatasource Get](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-236">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="288af-237">En este ejemplo se filtra para el volumen de Hola * D:\* que deseamos tooconfigure para copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="288af-237">In this example we are filtering for hello volume *D:\* that we want tooconfigure for backup.</span></span> <span data-ttu-id="288af-238">Este origen de datos, a continuación, se agrega toohello grupo de protección mediante hello [DPMChildDatasource agregar](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-238">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="288af-239">Recuerde hello toouse *modificable* objeto de grupo de protección ```$MPG``` adiciones de hello toomake.</span><span class="sxs-lookup"><span data-stu-id="288af-239">Remember toouse hello *modifiable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="288af-240">Repita este paso tantas veces como sea necesario, hasta que haya agregado todos los Hola elegido el grupo de protección de toohello de orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="288af-240">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="288af-241">También puede comenzar con un solo origen de datos y flujo de trabajo de hello completa para crear el grupo de protección de Hola y en un momento posterior, agregar más orígenes de datos toohello grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="288af-241">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="288af-242">Seleccionar método de protección de datos de hello</span><span class="sxs-lookup"><span data-stu-id="288af-242">Selecting hello data protection method</span></span>
<span data-ttu-id="288af-243">Una vez que se agregaron a orígenes de datos de hello toohello grupo de protección, Hola siguiente paso es método de protección de hello toospecify con hello [DPMProtectionType conjunto](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-243">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="288af-244">En este ejemplo, hello grupo de protección está configurado para el disco local y copia de seguridad en la nube.</span><span class="sxs-lookup"><span data-stu-id="288af-244">In this example, hello Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="288af-245">También necesita toospecify Hola datasource que desea toocloud tooprotect con hello [DPMChildDatasource agregar](https://technet.microsoft.com/library/hh881732.aspx) cmdlet con - marcador en línea.</span><span class="sxs-lookup"><span data-stu-id="288af-245">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="288af-246">Establecer la duración de retención de Hola</span><span class="sxs-lookup"><span data-stu-id="288af-246">Setting hello retention range</span></span>
<span data-ttu-id="288af-247">Establecer retención de Hola para puntos de copia de seguridad de hello mediante hello [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-247">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="288af-248">Pese a que podría parecer retención de hello tooset impar para definir programación de copia de seguridad de hello, con hello ```Set-DPMPolicyObjective``` cmdlet establece automáticamente una programación de copia de seguridad predeterminada que se pueden modificar.</span><span class="sxs-lookup"><span data-stu-id="288af-248">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="288af-249">Siempre es programar copia de seguridad de tooset posible Hola por primera vez y Hola directiva de retención después.</span><span class="sxs-lookup"><span data-stu-id="288af-249">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="288af-250">En el siguiente ejemplo de Hola, Hola establece los parámetros de retención de Hola para copias de seguridad de disco.</span><span class="sxs-lookup"><span data-stu-id="288af-250">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="288af-251">Esto conservarán las copias de seguridad de 10 días y sincronizar los datos cada 6 horas entre el servidor de producción de hello y el servidor DPM Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-251">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="288af-252">Hola ```SynchronizationFrequencyMinutes``` no se define con qué frecuencia se crea un punto de copia de seguridad, pero ¿cómo a menudo los datos están el servidor DPM toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="288af-252">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server.</span></span>  <span data-ttu-id="288af-253">Esto evita que las copias de seguridad se vuelvan demasiado grandes.</span><span class="sxs-lookup"><span data-stu-id="288af-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="288af-254">Para copias de seguridad que se va tooAzure (DPM hace referencia toothem como copias de seguridad en línea) se pueden configurar intervalos de retención de Hola para [utilizando un esquema de su Abuelo-padre-hijo (GFS) de retención a largo plazo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="288af-254">For backups going tooAzure (DPM refers toothem as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="288af-255">Es decir, puede definir una directiva de retención combinada que implique directivas de retención diaria, semanal, mensual y anual.</span><span class="sxs-lookup"><span data-stu-id="288af-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="288af-256">En este ejemplo, se crea una matriz que representa el esquema de retención complejos de Hola que queremos y, a continuación, configurar la duración de retención de hello mediante hello [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-256">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="288af-257">Programación de copia de seguridad de hello establecida</span><span class="sxs-lookup"><span data-stu-id="288af-257">Set hello backup schedule</span></span>
<span data-ttu-id="288af-258">DPM establece una programación de copia de seguridad predeterminada automáticamente si se especifica el objetivo de protección de hello mediante hello ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-258">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="288af-259">toochange las programaciones predeterminadas hello, usar hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet seguido por hello [DPMPolicySchedule conjunto](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-259">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="288af-260">Hola por encima de ejemplo, ```$onlineSch``` es una matriz con cuatro elementos que contiene la programación de protección en línea existente de Hola de hello grupo de protección en el esquema GFS hello:</span><span class="sxs-lookup"><span data-stu-id="288af-260">In hello above example, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="288af-261">```$onlineSch[0]```contiene las programaciones diarias Hola</span><span class="sxs-lookup"><span data-stu-id="288af-261">```$onlineSch[0]``` contains hello daily schedule</span></span>
2. <span data-ttu-id="288af-262">```$onlineSch[1]```contiene las programaciones semanales Hola</span><span class="sxs-lookup"><span data-stu-id="288af-262">```$onlineSch[1]``` contains hello weekly schedule</span></span>
3. <span data-ttu-id="288af-263">```$onlineSch[2]```contiene la programación mensual Hola</span><span class="sxs-lookup"><span data-stu-id="288af-263">```$onlineSch[2]``` contains hello monthly schedule</span></span>
4. <span data-ttu-id="288af-264">```$onlineSch[3]```contiene la programación anual Hola</span><span class="sxs-lookup"><span data-stu-id="288af-264">```$onlineSch[3]``` contains hello yearly schedule</span></span>

<span data-ttu-id="288af-265">Por ello, si necesita programación semanal de toomodify hello, debe toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="288af-265">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="288af-266">Copia de seguridad inicial</span><span class="sxs-lookup"><span data-stu-id="288af-266">Initial backup</span></span>
<span data-ttu-id="288af-267">Cuando copia de seguridad de un origen de datos para hello primera vez, DPM necesidades crea réplica inicial que crea una copia completa de hello toobe de origen de datos protegido en el volumen de réplica DPM.</span><span class="sxs-lookup"><span data-stu-id="288af-267">When backing up a datasource for hello first time, DPM needs creates initial replica that creates a full copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="288af-268">Esta actividad puede programarse para una hora específica o puede desencadenar manualmente, mediante hello [conjunto DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet con el parámetro hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="288af-268">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="288af-269">Cambiar el tamaño de Hola de réplica de DPM y el volumen de punto de recuperación</span><span class="sxs-lookup"><span data-stu-id="288af-269">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="288af-270">También puede cambiar tamaño de hello del volumen de réplica de DPM y el uso del volumen de instantánea [DPMDatasourceDiskAllocation conjunto](https://technet.microsoft.com/library/hh881618.aspx) cmdlet como en el siguiente ejemplo de Hola: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manual - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="288af-270">You can also change hello size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="288af-271">Confirmar Hola cambia toohello grupo de protección</span><span class="sxs-lookup"><span data-stu-id="288af-271">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="288af-272">Por último, cambios de hello necesitan toobe confirmado antes de que DPM puede realizar la copia de seguridad de Hola por la configuración del nuevo grupo de protección de Hola.</span><span class="sxs-lookup"><span data-stu-id="288af-272">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="288af-273">Esto puede lograrse mediante hello [DPMProtectionGroup conjunto](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-273">This can be achieved using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="288af-274">Ver los puntos de copia de seguridad Hola</span><span class="sxs-lookup"><span data-stu-id="288af-274">View hello backup points</span></span>
<span data-ttu-id="288af-275">Puede usar hello [DPMRecoveryPoint Get](https://technet.microsoft.com/library/hh881746) cmdlet tooget una lista de todos los puntos de recuperación para un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="288af-275">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="288af-276">En este ejemplo, se realiza lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="288af-276">In this example, we will:</span></span>

* <span data-ttu-id="288af-277">captura todas Hola documento en el servidor DPM hello y almacenados en una matriz```$PG```</span><span class="sxs-lookup"><span data-stu-id="288af-277">fetch all hello PGs on hello DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="288af-278">obtener toohello correspondiente de hello orígenes de datos```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="288af-278">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="288af-279">obtener todos los puntos de recuperación de Hola para un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="288af-279">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="288af-280">Restauración de datos protegidos en Azure</span><span class="sxs-lookup"><span data-stu-id="288af-280">Restore data protected on Azure</span></span>
<span data-ttu-id="288af-281">Restauración de datos es una combinación de un objeto ```RecoverableItem``` y un objeto ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="288af-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="288af-282">En la sección anterior de hello, que obtuvimos una lista de puntos de copia de seguridad de Hola para un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="288af-282">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="288af-283">En el ejemplo de Hola siguiente, se muestran la máquina virtual de Hyper-V toorestore de copia de seguridad de Azure puntos de copia de seguridad de combinación con hello de destino para la recuperación.</span><span class="sxs-lookup"><span data-stu-id="288af-283">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="288af-284">Este ejemplo incluye:</span><span class="sxs-lookup"><span data-stu-id="288af-284">This example includes:</span></span>

* <span data-ttu-id="288af-285">Crear una opción de recuperación utilizando hello [DPMRecoveryOption New](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-285">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="288af-286">Obteniendo Hola matriz de copia de seguridad puntos con hello ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="288af-286">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="288af-287">Elegir un toorestore de punto de copia de seguridad de.</span><span class="sxs-lookup"><span data-stu-id="288af-287">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="288af-288">comandos de Hola se pueden extender con facilidad para cualquier tipo de origen de datos.</span><span class="sxs-lookup"><span data-stu-id="288af-288">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="288af-289">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="288af-289">Next steps</span></span>
* <span data-ttu-id="288af-290">Para obtener más información acerca de DPM vea tooAzure copia de seguridad [Introducción tooDPM copia de seguridad](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="288af-290">For more information about DPM tooAzure Backup see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
