---
title: 'Azure Backup: Uso de PowerShell para hacer copias de seguridad de cargas de trabajo DPM | Microsoft Docs'
description: "Obtenga información acerca de cómo implementar y administrar Copia de seguridad de Azure para Data Protection Manager (DPM) mediante PowerShell"
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
ms.openlocfilehash: 943a12dcba49a114d206b9dab968da332ea99926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="5441d-103">Implementación y administración de copias de seguridad en Azure para servidores de Data Protection Manager (DPM) con PowerShell</span><span class="sxs-lookup"><span data-stu-id="5441d-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5441d-104">ARM</span><span class="sxs-lookup"><span data-stu-id="5441d-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="5441d-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="5441d-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="5441d-106">En este artículo se explica cómo usar PowerShell para la copia de seguridad y la recuperación de datos de DPM desde un almacén de Backup.</span><span class="sxs-lookup"><span data-stu-id="5441d-106">This article explains how to use PowerShell to back up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="5441d-107">Microsoft recomienda el uso de almacenes de Recovery Services para todas las implementaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="5441d-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="5441d-108">Si es un nuevo usuario de Azure Backup, les el artículo [Implementación y administración de copias de seguridad en Azure para servidores de Data Protection manager (DPM) con PowerShell](backup-dpm-automation.md) para almacenar los datos en un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="5441d-108">If you are a new Azure Backup user, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5441d-109">Ahora puede actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="5441d-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="5441d-110">Para más información, consulte el artículo [Actualización de un almacén de Backup a un almacén de Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="5441d-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="5441d-111">Microsoft anima a actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="5441d-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="5441d-112">A partir del 15 de octubre de 2017, no podrá usar PowerShell para crear almacenes de Backup.</span><span class="sxs-lookup"><span data-stu-id="5441d-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="5441d-113">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="5441d-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="5441d-114">Todos los almacenes de Backup restantes se actualizarán automáticamente a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="5441d-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="5441d-115">No podrá acceder a los datos de copia de seguridad en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="5441d-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="5441d-116">En su lugar, utilice Azure Portal para tener acceso a los datos de copia de seguridad en los almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="5441d-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="5441d-117">Configuración del entorno de PowerShell</span><span class="sxs-lookup"><span data-stu-id="5441d-117">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="5441d-118">Para poder usar PowerShell para administrar las copias de seguridad de Data Protection Manager en Azure, deberá tener el entorno adecuado en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5441d-118">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you will need to have the right environment in PowerShell.</span></span> <span data-ttu-id="5441d-119">Al principio de la sesión de PowerShell, asegúrese de ejecutar el siguiente comando para importar los módulos correctos y poder hacer referencia correctamente a los cmdlet de DPM:</span><span class="sxs-lookup"><span data-stu-id="5441d-119">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="5441d-120">Instalación y registro</span><span class="sxs-lookup"><span data-stu-id="5441d-120">Setup and Registration</span></span>
<span data-ttu-id="5441d-121">Para empezar:</span><span class="sxs-lookup"><span data-stu-id="5441d-121">To begin:</span></span>

1. <span data-ttu-id="5441d-122">[Descargue la versión de PowerShell más reciente](https://github.com/Azure/azure-powershell/releases) (la versión mínima necesaria es: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="5441d-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="5441d-123">Para empezar, habilite los commandlets de Copia de seguridad de Azure, para lo que debe cambiar al modo *AzureResourceManager* usando el commandlet **Switch-AzureMode** :</span><span class="sxs-lookup"><span data-stu-id="5441d-123">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="5441d-124">Las siguientes tareas de instalación y registro se pueden automatizar con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5441d-124">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="5441d-125">Creación de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="5441d-125">Create a backup vault</span></span>
* <span data-ttu-id="5441d-126">Instalación del agente de Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="5441d-126">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="5441d-127">Registro con el servicio de Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="5441d-127">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="5441d-128">Configuración de redes</span><span class="sxs-lookup"><span data-stu-id="5441d-128">Networking settings</span></span>
* <span data-ttu-id="5441d-129">Configuración de cifrado</span><span class="sxs-lookup"><span data-stu-id="5441d-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="5441d-130">Creación de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="5441d-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="5441d-131">La primera vez que los clientes usen Azure Backup deben registrar el proveedor de Azure Backup que se va a usar con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="5441d-131">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="5441d-132">Para ello, ejecute el siguiente comando: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="5441d-132">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="5441d-133">Puede crear un nuevo almacén de copia de seguridad con el commandlet **New-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="5441d-133">You can create a new backup vault using the **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="5441d-134">El almacén de copia de seguridad es un recurso ARM, por lo que necesita colocarlo dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5441d-134">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="5441d-135">En una consola de Azure PowerShell, ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5441d-135">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="5441d-136">Puede obtener una lista de todos los almacenes de copia de seguridad de una suscripción dada usando el commandlet **Get-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="5441d-136">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="5441d-137">Instalación del agente de copia de seguridad de Azure en un servidor DPM</span><span class="sxs-lookup"><span data-stu-id="5441d-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="5441d-138">Antes de instalar el agente de copia de seguridad de Azure, necesitará tener el instalador descargado y disponible en el servidor de Windows.</span><span class="sxs-lookup"><span data-stu-id="5441d-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="5441d-139">Puede obtener la versión más reciente del instalador en el [Centro de descarga de Microsoft](http://aka.ms/azurebackup_agent) o en la página Panel del almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="5441d-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="5441d-140">Guarde el instalador en una ubicación que tenga fácil acceso, como *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="5441d-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="5441d-141">Para instalar el agente, ejecute el comando siguiente en una consola de PowerShell con privilegios elevados **en el servidor DPM**:</span><span class="sxs-lookup"><span data-stu-id="5441d-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="5441d-142">Esto instala el agente con todas las opciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="5441d-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="5441d-143">La instalación está unos minutos en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="5441d-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="5441d-144">Si no se especifica la opción */nu* , se abrirá la ventana de **Windows Update** al final de la instalación para comprobar si hay actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="5441d-144">If you do not specify the */nu* option the **Windows Update** window will open at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="5441d-145">El agente se mostrará en la lista de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="5441d-145">The agent will show in the list of installed programs.</span></span> <span data-ttu-id="5441d-146">Para ver la lista de programas instalados, vaya a **Panel de Control** > **Programas** > **Programas y características**.</span><span class="sxs-lookup"><span data-stu-id="5441d-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="5441d-148">Opciones de instalación</span><span class="sxs-lookup"><span data-stu-id="5441d-148">Installation options</span></span>
<span data-ttu-id="5441d-149">Para ver todas las opciones disponibles a través de la línea de comandos, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5441d-149">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="5441d-150">Las opciones disponibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="5441d-150">The available options include:</span></span>

| <span data-ttu-id="5441d-151">Opción</span><span class="sxs-lookup"><span data-stu-id="5441d-151">Option</span></span> | <span data-ttu-id="5441d-152">Detalles</span><span class="sxs-lookup"><span data-stu-id="5441d-152">Details</span></span> | <span data-ttu-id="5441d-153">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5441d-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5441d-154">/q</span><span class="sxs-lookup"><span data-stu-id="5441d-154">/q</span></span> |<span data-ttu-id="5441d-155">Instalación silenciosa</span><span class="sxs-lookup"><span data-stu-id="5441d-155">Quiet installation</span></span> |- |
| <span data-ttu-id="5441d-156">/p:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="5441d-156">/p:"location"</span></span> |<span data-ttu-id="5441d-157">Ruta de acceso a la carpeta de instalación para el agente de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="5441d-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="5441d-158">C:\Archivos de programa\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="5441d-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="5441d-159">/s:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="5441d-159">/s:"location"</span></span> |<span data-ttu-id="5441d-160">Ruta de acceso a la carpeta de caché para el agente de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="5441d-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="5441d-161">C:\Archivos de programa\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="5441d-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="5441d-162">/m</span><span class="sxs-lookup"><span data-stu-id="5441d-162">/m</span></span> |<span data-ttu-id="5441d-163">Participación en Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="5441d-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="5441d-164">/nu</span><span class="sxs-lookup"><span data-stu-id="5441d-164">/nu</span></span> |<span data-ttu-id="5441d-165">No busca actualizaciones una vez completada la instalación</span><span class="sxs-lookup"><span data-stu-id="5441d-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="5441d-166">/d</span><span class="sxs-lookup"><span data-stu-id="5441d-166">/d</span></span> |<span data-ttu-id="5441d-167">Desinstala el agente de Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="5441d-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="5441d-168">/ph</span><span class="sxs-lookup"><span data-stu-id="5441d-168">/ph</span></span> |<span data-ttu-id="5441d-169">Dirección host del proxy</span><span class="sxs-lookup"><span data-stu-id="5441d-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="5441d-170">/po</span><span class="sxs-lookup"><span data-stu-id="5441d-170">/po</span></span> |<span data-ttu-id="5441d-171">Número de puerto del host de proxy</span><span class="sxs-lookup"><span data-stu-id="5441d-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="5441d-172">/pu</span><span class="sxs-lookup"><span data-stu-id="5441d-172">/pu</span></span> |<span data-ttu-id="5441d-173">Nombre de usuario del host de proxy</span><span class="sxs-lookup"><span data-stu-id="5441d-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="5441d-174">/pw</span><span class="sxs-lookup"><span data-stu-id="5441d-174">/pw</span></span> |<span data-ttu-id="5441d-175">Contraseña de proxy</span><span class="sxs-lookup"><span data-stu-id="5441d-175">Proxy Password</span></span> |- |

### <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="5441d-176">Registro con el servicio de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="5441d-176">Registering with the Azure Backup service</span></span>
<span data-ttu-id="5441d-177">Para poder registrarse con el servicio Azure Backup, debe asegurarse de que se cumplen los [requisitos previos](backup-azure-dpm-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="5441d-177">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="5441d-178">Debe:</span><span class="sxs-lookup"><span data-stu-id="5441d-178">You must:</span></span>

* <span data-ttu-id="5441d-179">Disponer de una suscripción válida a Azure</span><span class="sxs-lookup"><span data-stu-id="5441d-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="5441d-180">Disponer de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="5441d-180">Have a backup vault</span></span>

<span data-ttu-id="5441d-181">Para descargar las credenciales de almacén, ejecute el cmdlet **Get-AzureBackupVaultCredentials** en una consola de Azure PowerShell y almacénelas en una ubicación adecuada como *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="5441d-181">To download the vault credentials, run the **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="5441d-182">El registro de la máquina con el almacén de claves se realiza mediante el cmdlet [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) :</span><span class="sxs-lookup"><span data-stu-id="5441d-182">Registering the machine with the vault is done using the [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="5441d-183">Esto registrará el servidor DPM denominado "TestingServer" con Microsoft Azure Vault usando las credenciales del almacén especificadas.</span><span class="sxs-lookup"><span data-stu-id="5441d-183">This will register the DPM Server named “TestingServer” with Microsoft Azure Vault using the specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5441d-184">No use rutas de acceso relativas para especificar el archivo de credenciales del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="5441d-184">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="5441d-185">Debe proporcionar una ruta de acceso absoluta como entrada para el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5441d-185">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="5441d-186">Opciones de configuración inicial</span><span class="sxs-lookup"><span data-stu-id="5441d-186">Initial configuration settings</span></span>
<span data-ttu-id="5441d-187">Una vez que el servidor DPM se registra con el almacén de Copia de seguridad de Azure, se iniciará con la configuración de suscripción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5441d-187">Once the DPM Server is registered with the Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="5441d-188">Estas opciones de suscripción incluyen funciones de red, cifrado y el área de ensayo.</span><span class="sxs-lookup"><span data-stu-id="5441d-188">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="5441d-189">Para empezar a cambiar la configuración de la suscripción, primero se debe obtener un identificador en la configuración (valor predeterminado) existente utilizando el cmdlet [DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) :</span><span class="sxs-lookup"><span data-stu-id="5441d-189">To begin changing the subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="5441d-190">Todas las modificaciones se realizan en este objeto de PowerShell local ```$setting``` y, a continuación, el objeto completo se confirma en DPM y Azure Backup para guardarlos con el cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="5441d-190">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="5441d-191">Deberá usar la marca ```–Commit``` para asegurarse de que los cambios se conservan.</span><span class="sxs-lookup"><span data-stu-id="5441d-191">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="5441d-192">Copia de seguridad de Azure no aplicará ni usará la configuración a menos que se confirme.</span><span class="sxs-lookup"><span data-stu-id="5441d-192">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="5441d-193">Redes</span><span class="sxs-lookup"><span data-stu-id="5441d-193">Networking</span></span>
<span data-ttu-id="5441d-194">Si la conectividad del equipo DPM para el servicio de Copia de seguridad de Azure en Internet es a través de un servidor proxy, se debe proporcionar la configuración del servidor proxy para que las copias de seguridad se efectúen correctamente.</span><span class="sxs-lookup"><span data-stu-id="5441d-194">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for backups to succeed.</span></span> <span data-ttu-id="5441d-195">Esto se realiza mediante los parámetros ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` y ```ProxyPassword``` con el cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="5441d-195">This is done by using the ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="5441d-196">En este ejemplo, no hay ningún servidor proxy y por tanto se borra explícitamente cualquier información relacionada con el proxy.</span><span class="sxs-lookup"><span data-stu-id="5441d-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="5441d-197">También puede controlar el uso de ancho de banda con las opciones de ```-WorkHourBandwidth``` y ```-NonWorkHourBandwidth``` para un conjunto determinado de días de la semana.</span><span class="sxs-lookup"><span data-stu-id="5441d-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="5441d-198">En este ejemplo no estamos definiendo ninguna limitación.</span><span class="sxs-lookup"><span data-stu-id="5441d-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-the-staging-area"></a><span data-ttu-id="5441d-199">Configuración del área de ensayo</span><span class="sxs-lookup"><span data-stu-id="5441d-199">Configuring the staging Area</span></span>
<span data-ttu-id="5441d-200">El agente de Copia de seguridad de Azure que se ejecuta en el servidor DPM necesita almacenamiento temporal para los datos restaurados desde la nube (área de almacenamiento provisional local).</span><span class="sxs-lookup"><span data-stu-id="5441d-200">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="5441d-201">Configure el área de ensayo mediante el cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) y el parámetro ```-StagingAreaPath```.</span><span class="sxs-lookup"><span data-stu-id="5441d-201">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="5441d-202">En el ejemplo anterior, el área de ensayo se establecerá en *C:\StagingArea* en el objeto de PowerShell ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="5441d-202">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="5441d-203">Asegúrese de que la carpeta especificada ya existe, o bien se producirá un error en la confirmación final de la configuración de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="5441d-203">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="5441d-204">Configuración de cifrado</span><span class="sxs-lookup"><span data-stu-id="5441d-204">Encryption settings</span></span>
<span data-ttu-id="5441d-205">Los datos de copia de seguridad enviados a Azure Backup se cifran para proteger la confidencialidad de los datos.</span><span class="sxs-lookup"><span data-stu-id="5441d-205">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="5441d-206">La frase de contraseña de cifrado es la "contraseña" que permite descifrar los datos en el momento de la restauración.</span><span class="sxs-lookup"><span data-stu-id="5441d-206">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="5441d-207">Es importante que mantenga esta información segura cuando la establezca.</span><span class="sxs-lookup"><span data-stu-id="5441d-207">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="5441d-208">En el ejemplo siguiente, el primer comando convierte la cadena ```passphrase123456789``` en una cadena segura y la asigna a la variable denominada ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="5441d-208">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="5441d-209">El segundo comando establece la cadena segura en ```$Passphrase``` como la contraseña para cifrar las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="5441d-209">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="5441d-210">Mantenga la información de la frase de contraseña segura una vez establecida.</span><span class="sxs-lookup"><span data-stu-id="5441d-210">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="5441d-211">No podrá restaurar los datos de Azure sin esta frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="5441d-211">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="5441d-212">En este punto, debería haber realizado todos los cambios necesarios al objeto ```$setting``` .</span><span class="sxs-lookup"><span data-stu-id="5441d-212">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="5441d-213">Recuerde que debe confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="5441d-213">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="5441d-214">Proteger los datos en Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="5441d-214">Protect data to Azure Backup</span></span>
<span data-ttu-id="5441d-215">En esta sección, agregará un servidor de producción a DPM y, a continuación, protegerá los datos en el almacenamiento de DPM local y, a continuación, en la copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="5441d-215">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="5441d-216">En los ejemplos, se mostrará cómo realizar copias de seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="5441d-216">In the examples we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="5441d-217">La lógica se puede ampliar fácilmente para efectuar una copia de seguridad de cualquier origen de datos compatible con DPM.</span><span class="sxs-lookup"><span data-stu-id="5441d-217">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="5441d-218">Las copias de seguridad de DPM se rigen por un grupo de protección (PG) con cuatro partes:</span><span class="sxs-lookup"><span data-stu-id="5441d-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="5441d-219">**Miembros del grupo** es una lista de todos los objetos que se pueden proteger (también conocidos como *Orígenes de datos* en DPM) que desea proteger en el mismo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="5441d-219">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="5441d-220">Por ejemplo, puede proteger las máquinas virtuales de producción en un grupo de protección y las bases de datos de SQL Server en otro grupo de protección, ya que pueden tener distintos requisitos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="5441d-220">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="5441d-221">Antes de que puedan realizar una copia de seguridad de cualquier origen de datos en un servidor de producción, deberá asegurarse de que el agente de DPM esté instalado en el servidor y administrado por DPM.</span><span class="sxs-lookup"><span data-stu-id="5441d-221">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="5441d-222">Siga los pasos para [instalar el agente de DPM](https://technet.microsoft.com/library/bb870935.aspx) y vincularlo al servidor DPM apropiado.</span><span class="sxs-lookup"><span data-stu-id="5441d-222">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="5441d-223">**Método de protección de datos** especifica las ubicaciones de copia de seguridad de destino: cinta, disco y nube.</span><span class="sxs-lookup"><span data-stu-id="5441d-223">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="5441d-224">En nuestro ejemplo se protegerán los datos en el disco local y en la nube.</span><span class="sxs-lookup"><span data-stu-id="5441d-224">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="5441d-225">Una **programación de copia de seguridad** que especifica cuándo deben realizarse copias de seguridad y la frecuencia con la que se deben sincronizar los datos entre el servidor DPM y el servidor de producción.</span><span class="sxs-lookup"><span data-stu-id="5441d-225">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="5441d-226">Una **programación de retención** que especifica cuánto tiempo se conservarán los puntos de recuperación en Azure.</span><span class="sxs-lookup"><span data-stu-id="5441d-226">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="5441d-227">Creación de un grupo de protección</span><span class="sxs-lookup"><span data-stu-id="5441d-227">Creating a protection group</span></span>
<span data-ttu-id="5441d-228">Empiece por crear un nuevo grupo de protección mediante el cmdlet [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) .</span><span class="sxs-lookup"><span data-stu-id="5441d-228">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="5441d-229">El cmdlet anterior creará un grupo de protección denominado *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="5441d-229">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="5441d-230">Un grupo de protección existente también se puede modificar más adelante para agregar la copia de seguridad a la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="5441d-230">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="5441d-231">Sin embargo, para realizar cambios en el grupo de protección (nuevo o existente), necesitamos obtener un identificador en un objeto *modificable* utilizando el cmdlet [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) .</span><span class="sxs-lookup"><span data-stu-id="5441d-231">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="5441d-232">Agregar miembros de grupo al grupo de protección</span><span class="sxs-lookup"><span data-stu-id="5441d-232">Adding group members to the Protection Group</span></span>
<span data-ttu-id="5441d-233">Cada agente de DPM conoce la lista de orígenes de datos del servidor en el que está instalado.</span><span class="sxs-lookup"><span data-stu-id="5441d-233">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="5441d-234">Para agregar un origen de datos al grupo de protección, el agente de DPM debe enviar primero una lista de los orígenes de datos al servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="5441d-234">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="5441d-235">A continuación, se agregan y seleccionan uno o más orígenes de datos al grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="5441d-235">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="5441d-236">Los pasos de PowerShell necesarios para lograrlo son:</span><span class="sxs-lookup"><span data-stu-id="5441d-236">The PowerShell steps needed to get achieve this are:</span></span>

1. <span data-ttu-id="5441d-237">Recuperar una lista de todos los servidores administrados por DPM a través del agente de DPM.</span><span class="sxs-lookup"><span data-stu-id="5441d-237">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="5441d-238">Elija un servidor específico.</span><span class="sxs-lookup"><span data-stu-id="5441d-238">Choose a specific server.</span></span>
3. <span data-ttu-id="5441d-239">Recupere una lista de todos los orígenes de datos del servidor.</span><span class="sxs-lookup"><span data-stu-id="5441d-239">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="5441d-240">Elija uno o más orígenes de datos y agréguelos al grupo de protección</span><span class="sxs-lookup"><span data-stu-id="5441d-240">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="5441d-241">La lista de servidores en los que está instalado el agente de DPM y está siendo administrando por el servidor DPM se adquiere con el cmdlet [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) .</span><span class="sxs-lookup"><span data-stu-id="5441d-241">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="5441d-242">En este ejemplo se van a filtrar y configurar solo PS con el nombre *productionserver01* para efectuar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="5441d-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="5441d-243">Ahora, capture la lista de orígenes de datos en ```$server``` con el cmdlet [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605).</span><span class="sxs-lookup"><span data-stu-id="5441d-243">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="5441d-244">En este ejemplo se filtra para el volumen *D:\* que queremos configurar para la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="5441d-244">In this example we are filtering for the volume *D:\* which we want to configure for backup.</span></span> <span data-ttu-id="5441d-245">A continuación, este origen de datos se agrega al grupo de protección mediante el cmdlet [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732).</span><span class="sxs-lookup"><span data-stu-id="5441d-245">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="5441d-246">Recuerde que debe usar el objeto de grupo de protecciones *modifable* ```$MPG``` para realizar las incorporaciones.</span><span class="sxs-lookup"><span data-stu-id="5441d-246">Remember to use the *modifable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="5441d-247">Repita este paso tantas veces como sea necesario hasta que haya agregado todos los orígenes de datos elegidos al grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="5441d-247">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="5441d-248">También puede comenzar con un solo origen de datos y completar el flujo de trabajo para crear el grupo de protección y, posteriormente, agregar más orígenes de datos al grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="5441d-248">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="5441d-249">Selección del método de protección de datos</span><span class="sxs-lookup"><span data-stu-id="5441d-249">Selecting the data protection method</span></span>
<span data-ttu-id="5441d-250">Una vez que los orígenes de datos se han agregado al grupo de protección, el siguiente paso es especificar el método de protección mediante el cmdlet [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) .</span><span class="sxs-lookup"><span data-stu-id="5441d-250">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="5441d-251">En este ejemplo, el grupo de protección será el programa de instalación de disco local y la copia de seguridad en la nube.</span><span class="sxs-lookup"><span data-stu-id="5441d-251">In this example, the Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="5441d-252">También tendrá que especificar el origen de datos que quiere proteger en la nube mediante el cmdlet [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) con la marca -Online.</span><span class="sxs-lookup"><span data-stu-id="5441d-252">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="5441d-253">Establecimiento del período de retención</span><span class="sxs-lookup"><span data-stu-id="5441d-253">Setting the retention range</span></span>
<span data-ttu-id="5441d-254">Establecer el período de retención de los puntos de copia de seguridad mediante el cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="5441d-254">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="5441d-255">Aunque puede parecer extraño establecer el período de retención antes de definir la programación de copia de seguridad, usando el cmdlet ```Set-DPMPolicyObjective``` se establece automáticamente una programación de copia de seguridad predeterminada que, a continuación, se puede modificar.</span><span class="sxs-lookup"><span data-stu-id="5441d-255">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="5441d-256">Siempre es posible establecer el programa de copia de seguridad en primer lugar y, a continuación, la directiva de retención.</span><span class="sxs-lookup"><span data-stu-id="5441d-256">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="5441d-257">En el ejemplo siguiente, el cmdlet establece los parámetros de retención de copias de seguridad de disco.</span><span class="sxs-lookup"><span data-stu-id="5441d-257">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="5441d-258">Esto conservará las copias de seguridad durante 10 días y sincronizará los datos cada 6 horas entre el servidor de producción y el servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="5441d-258">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="5441d-259">El ```SynchronizationFrequencyMinutes``` no define la frecuencia con la que se crea un punto de copia de seguridad, sino la frecuencia con la que se copian los datos en el servidor DPM; Esto evita que las copias de seguridad se vuelvan demasiado grandes.</span><span class="sxs-lookup"><span data-stu-id="5441d-259">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="5441d-260">Para las copias de seguridad que tienen como destino Azure (DPM hace referencia a estas como copias de seguridad en línea) se pueden configurar intervalos de retención para [retenciones a largo plazo usando un esquema abuelo-padre-hijo (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="5441d-260">For backups going to Azure (DPM refers to these as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="5441d-261">Es decir, puede definir una directiva de retención combinada que implique directivas de retención diaria, semanal, mensual y anual.</span><span class="sxs-lookup"><span data-stu-id="5441d-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="5441d-262">En este ejemplo, se crea una matriz que representa el esquema de retención complejo que se desea y, a continuación, se configura el intervalo de retención usando el cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="5441d-262">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="5441d-263">Establecer la programación de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="5441d-263">Set the backup schedule</span></span>
<span data-ttu-id="5441d-264">DPM establece automáticamente una programación de copia de seguridad predeterminada si especifica el objetivo de protección mediante el cmdlet ```Set-DPMPolicyObjective``` .</span><span class="sxs-lookup"><span data-stu-id="5441d-264">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="5441d-265">Para cambiar las programaciones predeterminadas, use el cmdlet [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) seguido por el cmdlet [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723).</span><span class="sxs-lookup"><span data-stu-id="5441d-265">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="5441d-266">En el ejemplo anterior, ```$onlineSch``` es una matriz con cuatro elementos que contiene la programación de protección en línea existente para el grupo de protección en el esquema de GFS:</span><span class="sxs-lookup"><span data-stu-id="5441d-266">In the example above, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="5441d-267">```$onlineSch[0]``` contendrá la programación diaria</span><span class="sxs-lookup"><span data-stu-id="5441d-267">```$onlineSch[0]``` will contain the daily schedule</span></span>
2. <span data-ttu-id="5441d-268">```$onlineSch[1]``` contendrá la programación semanal</span><span class="sxs-lookup"><span data-stu-id="5441d-268">```$onlineSch[1]``` will contain the weekly schedule</span></span>
3. <span data-ttu-id="5441d-269">```$onlineSch[2]``` contendrá la programación mensual</span><span class="sxs-lookup"><span data-stu-id="5441d-269">```$onlineSch[2]``` will contain the monthly schedule</span></span>
4. <span data-ttu-id="5441d-270">```$onlineSch[3]``` contendrá la programación anual</span><span class="sxs-lookup"><span data-stu-id="5441d-270">```$onlineSch[3]``` will contain the yearly schedule</span></span>

<span data-ttu-id="5441d-271">Por ello, si necesita modificar la programación semanal, deberá hacer referencia a ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="5441d-271">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="5441d-272">Copia de seguridad inicial</span><span class="sxs-lookup"><span data-stu-id="5441d-272">Initial backup</span></span>
<span data-ttu-id="5441d-273">Cuando efectúa una copia de seguridad de un origen de datos por primera vez, DPM debe crear una réplica inicial que creará una copia del origen de datos que se debe proteger en el volumen de réplica DPM.</span><span class="sxs-lookup"><span data-stu-id="5441d-273">When backing up a datasource for the first time, DPM needs to create an initial replica which will create a copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="5441d-274">Esta actividad se puede programar para una hora específica o puede desencadenarse manualmente mediante el cmdlet [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) con el parámetro ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="5441d-274">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="5441d-275">Cambiar el tamaño de la réplica de DPM y el volumen de puntos de recuperación</span><span class="sxs-lookup"><span data-stu-id="5441d-275">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="5441d-276">También puede cambiar el tamaño del volumen de réplica de DPM, así como el volumen de instantánea mediante el cmdlet [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) , como en el ejemplo siguiente: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="5441d-276">You can also change the size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="5441d-277">Confirmar los cambios en el grupo de protección</span><span class="sxs-lookup"><span data-stu-id="5441d-277">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="5441d-278">Por último, los cambios deben confirmarse antes de que DPM pueda realizar la copia de seguridad según la configuración del nuevo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="5441d-278">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="5441d-279">Esto se realiza mediante el cmdlet [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) .</span><span class="sxs-lookup"><span data-stu-id="5441d-279">This is done using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="5441d-280">Ver los puntos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="5441d-280">View the backup points</span></span>
<span data-ttu-id="5441d-281">Puede usar el cmdlet [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) para obtener una lista de todos los puntos de recuperación para un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="5441d-281">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="5441d-282">En este ejemplo, se realiza lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5441d-282">In this example, we will:</span></span>

* <span data-ttu-id="5441d-283">se capturan todos los grupos de protección del servidor DPM, que se almacenarán en una matriz ```$PG```</span><span class="sxs-lookup"><span data-stu-id="5441d-283">fetch all the PGs on the DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="5441d-284">se obtienen los orígenes de datos correspondientes a ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="5441d-284">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="5441d-285">se obtienen todos los puntos de recuperación de un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="5441d-285">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="5441d-286">Restauración de datos protegidos en Azure</span><span class="sxs-lookup"><span data-stu-id="5441d-286">Restore data protected on Azure</span></span>
<span data-ttu-id="5441d-287">Restauración de datos es una combinación de un objeto ```RecoverableItem``` y un objeto ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="5441d-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="5441d-288">En la sección anterior se facilita una lista de los puntos de la copia de seguridad de un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="5441d-288">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="5441d-289">En el ejemplo siguiente, demostraremos cómo restaurar una máquina virtual de Hyper-V de Copia de seguridad de Azure mediante la combinación de puntos de copia de seguridad con el destino para la recuperación.</span><span class="sxs-lookup"><span data-stu-id="5441d-289">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="5441d-290">En ella se incluye:</span><span class="sxs-lookup"><span data-stu-id="5441d-290">This includes:</span></span>

* <span data-ttu-id="5441d-291">Creación de una opción de recuperación mediante el cmdlet [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592).</span><span class="sxs-lookup"><span data-stu-id="5441d-291">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="5441d-292">Recuperación de la matriz de puntos de copia de seguridad mediante el cmdlet ```Get-DPMRecoveryPoint``` .</span><span class="sxs-lookup"><span data-stu-id="5441d-292">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="5441d-293">Elegir un punto de copia de seguridad desde el que efectuar la restauración.</span><span class="sxs-lookup"><span data-stu-id="5441d-293">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="5441d-294">Los comandos se pueden ampliar fácilmente para cualquier tipo de origen de datos.</span><span class="sxs-lookup"><span data-stu-id="5441d-294">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5441d-295">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5441d-295">Next steps</span></span>
* <span data-ttu-id="5441d-296">Para obtener más información sobre Copia de seguridad de Azure para DPM, consulte [Introducción a Copia de seguridad de DPM](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="5441d-296">For more information about Azure Backup for DPM see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
