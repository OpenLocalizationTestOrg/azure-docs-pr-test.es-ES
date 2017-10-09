---
title: aaaUse copias de seguridad de Windows Server de toomanage de PowerShell de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="7379e-103">Implementar y administrar tooAzure copia de seguridad para el cliente de Windows del servidor de Windows con PowerShell</span><span class="sxs-lookup"><span data-stu-id="7379e-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7379e-104">ARM</span><span class="sxs-lookup"><span data-stu-id="7379e-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="7379e-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="7379e-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="7379e-106">Este artículo explica cómo toouse PowerShell tooback tooa de datos de estación de trabajo de Windows de servidor de Windows o una copia de seguridad el almacén.</span><span class="sxs-lookup"><span data-stu-id="7379e-106">This article explains how toouse PowerShell tooback up Windows Server or Windows workstation data tooa backup vault.</span></span> <span data-ttu-id="7379e-107">Microsoft recomienda el uso de almacenes de Recovery Services para todas las implementaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="7379e-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="7379e-108">Si es un nuevo usuario de copia de seguridad de Azure y no se ha creado un almacén de copia de seguridad en su suscripción, use el artículo de hello, [implementar y administrar tooAzure de datos de Data Protection Manager mediante PowerShell](backup-client-automation.md) para almacenar los datos en un almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="7379e-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7379e-109">Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7379e-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="7379e-110">Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="7379e-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="7379e-111">Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7379e-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="7379e-112">Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7379e-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="7379e-113">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="7379e-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="7379e-114">Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7379e-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="7379e-115">No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="7379e-116">En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="7379e-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="7379e-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7379e-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="7379e-118">En octubre de 2015, se lanzó Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="7379e-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="7379e-119">Esta versión se realizó correctamente la versión de Hola 0.9.8 e imperiosa algunos cambios importantes, especialmente en el patrón de nomenclatura de Hola de cmdlets de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-119">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="7379e-120">1.0 seguimiento cmdlets Hola patrón de nomenclatura {verbo}-AzureRm {nombre}; mientras que no incluyen nombres de hello 0.9.8 **Rm** (por ejemplo, New-AzureRmResourceGroup en lugar de New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="7379e-120">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="7379e-121">Al usar Azure PowerShell 0.9.8, primero debe habilitar el modo de administrador de recursos de hello ejecutando hello **Switch-AzureMode AzureResourceManager** comando.</span><span class="sxs-lookup"><span data-stu-id="7379e-121">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="7379e-122">Este comando no es necesario en la versión 1.0 o posteriores.</span><span class="sxs-lookup"><span data-stu-id="7379e-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="7379e-123">Si desea toouse los scripts escritos para el entorno de hello 0.9.8, en Hola 1.0 o posterior entorno, cuidadosamente debe probar las secuencias de comandos de hello en un entorno de preproducción antes de usarlos en producción tooavoid impacto inesperado.</span><span class="sxs-lookup"><span data-stu-id="7379e-123">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="7379e-124">[Descargar la versión más reciente de PowerShell de hello](https://github.com/Azure/azure-powershell/releases) (versión mínima necesaria es: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="7379e-124">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="7379e-125">Creación de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="7379e-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="7379e-126">Para los clientes mediante copia de seguridad de Azure Hola primera vez, deberá toobe de proveedor de copia de seguridad de Azure tooregister Hola usado con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="7379e-126">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="7379e-127">Puede hacerlo ejecutando el siguiente comando de hello: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="7379e-127">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="7379e-128">Puede crear un nuevo almacén de copia de seguridad mediante hello **AzureRMBackupVault New** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7379e-128">You can create a new backup vault using hello **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="7379e-129">almacén de copia de seguridad de Hello es un recurso ARM, por lo que necesita tooplace dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7379e-129">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="7379e-130">En una consola de Azure PowerShell con privilegios elevados, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="7379e-130">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="7379e-131">Hola de uso **AzureRMBackupVault Get** almacenes de credenciales de copia de seguridad de cmdlet toolist hello en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="7379e-131">Use hello **Get-AzureRMBackupVault** cmdlet toolist hello backup vaults in a subscription.</span></span>

## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="7379e-132">Instalar el agente de copia de seguridad de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="7379e-132">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="7379e-133">Antes de instalar el agente de copia de seguridad de Azure de hello, necesita a instalador de hello toohave descargado y presente en hello Windows Server.</span><span class="sxs-lookup"><span data-stu-id="7379e-133">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="7379e-134">Puede obtener última versión del instalador de Hola de Hola de hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o desde la página del panel del almacén de hello copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7379e-134">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="7379e-135">Guardar instalador hello tooan ubicación fácilmente accesible como * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="7379e-135">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="7379e-136">agente de hello tooinstall, ejecute el siguiente comando en una consola de PowerShell con privilegios elevados de Hola:</span><span class="sxs-lookup"><span data-stu-id="7379e-136">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="7379e-137">Agente de Hola se instala con todas las opciones predeterminadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-137">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="7379e-138">instalación de Hello tarda unos minutos en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-138">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="7379e-139">Si no se especifica hello */nu* opción, a continuación, hello **Windows Update** se abrirá la ventana final Hola de hello toocheck de instalación para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="7379e-139">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="7379e-140">Una vez instalado, agente de Hola se mostrará en la lista de Hola de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="7379e-140">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="7379e-141">lista de hello toosee de programas instalados, vaya demasiado**el Panel de Control** > **programas** > **programas y características**.</span><span class="sxs-lookup"><span data-stu-id="7379e-141">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="7379e-143">Opciones de instalación</span><span class="sxs-lookup"><span data-stu-id="7379e-143">Installation options</span></span>
<span data-ttu-id="7379e-144">toosee todas las opciones disponibles a través de Hola Hola de línea de comandos, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7379e-144">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="7379e-145">Hola las opciones disponibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="7379e-145">hello available options include:</span></span>

| <span data-ttu-id="7379e-146">Opción</span><span class="sxs-lookup"><span data-stu-id="7379e-146">Option</span></span> | <span data-ttu-id="7379e-147">Detalles</span><span class="sxs-lookup"><span data-stu-id="7379e-147">Details</span></span> | <span data-ttu-id="7379e-148">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="7379e-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7379e-149">/q</span><span class="sxs-lookup"><span data-stu-id="7379e-149">/q</span></span> |<span data-ttu-id="7379e-150">Instalación silenciosa</span><span class="sxs-lookup"><span data-stu-id="7379e-150">Quiet installation</span></span> |- |
| <span data-ttu-id="7379e-151">/p:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="7379e-151">/p:"location"</span></span> |<span data-ttu-id="7379e-152">Carpeta de instalación de toohello de ruta de acceso para el agente de copia de seguridad de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-152">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="7379e-153">C:\Archivos de programa\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="7379e-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="7379e-154">/s:"ubicación"</span><span class="sxs-lookup"><span data-stu-id="7379e-154">/s:"location"</span></span> |<span data-ttu-id="7379e-155">Carpeta de caché de ruta de acceso toohello para el agente de copia de seguridad de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-155">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="7379e-156">C:\Archivos de programa\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="7379e-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="7379e-157">/m</span><span class="sxs-lookup"><span data-stu-id="7379e-157">/m</span></span> |<span data-ttu-id="7379e-158">Participación en tooMicrosoft actualización</span><span class="sxs-lookup"><span data-stu-id="7379e-158">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="7379e-159">/nu</span><span class="sxs-lookup"><span data-stu-id="7379e-159">/nu</span></span> |<span data-ttu-id="7379e-160">No busca actualizaciones una vez completada la instalación</span><span class="sxs-lookup"><span data-stu-id="7379e-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="7379e-161">/d</span><span class="sxs-lookup"><span data-stu-id="7379e-161">/d</span></span> |<span data-ttu-id="7379e-162">Desinstala el agente de Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="7379e-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="7379e-163">/ph</span><span class="sxs-lookup"><span data-stu-id="7379e-163">/ph</span></span> |<span data-ttu-id="7379e-164">Dirección host del proxy</span><span class="sxs-lookup"><span data-stu-id="7379e-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="7379e-165">/po</span><span class="sxs-lookup"><span data-stu-id="7379e-165">/po</span></span> |<span data-ttu-id="7379e-166">Número de puerto del host de proxy</span><span class="sxs-lookup"><span data-stu-id="7379e-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="7379e-167">/pu</span><span class="sxs-lookup"><span data-stu-id="7379e-167">/pu</span></span> |<span data-ttu-id="7379e-168">Nombre de usuario del host de proxy</span><span class="sxs-lookup"><span data-stu-id="7379e-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="7379e-169">/pw</span><span class="sxs-lookup"><span data-stu-id="7379e-169">/pw</span></span> |<span data-ttu-id="7379e-170">Contraseña de proxy</span><span class="sxs-lookup"><span data-stu-id="7379e-170">Proxy Password</span></span> |- |

## <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="7379e-171">Registrar con hello servicio de copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="7379e-171">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="7379e-172">Para poder registrar con hello servicio de copia de seguridad de Azure, necesita tooensure ese hello [requisitos previos](backup-configure-vault.md) se cumplen.</span><span class="sxs-lookup"><span data-stu-id="7379e-172">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="7379e-173">Debe:</span><span class="sxs-lookup"><span data-stu-id="7379e-173">You must:</span></span>

* <span data-ttu-id="7379e-174">Disponer de una suscripción válida a Azure</span><span class="sxs-lookup"><span data-stu-id="7379e-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="7379e-175">Disponer de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="7379e-175">Have a backup vault</span></span>

<span data-ttu-id="7379e-176">las credenciales de almacén de hello toodownload, ejecute hello **Get AzureRMBackupVaultCredentials** cmdlet en una consola de PowerShell de Azure y el almacén en una ubicación conveniente, como * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="7379e-176">toodownload hello vault credentials, run hello **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="7379e-177">Máquina de hello registrar con el almacén de Hola se lleva a cabo mediante hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7379e-177">Registering hello machine with hello vault is done using hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

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
> <span data-ttu-id="7379e-178">No utilice el archivo de credenciales de almacén de rutas de acceso relativas toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-178">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="7379e-179">Debe proporcionar una ruta de acceso absoluta como un cmdlet de entrada toohello.</span><span class="sxs-lookup"><span data-stu-id="7379e-179">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="7379e-180">Configuración de redes</span><span class="sxs-lookup"><span data-stu-id="7379e-180">Networking settings</span></span>
<span data-ttu-id="7379e-181">Cuando la conectividad de Hola de hello Windows máquina toohello que Internet es a través de un servidor proxy, configuración de proxy de hello también puede proporcionarse a toohello agente.</span><span class="sxs-lookup"><span data-stu-id="7379e-181">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="7379e-182">En este ejemplo, no hay ningún servidor proxy y por tanto se borra explícitamente cualquier información relacionada con el proxy.</span><span class="sxs-lookup"><span data-stu-id="7379e-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="7379e-183">Uso de ancho de banda también puede controlarse con opciones de Hola de ```work hour bandwidth``` y ```non-work hour bandwidth``` para un conjunto determinado de días de la semana de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-183">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="7379e-184">Establecer detalles de servidor proxy y el ancho de banda de Hola se realiza mediante hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7379e-184">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="7379e-185">Configuración de cifrado</span><span class="sxs-lookup"><span data-stu-id="7379e-185">Encryption settings</span></span>
<span data-ttu-id="7379e-186">Hola copia de seguridad de datos enviados tooAzure copia de seguridad es cifrada tooprotect Hola confidencialidad de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-186">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="7379e-187">Hola frase de contraseña es datos de contraseña"hello" toodecrypt hello en tiempo de Hola de restauración.</span><span class="sxs-lookup"><span data-stu-id="7379e-187">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="7379e-188">Almacenar información de la frase de contraseña de hello seguro y protegido una vez que se establece.</span><span class="sxs-lookup"><span data-stu-id="7379e-188">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="7379e-189">No será capaz de toorestore datos de Azure sin esta frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="7379e-189">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="7379e-190">Realizar copias de seguridad de archivos y carpetas</span><span class="sxs-lookup"><span data-stu-id="7379e-190">Back up files and folders</span></span>
<span data-ttu-id="7379e-191">Todas las copias de seguridad de clientes y servidores de Windows tooAzure copia de seguridad se rigen por una directiva.</span><span class="sxs-lookup"><span data-stu-id="7379e-191">All your backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="7379e-192">Directiva de Hello consta de tres partes:</span><span class="sxs-lookup"><span data-stu-id="7379e-192">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="7379e-193">A **programar copia de seguridad** que especifica si las copias de seguridad necesitan toobe realizada y se sincronice con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-193">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="7379e-194">A **programación de retención** que especifica cuánto tiempo los puntos de recuperación de hello tooretain en Azure.</span><span class="sxs-lookup"><span data-stu-id="7379e-194">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="7379e-195">Una **especificación de inclusión o exclusión de archivo** que determina los elementos de los que se debe efectuar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7379e-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="7379e-196">En este documento, dado que se está automatizando la copia de seguridad, supondremos que no se ha configurado nada.</span><span class="sxs-lookup"><span data-stu-id="7379e-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="7379e-197">Comenzamos creando una nueva directiva de copia de seguridad mediante hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet y utilizándolo.</span><span class="sxs-lookup"><span data-stu-id="7379e-197">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="7379e-198">En este Hola tiempo directiva está vacía y otros cmdlets están toodefine necesario qué elementos se pueden incluir o excluir, cuando las copias de seguridad se ejecuta y Hola donde se almacenarán las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7379e-198">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="7379e-199">Configuración de programación de copia de seguridad de Hola</span><span class="sxs-lookup"><span data-stu-id="7379e-199">Configuring hello backup schedule</span></span>
<span data-ttu-id="7379e-200">Hola primero de hello 3 partes de una directiva es la programación de copia de seguridad hello, que se crea utilizando hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7379e-200">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="7379e-201">programación de copia de seguridad de Hello define cuándo las copias de seguridad necesitan toobe realizada.</span><span class="sxs-lookup"><span data-stu-id="7379e-201">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="7379e-202">Al crear una programación tiene parámetros de entrada de toospecify 2:</span><span class="sxs-lookup"><span data-stu-id="7379e-202">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="7379e-203">**Días de la semana de hello** debe ejecutar esa copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-203">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="7379e-204">Puede ejecutar el trabajo de copia de seguridad de hello en sólo un día o cada día de semana de Hola o cualquier combinación de entre.</span><span class="sxs-lookup"><span data-stu-id="7379e-204">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="7379e-205">**Horas del día de hello** cuándo se debe ejecutar copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-205">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="7379e-206">Puede definir una too3 diferentes horas del día de hello cuando se activará la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-206">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="7379e-207">Por ejemplo, podría configurar una directiva de copia de seguridad que se ejecute a las 4 p.m. cada sábado y domingo.</span><span class="sxs-lookup"><span data-stu-id="7379e-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="7379e-208">programación de copia de seguridad de Hello necesita toobe asociado a una directiva, y esto puede lograrse mediante el uso de hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7379e-208">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="7379e-209">Configuración de una directiva de retención</span><span class="sxs-lookup"><span data-stu-id="7379e-209">Configuring a retention policy</span></span>
<span data-ttu-id="7379e-210">Directiva de retención de Hello define cuánto tiempo de recuperación se conservan los puntos creados a partir de los trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7379e-210">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="7379e-211">Al crear una nueva directiva de retención mediante hello [OBRetentionPolicy New](https://technet.microsoft.com/library/hh770425) cmdlet, puede especificar el número de Hola de días que Hola puntos de recuperación de copia de seguridad necesita toobe conservan con copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="7379e-211">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="7379e-212">ejemplo de Hola siguiente establece una directiva de retención de 7 días.</span><span class="sxs-lookup"><span data-stu-id="7379e-212">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="7379e-213">Hello directiva de retención debe estar asociada con la directiva principal hello mediante el cmdlet de hello [OBRetentionPolicy conjunto](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="7379e-213">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="7379e-214">Incluir y excluir archivos toobe copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="7379e-214">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="7379e-215">Un ```OBFileSpec``` objeto define hello toobe de archivos incluidos y excluidos de una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7379e-215">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="7379e-216">Se trata de un conjunto de reglas que ámbito out Hola proteger archivos y carpetas en un equipo.</span><span class="sxs-lookup"><span data-stu-id="7379e-216">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="7379e-217">Puede tener tantas reglas de inclusión o exclusión de archivos como se necesiten y asociarlas con una directiva.</span><span class="sxs-lookup"><span data-stu-id="7379e-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="7379e-218">Al crear un nuevo objeto OBFileSpec, puede:</span><span class="sxs-lookup"><span data-stu-id="7379e-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="7379e-219">Especificar hello toobe de archivos y carpetas incluido</span><span class="sxs-lookup"><span data-stu-id="7379e-219">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="7379e-220">Especificar hello toobe de archivos y carpetas excluido</span><span class="sxs-lookup"><span data-stu-id="7379e-220">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="7379e-221">Especifique recursiva copia de seguridad de datos en una carpeta (o) si deben respaldar solo Hola archivos de nivel superior en la carpeta especificada de hello hasta.</span><span class="sxs-lookup"><span data-stu-id="7379e-221">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="7379e-222">Hola este último se logra mediante la marca de - no recursivas de hello en el comando New-OBFileSpec Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-222">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="7379e-223">En el siguiente ejemplo de Hola, comenzaremos hacer una copia de volumen C: y D: y excluir los archivos binarios de sistema operativo de hello en la carpeta de Windows hello y las carpetas temporales.</span><span class="sxs-lookup"><span data-stu-id="7379e-223">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="7379e-224">toodo por lo que vamos a crear dos especificaciones de archivo mediante hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet: uno para la inclusión y uno para su exclusión.</span><span class="sxs-lookup"><span data-stu-id="7379e-224">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="7379e-225">Una vez que se han creado las especificaciones de archivo hello, está asociados con la directiva de hello mediante hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7379e-225">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="7379e-226">Aplicar una directiva de Hola</span><span class="sxs-lookup"><span data-stu-id="7379e-226">Applying hello policy</span></span>
<span data-ttu-id="7379e-227">Ahora el objeto de directiva de hello está finalizado y tiene una programación de copia de seguridad asociada, directiva de retención y una lista de inclusión/exclusión de archivos.</span><span class="sxs-lookup"><span data-stu-id="7379e-227">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="7379e-228">Ahora se puede confirmar para copia de seguridad de Azure toouse esta directiva.</span><span class="sxs-lookup"><span data-stu-id="7379e-228">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="7379e-229">Antes de aplicar Hola recién creado directiva asegurarse de que no hay ninguna directiva de copia de seguridad existente asociada con el servidor de hello mediante hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7379e-229">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="7379e-230">Quitar la directiva de hello le pedirá confirmación.</span><span class="sxs-lookup"><span data-stu-id="7379e-230">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="7379e-231">confirmación de hello tooskip usar hello ```-Confirm:$false``` marca con el cmdlet de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-231">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="7379e-232">Objeto de directiva de hello confirmación se realiza mediante hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7379e-232">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="7379e-233">Esto también requerirá confirmación.</span><span class="sxs-lookup"><span data-stu-id="7379e-233">This will also ask for confirmation.</span></span> <span data-ttu-id="7379e-234">confirmación de hello tooskip usar hello ```-Confirm:$false``` marca con el cmdlet de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-234">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
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

<span data-ttu-id="7379e-235">Puede ver los detalles de Hola de directiva de copia de seguridad existente de hello mediante hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7379e-235">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="7379e-236">Puede desplazarse mediante hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet para programar copia de seguridad de Hola y Hola [OBRetentionPolicy Get](https://technet.microsoft.com/library/hh770427) cmdlet para las directivas de retención de Hola</span><span class="sxs-lookup"><span data-stu-id="7379e-236">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="7379e-237">Realización de una copia de seguridad ad-hoc</span><span class="sxs-lookup"><span data-stu-id="7379e-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="7379e-238">Una vez que se ha establecido una directiva de copia de seguridad realizar copias de seguridad de hello según la programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-238">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="7379e-239">También es posible usar Hola desencadenar una copia de seguridad de ad-hoc [OBBackup inicio](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7379e-239">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="7379e-240">Restaurar datos de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="7379e-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="7379e-241">En esta sección le guiará a través de los pasos de Hola para automatizar la recuperación de datos de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="7379e-241">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="7379e-242">Hacerlo implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7379e-242">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="7379e-243">Seleccione el volumen de origen de Hola</span><span class="sxs-lookup"><span data-stu-id="7379e-243">Pick hello source volume</span></span>
2. <span data-ttu-id="7379e-244">Elija un toorestore de punto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="7379e-244">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="7379e-245">Elija un elemento toorestore</span><span class="sxs-lookup"><span data-stu-id="7379e-245">Choose an item toorestore</span></span>
4. <span data-ttu-id="7379e-246">Proceso de restauración de Hola de desencadenador</span><span class="sxs-lookup"><span data-stu-id="7379e-246">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="7379e-247">Seleccionar volumen de origen de Hola</span><span class="sxs-lookup"><span data-stu-id="7379e-247">Picking hello source volume</span></span>
<span data-ttu-id="7379e-248">En orden toorestore un elemento de la copia de seguridad de Azure, primero debe origen de hello tooidentify de elemento de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-248">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="7379e-249">Porque nos estamos ejecutando comandos de hello en contexto de Hola de un servidor de Windows o un cliente de Windows, ya se ha identificado máquina Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-249">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="7379e-250">Hola siguiente paso para identificar el origen de hello es volumen de hello tooidentify que lo contiene.</span><span class="sxs-lookup"><span data-stu-id="7379e-250">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="7379e-251">Una lista de volúmenes u orígenes haciendo copias de seguridad de este equipo se puede recuperar mediante la ejecución de hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7379e-251">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="7379e-252">Este comando devuelve una matriz de todos los orígenes de Hola de este cliente/servidor de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7379e-252">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-toorestore"></a><span data-ttu-id="7379e-253">Elegir un toorestore de punto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="7379e-253">Choosing a backup point toorestore</span></span>
<span data-ttu-id="7379e-254">Hello lista de puntos de copia de seguridad se puede recuperar mediante la ejecución de hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet con parámetros adecuados.</span><span class="sxs-lookup"><span data-stu-id="7379e-254">hello list of backup points can be retrieved by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="7379e-255">En nuestro ejemplo, elegiremos punto de copia de seguridad más reciente de hello para el volumen de origen de hello *D:* y usar toorecover un archivo específico.</span><span class="sxs-lookup"><span data-stu-id="7379e-255">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="7379e-256">objeto de Hello ```$rps``` es una matriz de puntos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7379e-256">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="7379e-257">Hola primer elemento es el último punto de Hola y elemento n-ésima de hello es punto más antiguo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-257">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="7379e-258">punto más reciente de toochoose hello, usaremos ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="7379e-258">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="7379e-259">Elegir un elemento toorestore</span><span class="sxs-lookup"><span data-stu-id="7379e-259">Choosing an item toorestore</span></span>
<span data-ttu-id="7379e-260">tooidentify Hola exacto del archivo o carpeta toorestore, recursivamente usar hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7379e-260">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="7379e-261">Se pueden examinar esa jerarquía de carpetas de manera Hola únicamente con hello ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="7379e-261">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="7379e-262">En este ejemplo, si queremos que el archivo de hello toorestore *finances.xls* podemos hacer referencia a que cuando se utiliza el objeto de hello ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="7379e-262">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="7379e-263">También puede buscar toorestore elementos mediante hello ```Get-OBRecoverableItem``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7379e-263">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="7379e-264">En nuestro ejemplo, toosearch para *finances.xls* se pudo obtener un identificador en el archivo hello, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="7379e-264">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="7379e-265">Proceso de restauración de desencadenamiento Hola</span><span class="sxs-lookup"><span data-stu-id="7379e-265">Triggering hello restore process</span></span>
<span data-ttu-id="7379e-266">proceso de restauración de hello tootrigger, primero necesitamos opciones de recuperación de toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-266">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="7379e-267">Esto puede hacerse mediante el uso de hello [OBRecoveryOption New](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7379e-267">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="7379e-268">En este ejemplo, supongamos que queremos archivos de hello toorestore demasiado*C:\temp*. Supongamos también que deseamos tooskip archivos que ya existen en la carpeta de destino de hello *C:\temp*. toocreate tal una opción de recuperación, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7379e-268">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="7379e-269">Ahora desencadenar restauración mediante hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) comando hello seleccionado ```$item``` de salida de hello de hello ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7379e-269">Now trigger restore by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="7379e-270">La desinstalación de agente de copia de seguridad de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="7379e-270">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="7379e-271">Desinstalar agente de copia de seguridad de Azure de hello puede hacerse mediante el uso de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7379e-271">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="7379e-272">Desinstalación de archivos binarios del agente de hello de la máquina de hello tiene algunos tooconsider consecuencias:</span><span class="sxs-lookup"><span data-stu-id="7379e-272">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="7379e-273">Quita el filtro de archivos Hola de máquina de Hola y se detiene el seguimiento de cambios.</span><span class="sxs-lookup"><span data-stu-id="7379e-273">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="7379e-274">Se quita toda la información de directiva de máquina de hello, pero información de la directiva de hello continúa toobe almacenado en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-274">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="7379e-275">Se eliminan todas las programaciones de copia de seguridad y no se realizan más copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7379e-275">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="7379e-276">Sin embargo, Hola datos almacenados en Azure permanece y se mantiene según la configuración de directiva de retención de Hola por parte del usuario.</span><span class="sxs-lookup"><span data-stu-id="7379e-276">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="7379e-277">Los puntos más antiguos vencen automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7379e-277">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="7379e-278">Administración remota</span><span class="sxs-lookup"><span data-stu-id="7379e-278">Remote management</span></span>
<span data-ttu-id="7379e-279">Toda la administración de hello alrededor de agente de copia de seguridad de Azure de hello, directivas y orígenes de datos puede realizarse de forma remota a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7379e-279">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="7379e-280">máquina de Hola que se administrará de forma remota debe toobe preparado correctamente.</span><span class="sxs-lookup"><span data-stu-id="7379e-280">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="7379e-281">De forma predeterminada, Hola servicio WinRM está configurado para iniciarse manualmente.</span><span class="sxs-lookup"><span data-stu-id="7379e-281">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="7379e-282">tipo de inicio de Hello debe establecerse demasiado*automática* y se debe iniciar el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-282">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="7379e-283">tooverify que Hola servicio WinRM se está ejecutando, debería Hola el valor de la propiedad Status de hello *ejecutando*.</span><span class="sxs-lookup"><span data-stu-id="7379e-283">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="7379e-284">PowerShell debe configurarse para la comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="7379e-284">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="7379e-285">máquina de Hello ahora pueden administrarse de forma remota: a partir de la instalación de Hola de agente de Hola.</span><span class="sxs-lookup"><span data-stu-id="7379e-285">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="7379e-286">Por ejemplo, hello siguiente secuencia de comandos copia máquina remota de hello agente toohello y lo instala.</span><span class="sxs-lookup"><span data-stu-id="7379e-286">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="7379e-287">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7379e-287">Next steps</span></span>
<span data-ttu-id="7379e-288">Para obtener más información sobre Azure Backup para Windows Server o cliente de Windows, consulte</span><span class="sxs-lookup"><span data-stu-id="7379e-288">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="7379e-289">Introducción tooAzure copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="7379e-289">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="7379e-290">Copia de seguridad de servidores Windows</span><span class="sxs-lookup"><span data-stu-id="7379e-290">Back up Windows Servers</span></span>](backup-configure-vault.md)
