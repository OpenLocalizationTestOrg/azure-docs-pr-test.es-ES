---
title: Ejemplo de Script de PowerShell - aaaAzure cifrar una VM de Windows | Documentos de Microsoft
description: "Ejemplo de script de Azure PowerShell: cifrado de una máquina virtual Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="8cb19-103">Cifrado de una máquina virtual Windows con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cb19-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="8cb19-104">Este script crea un almacén Azure Key Vault seguro, claves de cifrado, una entidad de servicio de Azure Active Directory y una máquina virtual (VM) Windows.</span><span class="sxs-lookup"><span data-stu-id="8cb19-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="8cb19-105">Hola VM, a continuación, se cifra mediante la clave de cifrado de Hola desde el almacén de claves y credenciales de servicio principal.</span><span class="sxs-lookup"><span data-stu-id="8cb19-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8cb19-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8cb19-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8cb19-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="8cb19-107">Clean up deployment</span></span> 

<span data-ttu-id="8cb19-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="8cb19-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8cb19-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="8cb19-109">Script explanation</span></span>

<span data-ttu-id="8cb19-110">Este script utiliza Hola después de la implementación de comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="8cb19-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="8cb19-111">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="8cb19-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8cb19-112">Comando</span><span class="sxs-lookup"><span data-stu-id="8cb19-112">Command</span></span> | <span data-ttu-id="8cb19-113">Notas</span><span class="sxs-lookup"><span data-stu-id="8cb19-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8cb19-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8cb19-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8cb19-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="8cb19-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8cb19-116">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="8cb19-116">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="8cb19-117">Crea un almacén de claves de Azure toostore proteger los datos, como las claves de cifrado.</span><span class="sxs-lookup"><span data-stu-id="8cb19-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="8cb19-118">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="8cb19-118">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="8cb19-119">Crea una clave de cifrado en el almacén Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8cb19-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="8cb19-120">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="8cb19-120">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="8cb19-121">Crea un servicio de Azure Active Directory principal toosecurely autenticar y acceso tooencryption teclas de control.</span><span class="sxs-lookup"><span data-stu-id="8cb19-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="8cb19-122">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="8cb19-122">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="8cb19-123">Establece permisos en toogrant de almacén de claves de hello claves de tooencryption de acceso principal de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cb19-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="8cb19-124">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8cb19-124">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="8cb19-125">Crea una configuración de subred.</span><span class="sxs-lookup"><span data-stu-id="8cb19-125">Creates a subnet configuration.</span></span> <span data-ttu-id="8cb19-126">Esta configuración se utiliza con el proceso de creación de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cb19-126">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="8cb19-127">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="8cb19-127">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="8cb19-128">Crea una red virtual.</span><span class="sxs-lookup"><span data-stu-id="8cb19-128">Creates a virtual network.</span></span> |
| [<span data-ttu-id="8cb19-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="8cb19-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="8cb19-130">Crea una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="8cb19-130">Creates a public IP address.</span></span> |
| [<span data-ttu-id="8cb19-131">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="8cb19-131">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="8cb19-132">Crea configuración de regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="8cb19-132">Creates a network security group rule configuration.</span></span> <span data-ttu-id="8cb19-133">Esta configuración es toocreate usa una regla de NSG cuando se crea hello NSG.</span><span class="sxs-lookup"><span data-stu-id="8cb19-133">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="8cb19-134">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="8cb19-134">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="8cb19-135">Crea un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="8cb19-135">Creates a network security group.</span></span> |
| [<span data-ttu-id="8cb19-136">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8cb19-136">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="8cb19-137">Obtiene la información de subred.</span><span class="sxs-lookup"><span data-stu-id="8cb19-137">Gets subnet information.</span></span> <span data-ttu-id="8cb19-138">Esta información se usa al crear una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="8cb19-138">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="8cb19-139">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="8cb19-139">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="8cb19-140">Crea una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="8cb19-140">Creates a network interface.</span></span> |
| [<span data-ttu-id="8cb19-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="8cb19-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="8cb19-142">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8cb19-142">Creates a VM configuration.</span></span> <span data-ttu-id="8cb19-143">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="8cb19-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="8cb19-144">configuración de Hola se utiliza durante la creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8cb19-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="8cb19-145">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="8cb19-145">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="8cb19-146">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8cb19-146">Create a virtual machine.</span></span> |
| [<span data-ttu-id="8cb19-147">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="8cb19-147">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="8cb19-148">Obtiene la información necesaria en el almacén de claves de Hola</span><span class="sxs-lookup"><span data-stu-id="8cb19-148">Gets required information on hello Key Vault</span></span> |
| [<span data-ttu-id="8cb19-149">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="8cb19-149">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="8cb19-150">Habilita el cifrado en una máquina virtual usando las credenciales de entidad de seguridad de servicio de Hola y clave de cifrado.</span><span class="sxs-lookup"><span data-stu-id="8cb19-150">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="8cb19-151">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="8cb19-151">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="8cb19-152">Muestra el estado de Hola de hello proceso de cifrado de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8cb19-152">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="8cb19-153">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8cb19-153">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8cb19-154">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="8cb19-154">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8cb19-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8cb19-155">Next steps</span></span>

<span data-ttu-id="8cb19-156">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8cb19-156">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8cb19-157">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8cb19-157">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
