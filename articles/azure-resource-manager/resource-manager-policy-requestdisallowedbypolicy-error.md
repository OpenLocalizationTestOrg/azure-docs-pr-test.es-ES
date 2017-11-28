---
title: error de aaaRequestDisallowedByPolicy con la directiva de recursos de Azure | Documentos de Microsoft
description: Describe la causa de Hola de hello RequestDisallowedByPolicy error.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="b9799-103">Error RequestDisallowedByPolicy con la directiva de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="b9799-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="b9799-104">Este artículo describe la causa de Hola de error de hello RequestDisallowedByPolicy, también proporciona soluciones para este error.</span><span class="sxs-lookup"><span data-stu-id="b9799-104">This article describes hello cause of hello RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="b9799-105">Síntoma</span><span class="sxs-lookup"><span data-stu-id="b9799-105">Symptom</span></span>

<span data-ttu-id="b9799-106">Cuando intente toodo una acción durante la implementación, es posible que reciba un **RequestDisallowedByPolicy** error que impide la acción de hello realizarse.</span><span class="sxs-lookup"><span data-stu-id="b9799-106">When you try toodo an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents hello action be performed.</span></span> <span data-ttu-id="b9799-107">Hola te mostramos un ejemplo de error de hello:</span><span class="sxs-lookup"><span data-stu-id="b9799-107">hello following is a sample of hello error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="b9799-108">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="b9799-108">Troubleshooting</span></span>

<span data-ttu-id="b9799-109">tooretrieve obtener más información acerca de la directiva de Hola que bloquea la implementación, use Hola siguiendo uno de los métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="b9799-109">tooretrieve details about hello policy that blocked your deployment, use hello following one of hello methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="b9799-110">Método 1</span><span class="sxs-lookup"><span data-stu-id="b9799-110">Method 1</span></span>

<span data-ttu-id="b9799-111">En PowerShell, proporcionar ese identificador de directiva como hello **identificador** detalles del parámetro tooretrieve acerca de la directiva de Hola que bloquea la implementación.</span><span class="sxs-lookup"><span data-stu-id="b9799-111">In PowerShell, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="b9799-112">Método 2</span><span class="sxs-lookup"><span data-stu-id="b9799-112">Method 2</span></span> 

<span data-ttu-id="b9799-113">En Azure CLI 2.0, proporcione el nombre de Hola de definición de directiva de hello:</span><span class="sxs-lookup"><span data-stu-id="b9799-113">In Azure CLI 2.0, provide hello name of hello policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="b9799-114">Solución</span><span class="sxs-lookup"><span data-stu-id="b9799-114">Solution</span></span>

<span data-ttu-id="b9799-115">Para la seguridad o el cumplimiento, el departamento de TI imponer una directiva de recursos que prohíba la creación de direcciones IP públicas, grupos de seguridad de red, rutas definidas por el usuario o tablas de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="b9799-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="b9799-116">En el ejemplo de Hola Hola de mensaje de error que se describe en la sección "Síntomas" Hola, se denomina directiva de hello **regionPolicyDefinition**, pero podría ser diferente.</span><span class="sxs-lookup"><span data-stu-id="b9799-116">In hello sample of hello error message that is described in hello "Symptoms" section, hello policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="b9799-117">tooresolve este problema, trabajar con las directivas de recursos de TI departamento tooreview hello y determinar cómo tooperform Hola solicitado la acción de acuerdo con esas directivas.</span><span class="sxs-lookup"><span data-stu-id="b9799-117">tooresolve this problem, work with your IT department tooreview hello resource policies, and determine how tooperform hello requested action in compliance with those policies.</span></span>


<span data-ttu-id="b9799-118">Para obtener más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="b9799-118">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="b9799-119">Información general sobre las directivas de recursos</span><span class="sxs-lookup"><span data-stu-id="b9799-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="b9799-120">Errores comunes de implementación: RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="b9799-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


