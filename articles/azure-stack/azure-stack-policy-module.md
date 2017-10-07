---
title: "Hola aaaUse módulo de directivas de pila de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconstrain una toobehave de suscripción de Azure como una suscripción de la pila de Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 937ef34f-14d4-4ea9-960b-362ba986f000
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/28/2017
ms.author: helaw
ms.openlocfilehash: a9d01b759d7c4a248f727de682a71a7655ed12d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-policy-using-hello-azure-stack-policy-module"></a>Administrar la directiva de Azure mediante Hola módulo de directivas de pila de Azure
módulo de directivas de la pila de Azure de Hello permite tooconfigure una suscripción de Azure con hello mismo control de versiones y el servicio de disponibilidad como la pila de Azure.  módulo de Hello usa hello **AzureRMPolicyAssignment New** cmdlet toocreate una directiva de Azure, que limita los tipos de recursos de Hola y de servicios disponibles en una suscripción.  Una vez completado, puede usar las aplicaciones de toodevelop de suscripción de Azure destinadas a la pila de Azure.  

## <a name="install-hello-module"></a>Instalar el módulo de Hola
1. Instalar versión requerida de Hola de hello AzureRM PowerShell módulo, como se describe en el paso 1 de [instale PowerShell para Azure pila](azure-stack-powershell-install.md).   
2. [Descargar herramientas de Azure pila Hola desde GitHub](azure-stack-powershell-download.md)  
3. [Configure PowerShell for use with Azure Stack](azure-stack-powershell-configure-user.md) (Configuración de PowerShell para usarlo con Azure Stack)

4. Importe el módulo de Hola AzureStack.Policy.psm1:

   ```PowerShell
   Import-Module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-toosubscription"></a>Aplicar directiva toosubscription
Hola siguiente comando puede ser tooapply usa una directiva predeterminada de la pila de Azure con su suscripción de Azure. Antes de ejecutarla, reemplace *Azure Subscription Name* por el nombre de su suscripción de Azure.

```PowerShell
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
$rgName = 'AzureStack'
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-tooa-resource-group"></a>Aplicar el grupo de recursos de tooa de directiva
Puede que desee tooapply directivas en un método más granular.  Por ejemplo, puede tener otros recursos que se ejecutan en hello misma suscripción.  Puede establecer el ámbito de hello directiva aplicación tooa grupo de recursos específico, lo que le permite probar sus aplicaciones para la pila de Azure con recursos de Azure. Antes de ejecutarla, reemplace *Azure Subscription Name* por el nombre de su suscripción de Azure.

```PowerShell
$resourceGroupName = ‘myRG01’
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a>Directiva en acción
Una vez haya implementado Hola directiva de Azure, recibirá un error cuando intente toodeploy un recurso que prohibido por la directiva.  

![Resultado del error de implementación de un recurso debido a la restricción de la directiva](./media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a>Pasos siguientes
[Implementación de plantillas con PowerShell](azure-stack-deploy-template-powershell.md)

[Implementación de plantillas con la CLI de Azure](azure-stack-deploy-template-command-line.md)

[Implementación de plantillas con Visual Studio](azure-stack-deploy-template-visual-studio.md)
