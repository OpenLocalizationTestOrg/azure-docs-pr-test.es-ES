---
title: "Concesión de permisos para que muchas aplicaciones tengan acceso a un almacén de Azure Key Vault | Microsoft Docs"
description: "Obtenga información sobre cómo conceder permisos para que muchas aplicaciones tengan acceso a almacén de claves."
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 785d4e40-fb7b-485a-8cbc-d9c8c87708e6
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: ambapat
ms.openlocfilehash: f58b633de2e4b5702ff2df9b3722662b09510200
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permission-to-many-applications-to-access-a-key-vault"></a><span data-ttu-id="e236b-103">Concesión de permisos para que muchas aplicaciones tengan acceso a almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e236b-103">Grant permission to many applications to access a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-to-access-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="e236b-104">P.: Tengo varias aplicaciones (más de 16) que necesitan tener acceso a un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e236b-104">Q: I have several (over 16) applications that need to access a key vault.</span></span> <span data-ttu-id="e236b-105">Puesto que Key Vault solo acepta 16 entradas de control de acceso, ¿cómo puedo conseguirlo?</span><span class="sxs-lookup"><span data-stu-id="e236b-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="e236b-106">La directiva de control de acceso de Key Vault solo admite 16 entradas.</span><span class="sxs-lookup"><span data-stu-id="e236b-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="e236b-107">Sin embargo, puede crear un grupo de seguridad de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e236b-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="e236b-108">Agregue todas las entidades de servicio asociadas a este grupo de seguridad y, luego, conceda acceso a este grupo de seguridad a Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e236b-108">Add all the associated service principals to this security group and then grant access to this security group to Key Vault.</span></span>

<span data-ttu-id="e236b-109">Instalación de los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="e236b-109">Here are the pre-requisites:</span></span>
* <span data-ttu-id="e236b-110">[Instale el módulo PowerShell de Azure Active Directory V2](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="e236b-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="e236b-111">[Instale Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e236b-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e236b-112">Para ejecutar los siguientes comandos, necesita permisos para crear y editar grupos en el inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e236b-112">To run the following commands, you need permissions to create/edit groups in the Azure Active Directory tenant.</span></span> <span data-ttu-id="e236b-113">Si no tiene permisos, debe ponerse en contacto con el administrador de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e236b-113">If you don't have permissions, you may need to contact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="e236b-114">Ejecute los siguientes comandos en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e236b-114">Now run the following commands in PowerShell.</span></span>

```powershell
# Connect to Azure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members to this group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members to this group, in this fashion. 
 
# Set the Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust the permissions as required 
```

<span data-ttu-id="e236b-115">Si tiene que conceder un conjunto de permisos diferente para un grupo de aplicaciones, cree un grupo de seguridad de Azure Active Directory independiente para dichas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e236b-115">If you need to grant a different set of permissions to a group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e236b-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e236b-116">Next steps</span></span>

<span data-ttu-id="e236b-117">Más información sobre cómo [proteger el almacén de claves](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e236b-117">Learn more about how to [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
