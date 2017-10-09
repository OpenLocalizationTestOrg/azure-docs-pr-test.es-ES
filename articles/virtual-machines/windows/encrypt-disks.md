---
title: "aaaEncrypt discos en una máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "¿Cómo tooencrypt discos virtuales en una máquina virtual de Windows para mejorar la seguridad con Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="1f390-103">¿Cómo tooencrypt discos virtuales en una máquina virtual de Windows</span><span class="sxs-lookup"><span data-stu-id="1f390-103">How tooencrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="1f390-104">Para mejorar la seguridad y el cumplimiento de las máquinas virtuales, se pueden cifrar los discos virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="1f390-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="1f390-105">Los discos se cifran mediante claves criptográficas que están protegidas en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f390-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="1f390-106">Estas claves criptográficas se pueden controlar y se puede auditar su uso.</span><span class="sxs-lookup"><span data-stu-id="1f390-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="1f390-107">Este artículo detalles de cómo tooencrypt discos virtuales en una máquina virtual de Windows con PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="1f390-107">This article details how tooencrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="1f390-108">También puede [cifrar una VM de Linux con hello Azure CLI 2.0](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="1f390-108">You can also [encrypt a Linux VM using hello Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="1f390-109">Introducción al cifrado de discos</span><span class="sxs-lookup"><span data-stu-id="1f390-109">Overview of disk encryption</span></span>
<span data-ttu-id="1f390-110">Los discos virtuales en máquinas virtuales de Windows se cifran en reposo mediante BitLocker.</span><span class="sxs-lookup"><span data-stu-id="1f390-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="1f390-111">El cifrado de los discos virtuales en Azure no conlleva ningún cargo.</span><span class="sxs-lookup"><span data-stu-id="1f390-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="1f390-112">Las claves criptográficas se almacenan en el almacén de claves de Azure mediante la protección de software, o puede importar o generar las claves en módulos de seguridad de Hardware (HSM) de certificados tooFIPS estándares de 140-2 nivel 2.</span><span class="sxs-lookup"><span data-stu-id="1f390-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="1f390-113">Estas claves criptográficas son tooencrypt usado y descifrar los discos virtuales conectados tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1f390-113">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="1f390-114">Estas claves criptográficas se pueden controlar y se puede auditar su uso.</span><span class="sxs-lookup"><span data-stu-id="1f390-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="1f390-115">Como las máquinas virtuales se encienden y se apagan, una entidad de servicio de Azure Active Directory proporciona un mecanismos seguro para la emisión de estas claves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="1f390-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="1f390-116">proceso de Hola para cifrar una máquina virtual es como sigue:</span><span class="sxs-lookup"><span data-stu-id="1f390-116">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="1f390-117">Cree una clave criptográfica en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f390-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="1f390-118">Configurar el número de toobe criptográficos clave de hello utilizable para el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="1f390-118">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="1f390-119">clave criptográfica de hello tooread de hello almacén de claves de Azure, cree un servicio de Azure Active Directory principal con los permisos adecuados de Hola.</span><span class="sxs-lookup"><span data-stu-id="1f390-119">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="1f390-120">Emitir Hola comando tooencrypt los discos virtuales, especificación de entidad de servicio de Azure Active Directory de Hola y adecuado toobe clave criptográfica utilizado.</span><span class="sxs-lookup"><span data-stu-id="1f390-120">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="1f390-121">solicitudes de entidad de seguridad de servicio de Azure Active Directory de Hola Hola requiere la clave criptográfica de almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="1f390-121">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="1f390-122">discos virtuales de Hola se cifran mediante la clave criptográfica de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="1f390-122">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="1f390-123">Proceso de cifrado</span><span class="sxs-lookup"><span data-stu-id="1f390-123">Encryption process</span></span>
<span data-ttu-id="1f390-124">Cifrado del disco se basa en hello adicionales de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="1f390-124">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="1f390-125">**Almacén de claves de Azure** -utilizar claves criptográficas toosafeguard y secretos usados para el proceso de cifrado y descifrado de hello del disco.</span><span class="sxs-lookup"><span data-stu-id="1f390-125">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="1f390-126">Si ya existe un almacén de Azure Key Vault, puede utilizarlo.</span><span class="sxs-lookup"><span data-stu-id="1f390-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="1f390-127">No es necesario toodedicate los discos de tooencrypting de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="1f390-127">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="1f390-128">límites administrativos tooseparate y visibilidad de clave, puede crear un almacén de claves dedicado.</span><span class="sxs-lookup"><span data-stu-id="1f390-128">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="1f390-129">**Azure Active Directory** : Hola de identificadores de intercambio seguro de claves cifradas necesarias y autenticación para solicitado acciones.</span><span class="sxs-lookup"><span data-stu-id="1f390-129">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="1f390-130">Normalmente, puede usar un almacén existente de Azure Active Directory para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f390-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="1f390-131">entidad de servicio de Hello proporciona un mecanismo de seguridad toorequest y emitir claves criptográficas de hello adecuado.</span><span class="sxs-lookup"><span data-stu-id="1f390-131">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="1f390-132">No está desarrollando una aplicación real que se integrará con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1f390-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="1f390-133">Requisitos y limitaciones</span><span class="sxs-lookup"><span data-stu-id="1f390-133">Requirements and limitations</span></span>
<span data-ttu-id="1f390-134">Requisitos y escenarios admitidos para el cifrado de discos:</span><span class="sxs-lookup"><span data-stu-id="1f390-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="1f390-135">Habilitación del cifrado en nuevas máquinas virtuales de Windows desde imágenes de Azure Marketplace o una imagen de disco duro virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="1f390-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="1f390-136">Habilitación del cifrado en máquinas virtuales de Windows existentes en Azure.</span><span class="sxs-lookup"><span data-stu-id="1f390-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="1f390-137">Habilitación del cifrado en máquinas virtuales de Windows configuradas mediante Espacios de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1f390-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="1f390-138">Deshabilitación del cifrado en las unidades de datos y del sistema operativo en máquinas virtuales de Windows.</span><span class="sxs-lookup"><span data-stu-id="1f390-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="1f390-139">Todos los recursos (por ejemplo, el almacén de claves, la cuenta de almacenamiento y VM) deben estar en hello misma región de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="1f390-139">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="1f390-140">Nivel estándar de máquinas virtuales, como las máquinas virtuales de la serie A, D, DS, G y GS.</span><span class="sxs-lookup"><span data-stu-id="1f390-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="1f390-141">Cifrado del disco no se admite actualmente en hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="1f390-141">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="1f390-142">Máquina s virtuales de nivel básico</span><span class="sxs-lookup"><span data-stu-id="1f390-142">Basic tier VMs.</span></span>
* <span data-ttu-id="1f390-143">Máquinas virtuales creadas mediante el modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="1f390-143">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="1f390-144">Actualizar las claves criptográficas de hello en una máquina virtual ya se ha cifrado.</span><span class="sxs-lookup"><span data-stu-id="1f390-144">Updating hello cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="1f390-145">Integración con el Servicio de administración de claves local.</span><span class="sxs-lookup"><span data-stu-id="1f390-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="1f390-146">Creación de Azure Key Vault y claves</span><span class="sxs-lookup"><span data-stu-id="1f390-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="1f390-147">Antes de empezar, asegúrese de que esa versión más reciente de Hola de Hola se ha instalado el módulo de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="1f390-147">Before you start, make sure that hello latest version of hello Azure PowerShell module has been installed.</span></span> <span data-ttu-id="1f390-148">Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1f390-148">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="1f390-149">A lo largo de los ejemplos de comandos de hello, reemplace todos los parámetros de ejemplo con sus propios nombres, la ubicación y los valores de clave.</span><span class="sxs-lookup"><span data-stu-id="1f390-149">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="1f390-150">Hello en los ejemplos siguientes utilizan una convención de *myResourceGroup*, *myKeyVault*, *myVM*, etcetera.</span><span class="sxs-lookup"><span data-stu-id="1f390-150">hello following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="1f390-151">primer paso de Hello es un almacén de claves de Azure toostore toocreate las claves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="1f390-151">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="1f390-152">Almacén de claves de Azure puede almacenar secretos, claves o contraseñas que permiten toosecurely implementan en sus aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="1f390-152">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="1f390-153">Para el cifrado de disco virtual, crear un almacén de claves toostore una clave criptográfica que es usado tooencrypt o descifrar los discos virtuales.</span><span class="sxs-lookup"><span data-stu-id="1f390-153">For virtual disk encryption, you create a Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="1f390-154">Habilitar el proveedor de almacén de claves de Azure de hello dentro de su suscripción de Azure con [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), a continuación, cree un grupo de recursos con [AzureRmResourceGroup nuevo](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="1f390-154">Enable hello Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="1f390-155">Hello en el ejemplo siguiente se crea un nombre de grupo de recursos *myResourceGroup* en hello *UU* ubicación:</span><span class="sxs-lookup"><span data-stu-id="1f390-155">hello following example creates a resource group name *myResourceGroup* in hello *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="1f390-156">Hola almacén de claves de Azure que lo contiene hello las claves criptográfico y proceso asociado recursos como almacenamiento y Hola propia máquina virtual deben residir en Hola misma región.</span><span class="sxs-lookup"><span data-stu-id="1f390-156">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="1f390-157">Crear un almacén de claves de Azure con [AzureRmKeyVault New](/powershell/module/azurerm.keyvault/new-azurermkeyvault) y habilitar Hola el almacén de claves para su uso con el cifrado del disco.</span><span class="sxs-lookup"><span data-stu-id="1f390-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="1f390-158">Especifique un nombre de Key Vault único para *keyVaultName* de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="1f390-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="1f390-159">Puede almacenar las claves criptográficas mediante software o protección del modelo de seguridad de hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="1f390-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="1f390-160">Para usar HSM se necesita un almacén premium de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f390-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="1f390-161">Hay un costo adicional toocreating una prima el almacén de claves en lugar de almacén de claves estándar que almacena las claves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="1f390-161">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="1f390-162">toocreate un almacén de claves, premium Hola anterior paso Agregar hello *- Sku "Premium"* parámetros.</span><span class="sxs-lookup"><span data-stu-id="1f390-162">toocreate a premium Key Vault, in hello preceding step add hello *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="1f390-163">Hello en el ejemplo siguiente se usa claves protegidas por software ya que hemos creado un almacén de claves estándar.</span><span class="sxs-lookup"><span data-stu-id="1f390-163">hello following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="1f390-164">Para los dos modelos de protección, Hola plataforma Windows Azure debe toobe concede acceso toorequest hello las claves criptográficas cuando Hola VM arranca discos virtuales de toodecrypt Hola.</span><span class="sxs-lookup"><span data-stu-id="1f390-164">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="1f390-165">Cree una clave criptográfica en la instancia de Key Vault con [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="1f390-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="1f390-166">Hello en el ejemplo siguiente se crea una clave denominada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="1f390-166">hello following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="1f390-167">Crear Hola entidad de servicio de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f390-167">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="1f390-168">Cuando los discos virtuales se cifrada o descifrados, especifique una autenticación de cuentas de hello toohandle e intercambio de claves criptográficas del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="1f390-168">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="1f390-169">Esta cuenta, una entidad de seguridad de servicio de Active Directory de Azure, permite toorequest de la plataforma Windows Azure de Hola Hola adecuada las claves criptográficas en nombre de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="1f390-169">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="1f390-170">Su suscripción dispone de una instancia de Azure Active Directory predeterminada, aunque muchas organizaciones tienen directorios de Azure Active Directory dedicados.</span><span class="sxs-lookup"><span data-stu-id="1f390-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="1f390-171">Cree una entidad de seguridad de servicio en Azure Active Directory con [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="1f390-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="1f390-172">toospecify una contraseña segura, siga hello [restricciones y directivas de contraseña en Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="1f390-172">toospecify a secure password, follow hello [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="1f390-173">toosuccessfully cifrar o descifrar los discos virtuales, permisos de clave cifrado de hello almacenados en el almacén de claves deben ser conjunto toopermit hello Azure Active Directory service principal tooread Hola claves.</span><span class="sxs-lookup"><span data-stu-id="1f390-173">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="1f390-174">Establezca los permisos en Key Vault con [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="1f390-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="1f390-175">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="1f390-175">Create virtual machine</span></span>
<span data-ttu-id="1f390-176">tootest Hola proceso de cifrado, vamos a crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1f390-176">tootest hello encryption process, let's create a VM.</span></span> <span data-ttu-id="1f390-177">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* con un *Windows Server 2016 Datacenter* imagen:</span><span class="sxs-lookup"><span data-stu-id="1f390-177">hello following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="1f390-178">Cifrado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="1f390-178">Encrypt virtual machine</span></span>
<span data-ttu-id="1f390-179">discos virtuales de tooencrypt hello, reúne todos los componentes anteriores de hello:</span><span class="sxs-lookup"><span data-stu-id="1f390-179">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="1f390-180">Especificar Hola entidad de servicio de Azure Active Directory y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="1f390-180">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="1f390-181">Especificar Hola el almacén de claves toostore Hola metadatos para los discos cifrados.</span><span class="sxs-lookup"><span data-stu-id="1f390-181">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="1f390-182">Especifique hello toouse de claves criptográficas para hello real cifrado y descifrado.</span><span class="sxs-lookup"><span data-stu-id="1f390-182">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="1f390-183">Especifique si desea que tooencrypt disco de SO hello, discos de datos de Hola o todos.</span><span class="sxs-lookup"><span data-stu-id="1f390-183">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="1f390-184">Cifrar la máquina virtual con [AzureRmVMDiskEncryptionExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) con clave de almacén de claves de Azure de Hola y las credenciales principales de servicio de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1f390-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using hello Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="1f390-185">Hello en el ejemplo siguiente se recupera toda la información clave hello, a continuación, cifra Hola máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="1f390-185">hello following example retrieves all hello key information then encrypts hello VM named *myVM*:</span></span>

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

<span data-ttu-id="1f390-186">Aceptar hello toocontinue símbolo del sistema con el cifrado de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1f390-186">Accept hello prompt toocontinue with hello VM encryption.</span></span> <span data-ttu-id="1f390-187">Hola VM se reinicia durante el proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="1f390-187">hello VM restarts during hello process.</span></span> <span data-ttu-id="1f390-188">Una vez que se complete el proceso de cifrado de Hola y Hola máquina virtual se reinicie, revisar el estado de cifrado de hello con [AzureRmVmDiskEncryptionStatus Get](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="1f390-188">Once hello encryption process completes and hello VM has rebooted, review hello encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="1f390-189">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1f390-189">hello output is similar toohello following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="1f390-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1f390-190">Next steps</span></span>
* <span data-ttu-id="1f390-191">Para más información sobre cómo administrar Azure Key Vault, vea [Configuración de Key Vault para máquinas virtuales en Azure Resource Manager](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="1f390-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="1f390-192">Para obtener más información acerca del cifrado de disco, como preparar una tooAzure tooupload personalizado cifrado de VM, consulte [cifrado del disco de Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="1f390-192">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
