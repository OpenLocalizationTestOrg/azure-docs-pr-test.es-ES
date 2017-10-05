---
title: "Concesión de permisos de usuario a directivas específicas de laboratorio | Microsoft Docs"
description: "Obtenga información acerca de cómo conceder permisos de usuario para las directivas específicas de laboratorio en DevTest Labs según las necesidades de cada usuario"
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
ms.openlocfilehash: 0bd9f83257834d9681479ba9117c48ffd6d6e166
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a>Concesión de permisos de usuario a directivas específicas de laboratorio
## <a name="overview"></a>Información general
Este artículo muestra cómo usar PowerShell para conceder permisos de usuario a una directiva concreta de laboratorio. De este modo, se pueden aplicar permisos en función de las necesidades de cada usuario. Por ejemplo, quizá prefiera conceder a un usuario determinado la posibilidad de cambiar la configuración de directiva de máquina virtual, pero no las directivas de costos.

## <a name="policies-as-resources"></a>Directivas como recursos
Tal y como se describe en el artículo [Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md) , RBAC permite la administración de acceso específica de recursos para Azure. Gracias a RBAC puede dividir las tareas entre el equipo de DevOps, y conceder a los usuarios únicamente el nivel de acceso que necesitan para realizar su trabajo.

En DevTest Labs, una directiva es un tipo de recurso que permite la acción de RBAC **Microsoft.DevTestLab/labs/policySets/policies/**. Cada directiva de laboratorio es un recurso en el tipo de recurso Directiva, y se puede asignar como ámbito a un rol RBAC.

Por ejemplo, para conceder permiso de lectura/escritura de los usuarios para el **tamaños de máquina virtual permite** directiva, debe crear un rol personalizado que funcione con el **Microsoft.DevTestLab/labs/policySets/policies/*** acción y, a continuación, asignar los usuarios adecuados a este rol de seguridad en el ámbito de **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.

Para obtener más información sobre los roles personalizados de RBAC, consulte [Control de acceso de los roles personalizados](../active-directory/role-based-access-control-custom-roles.md).

## <a name="creating-a-lab-custom-role-using-powershell"></a>Creación de un rol personalizado de laboratorio con PowerShell
Para empezar, debe leer el artículo siguiente, donde se explica cómo instalar y configurar los cmdlets de Azure PowerShell: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).

Una vez haya configurado los cmdlets de Azure PowerShell, podrá realizar las siguientes tareas:

* Enumerar todas las operaciones y acciones para un proveedor de recursos
* Enumerar las acciones de un rol determinado
* Crear un rol personalizado

El siguiente script de PowerShell muestra ejemplos de cómo realizar estas tareas:

    ‘List all the operations/actions for a resource provider.
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

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a>Asignación de permisos a un usuario para una directiva determinada utilizando roles personalizados
Una vez haya definido los roles personalizados, puede asignárselos a los usuarios. A fin de asignar un rol personalizado a un usuario, primero debe obtener el **ObjectId** que representa a ese usuario. Para ello, utilice el cmdlet **Get-AzureRmADUser** .

En el ejemplo siguiente, el valor **ObjectId** del usuario *SomeUser* es 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

Una vez que tenga el **ObjectId** para el usuario y un nombre de rol personalizado, puede asignar ese rol al usuario con el cmdlet **New-AzureRmRoleAssignment**:

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

En el ejemplo anterior, se utiliza la directiva **AllowedVmSizesInLab** . Puede utilizar cualquiera de las directivas siguientes:

* MaxVmsAllowedPerUser
* MaxVmsAllowedPerLab
* AllowedVmSizesInLab
* LabVmsShutdown

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Pasos siguientes
Una vez que haya concedido permisos de usuario a las directivas específicas del laboratorio, estos son algunos de los siguientes pasos que debe considerar:

* [Acceso seguro a un laboratorio](devtest-lab-add-devtest-user.md)
* [Definición de directivas de laboratorio](devtest-lab-set-lab-policy.md)
* [Creación de una plantilla de laboratorio](devtest-lab-create-template.md)
* [Creación de artefactos personalizados para máquinas virtuales](devtest-lab-artifact-author.md)
* [Incorporación de una máquina virtual con artefactos a un laboratorio](devtest-lab-add-vm-with-artifacts.md)

