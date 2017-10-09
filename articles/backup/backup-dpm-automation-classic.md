---
title: 'Copia de seguridad de Azure: Usar PowerShell tooback seguridad cargas de trabajo DPM | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toodeploy y administrar copias de seguridad de Azure para Data Protection Manager (DPM) con PowerShell"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="960dc-103">Implementar y administrar tooAzure copia de seguridad de los servidores de Data Protection Manager (DPM) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="960dc-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="960dc-104">ARM</span><span class="sxs-lookup"><span data-stu-id="960dc-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="960dc-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="960dc-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="960dc-106">Este artículo se explica cómo toouse PowerShell tooback una copia de seguridad y recuperar datos DPM desde un almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="960dc-106">This article explains how toouse PowerShell tooback up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="960dc-107">Microsoft recomienda el uso de almacenes de Recovery Services para todas las implementaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="960dc-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="960dc-108">Si es un nuevo usuario de copia de seguridad de Azure, use el artículo de hello, [implementar y administrar tooAzure de datos de Data Protection Manager mediante PowerShell](backup-dpm-automation.md), por lo que los datos se almacenan en un almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="960dc-108">If you are a new Azure Backup user, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="960dc-109">Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="960dc-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="960dc-110">Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="960dc-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="960dc-111">Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="960dc-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="960dc-112">Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="960dc-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="960dc-113">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="960dc-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="960dc-114">Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="960dc-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="960dc-115">No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="960dc-116">En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="960dc-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="960dc-117">Configurar el entorno de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="960dc-117">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="960dc-118">Antes de realizar copias de seguridad de PowerShell toomanage desde tooAzure de Data Protection Manager, deberá toohave Hola entorno de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="960dc-118">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you will need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="960dc-119">En el inicio de Hola Hola de sesión de PowerShell, asegúrese de que ejecute hello después módulos derecho de comando tooimport hello y le permiten toocorrectly referencia Hola DPM cmdlets:</span><span class="sxs-lookup"><span data-stu-id="960dc-119">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="960dc-120">Instalación y registro</span><span class="sxs-lookup"><span data-stu-id="960dc-120">Setup and Registration</span></span>
<span data-ttu-id="960dc-121">toobegin:</span><span class="sxs-lookup"><span data-stu-id="960dc-121">toobegin:</span></span>

