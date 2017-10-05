---
title: Uso de PowerShell para administrar las copias de seguridad de Windows Server en Azure | Microsoft Docs
description: Implemente y administre las copias de seguridad de Windows Server mediante PowerShell.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: a8e20356ae383ee4fa2158ea544d5d0905028124
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="cb63b-103">Implementación y administración de copias de seguridad en Azure para Windows Server o cliente de Windows mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb63b-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb63b-104">ARM</span><span class="sxs-lookup"><span data-stu-id="cb63b-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="cb63b-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="cb63b-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="cb63b-106">En este artículo se explica cómo usar PowerShell para realizar una copia de seguridad de Windows Server o de datos de la estación de trabajo de Windows en un almacén de Backup.</span><span class="sxs-lookup"><span data-stu-id="cb63b-106">This article explains how to use PowerShell to back up Windows Server or Windows workstation data to a backup vault.</span></span> <span data-ttu-id="cb63b-107">Microsoft recomienda el uso de almacenes de Recovery Services para todas las implementaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="cb63b-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="cb63b-108">Si es un nuevo usuario de Azure Backup y todavía no ha creado un almacén de Backup en su suscripción, use artículo [Implementación y administración de copias de seguridad en Azure para Windows Server o cliente de Windows mediante PowerShell](backup-client-automation.md) para almacenar los datos en un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="cb63b-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="cb63b-109">Ahora puede actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="cb63b-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="cb63b-110">Para más información, consulte el artículo [Actualización de un almacén de Backup a un almacén de Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="cb63b-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="cb63b-111">Microsoft anima a actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="cb63b-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="cb63b-112">A partir del 15 de octubre de 2017, no podrá usar PowerShell para crear almacenes de Backup.</span><span class="sxs-lookup"><span data-stu-id="cb63b-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="cb63b-113">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="cb63b-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="cb63b-114">Todos los almacenes de Backup restantes se actualizarán automáticamente a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="cb63b-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="cb63b-115">No podrá acceder a los datos de copia de seguridad en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="cb63b-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="cb63b-116">En su lugar, utilice Azure Portal para tener acceso a los datos de copia de seguridad en los almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="cb63b-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="cb63b-117">Instalar Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="cb63b-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="cb63b-118">En octubre de 2015, se lanzó Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="cb63b-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="cb63b-119">Esta versión sucedió a la versión 0.9.8 e introdujo algunos cambios importantes, sobre todo en el patrón de nombres de los cmdlets.</span><span class="sxs-lookup"><span data-stu-id="cb63b-119">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="cb63b-120">Los cmdlets de 1.0 siguen el patrón de nomenclatura {verbo}-AzureRm{nombre}; en el que, los nombres de 0.9.8 no incluyen **Rm** (por ejemplo, New-AzureRmResourceGroup en lugar de New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="cb63b-120">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="cb63b-121">Al usar Azure PowerShell 0.9.8, primero debe habilitar el modo de Administrador de recursos mediante la ejecución del comando **Switch-AzureMode AzureResourceManager** .</span><span class="sxs-lookup"><span data-stu-id="cb63b-121">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="cb63b-122">Este comando no es necesario en la versión 1.0 o posteriores.</span><span class="sxs-lookup"><span data-stu-id="cb63b-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="cb63b-123">Si desea utilizar scripts escritos para los entornos de 0.9.8, de 1.0 o posterior, debe probar detenidamente los scripts en un entorno de preproducción antes de usarlos en producción para evitar un impacto inesperado.</span><span class="sxs-lookup"><span data-stu-id="cb63b-123">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="cb63b-124">[Descargue la versión de PowerShell más reciente](https://github.com/Azure/azure-powershell/releases) (la versión mínima necesaria es 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="cb63b-124">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="cb63b-125">Creación de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="cb63b-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="cb63b-126">La primera vez que los clientes usen Azure Backup deben registrar el proveedor de Azure Backup que se va a usar con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="cb63b-126">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="cb63b-127">Para ello, ejecute el siguiente comando: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="cb63b-127">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="cb63b-128">Puede crear un nuevo almacén de copia de seguridad mediante el cmdlet **New-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="cb63b-128">You can create a new backup vault using the **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="cb63b-129">El almacén de copia de seguridad es un recurso ARM, por lo que necesita colocarlo dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cb63b-129">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="cb63b-130">En una consola de Azure PowerShell, ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cb63b-130">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="cb63b-131">Use el cmdlet **Get-AzureRMBackupVault** para enumerar los almacenes de copia de seguridad en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="cb63b-131">Use the **Get-AzureRMBackupVault** cmdlet to list the backup vaults in a subscription.</span></span>

## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="cb63b-132">Instalación del agente de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="cb63b-132">Installing the Azure Backup agent</span></span>
<span data-ttu-id="cb63b-133">Antes de instalar el agente de Azure Backup, necesitará tener el instalador descargado y disponible en el servidor de Windows.</span><span class="sxs-lookup"><span data-stu-id="cb63b-133">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="cb63b-134">Puede obtener la versión más reciente del instalador en el [Centro de descarga de Microsoft](http://aka.ms/azurebackup_agent) o en la página Panel del almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb63b-134">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="cb63b-135">Guarde el instalador en una ubicación que tenga fácil acceso, como *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="cb63b-135">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="cb63b-136">Para instalar el agente, ejecute el comando siguiente en una consola de PowerShell con privilegios elevados:</span><span class="sxs-lookup"><span data-stu-id="cb63b-136">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="cb63b-137">Esto instala el agente con todas las opciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="cb63b-137">This installs the agent with all the default options.</span></span> <span data-ttu-id="cb63b-138">La instalación está unos minutos en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="cb63b-138">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="cb63b-139">Si no se especifica la opción */nu* , se abrirá la ventana de **Windows Update** al final de la instalación para comprobar si hay actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="cb63b-139">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="cb63b-140">Una vez instalado, el agente se mostrará en la lista de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="cb63b-140">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="cb63b-141">Para ver la lista de programas instalados, vaya a **Panel de Control** > **Programas** > **Programas y características**.</span><span class="sxs-lookup"><span data-stu-id="cb63b-141">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="cb63b-143">Opciones de instalación</span><span class="sxs-lookup"><span data-stu-id="cb63b-143">Installation options</span></span>
<span data-ttu-id="cb63b-144">Para ver todas las opciones disponibles a través de la línea de comandos, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cb63b-144">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="cb63b-145">Las opciones disponibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="cb63b-145">The available options include:</span></span>

| <span data-ttu-id="cb63b-146">Opción</span><span class="sxs-lookup"><span data-stu-id="cb63b-146">Option</span></span> | <span data-ttu-id="cb63b-147">Detalles</span><span class="sxs-lookup"><span data-stu-id="cb63b-147">Details</span></span> | <span data-ttu-id="cb63b-148">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="cb63b-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cb63b-149">/q</span><span class="sxs-lookup"><span data-stu-id="cb63b-149">/q</span></span> |<span data-ttu-id="cb63b-150">Instalación silenciosa</span><span class="sxs-lookup"><span data-stu-id="cb63b-150">Quiet installation</span></span> |- |
| <span data-ttu-id="cb63b-151">/p:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="cb63b-151">/p:"location"</span></span> |<span data-ttu-id="cb63b-152">Ruta de acceso a la carpeta de instalación para el agente de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="cb63b-152">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="cb63b-153">C:\Archivos de programa\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="cb63b-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="cb63b-154">/s:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="cb63b-154">/s:"location"</span></span> |<span data-ttu-id="cb63b-155">Ruta de acceso a la carpeta de caché para el agente de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="cb63b-155">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="cb63b-156">C:\Archivos de programa\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="cb63b-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="cb63b-157">/m</span><span class="sxs-lookup"><span data-stu-id="cb63b-157">/m</span></span> |<span data-ttu-id="cb63b-158">Participación en Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="cb63b-158">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="cb63b-159">/nu</span><span class="sxs-lookup"><span data-stu-id="cb63b-159">/nu</span></span> |<span data-ttu-id="cb63b-160">No busca actualizaciones una vez completada la instalación</span><span class="sxs-lookup"><span data-stu-id="cb63b-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="cb63b-161">/d</span><span class="sxs-lookup"><span data-stu-id="cb63b-161">/d</span></span> |<span data-ttu-id="cb63b-162">Desinstala el agente de Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="cb63b-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="cb63b-163">/ph</span><span class="sxs-lookup"><span data-stu-id="cb63b-163">/ph</span></span> |<span data-ttu-id="cb63b-164">Dirección host del proxy</span><span class="sxs-lookup"><span data-stu-id="cb63b-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="cb63b-165">/po</span><span class="sxs-lookup"><span data-stu-id="cb63b-165">/po</span></span> |<span data-ttu-id="cb63b-166">Número de puerto del host de proxy</span><span class="sxs-lookup"><span data-stu-id="cb63b-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="cb63b-167">/pu</span><span class="sxs-lookup"><span data-stu-id="cb63b-167">/pu</span></span> |<span data-ttu-id="cb63b-168">Nombre de usuario del host de proxy</span><span class="sxs-lookup"><span data-stu-id="cb63b-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="cb63b-169">/pw</span><span class="sxs-lookup"><span data-stu-id="cb63b-169">/pw</span></span> |<span data-ttu-id="cb63b-170">Contraseña de proxy</span><span class="sxs-lookup"><span data-stu-id="cb63b-170">Proxy Password</span></span> |- |

## <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="cb63b-171">Registro con el servicio de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="cb63b-171">Registering with the Azure Backup service</span></span>
<span data-ttu-id="cb63b-172">Para poder registrarse con el servicio Azure Backup, debe asegurarse de que se cumplen los [requisitos previos](backup-configure-vault.md) .</span><span class="sxs-lookup"><span data-stu-id="cb63b-172">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="cb63b-173">Debe:</span><span class="sxs-lookup"><span data-stu-id="cb63b-173">You must:</span></span>

* <span data-ttu-id="cb63b-174">Disponer de una suscripción válida a Azure</span><span class="sxs-lookup"><span data-stu-id="cb63b-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="cb63b-175">Disponer de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="cb63b-175">Have a backup vault</span></span>

<span data-ttu-id="cb63b-176">Para descargar las credenciales del almacén, ejecute el cmdlet **Get-AzureRMBackupVaultCredentials** en una consola de Azure PowerShell y almacénelo en una ubicación adecuada como *C:\Descargas\*.</span><span class="sxs-lookup"><span data-stu-id="cb63b-176">To download the vault credentials, run the **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="cb63b-177">El registro de la máquina con el almacén de claves se realiza mediante el cmdlet [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) :</span><span class="sxs-lookup"><span data-stu-id="cb63b-177">Registering the machine with the vault is done using the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="cb63b-178">No use rutas de acceso relativas para especificar el archivo de credenciales del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="cb63b-178">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="cb63b-179">Debe proporcionar una ruta de acceso absoluta como entrada para el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cb63b-179">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="cb63b-180">Configuración de redes</span><span class="sxs-lookup"><span data-stu-id="cb63b-180">Networking settings</span></span>
<span data-ttu-id="cb63b-181">Cuando la conectividad de la máquina de Windows a Internet se realiza a través de un servidor proxy, también se puede proporcionar la configuración del proxy al agente.</span><span class="sxs-lookup"><span data-stu-id="cb63b-181">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="cb63b-182">En este ejemplo, no hay ningún servidor proxy y por tanto se borra explícitamente cualquier información relacionada con el proxy.</span><span class="sxs-lookup"><span data-stu-id="cb63b-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="cb63b-183">También puede controlar el uso de ancho de banda con las opciones de ```work hour bandwidth``` y ```non-work hour bandwidth``` para un conjunto determinado de días de la semana.</span><span class="sxs-lookup"><span data-stu-id="cb63b-183">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="cb63b-184">El establecimiento de los detalles de ancho de banda y del proxy se realiza mediante el cmdlet [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) :</span><span class="sxs-lookup"><span data-stu-id="cb63b-184">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="cb63b-185">Configuración de cifrado</span><span class="sxs-lookup"><span data-stu-id="cb63b-185">Encryption settings</span></span>
<span data-ttu-id="cb63b-186">Los datos de copia de seguridad enviados a Azure Backup se cifran para proteger la confidencialidad de los datos.</span><span class="sxs-lookup"><span data-stu-id="cb63b-186">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="cb63b-187">La frase de contraseña de cifrado es la "contraseña" que permite descifrar los datos en el momento de la restauración.</span><span class="sxs-lookup"><span data-stu-id="cb63b-187">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="cb63b-188">Mantenga la información de la frase de contraseña segura una vez establecida.</span><span class="sxs-lookup"><span data-stu-id="cb63b-188">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="cb63b-189">No podrá restaurar los datos de Azure sin esta frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="cb63b-189">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="cb63b-190">Realizar copias de seguridad de archivos y carpetas</span><span class="sxs-lookup"><span data-stu-id="cb63b-190">Back up files and folders</span></span>
<span data-ttu-id="cb63b-191">Todas las copias de seguridad de servidores y clientes de Windows en Azure Backup se rigen por una directiva.</span><span class="sxs-lookup"><span data-stu-id="cb63b-191">All your backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="cb63b-192">La directiva consta de tres partes:</span><span class="sxs-lookup"><span data-stu-id="cb63b-192">The policy comprises three parts:</span></span>

1. <span data-ttu-id="cb63b-193">Un **programa de copia de seguridad** que especifica cuándo deben efectuarse y sincronizarse las copias de seguridad con el servicio.</span><span class="sxs-lookup"><span data-stu-id="cb63b-193">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="cb63b-194">Una **programación de retención** que especifica cuánto tiempo se conservarán los puntos de recuperación en Azure.</span><span class="sxs-lookup"><span data-stu-id="cb63b-194">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="cb63b-195">Una **especificación de inclusión o exclusión de archivo** que determina los elementos de los que se debe efectuar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb63b-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="cb63b-196">En este documento, dado que se está automatizando la copia de seguridad, supondremos que no se ha configurado nada.</span><span class="sxs-lookup"><span data-stu-id="cb63b-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="cb63b-197">Comenzamos creando una nueva directiva de copia de seguridad mediante el cmdlet [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) y usándolo.</span><span class="sxs-lookup"><span data-stu-id="cb63b-197">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="cb63b-198">En este momento la directiva está vacía y se necesitan otros cmdlet para definir qué elementos se incluirán o excluirán, cuándo se ejecutarán las copias de seguridad y dónde se almacenarán las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb63b-198">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="cb63b-199">Configuración de la programación de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="cb63b-199">Configuring the backup schedule</span></span>
<span data-ttu-id="cb63b-200">La primera de las tres partes de una directiva es la programación de copia de seguridad, que se crea usando el cmdlet [New-OBSchedule](https://technet.microsoft.com/library/hh770401) .</span><span class="sxs-lookup"><span data-stu-id="cb63b-200">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="cb63b-201">La programación de copia de seguridad define cuándo deben realizarse copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb63b-201">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="cb63b-202">Al crear una programación se deben especificar dos parámetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="cb63b-202">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="cb63b-203">**Días de la semana** en los que se debe ejecutar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb63b-203">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="cb63b-204">Puede ejecutar el trabajo de copia de seguridad en solo un día o cada día de la semana, o cualquier combinación intermedia.</span><span class="sxs-lookup"><span data-stu-id="cb63b-204">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="cb63b-205">**Horas del día** a las que se debe ejecutar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb63b-205">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="cb63b-206">Puede definir hasta tres horas distintas del día en las que se activará la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb63b-206">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="cb63b-207">Por ejemplo, podría configurar una directiva de copia de seguridad que se ejecute a las 4 p.m. cada sábado y domingo.</span><span class="sxs-lookup"><span data-stu-id="cb63b-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="cb63b-208">La programación de copia de seguridad debe estar asociada con una directiva y esto puede lograrse mediante el uso del cmdlet [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) .</span><span class="sxs-lookup"><span data-stu-id="cb63b-208">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="cb63b-209">Configuración de una directiva de retención</span><span class="sxs-lookup"><span data-stu-id="cb63b-209">Configuring a retention policy</span></span>
<span data-ttu-id="cb63b-210">La directiva de retención define cuánto tiempo se conservan los puntos de recuperación de los trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb63b-210">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="cb63b-211">Al crear una nueva directiva de retención mediante el cmdlet [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425), puede especificar el número de días que los puntos de recuperación de copia de seguridad deben conservarse con Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="cb63b-211">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="cb63b-212">En el ejemplo siguiente se establece una directiva de retención de 7 días.</span><span class="sxs-lookup"><span data-stu-id="cb63b-212">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="cb63b-213">La directiva de retención debe estar asociada con la directiva principal mediante el cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="cb63b-213">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="cb63b-214">Incluir y excluir archivos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="cb63b-214">Including and excluding files to be backed up</span></span>
<span data-ttu-id="cb63b-215">Un objeto ```OBFileSpec``` define los archivos incluidos y excluidos de una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb63b-215">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="cb63b-216">Se trata de un conjunto de reglas de ámbito de los archivos y carpetas protegidos de un equipo.</span><span class="sxs-lookup"><span data-stu-id="cb63b-216">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="cb63b-217">Puede tener tantas reglas de inclusión o exclusión de archivos como se necesiten y asociarlas con una directiva.</span><span class="sxs-lookup"><span data-stu-id="cb63b-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="cb63b-218">Al crear un nuevo objeto OBFileSpec, puede:</span><span class="sxs-lookup"><span data-stu-id="cb63b-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="cb63b-219">Especificar los archivos y carpetas que se van a incluir</span><span class="sxs-lookup"><span data-stu-id="cb63b-219">Specify the files and folders to be included</span></span>
* <span data-ttu-id="cb63b-220">Especificar los archivos y carpetas que se van a excluir</span><span class="sxs-lookup"><span data-stu-id="cb63b-220">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="cb63b-221">Especificar la copia de seguridad recursiva de los datos en una carpeta (o) si se deben copiar solo los archivos de nivel superior en la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="cb63b-221">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="cb63b-222">Esto último se consigue mediante la marca -NonRecursive del comando New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="cb63b-222">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="cb63b-223">En el ejemplo siguiente, crearemos copias de seguridad del volumen C: y D: y excluiremos los archivos binarios de sistema operativo de la carpeta de Windows y las carpetas temporales.</span><span class="sxs-lookup"><span data-stu-id="cb63b-223">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="cb63b-224">Para ello, crearemos dos especificaciones de archivos mediante el cmdlet [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) : uno para la inclusión y otro para la exclusión.</span><span class="sxs-lookup"><span data-stu-id="cb63b-224">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="cb63b-225">Una vez que se hayan creado las especificaciones de archivo, se asocian con la directiva mediante el cmdlet [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) .</span><span class="sxs-lookup"><span data-stu-id="cb63b-225">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-the-policy"></a><span data-ttu-id="cb63b-226">Aplicación de la directiva</span><span class="sxs-lookup"><span data-stu-id="cb63b-226">Applying the policy</span></span>
<span data-ttu-id="cb63b-227">Ahora el objeto de la directiva está finalizado y tiene una programación de copia de seguridad asociada, una directiva de retención y una lista de inclusión o exclusión de archivos.</span><span class="sxs-lookup"><span data-stu-id="cb63b-227">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="cb63b-228">Ahora se puede confirmar esta directiva para ser usada por Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="cb63b-228">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="cb63b-229">Antes de aplicar la directiva recién creada, asegúrese de que no haya ninguna directiva de copia de seguridad existente asociada con el servidor mediante el uso del cmdlet [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) .</span><span class="sxs-lookup"><span data-stu-id="cb63b-229">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="cb63b-230">Para eliminar la directiva, se le pedirá confirmación.</span><span class="sxs-lookup"><span data-stu-id="cb63b-230">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="cb63b-231">Para omitir el uso de la confirmación, use la marca ```-Confirm:$false``` con el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cb63b-231">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="cb63b-232">La confirmación del objeto de la directiva se lleva a cabo usando el cmdlet [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) .</span><span class="sxs-lookup"><span data-stu-id="cb63b-232">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="cb63b-233">Esto también requerirá confirmación.</span><span class="sxs-lookup"><span data-stu-id="cb63b-233">This will also ask for confirmation.</span></span> <span data-ttu-id="cb63b-234">Para omitir el uso de la confirmación, use la marca ```-Confirm:$false``` con el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cb63b-234">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

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

<span data-ttu-id="cb63b-235">Puede ver los detalles de la directiva de copia de seguridad existente con el cmdlet [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) .</span><span class="sxs-lookup"><span data-stu-id="cb63b-235">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="cb63b-236">Puede profundizar más mediante el cmdlet [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) de la programación de copia de seguridad y el cmdlet [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) de las directivas de retención</span><span class="sxs-lookup"><span data-stu-id="cb63b-236">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="cb63b-237">Realización de una copia de seguridad ad-hoc</span><span class="sxs-lookup"><span data-stu-id="cb63b-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="cb63b-238">Una vez establecida una directiva de copia de seguridad, las copias de seguridad se producirán en función de la programación.</span><span class="sxs-lookup"><span data-stu-id="cb63b-238">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="cb63b-239">Desencadenar una copia de seguridad ad-hoc también es posible usando el cmdlet [Start-OBBackup](https://technet.microsoft.com/library/hh770426) :</span><span class="sxs-lookup"><span data-stu-id="cb63b-239">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="cb63b-240">Restaurar datos de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="cb63b-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="cb63b-241">Esta sección le guiará por los pasos necesarios para automatizar la recuperación de datos de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="cb63b-241">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="cb63b-242">Esto implica los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cb63b-242">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="cb63b-243">Seleccionar el volumen de origen</span><span class="sxs-lookup"><span data-stu-id="cb63b-243">Pick the source volume</span></span>
2. <span data-ttu-id="cb63b-244">Elegir un punto de copia de seguridad desde el que efectuar la restauración</span><span class="sxs-lookup"><span data-stu-id="cb63b-244">Choose a backup point to restore</span></span>
3. <span data-ttu-id="cb63b-245">Selección de un elemento para restaurar</span><span class="sxs-lookup"><span data-stu-id="cb63b-245">Choose an item to restore</span></span>
4. <span data-ttu-id="cb63b-246">Desencadenar el proceso de restauración</span><span class="sxs-lookup"><span data-stu-id="cb63b-246">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="cb63b-247">Selección del volumen de origen</span><span class="sxs-lookup"><span data-stu-id="cb63b-247">Picking the source volume</span></span>
<span data-ttu-id="cb63b-248">Para restaurar un elemento de Azure Backup, primero deberá identificar el origen del elemento.</span><span class="sxs-lookup"><span data-stu-id="cb63b-248">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="cb63b-249">Dado que los comandos se están ejecutando en el contexto de un servidor o un cliente de Windows, el equipo ya se ha identificado.</span><span class="sxs-lookup"><span data-stu-id="cb63b-249">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="cb63b-250">El siguiente paso para identificar el origen es identificar el volumen que lo contiene.</span><span class="sxs-lookup"><span data-stu-id="cb63b-250">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="cb63b-251">Se puede recuperar una lista de los volúmenes u orígenes de los que se está efectuando una copia de seguridad desde esta máquina mediante la ejecución del cmdlet [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) .</span><span class="sxs-lookup"><span data-stu-id="cb63b-251">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="cb63b-252">Este comando devuelve una matriz de todos los orígenes de los que se ha efectuado una copia de seguridad desde este servidor/cliente.</span><span class="sxs-lookup"><span data-stu-id="cb63b-252">This command returns an array of all the sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-to-restore"></a><span data-ttu-id="cb63b-253">Elegir un punto de copia de seguridad para restaurar</span><span class="sxs-lookup"><span data-stu-id="cb63b-253">Choosing a backup point to restore</span></span>
<span data-ttu-id="cb63b-254">La lista de puntos de copia de seguridad se puede recuperar ejecutando el cmdlet [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) con los parámetros adecuados.</span><span class="sxs-lookup"><span data-stu-id="cb63b-254">The list of backup points can be retrieved by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="cb63b-255">En nuestro ejemplo, elegiremos el punto de copia de seguridad más reciente para el volumen de origen *D:* y lo usaremos para recuperar un archivo específico.</span><span class="sxs-lookup"><span data-stu-id="cb63b-255">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

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
<span data-ttu-id="cb63b-256">El objeto ```$rps``` es una matriz de puntos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb63b-256">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="cb63b-257">El primer elemento es el punto más reciente y el enésimo elemento es el punto más antiguo.</span><span class="sxs-lookup"><span data-stu-id="cb63b-257">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="cb63b-258">Para elegir el punto más reciente, usaremos ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="cb63b-258">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="cb63b-259">Selección de un elemento para restaurar</span><span class="sxs-lookup"><span data-stu-id="cb63b-259">Choosing an item to restore</span></span>
<span data-ttu-id="cb63b-260">Para identificar el archivo o carpeta exacto que desea restaurar, use de forma recursiva el cmdlet [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) .</span><span class="sxs-lookup"><span data-stu-id="cb63b-260">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="cb63b-261">De esta forma se puede examinar la jerarquía de carpetas exclusivamente mediante el ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="cb63b-261">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="cb63b-262">En este ejemplo, si se desea restaurar el archivo *finances.xls* se puede hacer referencia a este con el objeto ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="cb63b-262">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="cb63b-263">También puede buscar elementos para restaurar usando el cmdlet ```Get-OBRecoverableItem``` .</span><span class="sxs-lookup"><span data-stu-id="cb63b-263">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="cb63b-264">En nuestro ejemplo, para buscar *finances.xls* podríamos obtener un identificador en el archivo mediante la ejecución de este comando:</span><span class="sxs-lookup"><span data-stu-id="cb63b-264">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="cb63b-265">Desencadenar el proceso de restauración</span><span class="sxs-lookup"><span data-stu-id="cb63b-265">Triggering the restore process</span></span>
<span data-ttu-id="cb63b-266">Para desencadenar el proceso de restauración, primero es necesario especificar las opciones de recuperación.</span><span class="sxs-lookup"><span data-stu-id="cb63b-266">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="cb63b-267">Esto puede hacerse mediante el uso del cmdlet [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) .</span><span class="sxs-lookup"><span data-stu-id="cb63b-267">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="cb63b-268">En este ejemplo, supongamos que deseamos restaurar los archivos en *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="cb63b-268">For this example, let's assume that we want to restore the files to *C:\temp*.</span></span> <span data-ttu-id="cb63b-269">Supongamos también que deseamos omitir archivos que ya existen en la carpeta de destino *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="cb63b-269">Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*.</span></span> <span data-ttu-id="cb63b-270">Para crear dicha opción de recuperación, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cb63b-270">To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="cb63b-271">Ahora, desencadene la restauración con el comando [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) en el ```$item``` seleccionado desde la salida del cmdlet ```Get-OBRecoverableItem```:</span><span class="sxs-lookup"><span data-stu-id="cb63b-271">Now trigger restore by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="cb63b-272">Desinstalación del agente de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="cb63b-272">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="cb63b-273">La desinstalación del agente de Azure Backup se puede realizar con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="cb63b-273">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="cb63b-274">Desinstalación de los archivos binarios del agente de la máquina tiene algunas consecuencias a tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="cb63b-274">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="cb63b-275">Elimina el filtro de archivos de la máquina y se detiene el seguimiento de los cambios.</span><span class="sxs-lookup"><span data-stu-id="cb63b-275">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="cb63b-276">Se elimina toda la información de directivas de la máquina, pero continúa almacenada en el servicio.</span><span class="sxs-lookup"><span data-stu-id="cb63b-276">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="cb63b-277">Se eliminan todas las programaciones de copia de seguridad y no se realizan más copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cb63b-277">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="cb63b-278">Sin embargo, los datos almacenados en Azure permanecen y se mantienen de acuerdo con la configuración de la directiva de retención establecida por usted.</span><span class="sxs-lookup"><span data-stu-id="cb63b-278">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="cb63b-279">Los puntos más antiguos vencen automáticamente.</span><span class="sxs-lookup"><span data-stu-id="cb63b-279">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="cb63b-280">Administración remota</span><span class="sxs-lookup"><span data-stu-id="cb63b-280">Remote management</span></span>
<span data-ttu-id="cb63b-281">Toda la administración relacionada con el agente, las políticas y los orígenes de datos de Azure Backup puede realizarse de forma remota mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb63b-281">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="cb63b-282">La máquina que se administrará de forma remota debe estar preparada correctamente.</span><span class="sxs-lookup"><span data-stu-id="cb63b-282">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="cb63b-283">De forma predeterminada, el servicio WinRM está configurado para iniciarse manualmente.</span><span class="sxs-lookup"><span data-stu-id="cb63b-283">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="cb63b-284">El tipo de inicio debe establecerse en *Automatic* y se debe iniciar el servicio.</span><span class="sxs-lookup"><span data-stu-id="cb63b-284">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="cb63b-285">Para comprobar que el servicio WinRM se está ejecutando, el valor de la propiedad Status debe ser *Running*.</span><span class="sxs-lookup"><span data-stu-id="cb63b-285">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="cb63b-286">PowerShell debe configurarse para la comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="cb63b-286">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="cb63b-287">La máquina puede ahora administrarse de forma remota: empezando por la instalación del agente.</span><span class="sxs-lookup"><span data-stu-id="cb63b-287">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="cb63b-288">Por ejemplo, el script siguiente copia al agente en la máquina remota y lo instala.</span><span class="sxs-lookup"><span data-stu-id="cb63b-288">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="cb63b-289">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb63b-289">Next steps</span></span>
<span data-ttu-id="cb63b-290">Para obtener más información sobre Azure Backup para Windows Server o cliente de Windows, consulte</span><span class="sxs-lookup"><span data-stu-id="cb63b-290">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="cb63b-291">Introducción a Azure Backup</span><span class="sxs-lookup"><span data-stu-id="cb63b-291">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="cb63b-292">Copia de seguridad de servidores Windows</span><span class="sxs-lookup"><span data-stu-id="cb63b-292">Back up Windows Servers</span></span>](backup-configure-vault.md)
