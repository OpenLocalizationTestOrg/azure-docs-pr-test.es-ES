---
title: Azure Backup - Uso de PowerShell para hacer copias de seguridad de cargas de trabajo DPM | Microsoft Docs
description: "Obtenga información acerca de cómo implementar y administrar Copia de seguridad de Azure para Data Protection Manager (DPM) mediante PowerShell"
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
ms.openlocfilehash: 2e3b4a094511a59cfa02917efc2e3e053840af0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="415c9-103">Implementación y administración de copias de seguridad en Azure para servidores de Data Protection Manager (DPM) con PowerShell</span><span class="sxs-lookup"><span data-stu-id="415c9-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="415c9-104">ARM</span><span class="sxs-lookup"><span data-stu-id="415c9-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="415c9-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="415c9-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="415c9-106">En este artículo se muestra cómo usar PowerShell para configurar la copia de seguridad de Azure en un servidor DPM y para administrar copias de seguridad y recuperaciones.</span><span class="sxs-lookup"><span data-stu-id="415c9-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span></span>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="415c9-107">Configuración del entorno de PowerShell</span><span class="sxs-lookup"><span data-stu-id="415c9-107">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="415c9-108">Para poder usar PowerShell para administrar las copias de seguridad de Data Protection Manager en Azure, debe tener el entorno adecuado en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="415c9-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span></span> <span data-ttu-id="415c9-109">Al principio de la sesión de PowerShell, asegúrese de ejecutar el siguiente comando para importar los módulos correctos y poder hacer referencia correctamente a los cmdlet de DPM:</span><span class="sxs-lookup"><span data-stu-id="415c9-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="415c9-110">Instalación y registro</span><span class="sxs-lookup"><span data-stu-id="415c9-110">Setup and Registration</span></span>
<span data-ttu-id="415c9-111">Para empezar:</span><span class="sxs-lookup"><span data-stu-id="415c9-111">To begin:</span></span>

