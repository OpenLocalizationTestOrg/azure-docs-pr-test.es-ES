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
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a>Cambio del identificador de inquilino de Key Vault después de mover una suscripción
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a>P: ¿mi suscripción se ha movido de inquilino A tootenant B. ¿Cómo cambiar el Id. de inquilino de hello para el almacén de claves existente y establezca las listas ACL correctas para las entidades en el inquilino B?
Cuando se crea un nuevo almacén de claves en una suscripción, es toohello automáticamente relacionados de forma predeterminada el identificador de inquilino de Azure Active Directory para esa suscripción. Todas las entradas de directiva de acceso también están relacionados toothis identificador del inquilino. Cuando se mueve la suscripción de Azure de inquilino de un tootenant B, la clave existente almacenes son inaccesibles por hello las entidades de seguridad (usuarios y aplicaciones) en el inquilino B. toofix este problema, debe:

* Id. de inquilino de hello cambio asociado con todos los almacenes de claves existentes en este tootenant suscripción B.
* Quitar todas las entradas de la directiva de acceso existentes.
* Agregar nuevas entradas de la directiva de acceso asociadas al inquilino B.

Por ejemplo, si tienes el almacén de claves 'myvault' en una suscripción que se ha movido del inquilino A tootenant B, aquí cómo hello toochange identificador de inquilino para este almacén de claves y quitar directivas de acceso antiguos.

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

Dado que este almacén se estaba en el inquilino A antes de mover hello, Hola valor original de **$vault. Properties.TenantId** es un inquilino, while **(Get-AzureRmContext). Tenant.TenantId** se inquilino B.

Ahora que el almacén está asociado con el identificador de inquilino correcto de Hola y se quitan las entradas de la directiva de acceso antiguas, establecer acceso nuevas entradas de directiva con [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).

## <a name="next-steps"></a>Pasos siguientes
Si tiene alguna pregunta sobre el almacén de claves de Azure, visite hello [foros de almacén de claves de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

