---
title: "Cifrado de discos en una máquina virtual de Windows en Azure | Microsoft Docs"
description: "Cómo cifrar discos virtuales en una máquina virtual de Windows para mejorar la seguridad Azure PowerShell"
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
ms.openlocfilehash: 98b42b252a601af090579e3939f3c7ab91c3803b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="3dd8e-103">Cómo cifrar discos virtuales en una máquina virtual de Windows</span><span class="sxs-lookup"><span data-stu-id="3dd8e-103">How to encrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="3dd8e-104">Para mejorar la seguridad y el cumplimiento de las máquinas virtuales, se pueden cifrar los discos virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="3dd8e-105">Los discos se cifran mediante claves criptográficas que están protegidas en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="3dd8e-106">Estas claves criptográficas se pueden controlar y se puede auditar su uso.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="3dd8e-107">En este artículo se detalla cómo cifrar los discos virtuales en una máquina virtual de Windows con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-107">This article details how to encrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="3dd8e-108">También se puede [cifrar una máquina virtual de Linux mediante la CLI 2.0 de Azure](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="3dd8e-108">You can also [encrypt a Linux VM using the Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="3dd8e-109">Introducción al cifrado de discos</span><span class="sxs-lookup"><span data-stu-id="3dd8e-109">Overview of disk encryption</span></span>
<span data-ttu-id="3dd8e-110">Los discos virtuales en máquinas virtuales de Windows se cifran en reposo mediante BitLocker.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="3dd8e-111">El cifrado de los discos virtuales en Azure no conlleva ningún cargo.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="3dd8e-112">Las claves criptográficas se almacenan en Azure Key Vault con protección de software, o puede importar o generar las claves en módulos de seguridad de hardware (HSM) certificados conforme a las normas FIPS 140-2 de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="3dd8e-113">Las claves criptográficas se usan para cifrar y descifrar los discos virtuales conectados a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-113">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="3dd8e-114">Estas claves criptográficas se pueden controlar y se puede auditar su uso.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="3dd8e-115">Como las máquinas virtuales se encienden y se apagan, una entidad de servicio de Azure Active Directory proporciona un mecanismos seguro para la emisión de estas claves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="3dd8e-116">El proceso para cifrar una máquina virtual es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="3dd8e-116">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="3dd8e-117">Cree una clave criptográfica en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="3dd8e-118">Configure la clave criptográfica para poder utilizarla para el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-118">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="3dd8e-119">Para leer la clave criptográfica de Azure Key Vault, cree una entidad de servicio de Azure Active Directory con los permisos adecuados.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-119">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="3dd8e-120">Emita el comando para cifrar los discos virtuales y especifique la entidad de servicio de Azure Active Directory y la clave criptográfica adecuada que se deberá usar.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-120">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="3dd8e-121">La entidad de servicio de Azure Active Directory solicita la clave criptográfica necesaria a Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-121">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="3dd8e-122">Los discos virtuales se cifran con la clave criptográfica proporcionada.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-122">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="3dd8e-123">Proceso de cifrado</span><span class="sxs-lookup"><span data-stu-id="3dd8e-123">Encryption process</span></span>
<span data-ttu-id="3dd8e-124">El cifrado de discos utiliza los siguientes componentes adicionales:</span><span class="sxs-lookup"><span data-stu-id="3dd8e-124">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="3dd8e-125">**Azure Key Vault**: se usa para proteger las claves criptográficas y los secretos usados para el proceso de cifrado y descifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-125">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="3dd8e-126">Si ya existe un almacén de Azure Key Vault, puede utilizarlo.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="3dd8e-127">No es necesario dedicar un almacén de Key Vault para el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-127">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="3dd8e-128">Para separar los límites administrativos y la visibilidad de las claves, puede crear un almacén de Key Vault dedicado.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-128">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="3dd8e-129">**Azure Active Directory**: controla el intercambio seguro de las claves cifradas necesarias y la autenticación para las acciones solicitadas.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-129">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="3dd8e-130">Normalmente, puede usar un almacén existente de Azure Active Directory para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="3dd8e-131">La entidad de servicio proporciona un mecanismo seguro para solicitar y recibir las claves criptográficas correspondientes.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-131">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="3dd8e-132">No está desarrollando una aplicación real que se integrará con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="3dd8e-133">Requisitos y limitaciones</span><span class="sxs-lookup"><span data-stu-id="3dd8e-133">Requirements and limitations</span></span>
<span data-ttu-id="3dd8e-134">Requisitos y escenarios admitidos para el cifrado de discos:</span><span class="sxs-lookup"><span data-stu-id="3dd8e-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="3dd8e-135">Habilitación del cifrado en nuevas máquinas virtuales de Windows desde imágenes de Azure Marketplace o una imagen de disco duro virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="3dd8e-136">Habilitación del cifrado en máquinas virtuales de Windows existentes en Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="3dd8e-137">Habilitación del cifrado en máquinas virtuales de Windows configuradas mediante Espacios de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="3dd8e-138">Deshabilitación del cifrado en las unidades de datos y del sistema operativo en máquinas virtuales de Windows.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="3dd8e-139">Todos los recursos (por ejemplo: almacén de Key Vault, cuenta de almacenamiento, máquina virtual, etc.) deben pertenecer a la misma región y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-139">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="3dd8e-140">Nivel estándar de máquinas virtuales, como las máquinas virtuales de la serie A, D, DS, G y GS.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="3dd8e-141">El cifrado del disco no se admite actualmente en los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="3dd8e-141">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="3dd8e-142">Máquina s virtuales de nivel básico</span><span class="sxs-lookup"><span data-stu-id="3dd8e-142">Basic tier VMs.</span></span>
* <span data-ttu-id="3dd8e-143">Máquinas virtuales creadas con el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-143">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="3dd8e-144">Actualización de las claves criptográficas en una máquina virtual ya cifrada.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-144">Updating the cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="3dd8e-145">Integración con el Servicio de administración de claves local.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="3dd8e-146">Creación de Azure Key Vault y claves</span><span class="sxs-lookup"><span data-stu-id="3dd8e-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="3dd8e-147">Antes de empezar, asegúrese de tener instalada la versión más reciente del módulo de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-147">Before you start, make sure that the latest version of the Azure PowerShell module has been installed.</span></span> <span data-ttu-id="3dd8e-148">Para más información, vea [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3dd8e-148">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="3dd8e-149">En todos los ejemplos de comandos, reemplace todos los parámetros de ejemplo por sus propios nombres, ubicaciones y valores de clave.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-149">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="3dd8e-150">Los siguientes ejemplos usan una convención de *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-150">The following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="3dd8e-151">El primer paso es crear un almacén de Azure Key Vault para almacenar las claves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-151">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="3dd8e-152">Azure Key Vault puede almacenar claves, secretos o contraseñas que permiten su implementación segura en las aplicaciones y los servicios.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-152">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="3dd8e-153">Para el cifrado de discos virtuales, se crea un Key Vault para almacenar una clave criptográfica que se usa para cifrar o descifrar los discos virtuales.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-153">For virtual disk encryption, you create a Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="3dd8e-154">Habilite el proveedor Azure Key Vault dentro de la suscripción de Azure con [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider) y, a continuación, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="3dd8e-154">Enable the Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="3dd8e-155">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación del *este de EE. UU.*:</span><span class="sxs-lookup"><span data-stu-id="3dd8e-155">The following example creates a resource group name *myResourceGroup* in the *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="3dd8e-156">El almacén de Azure Key Vault que contiene las claves criptográficas y los recursos de proceso asociados, como el almacenamiento y la propia máquina virtual, debe residir en la misma región.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-156">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="3dd8e-157">Cree una instancia de Azure Key Vault con [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) y habilite Key Vault para usarlo con el cifrado de discos.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="3dd8e-158">Especifique un nombre de Key Vault único para *keyVaultName* de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="3dd8e-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="3dd8e-159">Puede almacenar las claves criptográficas mediante software o protección del modelo de seguridad de hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="3dd8e-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="3dd8e-160">Para usar HSM se necesita un almacén premium de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="3dd8e-161">La creación de un almacén premium de Key Vault conlleva un coste, frente al almacén estándar de Key Vault, que almacena las claves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-161">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="3dd8e-162">Para crear un Key Vault premium, en el paso anterior agregue los parámetros *-Sku "Premium"*.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-162">To create a premium Key Vault, in the preceding step add the *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="3dd8e-163">En el ejemplo siguiente se usa claves protegidas por software ya que hemos creado un almacén de Key Vault estándar.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-163">The following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="3dd8e-164">En ambos modelos de protección, la plataforma Windows Azure debe tener acceso para solicitar las claves criptográficas cuando la máquina virtual arranca para descifrar los discos virtuales.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-164">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="3dd8e-165">Cree una clave criptográfica en la instancia de Key Vault con [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="3dd8e-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="3dd8e-166">En el ejemplo siguiente se crea una clave llamada *myKey*:</span><span class="sxs-lookup"><span data-stu-id="3dd8e-166">The following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="3dd8e-167">Creación de la entidad de servicio de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dd8e-167">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="3dd8e-168">Cuando los discos virtuales se cifran o descifran, se especifica una cuenta para controlar la autenticación y el intercambio de claves criptográficas desde Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-168">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="3dd8e-169">Esta cuenta, una entidad de servicio de Azure Active Directory, permite que la plataforma de Azure solicite las claves criptográficas correspondientes en nombre de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-169">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="3dd8e-170">Su suscripción dispone de una instancia de Azure Active Directory predeterminada, aunque muchas organizaciones tienen directorios de Azure Active Directory dedicados.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="3dd8e-171">Cree una entidad de seguridad de servicio en Azure Active Directory con [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="3dd8e-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="3dd8e-172">Para especificar una contraseña segura, siga las [Restricciones y directivas de contraseñas en Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="3dd8e-172">To specify a secure password, follow the [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="3dd8e-173">Para cifrar o descifrar los discos virtuales correctamente, debe establecer los permisos de la clave criptográfica que se almacena en Key Vault para que permitan que la entidad de servicio de Azure Active Directory lea las claves.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-173">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="3dd8e-174">Establezca los permisos en Key Vault con [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="3dd8e-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="3dd8e-175">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="3dd8e-175">Create virtual machine</span></span>
<span data-ttu-id="3dd8e-176">Para probar el proceso de cifrado, se va a crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-176">To test the encryption process, let's create a VM.</span></span> <span data-ttu-id="3dd8e-177">En el ejemplo siguiente se crea una máquina virtual llamada *myVM* mediante una imagen de *Windows Server 2016 Datacenter*:</span><span class="sxs-lookup"><span data-stu-id="3dd8e-177">The following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

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


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="3dd8e-178">Cifrado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3dd8e-178">Encrypt virtual machine</span></span>
<span data-ttu-id="3dd8e-179">Para cifrar los discos virtuales, reúna todos los componentes anteriores:</span><span class="sxs-lookup"><span data-stu-id="3dd8e-179">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="3dd8e-180">Especifique la entidad de servicio de Azure Active Directory y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-180">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="3dd8e-181">Especifique el almacén de Key Vault donde se almacenarán los metadatos de los discos cifrados.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-181">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="3dd8e-182">Especifique las claves criptográficas que se utilizarán para el cifrado y descifrado.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-182">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="3dd8e-183">Especifique si desea cifrar el disco del sistema operativo, los discos de datos o todos.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-183">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="3dd8e-184">Cifre la VM con [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) mediante la clave de Azure Key Vault y las credenciales de entidad de seguridad de servicio de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using the Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="3dd8e-185">En el ejemplo siguiente se recupera toda la información de clave y después se cifra la máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3dd8e-185">The following example retrieves all the key information then encrypts the VM named *myVM*:</span></span>

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

<span data-ttu-id="3dd8e-186">Acepte el mensaje para continuar con el cifrado de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-186">Accept the prompt to continue with the VM encryption.</span></span> <span data-ttu-id="3dd8e-187">La VM se reinicia durante el proceso.</span><span class="sxs-lookup"><span data-stu-id="3dd8e-187">The VM restarts during the process.</span></span> <span data-ttu-id="3dd8e-188">Una vez que finalice el proceso de cifrado y se reinicie la máquina virtual, revise el estado del cifrado con [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="3dd8e-188">Once the encryption process completes and the VM has rebooted, review the encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="3dd8e-189">La salida es similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3dd8e-189">The output is similar to the following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="3dd8e-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3dd8e-190">Next steps</span></span>
* <span data-ttu-id="3dd8e-191">Para más información sobre cómo administrar Azure Key Vault, vea [Configuración de Key Vault para máquinas virtuales en Azure Resource Manager](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="3dd8e-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="3dd8e-192">Para obtener más información acerca del cifrado de discos, por ejemplo, cómo preparar una máquina virtual personalizada cifrada para cargar en Azure, consulte [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="3dd8e-192">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
