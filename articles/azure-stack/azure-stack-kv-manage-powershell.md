---
title: Administrar Key Vault en Azure Stack mediante PowerShell | Microsoft Docs
description: "Aprenda cómo administrar Key Vault en Azure Stack mediante PowerShell."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 71320f8c55d014db6843e6247c53cc07832efc32
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a><span data-ttu-id="7239c-103">Administrar Key Vault en Azure Stack mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="7239c-103">Manage Key Vault in Azure Stack using PowerShell</span></span>

<span data-ttu-id="7239c-104">En este artículo, encontrará ayuda para empezar a crear y administrar Key Vault en Azure Stack mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7239c-104">This article helps you get started to create and manage Key Vault in Azure Stack by using PowerShell.</span></span> <span data-ttu-id="7239c-105">Los cmdlets de PowerShell de Key Vault que se describen en este artículo están disponibles como parte del SDK de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7239c-105">The Key Vault PowerShell cmdlets described in this article are available as a part of the Azure PowerShell SDK.</span></span> <span data-ttu-id="7239c-106">En las secciones siguientes se describen los cmdlets de PowerShell necesarios para crear un almacén; almacenar y administrar claves y secretos criptográficos, y autorizar a los usuarios o aplicaciones a invocar operaciones en el almacén.</span><span class="sxs-lookup"><span data-stu-id="7239c-106">The following sections describe the PowerShell cmdlets that are required to create a vault, store, and manage cryptographic keys and secrets as well as authorize users or applications to invoke operations in the vault.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7239c-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7239c-107">Prerequisites</span></span>
* [<span data-ttu-id="7239c-108">Instalación de PowerShell para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7239c-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* <span data-ttu-id="7239c-109">Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7239c-109">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span></span>  
* <span data-ttu-id="7239c-110">Los usuarios tienen que [suscribirse a una oferta](azure-stack-subscribe-plan-provision-vm.md) que incluya el servicio Key Vault.</span><span class="sxs-lookup"><span data-stu-id="7239c-110">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span> 
* [<span data-ttu-id="7239c-111">Configuración del entorno de PowerShell del usuario de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7239c-111">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a><span data-ttu-id="7239c-112">Habilitación de la suscripción de inquilino para operaciones de almacén</span><span class="sxs-lookup"><span data-stu-id="7239c-112">Enable your tenant subscription for vault operations</span></span>

<span data-ttu-id="7239c-113">Para poder emitir cualquier operación en un almacén de claves, debe asegurarse de que su suscripción de inquilino esté habilitada para operaciones de almacén.</span><span class="sxs-lookup"><span data-stu-id="7239c-113">Before you can issue any operations against a key vault, you need to ensure that your tenant subscription is enabled for vault operations.</span></span> <span data-ttu-id="7239c-114">Para comprobarlo, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7239c-114">To verify, run the following command:</span></span>

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
<span data-ttu-id="7239c-115">**Salida**</span><span class="sxs-lookup"><span data-stu-id="7239c-115">**Output**</span></span>

<span data-ttu-id="7239c-116">Si la suscripción está habilitada para operaciones de almacén, la salida muestra el valor "Registrado" para "RegistrationState" para todos los tipos de recursos de un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7239c-116">If your subscription is enabled for vault operations, the output shows “RegistrationState” equals “Registered” for all resource types of a key vault.</span></span>

![estado de registro](media/azure-stack-kv-manage-powershell/image1.png)

<span data-ttu-id="7239c-118">Si no es así, invoque el comando siguiente para registrar el servicio Key Vault en su suscripción:</span><span class="sxs-lookup"><span data-stu-id="7239c-118">If that’s not the case, invoke the following command to register the Key Vault service in your subscription:</span></span>

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

<span data-ttu-id="7239c-119">**Salida**</span><span class="sxs-lookup"><span data-stu-id="7239c-119">**Output**</span></span>

<span data-ttu-id="7239c-120">Si el registro se realiza correctamente, se devuelve la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="7239c-120">If the registration is successful, the following output is returned:</span></span>

![registro](media/azure-stack-kv-manage-powershell/image2.png)

<span data-ttu-id="7239c-122">En las secciones siguientes se da por sentado que el servicio Key Vault está registrado en la suscripción del usuario.</span><span class="sxs-lookup"><span data-stu-id="7239c-122">The following sections assume Key Vault service is registered within the user subscription.</span></span> <span data-ttu-id="7239c-123">Al invocar comandos del almacén de claves, si aparece el error "La suscripción no está registrada para usar el espacio de nombres 'Microsoft.KeyVault'", confirme que tiene [habilitado el proveedor de recursos de Key Vault](#enable-your-tenant-subscription-for-vault-operations) según las instrucciones indicadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7239c-123">When invoking key vault commands, if you get an error- "The subscription is not registered to use namespace ‘Microsoft.KeyVault" then, confirm that you have [enabled the Key Vault resource provider](#enable-your-tenant-subscription-for-vault-operations) as per instructions mentioned earlier.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="7239c-124">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="7239c-124">Create a key vault</span></span> 

<span data-ttu-id="7239c-125">Antes de crear un almacén de claves, cree un grupo de recursos para que todos los recursos relacionados con el almacén de claves se encuentren en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7239c-125">Before you create a key vault, create a resource group so that all key vault related resources exist in a resource group.</span></span> <span data-ttu-id="7239c-126">Utilice el comando siguiente para crear un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="7239c-126">Use the following command to create a new resource group:</span></span>

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

<span data-ttu-id="7239c-127">**Salida**</span><span class="sxs-lookup"><span data-stu-id="7239c-127">**Output**</span></span>

![nuevo grupo de recursos](media/azure-stack-kv-manage-powershell/image3.png)

<span data-ttu-id="7239c-129">Ahora, utilice el comando **New-AzureRMKeyVault** para crear un almacén de claves en el grupo de recursos que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7239c-129">Now, use the **New-AzureRMKeyVault** command to create a key vault in the resource group that you created earlier.</span></span> <span data-ttu-id="7239c-130">Este comando lee tres parámetros obligatorios: el nombre del grupo de recursos, el nombre del almacén de claves y la ubicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="7239c-130">This command reads three mandatory parameters- resource group name, key vault name, and geographic location.</span></span> 

<span data-ttu-id="7239c-131">Ejecute el siguiente comando para crear un almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="7239c-131">Run the following command to create a key vault:</span></span>

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
<span data-ttu-id="7239c-132">**Salida**</span><span class="sxs-lookup"><span data-stu-id="7239c-132">**Output**</span></span>

![new kv](media/azure-stack-kv-manage-powershell/image4.png)

<span data-ttu-id="7239c-134">La salida de este comando muestra las propiedades del almacén de claves que ha creado.</span><span class="sxs-lookup"><span data-stu-id="7239c-134">The output of this command shows the properties of the key vault that you created.</span></span> <span data-ttu-id="7239c-135">Cuando una aplicación accede a este almacén, utiliza la propiedad **Vault URI** (URI de almacén) que se muestra en la salida.</span><span class="sxs-lookup"><span data-stu-id="7239c-135">When an application accesses this vault, it uses the **Vault URI** property shown in the output.</span></span> <span data-ttu-id="7239c-136">Por ejemplo, aquí el URI de almacén es **https://vault01.vault.local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="7239c-136">For example, the vault URI here is **https://vault01.vault.local.azurestack.external**.</span></span> <span data-ttu-id="7239c-137">Las aplicaciones que interactúan con este almacén de claves a través de la API de REST deben usar este URI.</span><span class="sxs-lookup"><span data-stu-id="7239c-137">Applications interacting with this key vault through REST API must use this URI.</span></span>

<span data-ttu-id="7239c-138">En implementaciones basadas en ADFS, al crear un almacén de claves mediante PowerShell, puede aparecer la advertencia "Access policy is not set.</span><span class="sxs-lookup"><span data-stu-id="7239c-138">In ADFS-based deployments, when you create a key vault by using PowerShell, you might receive a warning that says "Access policy is not set.</span></span> <span data-ttu-id="7239c-139">No user or application has access permission to use this vault" (La directiva de acceso no está definida. Ningún usuario ni ninguna aplicación tienen permiso de acceso para utilizar este almacén).</span><span class="sxs-lookup"><span data-stu-id="7239c-139">No user or application has access permission to use this vault".</span></span> <span data-ttu-id="7239c-140">Para resolver este problema, establezca una directiva de acceso para el almacén mediante el comando [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret):</span><span class="sxs-lookup"><span data-stu-id="7239c-140">To resolve this issue, set an access policy for the vault by using the [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) command:</span></span>

```PowerShell
# Obtain the security identifier(SID) of the active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set the key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="7239c-141">Administración de claves y secretos</span><span class="sxs-lookup"><span data-stu-id="7239c-141">Manage keys and secrets</span></span>

<span data-ttu-id="7239c-142">Después de crear un almacén, siga estos pasos para crear y administrar claves y secretos en el almacén.</span><span class="sxs-lookup"><span data-stu-id="7239c-142">After creating a vault, use the following steps to create and manage keys and secrets within the vault.</span></span>

### <a name="create-a-key"></a><span data-ttu-id="7239c-143">Crear una clave</span><span class="sxs-lookup"><span data-stu-id="7239c-143">Create a key</span></span>

<span data-ttu-id="7239c-144">Use el comando **Add-AzureKeyVaultKey** para crear o importar una clave protegida mediante software en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7239c-144">Use the **Add-AzureKeyVaultKey** command to create or import a software protected key in a key vault.</span></span> 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
<span data-ttu-id="7239c-145">El parámetro **Destination** (Destino) se utiliza para especificar que la clave está protegida mediante software.</span><span class="sxs-lookup"><span data-stu-id="7239c-145">The **Destination** parameter is used to specify that the key is software protected.</span></span> <span data-ttu-id="7239c-146">Cuando la clave se crea correctamente, el comando da como salida los detalles de la clave creada.</span><span class="sxs-lookup"><span data-stu-id="7239c-146">When the key is successfully created, the command outputs the details of the created key.</span></span>

<span data-ttu-id="7239c-147">**Salida**</span><span class="sxs-lookup"><span data-stu-id="7239c-147">**Output**</span></span>

![Nueva clave](media/azure-stack-kv-manage-powershell/image5.png)

<span data-ttu-id="7239c-149">Ahora puede hacer referencia a la clave creada utilizando su URI.</span><span class="sxs-lookup"><span data-stu-id="7239c-149">You can now reference the created key by using its URI.</span></span> <span data-ttu-id="7239c-150">Si crea o importa una clave con el mismo nombre que una clave existente, la clave original se actualiza con los valores que se especifican en la nueva clave.</span><span class="sxs-lookup"><span data-stu-id="7239c-150">If you create or import a key that has same name as an existing key, the original key is updated with the values that are specified in the new key.</span></span>  <span data-ttu-id="7239c-151">Puede acceder a la versión anterior utilizando el URI específico de la versión de la clave.</span><span class="sxs-lookup"><span data-stu-id="7239c-151">You can access the previous version by using the version-specific URI of the key.</span></span> <span data-ttu-id="7239c-152">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="7239c-152">For example,</span></span> 

* <span data-ttu-id="7239c-153">Use **https://vault10.vault.local.azurestack.external:443/keys/key01** para obtener siempre la versión actual.</span><span class="sxs-lookup"><span data-stu-id="7239c-153">Use **https://vault10.vault.local.azurestack.external:443/keys/key01** to always get the current version</span></span>  
* <span data-ttu-id="7239c-154">Use **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** para obtener esta versión concreta.</span><span class="sxs-lookup"><span data-stu-id="7239c-154">Use **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** to get this specific version</span></span>

### <a name="get-a-key"></a><span data-ttu-id="7239c-155">Obtener una clave</span><span class="sxs-lookup"><span data-stu-id="7239c-155">Get a key</span></span>

<span data-ttu-id="7239c-156">Use el comando **Get-AzureKeyVaultKey** para leer una clave y sus detalles.</span><span class="sxs-lookup"><span data-stu-id="7239c-156">Use the **Get-AzureKeyVaultKey** command to read a key and its details.</span></span>

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a><span data-ttu-id="7239c-157">Crear un secreto</span><span class="sxs-lookup"><span data-stu-id="7239c-157">Create a secret</span></span>

<span data-ttu-id="7239c-158">Use el comando **Set-AzureKeyVaultSecret** para crear o actualizar un secreto en un almacén.</span><span class="sxs-lookup"><span data-stu-id="7239c-158">Use the **Set-AzureKeyVaultSecret** command to create or update a secret in a vault.</span></span> <span data-ttu-id="7239c-159">Si aún no existe un secreto, se creará uno y, si ya existe, se creará una nueva versión del secreto.</span><span class="sxs-lookup"><span data-stu-id="7239c-159">A secret is created if it doesn’t already exist, and a new version of the secret is created if it already exists.</span></span>

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

<span data-ttu-id="7239c-160">**Salida**</span><span class="sxs-lookup"><span data-stu-id="7239c-160">**Output**</span></span>

![crear secreto](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a><span data-ttu-id="7239c-162">Obtener un secreto</span><span class="sxs-lookup"><span data-stu-id="7239c-162">Get a secret</span></span>

<span data-ttu-id="7239c-163">Use el comando **Get-AzureKeyVaultSecret** para leer un secreto en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7239c-163">Use the **Get-AzureKeyVaultSecret** command to read a secret in a key vault.</span></span> <span data-ttu-id="7239c-164">Este comando puede devolver todas las versiones de un secreto o algunas versiones concretas.</span><span class="sxs-lookup"><span data-stu-id="7239c-164">This command can return all or specific versions of a secret.</span></span> 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

<span data-ttu-id="7239c-165">Después de crear claves y secretos, puede autorizar aplicaciones externas para que los usen.</span><span class="sxs-lookup"><span data-stu-id="7239c-165">After creating keys and secrets, you can authorize external applications to use them.</span></span>

## <a name="authorize-an-application-to-use-a-key-or-secret"></a><span data-ttu-id="7239c-166">Autorización de una aplicación para que use una clave o un secreto</span><span class="sxs-lookup"><span data-stu-id="7239c-166">Authorize an application to use a key or secret</span></span>

<span data-ttu-id="7239c-167">Para autorizar a una aplicación a acceder a una clave o un secreto del almacén de claves, use el comando **Set-AzureRmKeyVaultAccessPolicy**.</span><span class="sxs-lookup"><span data-stu-id="7239c-167">To authorize an application to access a key or secret in the key vault, use the **Set-AzureRmKeyVaultAccessPolicy** command.</span></span>
<span data-ttu-id="7239c-168">Por ejemplo, si el nombre del almacén es ContosoKeyVault y la aplicación que desea autorizar tiene el identificador de cliente 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed,</span><span class="sxs-lookup"><span data-stu-id="7239c-168">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a Client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed.</span></span> <span data-ttu-id="7239c-169">Ejecute el comando siguiente para autorizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7239c-169">Run the following command to authorize the application.</span></span> <span data-ttu-id="7239c-170">Si lo desea, puede especificar el parámetro **PermissionsToKeys** para establecer permisos para un usuario, aplicación o grupo de seguridad:</span><span class="sxs-lookup"><span data-stu-id="7239c-170">Optionally, you can specify the **PermissionsToKeys** parameter to set permissions for a user, application, or a security group:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

<span data-ttu-id="7239c-171">Si desea autorizar a esa misma aplicación a leer los secretos del almacén, ejecute el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7239c-171">If you want to authorize that same application to read secrets in your vault, run the following cmdlet:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a><span data-ttu-id="7239c-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7239c-172">Next Steps</span></span>
* [<span data-ttu-id="7239c-173">Implementación de una máquina virtual con una contraseña almacenada en un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="7239c-173">Deploy a VM with password stored in a Key Vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="7239c-174">Implementación de una máquina virtual con un certificado almacenado en un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="7239c-174">Deploy a VM with certificate stored in Key Vault</span></span>](azure-stack-kv-push-secret-into-vm.md) 