1. <span data-ttu-id="960dc-122">[Descargue la versión de PowerShell más reciente](https://github.com/Azure/azure-powershell/releases) (la versión mínima necesaria es: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="960dc-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="960dc-123">Habilitar los cmdlets de copia de seguridad de Azure de hello cambiando demasiado*AzureResourceManager* modo mediante el uso de hello **Switch-AzureMode** commandlet:</span><span class="sxs-lookup"><span data-stu-id="960dc-123">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="960dc-124">Hello siguiente configuración y tareas de registro pueden automatizarse con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="960dc-124">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="960dc-125">Creación de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="960dc-125">Create a backup vault</span></span>
* <span data-ttu-id="960dc-126">Instalar el agente de copia de seguridad de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="960dc-126">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="960dc-127">Registrar con hello servicio de copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="960dc-127">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="960dc-128">Configuración de redes</span><span class="sxs-lookup"><span data-stu-id="960dc-128">Networking settings</span></span>
* <span data-ttu-id="960dc-129">Configuración de cifrado</span><span class="sxs-lookup"><span data-stu-id="960dc-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="960dc-130">Creación de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="960dc-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="960dc-131">Para los clientes mediante copia de seguridad de Azure Hola primera vez, deberá toobe de proveedor de copia de seguridad de Azure tooregister Hola usado con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="960dc-131">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="960dc-132">Puede hacerlo ejecutando el siguiente comando de hello: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="960dc-132">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="960dc-133">Puede crear un nuevo almacén de copia de seguridad mediante hello **AzureRMBackupVault New** commandlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-133">You can create a new backup vault using hello **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="960dc-134">almacén de copia de seguridad de Hello es un recurso ARM, por lo que necesita tooplace dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="960dc-134">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="960dc-135">En una consola de Azure PowerShell con privilegios elevados, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="960dc-135">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="960dc-136">Puede obtener una lista de todos los almacenes de copia de seguridad de hello en una suscripción determinada utilizando hello **AzureRMBackupVault Get** commandlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-136">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="960dc-137">Instalar el agente de copia de seguridad de Azure de hello en un servidor DPM</span><span class="sxs-lookup"><span data-stu-id="960dc-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="960dc-138">Antes de instalar el agente de copia de seguridad de Azure de hello, necesita a instalador de hello toohave descargado y presente en hello Windows Server.</span><span class="sxs-lookup"><span data-stu-id="960dc-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="960dc-139">Puede obtener última versión del instalador de Hola de Hola de hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o desde la página del panel del almacén de hello copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="960dc-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="960dc-140">Guardar instalador hello tooan ubicación fácilmente accesible como * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="960dc-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="960dc-141">agente de hello tooinstall, ejecute el siguiente comando en una consola de PowerShell con privilegios elevados de Hola **en el servidor DPM Hola**:</span><span class="sxs-lookup"><span data-stu-id="960dc-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="960dc-142">Agente de Hola se instala con todas las opciones predeterminadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="960dc-143">instalación de Hello tarda unos minutos en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="960dc-144">Si no se especifica hello */nu* Hola opción **Windows Update** se abrirá la ventana final Hola de hello toocheck de instalación para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="960dc-144">If you do not specify hello */nu* option hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="960dc-145">agente de Hola se mostrará en la lista de Hola de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="960dc-145">hello agent will show in hello list of installed programs.</span></span> <span data-ttu-id="960dc-146">lista de hello toosee de programas instalados, vaya demasiado**el Panel de Control** > **programas** > **programas y características**.</span><span class="sxs-lookup"><span data-stu-id="960dc-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="960dc-148">Opciones de instalación</span><span class="sxs-lookup"><span data-stu-id="960dc-148">Installation options</span></span>
<span data-ttu-id="960dc-149">toosee todas las opciones disponibles a través de Hola Hola de línea de comandos, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="960dc-149">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="960dc-150">Hola las opciones disponibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="960dc-150">hello available options include:</span></span>

| <span data-ttu-id="960dc-151">Opción</span><span class="sxs-lookup"><span data-stu-id="960dc-151">Option</span></span> | <span data-ttu-id="960dc-152">Detalles</span><span class="sxs-lookup"><span data-stu-id="960dc-152">Details</span></span> | <span data-ttu-id="960dc-153">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="960dc-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="960dc-154">/q</span><span class="sxs-lookup"><span data-stu-id="960dc-154">/q</span></span> |<span data-ttu-id="960dc-155">Instalación silenciosa</span><span class="sxs-lookup"><span data-stu-id="960dc-155">Quiet installation</span></span> |- |
| <span data-ttu-id="960dc-156">/p:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="960dc-156">/p:"location"</span></span> |<span data-ttu-id="960dc-157">Carpeta de instalación de toohello de ruta de acceso para el agente de copia de seguridad de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="960dc-158">C:\Archivos de programa\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="960dc-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="960dc-159">/s:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="960dc-159">/s:"location"</span></span> |<span data-ttu-id="960dc-160">Carpeta de caché de ruta de acceso toohello para el agente de copia de seguridad de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="960dc-161">C:\Archivos de programa\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="960dc-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="960dc-162">/m</span><span class="sxs-lookup"><span data-stu-id="960dc-162">/m</span></span> |<span data-ttu-id="960dc-163">Participación en tooMicrosoft actualización</span><span class="sxs-lookup"><span data-stu-id="960dc-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="960dc-164">/nu</span><span class="sxs-lookup"><span data-stu-id="960dc-164">/nu</span></span> |<span data-ttu-id="960dc-165">No busca actualizaciones una vez completada la instalación</span><span class="sxs-lookup"><span data-stu-id="960dc-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="960dc-166">/d</span><span class="sxs-lookup"><span data-stu-id="960dc-166">/d</span></span> |<span data-ttu-id="960dc-167">Desinstala el agente de Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="960dc-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="960dc-168">/ph</span><span class="sxs-lookup"><span data-stu-id="960dc-168">/ph</span></span> |<span data-ttu-id="960dc-169">Dirección host del proxy</span><span class="sxs-lookup"><span data-stu-id="960dc-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="960dc-170">/po</span><span class="sxs-lookup"><span data-stu-id="960dc-170">/po</span></span> |<span data-ttu-id="960dc-171">Número de puerto del host de proxy</span><span class="sxs-lookup"><span data-stu-id="960dc-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="960dc-172">/pu</span><span class="sxs-lookup"><span data-stu-id="960dc-172">/pu</span></span> |<span data-ttu-id="960dc-173">Nombre de usuario del host de proxy</span><span class="sxs-lookup"><span data-stu-id="960dc-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="960dc-174">/pw</span><span class="sxs-lookup"><span data-stu-id="960dc-174">/pw</span></span> |<span data-ttu-id="960dc-175">Contraseña de proxy</span><span class="sxs-lookup"><span data-stu-id="960dc-175">Proxy Password</span></span> |- |

### <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="960dc-176">Registrar con hello servicio de copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="960dc-176">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="960dc-177">Para poder registrar con hello servicio de copia de seguridad de Azure, necesita tooensure ese hello [requisitos previos](backup-azure-dpm-introduction.md) se cumplen.</span><span class="sxs-lookup"><span data-stu-id="960dc-177">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="960dc-178">Debe:</span><span class="sxs-lookup"><span data-stu-id="960dc-178">You must:</span></span>

* <span data-ttu-id="960dc-179">Disponer de una suscripción válida a Azure</span><span class="sxs-lookup"><span data-stu-id="960dc-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="960dc-180">Disponer de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="960dc-180">Have a backup vault</span></span>

<span data-ttu-id="960dc-181">las credenciales de almacén de hello toodownload, ejecute hello **Get AzureBackupVaultCredentials** commandlet en una consola de PowerShell de Azure y el almacén en una ubicación conveniente, como * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="960dc-181">toodownload hello vault credentials, run hello **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="960dc-182">Máquina de hello registrar con el almacén de Hola se lleva a cabo mediante hello [DPMCloudRegistration inicio](https://technet.microsoft.com/library/jj612787) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="960dc-182">Registering hello machine with hello vault is done using hello [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="960dc-183">Se registrarán Hola denominado "TestingServer" el servidor DPM con el almacén de Microsoft Azure con hello especificado del almacén de credenciales.</span><span class="sxs-lookup"><span data-stu-id="960dc-183">This will register hello DPM Server named “TestingServer” with Microsoft Azure Vault using hello specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="960dc-184">No utilice el archivo de credenciales de almacén de rutas de acceso relativas toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-184">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="960dc-185">Debe proporcionar una ruta de acceso absoluta como un cmdlet de entrada toohello.</span><span class="sxs-lookup"><span data-stu-id="960dc-185">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="960dc-186">Opciones de configuración inicial</span><span class="sxs-lookup"><span data-stu-id="960dc-186">Initial configuration settings</span></span>
<span data-ttu-id="960dc-187">Una vez hello servidor DPM está registrado con el almacén de copia de seguridad de Azure hello, se iniciará con la configuración de la suscripción de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="960dc-187">Once hello DPM Server is registered with hello Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="960dc-188">Estas opciones de suscripción incluyen hello área de almacenamiento provisional, cifrado y las redes.</span><span class="sxs-lookup"><span data-stu-id="960dc-188">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="960dc-189">toobegin cambiar la configuración de suscripción Hola necesita toofirst obtener un identificador de configuración (valor predeterminado) actual hello mediante hello [DPMCloudSubscriptionSetting Get](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="960dc-189">toobegin changing hello subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="960dc-190">Todas las modificaciones son objeto de PowerShell local realiza toothis ```$setting``` y, a continuación, objetos hello es confirmada tooDPM y toosave de copia de seguridad de Azure mediante hello [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-190">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="960dc-191">Necesita hello toouse ```–Commit``` tooensure de marca que Hola cambios se conservan.</span><span class="sxs-lookup"><span data-stu-id="960dc-191">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="960dc-192">configuración de Hello no se aplican y se usará copia de seguridad de Azure a menos que se confirma.</span><span class="sxs-lookup"><span data-stu-id="960dc-192">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="960dc-193">Redes</span><span class="sxs-lookup"><span data-stu-id="960dc-193">Networking</span></span>
<span data-ttu-id="960dc-194">Si la conectividad de Hola de hello DPM máquina toohello servicio de copia de seguridad de Azure en hello internet es a través de un servidor proxy, configuración del servidor proxy Hola debe proporcionarse para toosucceed de las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="960dc-194">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for backups toosucceed.</span></span> <span data-ttu-id="960dc-195">Esto se realiza mediante hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` hello y ```ProxyPassword``` parámetros con hello [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-195">This is done by using hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="960dc-196">En este ejemplo, no hay ningún servidor proxy y por tanto se borra explícitamente cualquier información relacionada con el proxy.</span><span class="sxs-lookup"><span data-stu-id="960dc-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="960dc-197">También se puede controlar el uso de ancho de banda con opciones de ```-WorkHourBandwidth``` y ```-NonWorkHourBandwidth``` para un conjunto determinado de días de la semana de Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="960dc-198">En este ejemplo no estamos definiendo ninguna limitación.</span><span class="sxs-lookup"><span data-stu-id="960dc-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a><span data-ttu-id="960dc-199">Configuración de área de almacenamiento provisional de Hola</span><span class="sxs-lookup"><span data-stu-id="960dc-199">Configuring hello staging Area</span></span>
<span data-ttu-id="960dc-200">agente de copia de seguridad de Azure Hola ejecutando en el servidor DPM Hola necesita almacenamiento temporal para los datos restaurados desde la nube de hello (área de almacenamiento provisional local).</span><span class="sxs-lookup"><span data-stu-id="960dc-200">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="960dc-201">Configurar el área de ensayo de hello mediante hello [conjunto DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet hello y ```-StagingAreaPath``` parámetro.</span><span class="sxs-lookup"><span data-stu-id="960dc-201">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="960dc-202">En el ejemplo de Hola anterior, área de almacenamiento provisional de Hola se establecerá demasiado*C:\StagingArea* en el objeto de PowerShell de hello ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="960dc-202">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="960dc-203">Asegúrese de que ya existe la carpeta especificada de hello, o bien se producirá un error en la confirmación final de Hola de configuración de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-203">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="960dc-204">Configuración de cifrado</span><span class="sxs-lookup"><span data-stu-id="960dc-204">Encryption settings</span></span>
<span data-ttu-id="960dc-205">Hola copia de seguridad de datos enviados tooAzure copia de seguridad es cifrada tooprotect Hola confidencialidad de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-205">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="960dc-206">Hola frase de contraseña es datos de contraseña"hello" toodecrypt hello en tiempo de Hola de restauración.</span><span class="sxs-lookup"><span data-stu-id="960dc-206">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="960dc-207">Importante tookeep esta información es segura para y proteger una vez que se establece.</span><span class="sxs-lookup"><span data-stu-id="960dc-207">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="960dc-208">En el siguiente ejemplo de Hola, primer comando de hello convierte la cadena de hello ```passphrase123456789``` tooa segura cadena y asigna Hola segura toohello variable de cadena denominada ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="960dc-208">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="960dc-209">Hola segundo comando establece cadena segura de hello ```$Passphrase``` como contraseña de Hola para cifrar las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="960dc-209">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="960dc-210">Almacenar información de la frase de contraseña de hello seguro y protegido una vez que se establece.</span><span class="sxs-lookup"><span data-stu-id="960dc-210">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="960dc-211">No será capaz de toorestore datos de Azure sin esta frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="960dc-211">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="960dc-212">En este punto, debería haber realizado todas las Hola requiere cambios toohello ```$setting``` objeto.</span><span class="sxs-lookup"><span data-stu-id="960dc-212">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="960dc-213">Recuerde los cambios de hello toocommit.</span><span class="sxs-lookup"><span data-stu-id="960dc-213">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="960dc-214">Proteger datos tooAzure copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="960dc-214">Protect data tooAzure Backup</span></span>
<span data-ttu-id="960dc-215">En esta sección, agregará un tooDPM del servidor de producción y, a continuación, proteger el almacenamiento DPM de hello datos toolocal y, a continuación, tooAzure copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="960dc-215">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="960dc-216">En los ejemplos de hello demostraremos cómo tooback seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="960dc-216">In hello examples we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="960dc-217">Hello lógica puede fácilmente ser extendido toobackup cualquier origen de datos compatibles con DPM.</span><span class="sxs-lookup"><span data-stu-id="960dc-217">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="960dc-218">Las copias de seguridad de DPM se rigen por un grupo de protección (PG) con cuatro partes:</span><span class="sxs-lookup"><span data-stu-id="960dc-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="960dc-219">**Miembros del grupo** es una lista de todos los objetos que se pueden proteger de hello (también conocido como *orígenes de datos* en DPM) que desea tooprotect Hola mismo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="960dc-219">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="960dc-220">Por ejemplo, puede que desee tooprotect producción máquinas virtuales en un grupo de protección y las bases de datos de SQL Server en otro grupo de protección como pueden tener distintos requisitos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="960dc-220">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="960dc-221">Antes de hacer copias de seguridad ningún origen de datos en un servidor de producción debe toomake seguro Hola agente de DPM está instalado en el servidor de Hola y administrado por DPM.</span><span class="sxs-lookup"><span data-stu-id="960dc-221">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="960dc-222">Siga los pasos de Hola para [instalar Hola agente DPM](https://technet.microsoft.com/library/bb870935.aspx) y vinculándolo toohello adecuados en el servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="960dc-222">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="960dc-223">**Método de protección de datos** especifica ubicaciones Hola destino de copia de seguridad - cinta y disco, en la nube.</span><span class="sxs-lookup"><span data-stu-id="960dc-223">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="960dc-224">En nuestro ejemplo protegemos datos toohello local disco y toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="960dc-224">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="960dc-225">A **programar copia de seguridad** que especifica si las copias de seguridad necesitan toobe realizada y con qué frecuencia hello datos se sincronicen entre Hola servidor DPM y el servidor de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="960dc-225">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="960dc-226">A **programación de retención** que especifica cuánto tiempo los puntos de recuperación de hello tooretain en Azure.</span><span class="sxs-lookup"><span data-stu-id="960dc-226">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="960dc-227">Creación de un grupo de protección</span><span class="sxs-lookup"><span data-stu-id="960dc-227">Creating a protection group</span></span>
<span data-ttu-id="960dc-228">Empiece por crear un nuevo grupo de protección mediante hello [DPMProtectionGroup New](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-228">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="960dc-229">Hola anteriormente cmdlet creará un grupo de protección denominado *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="960dc-229">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="960dc-230">También es posible modificar un grupo de protección posterior toohello de copia de seguridad de tooadd nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="960dc-230">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="960dc-231">Sin embargo, toomake cambios toohello grupo de protección: nuevos o existentes - necesitamos tooget un identificador en un *modificable* objeto mediante hello [DPMModifiableProtectionGroup Get](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-231">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="960dc-232">Agregar miembros de grupo toohello grupo de protección</span><span class="sxs-lookup"><span data-stu-id="960dc-232">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="960dc-233">Cada agente de DPM sabe lista Hola de orígenes de datos en el servidor de Hola que se instala en.</span><span class="sxs-lookup"><span data-stu-id="960dc-233">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="960dc-234">tooadd un grupo de protección de toohello de origen de datos, Hola agente DPM necesidades toofirst envíe una lista del servidor DPM de hello orígenes de datos back-toohello.</span><span class="sxs-lookup"><span data-stu-id="960dc-234">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="960dc-235">Uno o más orígenes de datos no están seleccionado y agregado toohello grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="960dc-235">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="960dc-236">Hola PowerShell pasos necesarios tooget lograr esto son:</span><span class="sxs-lookup"><span data-stu-id="960dc-236">hello PowerShell steps needed tooget achieve this are:</span></span>

1. <span data-ttu-id="960dc-237">Capturar una lista de todos los servidores administrados por DPM a través de hello agente DPM.</span><span class="sxs-lookup"><span data-stu-id="960dc-237">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="960dc-238">Elija un servidor específico.</span><span class="sxs-lookup"><span data-stu-id="960dc-238">Choose a specific server.</span></span>
3. <span data-ttu-id="960dc-239">Capturar una lista de todos los orígenes de datos en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-239">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="960dc-240">Elija uno o más orígenes de datos y agregarlas toohello grupo de protección</span><span class="sxs-lookup"><span data-stu-id="960dc-240">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="960dc-241">Hola lista de servidores en qué Hola agente de DPM está instalado y se está administrando mediante Hola servidor DPM se adquirió con hello [DPMProductionServer Get](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-241">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="960dc-242">En este ejemplo se van a filtrar y configurar solo PS con el nombre *productionserver01* para efectuar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="960dc-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="960dc-243">Ahora buscar de la lista de Hola de orígenes de datos ```$server``` con hello [DPMDatasource Get](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-243">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="960dc-244">En este ejemplo se filtra para el volumen de Hola * D:\* que deseamos tooconfigure para copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="960dc-244">In this example we are filtering for hello volume *D:\* which we want tooconfigure for backup.</span></span> <span data-ttu-id="960dc-245">Este origen de datos, a continuación, se agrega toohello grupo de protección mediante hello [DPMChildDatasource agregar](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-245">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="960dc-246">Recuerde hello toouse *modifable* objeto de grupo de protección ```$MPG``` adiciones de hello toomake.</span><span class="sxs-lookup"><span data-stu-id="960dc-246">Remember toouse hello *modifable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="960dc-247">Repita este paso tantas veces como sea necesario, hasta que haya agregado todos los Hola elegido el grupo de protección de toohello de orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="960dc-247">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="960dc-248">También puede comenzar con un solo origen de datos y flujo de trabajo de hello completa para crear el grupo de protección de Hola y en un momento posterior, agregar más orígenes de datos toohello grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="960dc-248">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="960dc-249">Seleccionar método de protección de datos de hello</span><span class="sxs-lookup"><span data-stu-id="960dc-249">Selecting hello data protection method</span></span>
<span data-ttu-id="960dc-250">Una vez que se agregaron a orígenes de datos de hello toohello grupo de protección, Hola siguiente paso es método de protección de hello toospecify con hello [DPMProtectionType conjunto](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-250">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="960dc-251">En este ejemplo, hello grupo de protección se configurará para el disco local y copia de seguridad en la nube.</span><span class="sxs-lookup"><span data-stu-id="960dc-251">In this example, hello Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="960dc-252">También necesita toospecify Hola datasource que desea toocloud tooprotect con hello [DPMChildDatasource agregar](https://technet.microsoft.com/library/hh881732.aspx) cmdlet con - marcador en línea.</span><span class="sxs-lookup"><span data-stu-id="960dc-252">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="960dc-253">Establecer la duración de retención de Hola</span><span class="sxs-lookup"><span data-stu-id="960dc-253">Setting hello retention range</span></span>
<span data-ttu-id="960dc-254">Establecer retención de Hola para puntos de copia de seguridad de hello mediante hello [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-254">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="960dc-255">Pese a que podría parecer retención de hello tooset impar para definir programación de copia de seguridad de hello, con hello ```Set-DPMPolicyObjective``` cmdlet establece automáticamente una programación de copia de seguridad predeterminada que se pueden modificar.</span><span class="sxs-lookup"><span data-stu-id="960dc-255">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="960dc-256">Siempre es programar copia de seguridad de tooset posible Hola por primera vez y Hola directiva de retención después.</span><span class="sxs-lookup"><span data-stu-id="960dc-256">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="960dc-257">En el siguiente ejemplo de Hola, Hola establece los parámetros de retención de Hola para copias de seguridad de disco.</span><span class="sxs-lookup"><span data-stu-id="960dc-257">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="960dc-258">Esto conservarán las copias de seguridad de 10 días y sincronizar los datos cada 6 horas entre el servidor de producción de hello y el servidor DPM Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-258">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="960dc-259">Hola ```SynchronizationFrequencyMinutes``` no se define con qué frecuencia se crea un punto de copia de seguridad, pero ¿cómo a menudo los datos están el servidor DPM toohello copiada; Esto evita que las copias de seguridad se vuelva demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="960dc-259">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="960dc-260">Para copias de seguridad que se va tooAzure (DPM hace referencia toothese como copias de seguridad en línea) se pueden configurar intervalos de retención de Hola para [utilizando un esquema de su Abuelo-padre-hijo (GFS) de retención a largo plazo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="960dc-260">For backups going tooAzure (DPM refers toothese as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="960dc-261">Es decir, puede definir una directiva de retención combinada que implique directivas de retención diaria, semanal, mensual y anual.</span><span class="sxs-lookup"><span data-stu-id="960dc-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="960dc-262">En este ejemplo, se crea una matriz que representa el esquema de retención complejos de Hola que queremos y, a continuación, configurar la duración de retención de hello mediante hello [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-262">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="960dc-263">Programación de copia de seguridad de hello establecida</span><span class="sxs-lookup"><span data-stu-id="960dc-263">Set hello backup schedule</span></span>
<span data-ttu-id="960dc-264">DPM establece una programación de copia de seguridad predeterminada automáticamente si se especifica el objetivo de protección de hello mediante hello ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-264">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="960dc-265">toochange las programaciones predeterminadas hello, usar hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet seguido por hello [DPMPolicySchedule conjunto](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-265">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="960dc-266">En el ejemplo de Hola anterior, ```$onlineSch``` es una matriz con cuatro elementos que contiene la programación de protección en línea existente de Hola de hello grupo de protección en el esquema GFS hello:</span><span class="sxs-lookup"><span data-stu-id="960dc-266">In hello example above, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="960dc-267">```$onlineSch[0]```contendrá las programaciones diarias Hola</span><span class="sxs-lookup"><span data-stu-id="960dc-267">```$onlineSch[0]``` will contain hello daily schedule</span></span>
2. <span data-ttu-id="960dc-268">```$onlineSch[1]```contendrá las programaciones semanales Hola</span><span class="sxs-lookup"><span data-stu-id="960dc-268">```$onlineSch[1]``` will contain hello weekly schedule</span></span>
3. <span data-ttu-id="960dc-269">```$onlineSch[2]```contendrá programación mensual Hola</span><span class="sxs-lookup"><span data-stu-id="960dc-269">```$onlineSch[2]``` will contain hello monthly schedule</span></span>
4. <span data-ttu-id="960dc-270">```$onlineSch[3]```contendrá programación anual Hola</span><span class="sxs-lookup"><span data-stu-id="960dc-270">```$onlineSch[3]``` will contain hello yearly schedule</span></span>

<span data-ttu-id="960dc-271">Por ello, si necesita programación semanal de toomodify hello, debe toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="960dc-271">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="960dc-272">Copia de seguridad inicial</span><span class="sxs-lookup"><span data-stu-id="960dc-272">Initial backup</span></span>
<span data-ttu-id="960dc-273">Cuando la copia de seguridad de un origen de datos para hello primera vez, DPM necesita toocreate una réplica inicial que se creará una copia de hello toobe de origen de datos protegido en el volumen de réplica DPM.</span><span class="sxs-lookup"><span data-stu-id="960dc-273">When backing up a datasource for hello first time, DPM needs toocreate an initial replica which will create a copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="960dc-274">Esta actividad puede programarse para una hora específica o puede desencadenar manualmente, mediante hello [conjunto DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet con el parámetro hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="960dc-274">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="960dc-275">Cambiar el tamaño de Hola de réplica de DPM y el volumen de punto de recuperación</span><span class="sxs-lookup"><span data-stu-id="960dc-275">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="960dc-276">También puede cambiar el tamaño de Hola de volumen de réplica de DPM, así como instantáneas de volumen con [DPMDatasourceDiskAllocation conjunto](https://technet.microsoft.com/library/hh881618.aspx) cmdlet como en hello debajo de ejemplo: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manual - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="960dc-276">You can also change hello size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="960dc-277">Confirmar Hola cambia toohello grupo de protección</span><span class="sxs-lookup"><span data-stu-id="960dc-277">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="960dc-278">Por último, cambios de hello necesitan toobe confirmado antes de que DPM puede realizar la copia de seguridad de Hola por la configuración del nuevo grupo de protección de Hola.</span><span class="sxs-lookup"><span data-stu-id="960dc-278">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="960dc-279">Esto se realiza mediante hello [DPMProtectionGroup conjunto](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-279">This is done using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="960dc-280">Ver los puntos de copia de seguridad Hola</span><span class="sxs-lookup"><span data-stu-id="960dc-280">View hello backup points</span></span>
<span data-ttu-id="960dc-281">Puede usar hello [DPMRecoveryPoint Get](https://technet.microsoft.com/library/hh881746) cmdlet tooget una lista de todos los puntos de recuperación para un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="960dc-281">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="960dc-282">En este ejemplo, se realiza lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="960dc-282">In this example, we will:</span></span>

* <span data-ttu-id="960dc-283">capturar todos los documento hello en el servidor DPM Hola que se almacenará en una matriz```$PG```</span><span class="sxs-lookup"><span data-stu-id="960dc-283">fetch all hello PGs on hello DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="960dc-284">obtener toohello correspondiente de hello orígenes de datos```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="960dc-284">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="960dc-285">obtener todos los puntos de recuperación de Hola para un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="960dc-285">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="960dc-286">Restauración de datos protegidos en Azure</span><span class="sxs-lookup"><span data-stu-id="960dc-286">Restore data protected on Azure</span></span>
<span data-ttu-id="960dc-287">Restauración de datos es una combinación de un objeto ```RecoverableItem``` y un objeto ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="960dc-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="960dc-288">En la sección anterior de hello, que obtuvimos una lista de puntos de copia de seguridad de Hola para un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="960dc-288">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="960dc-289">En el ejemplo de Hola siguiente, se muestran la máquina virtual de Hyper-V toorestore de copia de seguridad de Azure puntos de copia de seguridad de combinación con hello de destino para la recuperación.</span><span class="sxs-lookup"><span data-stu-id="960dc-289">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="960dc-290">En ella se incluye:</span><span class="sxs-lookup"><span data-stu-id="960dc-290">This includes:</span></span>

* <span data-ttu-id="960dc-291">Crear una opción de recuperación utilizando hello [DPMRecoveryOption New](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-291">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="960dc-292">Obteniendo Hola matriz de copia de seguridad puntos con hello ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="960dc-292">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="960dc-293">Elegir un toorestore de punto de copia de seguridad de.</span><span class="sxs-lookup"><span data-stu-id="960dc-293">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="960dc-294">comandos de Hola se pueden extender con facilidad para cualquier tipo de origen de datos.</span><span class="sxs-lookup"><span data-stu-id="960dc-294">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="960dc-295">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="960dc-295">Next steps</span></span>
* <span data-ttu-id="960dc-296">Para obtener más información acerca de la copia de seguridad de Azure de DPM vea [Introducción tooDPM copia de seguridad](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="960dc-296">For more information about Azure Backup for DPM see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
