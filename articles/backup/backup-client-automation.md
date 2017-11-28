---
title: Uso de PowerShell para hacer una copia de seguridad de Windows Server en Azure | Microsoft Docs
description: "Obtenga información sobre cómo implementar y administrar Copia de seguridad de Azure mediante PowerShell"
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
ms.openlocfilehash: d3f165c749af0553c4918b33b0d24cc1e21af2a9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="b9f62-103">Implementación y administración de copias de seguridad en Azure para Windows Server o cliente de Windows mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9f62-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b9f62-104">ARM</span><span class="sxs-lookup"><span data-stu-id="b9f62-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="b9f62-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="b9f62-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="b9f62-106">En este artículo se muestra cómo usar PowerShell para configurar la Copia de seguridad de Azure en un servidor o un cliente de Windows y para administrar copias de seguridad y recuperaciones.</span><span class="sxs-lookup"><span data-stu-id="b9f62-106">This article shows you how to use PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="b9f62-107">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9f62-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="b9f62-108">Este artículo se centra en los cmdlets de PowerShell de Azure Resource Manager (ARM) y MS Online Backup, que le permiten usar un almacén de Recovery Services en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b9f62-108">This article focuses on the Azure Resource Manager (ARM) and the MS Online Backup PowerShell cmdlets that enable you to use a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="b9f62-109">En octubre de 2015, se lanzó Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="b9f62-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="b9f62-110">Esta versión sucedió a la versión 0.9.8 e introdujo algunos cambios importantes, sobre todo en el patrón de nombres de los cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b9f62-110">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="b9f62-111">Los cmdlets de 1.0 siguen el patrón de nomenclatura {verbo}-AzureRm{nombre}; en el que, los nombres de 0.9.8 no incluyen **Rm** (por ejemplo, New-AzureRmResourceGroup en lugar de New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="b9f62-111">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="b9f62-112">Al usar Azure PowerShell 0.9.8, primero debe habilitar el modo de Administrador de recursos mediante la ejecución del comando **Switch-AzureMode AzureResourceManager** .</span><span class="sxs-lookup"><span data-stu-id="b9f62-112">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="b9f62-113">Este comando no es necesario en la versión 1.0 o posteriores.</span><span class="sxs-lookup"><span data-stu-id="b9f62-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="b9f62-114">Si desea utilizar scripts escritos para los entornos de 0.9.8, de 1.0 o posterior, debe actualizar y probar detenidamente los scripts en un entorno de preproducción antes de usarlos en producción para evitar un impacto inesperado.</span><span class="sxs-lookup"><span data-stu-id="b9f62-114">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully update and test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="b9f62-115">[Descargue la versión de PowerShell más reciente](https://github.com/Azure/azure-powershell/releases) (la versión mínima necesaria es 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="b9f62-115">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="b9f62-116">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="b9f62-116">Create a recovery services vault</span></span>
<span data-ttu-id="b9f62-117">Los siguientes pasos le guiarán por el proceso de creación de un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="b9f62-117">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="b9f62-118">Un almacén de Servicios de recuperación no es lo mismo que un almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b9f62-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="b9f62-119">Si utiliza Azure Backup por primera vez, debe utilizar el cmdlet **Register-AzureRMResourceProvider** para registrar el proveedor de Azure Recovery Services con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="b9f62-119">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="b9f62-120">El almacén de Servicios de recuperación es un recurso de ARM, por lo que deberá colocarlo dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b9f62-120">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="b9f62-121">Puede usar un grupo de recursos existente o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="b9f62-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="b9f62-122">Al crear un nuevo grupo de recursos, especifique su nombre y su ubicación.</span><span class="sxs-lookup"><span data-stu-id="b9f62-122">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="b9f62-123">Utilice el cmdlet **New-AzureRmRecoveryServicesVault** para crear el nuevo almacén.</span><span class="sxs-lookup"><span data-stu-id="b9f62-123">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create the new vault.</span></span> <span data-ttu-id="b9f62-124">Asegúrese de especificar para el almacén la misma ubicación del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b9f62-124">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="b9f62-125">Especifique el tipo de redundancia de almacenamiento que se usará: [almacenamiento con redundancia local (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [almacenamiento con redundancia geográfica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="b9f62-125">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="b9f62-126">En el ejemplo siguiente se muestra que la opción -BackupStorageRedundancy para testVault está establecida en GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="b9f62-126">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="b9f62-127">Muchos de los cmdlets de Azure Backup requieren el objeto de almacén de Recovery Services como entrada.</span><span class="sxs-lookup"><span data-stu-id="b9f62-127">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="b9f62-128">Por este motivo, es conveniente almacenar el objeto de almacén de Recovery Services de Backup en una variable.</span><span class="sxs-lookup"><span data-stu-id="b9f62-128">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="b9f62-129">Visualización de los almacenes de una suscripción</span><span class="sxs-lookup"><span data-stu-id="b9f62-129">View the vaults in a subscription</span></span>
<span data-ttu-id="b9f62-130">Utilice **Get-AzureRmRecoveryServicesVault** para ver la lista de todos los almacenes de la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="b9f62-130">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="b9f62-131">Este comando se puede usar para comprobar que se ha creado un almacén o para ver qué almacenes están disponibles en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b9f62-131">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="b9f62-132">Ejecute el comando **Get-AzureRmRecoveryServicesVault** y se mostrarán todos los almacenes de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b9f62-132">Run the command, **Get-AzureRmRecoveryServicesVault**, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="b9f62-133">Instalación del agente de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="b9f62-133">Installing the Azure Backup agent</span></span>
<span data-ttu-id="b9f62-134">Antes de instalar el agente de copia de seguridad de Azure, necesitará tener el instalador descargado y disponible en el servidor de Windows.</span><span class="sxs-lookup"><span data-stu-id="b9f62-134">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="b9f62-135">Puede obtener la versión más reciente del instalador en el [Centro de descarga de Microsoft](http://aka.ms/azurebackup_agent) o en la página Panel del almacén de Servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b9f62-135">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="b9f62-136">Guarde el instalador en una ubicación que tenga fácil acceso, como *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="b9f62-136">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="b9f62-137">Como alternativa, use PowerShell para obtener la aplicación de descarga:</span><span class="sxs-lookup"><span data-stu-id="b9f62-137">Alternatively, use PowerShell to get the downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="b9f62-138">Para instalar el agente, ejecute el comando siguiente en una consola de PowerShell con privilegios elevados:</span><span class="sxs-lookup"><span data-stu-id="b9f62-138">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="b9f62-139">Esto instala el agente con todas las opciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="b9f62-139">This installs the agent with all the default options.</span></span> <span data-ttu-id="b9f62-140">La instalación está unos minutos en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="b9f62-140">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="b9f62-141">Si no se especifica la opción */nu* , se abrirá la ventana de **Windows Update** al final de la instalación para comprobar si hay actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="b9f62-141">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="b9f62-142">Una vez instalado, el agente se mostrará en la lista de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="b9f62-142">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="b9f62-143">Para ver la lista de programas instalados, vaya a **Panel de Control** > **Programas** > **Programas y características**.</span><span class="sxs-lookup"><span data-stu-id="b9f62-143">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="b9f62-145">Opciones de instalación</span><span class="sxs-lookup"><span data-stu-id="b9f62-145">Installation options</span></span>
<span data-ttu-id="b9f62-146">Para ver todas las opciones disponibles a través de la línea de comandos, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b9f62-146">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="b9f62-147">Las opciones disponibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="b9f62-147">The available options include:</span></span>

| <span data-ttu-id="b9f62-148">Opción</span><span class="sxs-lookup"><span data-stu-id="b9f62-148">Option</span></span> | <span data-ttu-id="b9f62-149">Detalles</span><span class="sxs-lookup"><span data-stu-id="b9f62-149">Details</span></span> | <span data-ttu-id="b9f62-150">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="b9f62-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9f62-151">/q</span><span class="sxs-lookup"><span data-stu-id="b9f62-151">/q</span></span> |<span data-ttu-id="b9f62-152">Instalación silenciosa</span><span class="sxs-lookup"><span data-stu-id="b9f62-152">Quiet installation</span></span> |- |
| <span data-ttu-id="b9f62-153">/p:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="b9f62-153">/p:"location"</span></span> |<span data-ttu-id="b9f62-154">Ruta de acceso a la carpeta de instalación para el agente de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="b9f62-154">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="b9f62-155">C:\Archivos de programa\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="b9f62-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="b9f62-156">/s:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="b9f62-156">/s:"location"</span></span> |<span data-ttu-id="b9f62-157">Ruta de acceso a la carpeta de caché para el agente de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="b9f62-157">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="b9f62-158">C:\Archivos de programa\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="b9f62-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="b9f62-159">/m</span><span class="sxs-lookup"><span data-stu-id="b9f62-159">/m</span></span> |<span data-ttu-id="b9f62-160">Participación en Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="b9f62-160">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="b9f62-161">/nu</span><span class="sxs-lookup"><span data-stu-id="b9f62-161">/nu</span></span> |<span data-ttu-id="b9f62-162">No busca actualizaciones una vez completada la instalación</span><span class="sxs-lookup"><span data-stu-id="b9f62-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="b9f62-163">/d</span><span class="sxs-lookup"><span data-stu-id="b9f62-163">/d</span></span> |<span data-ttu-id="b9f62-164">Desinstala el agente de Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="b9f62-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="b9f62-165">/ph</span><span class="sxs-lookup"><span data-stu-id="b9f62-165">/ph</span></span> |<span data-ttu-id="b9f62-166">Dirección host del proxy</span><span class="sxs-lookup"><span data-stu-id="b9f62-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="b9f62-167">/po</span><span class="sxs-lookup"><span data-stu-id="b9f62-167">/po</span></span> |<span data-ttu-id="b9f62-168">Número de puerto del host de proxy</span><span class="sxs-lookup"><span data-stu-id="b9f62-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="b9f62-169">/pu</span><span class="sxs-lookup"><span data-stu-id="b9f62-169">/pu</span></span> |<span data-ttu-id="b9f62-170">Nombre de usuario del host de proxy</span><span class="sxs-lookup"><span data-stu-id="b9f62-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="b9f62-171">/pw</span><span class="sxs-lookup"><span data-stu-id="b9f62-171">/pw</span></span> |<span data-ttu-id="b9f62-172">Contraseña de proxy</span><span class="sxs-lookup"><span data-stu-id="b9f62-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-to-a-recovery-services-vault"></a><span data-ttu-id="b9f62-173">Registro de Windows Server o el equipo cliente de Windows en un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="b9f62-173">Registering Windows Server or Windows client machine to a Recovery Services Vault</span></span>
<span data-ttu-id="b9f62-174">Después de crear el almacén de Servicios de recuperación, descargue el agente más reciente y las credenciales de almacén y guárdelas en una ubicación adecuada como C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="b9f62-174">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="b9f62-175">En el sistema con Windows Server o el equipo cliente de Windows, ejecute el cmdlet [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) para registrar la máquina en el almacén.</span><span class="sxs-lookup"><span data-stu-id="b9f62-175">On the Windows Server or Windows client machine, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>
<span data-ttu-id="b9f62-176">Este y otros cmdlets usados para copias de seguridad son del módulo MSONLINE que el instalador del agente de Mars agregó como parte del proceso de instalación.</span><span class="sxs-lookup"><span data-stu-id="b9f62-176">This, and other cmdlets used for backup, are from the MSONLINE module which the Mars AgentInstaller added as part of the installation process.</span></span> 

<span data-ttu-id="b9f62-177">El instalador del agente no actualiza la variable $Env:PSModulePath.</span><span class="sxs-lookup"><span data-stu-id="b9f62-177">The Agent installer does not update the $Env:PSModulePath variable.</span></span> <span data-ttu-id="b9f62-178">Esto significa que se produce un error en la carga automática del módulo.</span><span class="sxs-lookup"><span data-stu-id="b9f62-178">This means module auto-load fails.</span></span> <span data-ttu-id="b9f62-179">Para resolver este problema, puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b9f62-179">To resolve this you can do the following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="b9f62-180">Como alternativa, puede cargar manualmente el módulo en el script como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b9f62-180">Alternatively, you can manually load the module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="b9f62-181">Después de cargar los cmdlets de Online Backup, registre las credenciales del almacén:</span><span class="sxs-lookup"><span data-stu-id="b9f62-181">Once you load the Online Backup cmdlets, you register the vault credentials:</span></span>


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
> <span data-ttu-id="b9f62-182">No use rutas de acceso relativas para especificar el archivo de credenciales del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="b9f62-182">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="b9f62-183">Debe proporcionar una ruta de acceso absoluta como entrada para el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9f62-183">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="b9f62-184">Configuración de redes</span><span class="sxs-lookup"><span data-stu-id="b9f62-184">Networking settings</span></span>
<span data-ttu-id="b9f62-185">Cuando la conectividad de la máquina de Windows a Internet se realiza a través de un servidor proxy, también se puede proporcionar la configuración del proxy al agente.</span><span class="sxs-lookup"><span data-stu-id="b9f62-185">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="b9f62-186">En este ejemplo, no hay ningún servidor proxy y por tanto se borra explícitamente cualquier información relacionada con el proxy.</span><span class="sxs-lookup"><span data-stu-id="b9f62-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="b9f62-187">También puede controlar el uso de ancho de banda con las opciones de ```work hour bandwidth``` y ```non-work hour bandwidth``` para un conjunto determinado de días de la semana.</span><span class="sxs-lookup"><span data-stu-id="b9f62-187">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="b9f62-188">El establecimiento de los detalles de ancho de banda y del proxy se realiza mediante el cmdlet [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) :</span><span class="sxs-lookup"><span data-stu-id="b9f62-188">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="b9f62-189">Configuración de cifrado</span><span class="sxs-lookup"><span data-stu-id="b9f62-189">Encryption settings</span></span>
<span data-ttu-id="b9f62-190">Los datos de copia de seguridad enviados a Azure Backup se cifran para proteger la confidencialidad de los datos.</span><span class="sxs-lookup"><span data-stu-id="b9f62-190">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="b9f62-191">La frase de contraseña de cifrado es la "contraseña" que permite descifrar los datos en el momento de la restauración.</span><span class="sxs-lookup"><span data-stu-id="b9f62-191">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="b9f62-192">Mantenga la información de la frase de contraseña segura una vez establecida.</span><span class="sxs-lookup"><span data-stu-id="b9f62-192">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="b9f62-193">No podrá restaurar los datos de Azure sin esta frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="b9f62-193">You are not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="b9f62-194">Realizar copias de seguridad de archivos y carpetas</span><span class="sxs-lookup"><span data-stu-id="b9f62-194">Back up files and folders</span></span>
<span data-ttu-id="b9f62-195">Todas las copias de seguridad de servidores y clientes de Windows en Copia de seguridad de Azure se rigen por una directiva.</span><span class="sxs-lookup"><span data-stu-id="b9f62-195">All backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="b9f62-196">La directiva consta de tres partes:</span><span class="sxs-lookup"><span data-stu-id="b9f62-196">The policy comprises three parts:</span></span>

1. <span data-ttu-id="b9f62-197">Un **programa de copia de seguridad** que especifica cuándo deben efectuarse y sincronizarse las copias de seguridad con el servicio.</span><span class="sxs-lookup"><span data-stu-id="b9f62-197">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="b9f62-198">Una **programación de retención** que especifica cuánto tiempo se conservarán los puntos de recuperación en Azure.</span><span class="sxs-lookup"><span data-stu-id="b9f62-198">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="b9f62-199">Una **especificación de inclusión o exclusión de archivo** que determina los elementos de los que se debe efectuar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b9f62-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="b9f62-200">En este documento, dado que se está automatizando la copia de seguridad, supondremos que no se ha configurado nada.</span><span class="sxs-lookup"><span data-stu-id="b9f62-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="b9f62-201">Comenzamos creando una nueva directiva de copia de seguridad mediante el cmdlet [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b9f62-201">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="b9f62-202">En este momento la directiva está vacía y se necesitan otros cmdlet para definir qué elementos se incluirán o excluirán, cuándo se ejecutarán las copias de seguridad y dónde se almacenarán las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b9f62-202">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="b9f62-203">Configuración de la programación de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b9f62-203">Configuring the backup schedule</span></span>
<span data-ttu-id="b9f62-204">La primera de las tres partes de una directiva es la programación de copia de seguridad, que se crea usando el cmdlet [New-OBSchedule](https://technet.microsoft.com/library/hh770401) .</span><span class="sxs-lookup"><span data-stu-id="b9f62-204">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="b9f62-205">La programación de copia de seguridad define cuándo deben realizarse copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b9f62-205">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="b9f62-206">Al crear una programación se deben especificar dos parámetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="b9f62-206">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="b9f62-207">**Días de la semana** en los que se debe ejecutar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b9f62-207">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="b9f62-208">Puede ejecutar el trabajo de copia de seguridad en solo un día o cada día de la semana, o cualquier combinación intermedia.</span><span class="sxs-lookup"><span data-stu-id="b9f62-208">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="b9f62-209">**Horas del día** a las que se debe ejecutar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b9f62-209">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="b9f62-210">Puede definir hasta tres horas distintas del día en las que se activará la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b9f62-210">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="b9f62-211">Por ejemplo, podría configurar una directiva de copia de seguridad que se ejecute a las 4 p.m. cada sábado y domingo.</span><span class="sxs-lookup"><span data-stu-id="b9f62-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="b9f62-212">La programación de copia de seguridad debe estar asociada con una directiva y esto puede lograrse mediante el uso del cmdlet [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) .</span><span class="sxs-lookup"><span data-stu-id="b9f62-212">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="b9f62-213">Configuración de una directiva de retención</span><span class="sxs-lookup"><span data-stu-id="b9f62-213">Configuring a retention policy</span></span>
<span data-ttu-id="b9f62-214">La directiva de retención define cuánto tiempo se conservan los puntos de recuperación de los trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b9f62-214">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="b9f62-215">Al crear una nueva directiva de retención mediante el cmdlet [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425), puede especificar el número de días que los puntos de recuperación de copia de seguridad deben conservarse con Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="b9f62-215">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="b9f62-216">En el ejemplo siguiente se establece una directiva de retención de 7 días.</span><span class="sxs-lookup"><span data-stu-id="b9f62-216">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="b9f62-217">La directiva de retención debe estar asociada con la directiva principal mediante el cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="b9f62-217">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="b9f62-218">Incluir y excluir archivos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b9f62-218">Including and excluding files to be backed up</span></span>
<span data-ttu-id="b9f62-219">Un objeto ```OBFileSpec``` define los archivos incluidos y excluidos de una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b9f62-219">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="b9f62-220">Se trata de un conjunto de reglas de ámbito de los archivos y carpetas protegidos de un equipo.</span><span class="sxs-lookup"><span data-stu-id="b9f62-220">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="b9f62-221">Puede tener tantas reglas de inclusión o exclusión de archivos como se necesiten y asociarlas con una directiva.</span><span class="sxs-lookup"><span data-stu-id="b9f62-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="b9f62-222">Al crear un nuevo objeto OBFileSpec, puede:</span><span class="sxs-lookup"><span data-stu-id="b9f62-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="b9f62-223">Especificar los archivos y carpetas que se van a incluir</span><span class="sxs-lookup"><span data-stu-id="b9f62-223">Specify the files and folders to be included</span></span>
* <span data-ttu-id="b9f62-224">Especificar los archivos y carpetas que se van a excluir</span><span class="sxs-lookup"><span data-stu-id="b9f62-224">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="b9f62-225">Especificar la copia de seguridad recursiva de los datos en una carpeta (o) si se deben copiar solo los archivos de nivel superior en la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="b9f62-225">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="b9f62-226">Esto último se consigue mediante la marca -NonRecursive del comando New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="b9f62-226">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="b9f62-227">En el ejemplo siguiente, crearemos copias de seguridad del volumen C: y D: y excluiremos los archivos binarios de sistema operativo de la carpeta de Windows y las carpetas temporales.</span><span class="sxs-lookup"><span data-stu-id="b9f62-227">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="b9f62-228">Para ello, crearemos dos especificaciones de archivos mediante el cmdlet [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) : uno para la inclusión y otro para la exclusión.</span><span class="sxs-lookup"><span data-stu-id="b9f62-228">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="b9f62-229">Una vez que se hayan creado las especificaciones de archivo, se asocian con la directiva mediante el cmdlet [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) .</span><span class="sxs-lookup"><span data-stu-id="b9f62-229">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-the-policy"></a><span data-ttu-id="b9f62-230">Aplicación de la directiva</span><span class="sxs-lookup"><span data-stu-id="b9f62-230">Applying the policy</span></span>
<span data-ttu-id="b9f62-231">Ahora el objeto de la directiva está finalizado y tiene una programación de copia de seguridad asociada, una directiva de retención y una lista de inclusión o exclusión de archivos.</span><span class="sxs-lookup"><span data-stu-id="b9f62-231">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="b9f62-232">Ahora se puede confirmar esta directiva para ser usada por Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="b9f62-232">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="b9f62-233">Antes de aplicar la directiva recién creada, asegúrese de que no haya ninguna directiva de copia de seguridad existente asociada con el servidor mediante el uso del cmdlet [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) .</span><span class="sxs-lookup"><span data-stu-id="b9f62-233">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="b9f62-234">Para eliminar la directiva, se le pedirá confirmación.</span><span class="sxs-lookup"><span data-stu-id="b9f62-234">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="b9f62-235">Para omitir el uso de la confirmación, use la marca ```-Confirm:$false``` con el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9f62-235">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="b9f62-236">La confirmación del objeto de la directiva se lleva a cabo usando el cmdlet [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) .</span><span class="sxs-lookup"><span data-stu-id="b9f62-236">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="b9f62-237">Esto también requerirá confirmación.</span><span class="sxs-lookup"><span data-stu-id="b9f62-237">This will also ask for confirmation.</span></span> <span data-ttu-id="b9f62-238">Para omitir el uso de la confirmación, use la marca ```-Confirm:$false``` con el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9f62-238">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want to save this backup policy ? [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
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

<span data-ttu-id="b9f62-239">Puede ver los detalles de la directiva de copia de seguridad existente con el cmdlet [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) .</span><span class="sxs-lookup"><span data-stu-id="b9f62-239">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="b9f62-240">Puede profundizar más mediante el cmdlet [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) de la programación de copia de seguridad y el cmdlet [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) de las directivas de retención</span><span class="sxs-lookup"><span data-stu-id="b9f62-240">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="b9f62-241">Realización de una copia de seguridad ad-hoc</span><span class="sxs-lookup"><span data-stu-id="b9f62-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="b9f62-242">Una vez establecida una directiva de copia de seguridad, las copias de seguridad se producirán en función de la programación.</span><span class="sxs-lookup"><span data-stu-id="b9f62-242">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="b9f62-243">Desencadenar una copia de seguridad ad-hoc también es posible usando el cmdlet [Start-OBBackup](https://technet.microsoft.com/library/hh770426) :</span><span class="sxs-lookup"><span data-stu-id="b9f62-243">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing the metadata VHD...
Data transfer is in progress. It might take longer since it is the first backup and all data needs to be transferred...
Data transfer completed and all backed up data is in the cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="b9f62-244">Restaurar datos de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="b9f62-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="b9f62-245">Esta sección le guiará por los pasos necesarios para automatizar la recuperación de datos de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="b9f62-245">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="b9f62-246">Esto implica los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b9f62-246">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="b9f62-247">Seleccionar el volumen de origen</span><span class="sxs-lookup"><span data-stu-id="b9f62-247">Pick the source volume</span></span>
2. <span data-ttu-id="b9f62-248">Elegir un punto de copia de seguridad desde el que efectuar la restauración</span><span class="sxs-lookup"><span data-stu-id="b9f62-248">Choose a backup point to restore</span></span>
3. <span data-ttu-id="b9f62-249">Selección de un elemento para restaurar</span><span class="sxs-lookup"><span data-stu-id="b9f62-249">Choose an item to restore</span></span>
4. <span data-ttu-id="b9f62-250">Desencadenar el proceso de restauración</span><span class="sxs-lookup"><span data-stu-id="b9f62-250">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="b9f62-251">Selección del volumen de origen</span><span class="sxs-lookup"><span data-stu-id="b9f62-251">Picking the source volume</span></span>
<span data-ttu-id="b9f62-252">Para restaurar un elemento de Azure Backup, primero deberá identificar el origen del elemento.</span><span class="sxs-lookup"><span data-stu-id="b9f62-252">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="b9f62-253">Dado que los comandos se están ejecutando en el contexto de un servidor o un cliente de Windows, el equipo ya se ha identificado.</span><span class="sxs-lookup"><span data-stu-id="b9f62-253">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="b9f62-254">El siguiente paso para identificar el origen es identificar el volumen que lo contiene.</span><span class="sxs-lookup"><span data-stu-id="b9f62-254">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="b9f62-255">Se puede recuperar una lista de los volúmenes u orígenes de los que se está efectuando una copia de seguridad desde esta máquina mediante la ejecución del cmdlet [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) .</span><span class="sxs-lookup"><span data-stu-id="b9f62-255">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="b9f62-256">Este comando devuelve una matriz de todos los orígenes de los que se ha efectuado una copia de seguridad desde este servidor/cliente.</span><span class="sxs-lookup"><span data-stu-id="b9f62-256">This command returns an array of all the sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-from-which-to-restore"></a><span data-ttu-id="b9f62-257">Elección de un punto de copia de seguridad desde el que efectuar la restauración</span><span class="sxs-lookup"><span data-stu-id="b9f62-257">Choosing a backup point from which to restore</span></span>
<span data-ttu-id="b9f62-258">La lista de puntos de copia de seguridad se puede recuperar ejecutando el cmdlet [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) con los parámetros adecuados.</span><span class="sxs-lookup"><span data-stu-id="b9f62-258">You retreive a list of backup points by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="b9f62-259">En nuestro ejemplo, elegiremos el punto de copia de seguridad más reciente para el volumen de origen *D:* y lo usaremos para recuperar un archivo específico.</span><span class="sxs-lookup"><span data-stu-id="b9f62-259">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

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
<span data-ttu-id="b9f62-260">El objeto ```$rps``` es una matriz de puntos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b9f62-260">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="b9f62-261">El primer elemento es el punto más reciente y el enésimo elemento es el punto más antiguo.</span><span class="sxs-lookup"><span data-stu-id="b9f62-261">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="b9f62-262">Para elegir el punto más reciente, usaremos ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="b9f62-262">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="b9f62-263">Selección de un elemento para restaurar</span><span class="sxs-lookup"><span data-stu-id="b9f62-263">Choosing an item to restore</span></span>
<span data-ttu-id="b9f62-264">Para identificar el archivo o carpeta exacto que desea restaurar, use de forma recursiva el cmdlet [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b9f62-264">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="b9f62-265">De esta forma se puede examinar la jerarquía de carpetas exclusivamente mediante el ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="b9f62-265">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="b9f62-266">En este ejemplo, si se desea restaurar el archivo *finances.xls* se puede hacer referencia a este con el objeto ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="b9f62-266">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="b9f62-267">También puede buscar elementos para restaurar usando el cmdlet ```Get-OBRecoverableItem``` .</span><span class="sxs-lookup"><span data-stu-id="b9f62-267">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="b9f62-268">En nuestro ejemplo, para buscar *finances.xls* podríamos obtener un identificador en el archivo mediante la ejecución de este comando:</span><span class="sxs-lookup"><span data-stu-id="b9f62-268">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="b9f62-269">Desencadenar el proceso de restauración</span><span class="sxs-lookup"><span data-stu-id="b9f62-269">Triggering the restore process</span></span>
<span data-ttu-id="b9f62-270">Para desencadenar el proceso de restauración, primero es necesario especificar las opciones de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b9f62-270">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="b9f62-271">Esto puede hacerse mediante el uso del cmdlet [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b9f62-271">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="b9f62-272">En este ejemplo, supongamos que deseamos restaurar los archivos en *C:\temp*. Supongamos también que deseamos omitir archivos que ya existen en la carpeta de destino *C:\temp*. Para crear dicha opción de recuperación, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b9f62-272">For this example, let's assume that we want to restore the files to *C:\temp*. Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*. To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="b9f62-273">Ahora, desencadene el proceso de restauración con el comando [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) en el ```$item``` seleccionado desde la salida del cmdlet ```Get-OBRecoverableItem```:</span><span class="sxs-lookup"><span data-stu-id="b9f62-273">Now trigger the restore process by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="b9f62-274">Desinstalación del agente de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="b9f62-274">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="b9f62-275">La desinstalación del agente de Azure Backup se puede realizar con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b9f62-275">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="b9f62-276">Desinstalación de los archivos binarios del agente de la máquina tiene algunas consecuencias a tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="b9f62-276">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="b9f62-277">Elimina el filtro de archivos de la máquina y se detiene el seguimiento de los cambios.</span><span class="sxs-lookup"><span data-stu-id="b9f62-277">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="b9f62-278">Se elimina toda la información de directivas de la máquina, pero continúa almacenada en el servicio.</span><span class="sxs-lookup"><span data-stu-id="b9f62-278">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="b9f62-279">Se eliminan todas las programaciones de copia de seguridad y no se realizan más copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b9f62-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="b9f62-280">Sin embargo, los datos almacenados en Azure permanecen y se mantienen de acuerdo con la configuración de la directiva de retención establecida por usted.</span><span class="sxs-lookup"><span data-stu-id="b9f62-280">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="b9f62-281">Los puntos más antiguos vencen automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b9f62-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="b9f62-282">Administración remota</span><span class="sxs-lookup"><span data-stu-id="b9f62-282">Remote management</span></span>
<span data-ttu-id="b9f62-283">Toda la administración relacionada con el agente, las políticas y los orígenes de datos de Azure Backup puede realizarse de forma remota mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9f62-283">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="b9f62-284">La máquina que se administrará de forma remota debe estar preparada correctamente.</span><span class="sxs-lookup"><span data-stu-id="b9f62-284">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="b9f62-285">De forma predeterminada, el servicio WinRM está configurado para iniciarse manualmente.</span><span class="sxs-lookup"><span data-stu-id="b9f62-285">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="b9f62-286">El tipo de inicio debe establecerse en *Automatic* y se debe iniciar el servicio.</span><span class="sxs-lookup"><span data-stu-id="b9f62-286">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="b9f62-287">Para comprobar que el servicio WinRM se está ejecutando, el valor de la propiedad Status debe ser *Running*.</span><span class="sxs-lookup"><span data-stu-id="b9f62-287">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="b9f62-288">PowerShell debe configurarse para la comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="b9f62-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="b9f62-289">La máquina puede ahora administrarse de forma remota: empezando por la instalación del agente.</span><span class="sxs-lookup"><span data-stu-id="b9f62-289">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="b9f62-290">Por ejemplo, el script siguiente copia al agente en la máquina remota y lo instala.</span><span class="sxs-lookup"><span data-stu-id="b9f62-290">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="b9f62-291">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b9f62-291">Next steps</span></span>
<span data-ttu-id="b9f62-292">Para obtener más información sobre Azure Backup para Windows Server o cliente de Windows, consulte</span><span class="sxs-lookup"><span data-stu-id="b9f62-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="b9f62-293">Introducción a Azure Backup</span><span class="sxs-lookup"><span data-stu-id="b9f62-293">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="b9f62-294">Copia de seguridad de servidores Windows</span><span class="sxs-lookup"><span data-stu-id="b9f62-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
