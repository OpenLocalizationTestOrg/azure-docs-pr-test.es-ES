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
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a>Conceder permiso toomany aplicaciones tooaccess un almacén de claves

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a>P: ¿puedo tener varios (más de 16) aplicaciones que necesitan tooaccess un almacén de claves. Puesto que Key Vault solo acepta 16 entradas de control de acceso, ¿cómo puedo conseguirlo?

La directiva de control de acceso de Key Vault solo admite 16 entradas. Sin embargo, puede crear un grupo de seguridad de Azure Active Directory. Agregue todos los hello asociado el grupo de seguridad de toothis de entidades de seguridad de servicio y, a continuación, concede acceso toothis seguridad grupo tooKey almacén.

Estos son los requisitos previos de hello:
* [Instale el módulo PowerShell de Azure Active Directory V2](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).
* [Instale Azure PowerShell](/powershell/azure/overview).
* los comandos siguientes de hello toorun, necesita permisos toocreate/editar grupos de inquilino de Azure Active Directory de Hola. Si no tiene permisos, deberá toocontact el Administrador de Azure Active Directory.

Ahora ejecute hello siga los comandos de PowerShell.

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

Si necesita toogrant un conjunto diferente de grupo de permisos tooa de aplicaciones, cree un grupo de seguridad de Azure Active Directory independiente para dichas aplicaciones.

## <a name="next-steps"></a>Pasos siguientes

Más información acerca de cómo demasiado[proteger el almacén de claves](key-vault-secure-your-key-vault.md).
