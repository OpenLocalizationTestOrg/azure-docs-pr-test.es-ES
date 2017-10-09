---
title: las directivas de laboratorio de aaaGrant usuario permisos toospecific | Documentos de Microsoft
description: "Obtenga información acerca de cómo toogrant permisos toospecific laboratorio las directivas de usuario en los laboratorios de desarrollo y pruebas según las necesidades de cada usuario"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a>Conceder permisos de usuario toospecific directivas de laboratorio
## <a name="overview"></a>Información general
Este artículo se explica cómo toouse directiva de PowerShell toogrant a los usuarios permisos tooa laboratorio determinado. De este modo, se pueden aplicar permisos en función de las necesidades de cada usuario. Por ejemplo, puede toogrant una configuración de directiva de usuario determinado Hola capacidad toochange Hola VM, pero no Hola costo directivas.

## <a name="policies-as-resources"></a>Directivas como recursos
Según lo descrito en hello [el Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md) artículo, RBAC permite la administración de acceso específico de recursos de Azure. Usar RBAC, puede separar los derechos en el equipo de DevOps y conceder únicamente una cantidad Hola de toousers de acceso que necesitan tooperform sus trabajos.

En los laboratorios de desarrollo y pruebas, una directiva es un tipo de recurso que permite la acción de RBAC hello **Microsoft.DevTestLab/labs/policySets/policies/**. Cada directiva de laboratorio es un recurso en el tipo de recurso de directiva de Hola y puede asignarse como un ámbito de la función de RBAC tooan.

Por ejemplo, en toohello de permiso de lectura/escritura de orden toogrant usuarios **tamaños de máquina virtual permite** directiva, debe crear un rol personalizado que funcione con hello **Microsoft.DevTestLab/labs/policySets/policies/** * acción y, a continuación, asignar Hola usuarios adecuados toothis rol personalizado en el ámbito de Hola de **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.

toolearn más información acerca de las funciones personalizadas en RBAC, vea hello [control de acceso de roles personalizados](../active-directory/role-based-access-control-custom-roles.md).

## <a name="creating-a-lab-custom-role-using-powershell"></a>Creación de un rol personalizado de laboratorio con PowerShell
En orden tooget iniciado, necesitará hello tooread después de artículo, que se explicará cómo tooinstall y configurar los cmdlets de PowerShell de Azure de hello: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).

Una vez haya configurado Hola cmdlets de PowerShell de Azure, puede realizar Hola siguientes tareas:

* Lista de todas las operaciones de Hola/acciones para un proveedor de recursos
* Enumerar las acciones de un rol determinado
* Crear un rol personalizado

Hola siguiente script de PowerShell muestra ejemplos de cómo tooperform estas tareas:

    ‘List all hello operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a>Asignar permisos de usuario de tooa para una directiva determinada utilizando roles personalizados
Una vez que haya definido sus funciones personalizadas, puede asignarlos toousers. En orden tooassign un usuario de tooa roles personalizados, primero debe obtener hello **ObjectId** que representa ese usuario. toodo que usar hello **AzureRmADUser Get** cmdlet.

En el siguiente ejemplo de Hola Hola **ObjectId** de hello *SomeUser* usuario es 05DEFF7B 0AC3 4ABF B74D 6A72CD5BF3F3.

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

Una vez que tenga hello **ObjectId** de usuario de Hola y el nombre de rol personalizado, puede asignar ese usuario toohello de rol con hello **AzureRmRoleAssignment New** cmdlet:

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

En el ejemplo anterior de hello, Hola **AllowedVmSizesInLab** se utiliza la directiva. Puede usar cualquiera de hello las directivas siguientes:

* MaxVmsAllowedPerUser
* MaxVmsAllowedPerLab
* AllowedVmSizesInLab
* LabVmsShutdown

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Pasos siguientes
Una vez haya concedido directivas de laboratorio de toospecific de permisos de usuario, estas son algunas tooconsider de pasos siguiente:

* [Laboratorio de acceso seguro tooa](devtest-lab-add-devtest-user.md).
* [Definición de directivas de laboratorio](devtest-lab-set-lab-policy.md)
* [Creación de una plantilla de laboratorio](devtest-lab-create-template.md)
* [Creación de artefactos personalizados para máquinas virtuales](devtest-lab-artifact-author.md)
* [Agregar una máquina virtual con el laboratorio de artefactos tooa](devtest-lab-add-vm-with-artifacts.md).