1. <span data-ttu-id="415c9-112">[Descargue la última versión de PowerShell](https://github.com/Azure/azure-powershell/releases) (la versión mínima necesaria es: 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="415c9-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="415c9-113">Para empezar, habilite los commandlets de Copia de seguridad de Azure, para lo que debe cambiar al modo *AzureResourceManager* usando el commandlet **Switch-AzureMode** :</span><span class="sxs-lookup"><span data-stu-id="415c9-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="415c9-114">Las siguientes tareas de instalación y registro se pueden automatizar con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="415c9-114">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="415c9-115">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="415c9-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="415c9-116">Instalación del agente de Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="415c9-116">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="415c9-117">Registro con el servicio de Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="415c9-117">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="415c9-118">Configuración de redes</span><span class="sxs-lookup"><span data-stu-id="415c9-118">Networking settings</span></span>
* <span data-ttu-id="415c9-119">Configuración de cifrado</span><span class="sxs-lookup"><span data-stu-id="415c9-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="415c9-120">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="415c9-120">Create a recovery services vault</span></span>
<span data-ttu-id="415c9-121">Los siguientes pasos le guiarán por el proceso de creación de un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="415c9-121">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="415c9-122">Un almacén de Servicios de recuperación no es lo mismo que un almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="415c9-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="415c9-123">Si utiliza Azure Backup por primera vez, debe utilizar el cmdlet **Register-AzureRMResourceProvider** para registrar el proveedor de Azure Recovery Services con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="415c9-123">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="415c9-124">El almacén de Servicios de recuperación es un recurso de ARM, por lo que deberá colocarlo dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="415c9-124">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="415c9-125">Puede usar un grupo de recursos existente o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="415c9-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="415c9-126">Al crear un nuevo grupo de recursos, especifique su nombre y su ubicación.</span><span class="sxs-lookup"><span data-stu-id="415c9-126">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="415c9-127">Utilice el cmdlet **New-AzureRmRecoveryServicesVault** para crear un nuevo almacén.</span><span class="sxs-lookup"><span data-stu-id="415c9-127">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span></span> <span data-ttu-id="415c9-128">Asegúrese de especificar para el almacén la misma ubicación del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="415c9-128">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="415c9-129">Especifique el tipo de redundancia de almacenamiento que se usará: [almacenamiento con redundancia local (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [almacenamiento con redundancia geográfica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="415c9-129">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="415c9-130">En el ejemplo siguiente se muestra que la opción -BackupStorageRedundancy para testVault está establecida en GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="415c9-130">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="415c9-131">Muchos de los cmdlets de Azure Backup requieren el objeto de almacén de Recovery Services como entrada.</span><span class="sxs-lookup"><span data-stu-id="415c9-131">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="415c9-132">Por este motivo, es conveniente almacenar el objeto de almacén de Recovery Services de Backup en una variable.</span><span class="sxs-lookup"><span data-stu-id="415c9-132">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="415c9-133">Visualización de los almacenes de una suscripción</span><span class="sxs-lookup"><span data-stu-id="415c9-133">View the vaults in a subscription</span></span>
<span data-ttu-id="415c9-134">Utilice **Get-AzureRmRecoveryServicesVault** para ver la lista de todos los almacenes de la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="415c9-134">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="415c9-135">Este comando se puede usar para comprobar que se ha creado un almacén o para ver qué almacenes están disponibles en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="415c9-135">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="415c9-136">Ejecute el comando Get-AzureRmRecoveryServicesVault, y se mostrarán todos los almacenes de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="415c9-136">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="415c9-137">Instalación del agente de copia de seguridad de Azure en un servidor DPM</span><span class="sxs-lookup"><span data-stu-id="415c9-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="415c9-138">Antes de instalar el agente de copia de seguridad de Azure, necesitará tener el instalador descargado y disponible en el servidor de Windows.</span><span class="sxs-lookup"><span data-stu-id="415c9-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="415c9-139">Puede obtener la versión más reciente del instalador en el [Centro de descarga de Microsoft](http://aka.ms/azurebackup_agent) o en la página Panel del almacén de Servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="415c9-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="415c9-140">Guarde el instalador en una ubicación que tenga fácil acceso, como *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="415c9-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="415c9-141">Para instalar el agente, ejecute el comando siguiente en una consola de PowerShell con privilegios elevados **en el servidor DPM**:</span><span class="sxs-lookup"><span data-stu-id="415c9-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="415c9-142">Esto instala el agente con todas las opciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="415c9-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="415c9-143">La instalación está unos minutos en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="415c9-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="415c9-144">Si no se especifica la opción */nu* , se abre la ventana de **Windows Update** al final de la instalación para comprobar si hay actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="415c9-144">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="415c9-145">El agente se muestra en la lista de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="415c9-145">The agent shows up in the list of installed programs.</span></span> <span data-ttu-id="415c9-146">Para ver la lista de programas instalados, vaya a **Panel de Control** > **Programas** > **Programas y características**.</span><span class="sxs-lookup"><span data-stu-id="415c9-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="415c9-148">Opciones de instalación</span><span class="sxs-lookup"><span data-stu-id="415c9-148">Installation options</span></span>
<span data-ttu-id="415c9-149">Para ver todas las opciones disponibles a través de la línea de comandos, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="415c9-149">To see all the options available via the commandline, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="415c9-150">Las opciones disponibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="415c9-150">The available options include:</span></span>

| <span data-ttu-id="415c9-151">Opción</span><span class="sxs-lookup"><span data-stu-id="415c9-151">Option</span></span> | <span data-ttu-id="415c9-152">Detalles</span><span class="sxs-lookup"><span data-stu-id="415c9-152">Details</span></span> | <span data-ttu-id="415c9-153">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="415c9-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="415c9-154">/q</span><span class="sxs-lookup"><span data-stu-id="415c9-154">/q</span></span> |<span data-ttu-id="415c9-155">Instalación silenciosa</span><span class="sxs-lookup"><span data-stu-id="415c9-155">Quiet installation</span></span> |- |
| <span data-ttu-id="415c9-156">/p:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="415c9-156">/p:"location"</span></span> |<span data-ttu-id="415c9-157">Ruta de acceso a la carpeta de instalación para el agente de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="415c9-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="415c9-158">C:\Archivos de programa\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="415c9-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="415c9-159">/s:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="415c9-159">/s:"location"</span></span> |<span data-ttu-id="415c9-160">Ruta de acceso a la carpeta de caché para el agente de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="415c9-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="415c9-161">C:\Archivos de programa\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="415c9-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="415c9-162">/m</span><span class="sxs-lookup"><span data-stu-id="415c9-162">/m</span></span> |<span data-ttu-id="415c9-163">Participación en Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="415c9-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="415c9-164">/nu</span><span class="sxs-lookup"><span data-stu-id="415c9-164">/nu</span></span> |<span data-ttu-id="415c9-165">No busca actualizaciones una vez completada la instalación</span><span class="sxs-lookup"><span data-stu-id="415c9-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="415c9-166">/d</span><span class="sxs-lookup"><span data-stu-id="415c9-166">/d</span></span> |<span data-ttu-id="415c9-167">Desinstala el agente de Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="415c9-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="415c9-168">/ph</span><span class="sxs-lookup"><span data-stu-id="415c9-168">/ph</span></span> |<span data-ttu-id="415c9-169">Dirección host del proxy</span><span class="sxs-lookup"><span data-stu-id="415c9-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="415c9-170">/po</span><span class="sxs-lookup"><span data-stu-id="415c9-170">/po</span></span> |<span data-ttu-id="415c9-171">Número de puerto del host de proxy</span><span class="sxs-lookup"><span data-stu-id="415c9-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="415c9-172">/pu</span><span class="sxs-lookup"><span data-stu-id="415c9-172">/pu</span></span> |<span data-ttu-id="415c9-173">Nombre de usuario del host de proxy</span><span class="sxs-lookup"><span data-stu-id="415c9-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="415c9-174">/pw</span><span class="sxs-lookup"><span data-stu-id="415c9-174">/pw</span></span> |<span data-ttu-id="415c9-175">Contraseña de proxy</span><span class="sxs-lookup"><span data-stu-id="415c9-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-to-a-recovery-services-vault"></a><span data-ttu-id="415c9-176">Registro de DPM en un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="415c9-176">Registering DPM to a Recovery Services Vault</span></span>
<span data-ttu-id="415c9-177">Después de crear el almacén de Servicios de recuperación, descargue el agente más reciente y las credenciales de almacén y guárdelas en una ubicación adecuada como C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="415c9-177">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="415c9-178">En el servidor de DPM, ejecute el cmdlet [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) para registrar la máquina en el almacén.</span><span class="sxs-lookup"><span data-stu-id="415c9-178">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="415c9-179">Opciones de configuración inicial</span><span class="sxs-lookup"><span data-stu-id="415c9-179">Initial configuration settings</span></span>
<span data-ttu-id="415c9-180">Una vez que el servidor DPM se registra con el almacén de Recovery Services, se inicia con la configuración de suscripción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="415c9-180">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="415c9-181">Estas opciones de suscripción incluyen funciones de red, cifrado y el área de ensayo.</span><span class="sxs-lookup"><span data-stu-id="415c9-181">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="415c9-182">Para cambiar la configuración de la suscripción, primero se debe obtener un identificador en la configuración (valor predeterminado) existente con el cmdlet [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) :</span><span class="sxs-lookup"><span data-stu-id="415c9-182">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="415c9-183">Todas las modificaciones se realizan en este objeto de PowerShell local ```$setting``` y, a continuación, el objeto completo se confirma en DPM y Azure Backup para guardarlos con el cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="415c9-183">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="415c9-184">Deberá usar la marca ```–Commit``` para asegurarse de que los cambios se conservan.</span><span class="sxs-lookup"><span data-stu-id="415c9-184">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="415c9-185">Copia de seguridad de Azure no aplicará ni usará la configuración a menos que se confirme.</span><span class="sxs-lookup"><span data-stu-id="415c9-185">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="415c9-186">Redes</span><span class="sxs-lookup"><span data-stu-id="415c9-186">Networking</span></span>
<span data-ttu-id="415c9-187">Si la conectividad del equipo DPM para el servicio de Azure Backup en Internet es a través de un servidor proxy, se debe proporcionar la configuración del servidor proxy para que las copias de seguridad se efectúen correctamente.</span><span class="sxs-lookup"><span data-stu-id="415c9-187">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="415c9-188">Esto se realiza mediante los parámetros ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` y ```ProxyPassword``` con el cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="415c9-188">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="415c9-189">En este ejemplo, no hay ningún servidor proxy y por tanto se borra explícitamente cualquier información relacionada con el proxy.</span><span class="sxs-lookup"><span data-stu-id="415c9-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="415c9-190">También puede controlar el uso de ancho de banda con las opciones de ```-WorkHourBandwidth``` y ```-NonWorkHourBandwidth``` para un conjunto determinado de días de la semana.</span><span class="sxs-lookup"><span data-stu-id="415c9-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="415c9-191">En este ejemplo no se define ninguna limitación.</span><span class="sxs-lookup"><span data-stu-id="415c9-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-the-staging-area"></a><span data-ttu-id="415c9-192">Configuración del área de ensayo</span><span class="sxs-lookup"><span data-stu-id="415c9-192">Configuring the staging Area</span></span>
<span data-ttu-id="415c9-193">El agente de Copia de seguridad de Azure que se ejecuta en el servidor DPM necesita almacenamiento temporal para los datos restaurados desde la nube (área de almacenamiento provisional local).</span><span class="sxs-lookup"><span data-stu-id="415c9-193">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="415c9-194">Configure el área de ensayo mediante el cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) y el parámetro ```-StagingAreaPath```.</span><span class="sxs-lookup"><span data-stu-id="415c9-194">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="415c9-195">En el ejemplo anterior, el área de ensayo se establecerá en *C:\StagingArea* en el objeto de PowerShell ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="415c9-195">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="415c9-196">Asegúrese de que la carpeta especificada ya existe, o bien se producirá un error en la confirmación final de la configuración de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="415c9-196">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="415c9-197">Configuración de cifrado</span><span class="sxs-lookup"><span data-stu-id="415c9-197">Encryption settings</span></span>
<span data-ttu-id="415c9-198">Los datos de copia de seguridad enviados a Azure Backup se cifran para proteger la confidencialidad de los datos.</span><span class="sxs-lookup"><span data-stu-id="415c9-198">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="415c9-199">La frase de contraseña de cifrado es la "contraseña" que permite descifrar los datos en el momento de la restauración.</span><span class="sxs-lookup"><span data-stu-id="415c9-199">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="415c9-200">Es importante que mantenga esta información segura cuando la establezca.</span><span class="sxs-lookup"><span data-stu-id="415c9-200">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="415c9-201">En el ejemplo siguiente, el primer comando convierte la cadena ```passphrase123456789``` en una cadena segura y la asigna a la variable denominada ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="415c9-201">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="415c9-202">El segundo comando establece la cadena segura en ```$Passphrase``` como la contraseña para cifrar las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="415c9-202">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="415c9-203">Mantenga la información de la frase de contraseña segura una vez establecida.</span><span class="sxs-lookup"><span data-stu-id="415c9-203">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="415c9-204">No podrá restaurar los datos de Azure sin esta frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="415c9-204">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="415c9-205">En este punto, debería haber realizado todos los cambios necesarios al objeto ```$setting``` .</span><span class="sxs-lookup"><span data-stu-id="415c9-205">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="415c9-206">Recuerde que debe confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="415c9-206">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="415c9-207">Proteger los datos en Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="415c9-207">Protect data to Azure Backup</span></span>
<span data-ttu-id="415c9-208">En esta sección, agregará un servidor de producción a DPM y, a continuación, protegerá los datos en el almacenamiento de DPM local y, a continuación, en la copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="415c9-208">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="415c9-209">En los ejemplos, se mostrará cómo realizar copias de seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="415c9-209">In the examples, we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="415c9-210">La lógica se puede ampliar fácilmente para efectuar una copia de seguridad de cualquier origen de datos compatible con DPM.</span><span class="sxs-lookup"><span data-stu-id="415c9-210">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="415c9-211">Las copias de seguridad de DPM se rigen por un grupo de protección (PG) con cuatro partes:</span><span class="sxs-lookup"><span data-stu-id="415c9-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="415c9-212">**Miembros del grupo** es una lista de todos los objetos que se pueden proteger (también conocidos como *Orígenes de datos* en DPM) que desea proteger en el mismo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="415c9-212">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="415c9-213">Por ejemplo, puede proteger las máquinas virtuales de producción en un grupo de protección y las bases de datos de SQL Server en otro grupo de protección, ya que pueden tener distintos requisitos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="415c9-213">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="415c9-214">Antes de que puedan realizar una copia de seguridad de cualquier origen de datos en un servidor de producción, deberá asegurarse de que el agente de DPM esté instalado en el servidor y administrado por DPM.</span><span class="sxs-lookup"><span data-stu-id="415c9-214">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="415c9-215">Siga los pasos para [instalar el agente de DPM](https://technet.microsoft.com/library/bb870935.aspx) y vincularlo al servidor DPM apropiado.</span><span class="sxs-lookup"><span data-stu-id="415c9-215">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="415c9-216">**Método de protección de datos** especifica las ubicaciones de copia de seguridad de destino: cinta, disco y nube.</span><span class="sxs-lookup"><span data-stu-id="415c9-216">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="415c9-217">En nuestro ejemplo se protegerán los datos en el disco local y en la nube.</span><span class="sxs-lookup"><span data-stu-id="415c9-217">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="415c9-218">Una **programación de copia de seguridad** que especifica cuándo deben realizarse copias de seguridad y la frecuencia con la que se deben sincronizar los datos entre el servidor DPM y el servidor de producción.</span><span class="sxs-lookup"><span data-stu-id="415c9-218">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="415c9-219">Una **programación de retención** que especifica cuánto tiempo se conservarán los puntos de recuperación en Azure.</span><span class="sxs-lookup"><span data-stu-id="415c9-219">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="415c9-220">Creación de un grupo de protección</span><span class="sxs-lookup"><span data-stu-id="415c9-220">Creating a protection group</span></span>
<span data-ttu-id="415c9-221">Empiece por crear un nuevo grupo de protección mediante el cmdlet [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) .</span><span class="sxs-lookup"><span data-stu-id="415c9-221">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="415c9-222">El cmdlet anterior creará un grupo de protección denominado *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="415c9-222">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="415c9-223">Un grupo de protección existente también se puede modificar más adelante para agregar la copia de seguridad a la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="415c9-223">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="415c9-224">Sin embargo, para realizar cambios en el grupo de protección (nuevo o existente), necesitamos obtener un identificador en un objeto *modificable* utilizando el cmdlet [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) .</span><span class="sxs-lookup"><span data-stu-id="415c9-224">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="415c9-225">Agregar miembros de grupo al grupo de protección</span><span class="sxs-lookup"><span data-stu-id="415c9-225">Adding group members to the Protection Group</span></span>
<span data-ttu-id="415c9-226">Cada agente de DPM conoce la lista de orígenes de datos del servidor en el que está instalado.</span><span class="sxs-lookup"><span data-stu-id="415c9-226">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="415c9-227">Para agregar un origen de datos al grupo de protección, el agente de DPM debe enviar primero una lista de los orígenes de datos al servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="415c9-227">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="415c9-228">A continuación, se agregan y seleccionan uno o más orígenes de datos al grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="415c9-228">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="415c9-229">Los pasos de PowerShell necesarios para lograrlo son:</span><span class="sxs-lookup"><span data-stu-id="415c9-229">The PowerShell steps needed to achieve this are:</span></span>

1. <span data-ttu-id="415c9-230">Recuperar una lista de todos los servidores administrados por DPM a través del agente de DPM.</span><span class="sxs-lookup"><span data-stu-id="415c9-230">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="415c9-231">Elija un servidor específico.</span><span class="sxs-lookup"><span data-stu-id="415c9-231">Choose a specific server.</span></span>
3. <span data-ttu-id="415c9-232">Recupere una lista de todos los orígenes de datos del servidor.</span><span class="sxs-lookup"><span data-stu-id="415c9-232">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="415c9-233">Elija uno o más orígenes de datos y agréguelos al grupo de protección</span><span class="sxs-lookup"><span data-stu-id="415c9-233">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="415c9-234">La lista de servidores en los que está instalado el agente de DPM y está siendo administrando por el servidor DPM se adquiere con el cmdlet [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) .</span><span class="sxs-lookup"><span data-stu-id="415c9-234">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="415c9-235">En este ejemplo se van a filtrar y configurar solo PS con el nombre *productionserver01* para efectuar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="415c9-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="415c9-236">Ahora, capture la lista de orígenes de datos en ```$server``` con el cmdlet [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605).</span><span class="sxs-lookup"><span data-stu-id="415c9-236">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="415c9-237">En este ejemplo se filtra para el volumen *D:\* que se quiere configurar para la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="415c9-237">In this example we are filtering for the volume *D:\* that we want to configure for backup.</span></span> <span data-ttu-id="415c9-238">A continuación, este origen de datos se agrega al grupo de protección mediante el cmdlet [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732).</span><span class="sxs-lookup"><span data-stu-id="415c9-238">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="415c9-239">Recuerde usar el objeto de grupo de protección *modifiable* ```$MPG``` para realizar las incorporaciones.</span><span class="sxs-lookup"><span data-stu-id="415c9-239">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="415c9-240">Repita este paso tantas veces como sea necesario hasta que haya agregado todos los orígenes de datos elegidos al grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="415c9-240">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="415c9-241">También puede comenzar con un solo origen de datos y completar el flujo de trabajo para crear el grupo de protección y, posteriormente, agregar más orígenes de datos al grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="415c9-241">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="415c9-242">Selección del método de protección de datos</span><span class="sxs-lookup"><span data-stu-id="415c9-242">Selecting the data protection method</span></span>
<span data-ttu-id="415c9-243">Una vez que los orígenes de datos se han agregado al grupo de protección, el siguiente paso es especificar el método de protección mediante el cmdlet [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) .</span><span class="sxs-lookup"><span data-stu-id="415c9-243">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="415c9-244">En este ejemplo, el grupo de protección es el programa de instalación de disco local y la copia de seguridad en la nube.</span><span class="sxs-lookup"><span data-stu-id="415c9-244">In this example, the Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="415c9-245">También tendrá que especificar el origen de datos que quiere proteger en la nube mediante el cmdlet [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) con la marca -Online.</span><span class="sxs-lookup"><span data-stu-id="415c9-245">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="415c9-246">Establecimiento del período de retención</span><span class="sxs-lookup"><span data-stu-id="415c9-246">Setting the retention range</span></span>
<span data-ttu-id="415c9-247">Establecer el período de retención de los puntos de copia de seguridad mediante el cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="415c9-247">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="415c9-248">Aunque puede parecer extraño establecer el período de retención antes de definir la programación de copia de seguridad, usando el cmdlet ```Set-DPMPolicyObjective``` se establece automáticamente una programación de copia de seguridad predeterminada que, a continuación, se puede modificar.</span><span class="sxs-lookup"><span data-stu-id="415c9-248">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="415c9-249">Siempre es posible establecer el programa de copia de seguridad en primer lugar y, a continuación, la directiva de retención.</span><span class="sxs-lookup"><span data-stu-id="415c9-249">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="415c9-250">En el ejemplo siguiente, el cmdlet establece los parámetros de retención de copias de seguridad de disco.</span><span class="sxs-lookup"><span data-stu-id="415c9-250">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="415c9-251">Esto conservará las copias de seguridad durante 10 días y sincronizará los datos cada 6 horas entre el servidor de producción y el servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="415c9-251">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="415c9-252">```SynchronizationFrequencyMinutes``` no define la frecuencia con la que se crea un punto de copia de seguridad, sino la frecuencia con la que se copian los datos en el servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="415c9-252">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span></span>  <span data-ttu-id="415c9-253">Esto evita que las copias de seguridad se vuelvan demasiado grandes.</span><span class="sxs-lookup"><span data-stu-id="415c9-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="415c9-254">Para las copias de seguridad que tienen como destino Azure (DPM hace referencia a estas como copias de seguridad en línea) se pueden configurar intervalos de retención para [retenciones a largo plazo usando un esquema abuelo-padre-hijo (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="415c9-254">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="415c9-255">Es decir, puede definir una directiva de retención combinada que implique directivas de retención diaria, semanal, mensual y anual.</span><span class="sxs-lookup"><span data-stu-id="415c9-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="415c9-256">En este ejemplo, se crea una matriz que representa el esquema de retención complejo que se desea y, a continuación, se configura el intervalo de retención usando el cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="415c9-256">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="415c9-257">Establecer la programación de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="415c9-257">Set the backup schedule</span></span>
<span data-ttu-id="415c9-258">DPM establece automáticamente una programación de copia de seguridad predeterminada si especifica el objetivo de protección mediante el cmdlet ```Set-DPMPolicyObjective``` .</span><span class="sxs-lookup"><span data-stu-id="415c9-258">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="415c9-259">Para cambiar las programaciones predeterminadas, use el cmdlet [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) seguido por el cmdlet [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723).</span><span class="sxs-lookup"><span data-stu-id="415c9-259">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="415c9-260">En el ejemplo anterior, ```$onlineSch``` es una matriz con cuatro elementos que contiene la programación de protección en línea existente para el grupo de protección en el esquema de GFS:</span><span class="sxs-lookup"><span data-stu-id="415c9-260">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="415c9-261">```$onlineSch[0]``` contiene la programación diaria</span><span class="sxs-lookup"><span data-stu-id="415c9-261">```$onlineSch[0]``` contains the daily schedule</span></span>
2. <span data-ttu-id="415c9-262">```$onlineSch[1]``` contiene la programación semanal</span><span class="sxs-lookup"><span data-stu-id="415c9-262">```$onlineSch[1]``` contains the weekly schedule</span></span>
3. <span data-ttu-id="415c9-263">```$onlineSch[2]``` contiene la programación mensual</span><span class="sxs-lookup"><span data-stu-id="415c9-263">```$onlineSch[2]``` contains the monthly schedule</span></span>
4. <span data-ttu-id="415c9-264">```$onlineSch[3]``` contiene la programación anual</span><span class="sxs-lookup"><span data-stu-id="415c9-264">```$onlineSch[3]``` contains the yearly schedule</span></span>

<span data-ttu-id="415c9-265">Por ello, si necesita modificar la programación semanal, deberá hacer referencia a ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="415c9-265">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="415c9-266">Copia de seguridad inicial</span><span class="sxs-lookup"><span data-stu-id="415c9-266">Initial backup</span></span>
<span data-ttu-id="415c9-267">Cuando efectúa una copia de seguridad de un origen de datos por primera vez, DPM debe crear una réplica inicial que genera una copia completa del origen de datos que se debe proteger en el volumen de réplica DPM.</span><span class="sxs-lookup"><span data-stu-id="415c9-267">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="415c9-268">Esta actividad se puede programar para una hora específica o puede desencadenarse manualmente mediante el cmdlet [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) con el parámetro ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="415c9-268">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="415c9-269">Cambiar el tamaño de la réplica de DPM y el volumen de puntos de recuperación</span><span class="sxs-lookup"><span data-stu-id="415c9-269">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="415c9-270">También puede cambiar el tamaño del volumen de réplica de DPM, así como el volumen de instantánea mediante el cmdlet [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) , como en el ejemplo siguiente: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb).</span><span class="sxs-lookup"><span data-stu-id="415c9-270">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="415c9-271">Confirmar los cambios en el grupo de protección</span><span class="sxs-lookup"><span data-stu-id="415c9-271">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="415c9-272">Por último, los cambios deben confirmarse antes de que DPM pueda realizar la copia de seguridad según la configuración del nuevo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="415c9-272">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="415c9-273">Esto se realiza mediante el cmdlet [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) .</span><span class="sxs-lookup"><span data-stu-id="415c9-273">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="415c9-274">Ver los puntos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="415c9-274">View the backup points</span></span>
<span data-ttu-id="415c9-275">Puede usar el cmdlet [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) para obtener una lista de todos los puntos de recuperación para un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="415c9-275">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="415c9-276">En este ejemplo, se realiza lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="415c9-276">In this example, we will:</span></span>

* <span data-ttu-id="415c9-277">se capturan todos los grupos de protección del servidor DPM, que se almacenan en una matriz ```$PG```</span><span class="sxs-lookup"><span data-stu-id="415c9-277">fetch all the PGs on the DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="415c9-278">se obtienen los orígenes de datos correspondientes a ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="415c9-278">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="415c9-279">se obtienen todos los puntos de recuperación de un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="415c9-279">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="415c9-280">Restauración de datos protegidos en Azure</span><span class="sxs-lookup"><span data-stu-id="415c9-280">Restore data protected on Azure</span></span>
<span data-ttu-id="415c9-281">Restauración de datos es una combinación de un objeto ```RecoverableItem``` y un objeto ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="415c9-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="415c9-282">En la sección anterior se facilita una lista de los puntos de la copia de seguridad de un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="415c9-282">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="415c9-283">En el ejemplo siguiente, demostraremos cómo restaurar una máquina virtual de Hyper-V de Copia de seguridad de Azure mediante la combinación de puntos de copia de seguridad con el destino para la recuperación.</span><span class="sxs-lookup"><span data-stu-id="415c9-283">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="415c9-284">Este ejemplo incluye:</span><span class="sxs-lookup"><span data-stu-id="415c9-284">This example includes:</span></span>

* <span data-ttu-id="415c9-285">Creación de una opción de recuperación mediante el cmdlet [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592).</span><span class="sxs-lookup"><span data-stu-id="415c9-285">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="415c9-286">Recuperación de la matriz de puntos de copia de seguridad mediante el cmdlet ```Get-DPMRecoveryPoint``` .</span><span class="sxs-lookup"><span data-stu-id="415c9-286">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="415c9-287">Elegir un punto de copia de seguridad desde el que efectuar la restauración.</span><span class="sxs-lookup"><span data-stu-id="415c9-287">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="415c9-288">Los comandos se pueden ampliar fácilmente para cualquier tipo de origen de datos.</span><span class="sxs-lookup"><span data-stu-id="415c9-288">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="415c9-289">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="415c9-289">Next steps</span></span>
* <span data-ttu-id="415c9-290">Para obtener más información sobre DPM para Azure Backup, vea [Introducción a Copia de seguridad de DPM](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="415c9-290">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
