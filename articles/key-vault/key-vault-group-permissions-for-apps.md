---
title: "aaaGrant permiso toomany aplicaciones tooaccess un almacén de claves de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toogrant permiso toomany aplicaciones tooaccess una clave de almacén"
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
ms.openlocfilehash: 5258149f939856f91b3848fc50399e58e5894f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a><span data-ttu-id="5cb3d-103">Conceder permiso toomany aplicaciones tooaccess un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="5cb3d-103">Grant permission toomany applications tooaccess a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="5cb3d-104">P: ¿puedo tener varios (más de 16) aplicaciones que necesitan tooaccess un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-104">Q: I have several (over 16) applications that need tooaccess a key vault.</span></span> <span data-ttu-id="5cb3d-105">Puesto que Key Vault solo acepta 16 entradas de control de acceso, ¿cómo puedo conseguirlo?</span><span class="sxs-lookup"><span data-stu-id="5cb3d-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="5cb3d-106">La directiva de control de acceso de Key Vault solo admite 16 entradas.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="5cb3d-107">Sin embargo, puede crear un grupo de seguridad de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="5cb3d-108">Agregue todos los hello asociado el grupo de seguridad de toothis de entidades de seguridad de servicio y, a continuación, concede acceso toothis seguridad grupo tooKey almacén.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-108">Add all hello associated service principals toothis security group and then grant access toothis security group tooKey Vault.</span></span>

<span data-ttu-id="5cb3d-109">Estos son los requisitos previos de hello:</span><span class="sxs-lookup"><span data-stu-id="5cb3d-109">Here are hello pre-requisites:</span></span>
* <span data-ttu-id="5cb3d-110">[Instale el módulo PowerShell de Azure Active Directory V2](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="5cb3d-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="5cb3d-111">[Instale Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5cb3d-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="5cb3d-112">los comandos siguientes de hello toorun, necesita permisos toocreate/editar grupos de inquilino de Azure Active Directory de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-112">toorun hello following commands, you need permissions toocreate/edit groups in hello Azure Active Directory tenant.</span></span> <span data-ttu-id="5cb3d-113">Si no tiene permisos, deberá toocontact el Administrador de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-113">If you don't have permissions, you may need toocontact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="5cb3d-114">Ahora ejecute hello siga los comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-114">Now run hello following commands in PowerShell.</span></span>

```powershell
# Connect tooAzure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members toothis group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members toothis group, in this fashion. 
 
# Set hello Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust hello permissions as required 
```

<span data-ttu-id="5cb3d-115">Si necesita toogrant un conjunto diferente de grupo de permisos tooa de aplicaciones, cree un grupo de seguridad de Azure Active Directory independiente para dichas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5cb3d-115">If you need toogrant a different set of permissions tooa group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cb3d-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5cb3d-116">Next steps</span></span>

<span data-ttu-id="5cb3d-117">Más información acerca de cómo demasiado[proteger el almacén de claves](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="5cb3d-117">Learn more about how too[Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
