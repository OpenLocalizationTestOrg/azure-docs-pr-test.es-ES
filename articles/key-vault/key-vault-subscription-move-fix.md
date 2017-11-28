---
title: "Identificador de inquilino de almacén de claves de aaaChange Hola después de mover una suscripción | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooswitch Hola el Id. de inquilino para un almacén de claves después de una suscripción es mover a inquilino diferente tooa"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 4d0607208c61c57959439d2d0bd8feade4141fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="e186b-103">Cambio del identificador de inquilino de Key Vault después de mover una suscripción</span><span class="sxs-lookup"><span data-stu-id="e186b-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="e186b-104">P: ¿mi suscripción se ha movido de inquilino A tootenant B. ¿Cómo cambiar el Id. de inquilino de hello para el almacén de claves existente y establezca las listas ACL correctas para las entidades en el inquilino B?</span><span class="sxs-lookup"><span data-stu-id="e186b-104">Q: My subscription was moved from tenant A tootenant B. How do I change hello tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="e186b-105">Cuando se crea un nuevo almacén de claves en una suscripción, es toohello automáticamente relacionados de forma predeterminada el identificador de inquilino de Azure Active Directory para esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="e186b-105">When you create a new key vault in a subscription, it is automatically tied toohello default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="e186b-106">Todas las entradas de directiva de acceso también están relacionados toothis identificador del inquilino.</span><span class="sxs-lookup"><span data-stu-id="e186b-106">All access policy entries are also tied toothis tenant ID.</span></span> <span data-ttu-id="e186b-107">Cuando se mueve la suscripción de Azure de inquilino de un tootenant B, la clave existente almacenes son inaccesibles por hello las entidades de seguridad (usuarios y aplicaciones) en el inquilino B. toofix este problema, debe:</span><span class="sxs-lookup"><span data-stu-id="e186b-107">When you move your Azure subscription from tenant A tootenant B, your existing key vaults are inaccessible by hello principals (users and applications) in tenant B. toofix this issue, you need to:</span></span>

* <span data-ttu-id="e186b-108">Id. de inquilino de hello cambio asociado con todos los almacenes de claves existentes en este tootenant suscripción B.</span><span class="sxs-lookup"><span data-stu-id="e186b-108">Change hello tenant ID associated with all existing key vaults in this subscription tootenant B.</span></span>
* <span data-ttu-id="e186b-109">Quitar todas las entradas de la directiva de acceso existentes.</span><span class="sxs-lookup"><span data-stu-id="e186b-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="e186b-110">Agregar nuevas entradas de la directiva de acceso asociadas al inquilino B.</span><span class="sxs-lookup"><span data-stu-id="e186b-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="e186b-111">Por ejemplo, si tienes el almacén de claves 'myvault' en una suscripción que se ha movido del inquilino A tootenant B, aquí cómo hello toochange identificador de inquilino para este almacén de claves y quitar directivas de acceso antiguos.</span><span class="sxs-lookup"><span data-stu-id="e186b-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A tootenant B, here's how toochange hello tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="e186b-112">Dado que este almacén se estaba en el inquilino A antes de mover hello, Hola valor original de **$vault. Properties.TenantId** es un inquilino, while **(Get-AzureRmContext). Tenant.TenantId** se inquilino B.</span><span class="sxs-lookup"><span data-stu-id="e186b-112">Because this vault was in tenant A before hello move, hello original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="e186b-113">Ahora que el almacén está asociado con el identificador de inquilino correcto de Hola y se quitan las entradas de la directiva de acceso antiguas, establecer acceso nuevas entradas de directiva con [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="e186b-113">Now that your vault is associated with hello correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e186b-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e186b-114">Next steps</span></span>
<span data-ttu-id="e186b-115">Si tiene alguna pregunta sobre el almacén de claves de Azure, visite hello [foros de almacén de claves de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="e186b-115">If you have questions about Azure Key Vault, visit hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

