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
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Error RequestDisallowedByPolicy con la directiva de recursos de Azure

Este artículo describe la causa de Hola de error de hello RequestDisallowedByPolicy, también proporciona soluciones para este error.

## <a name="symptom"></a>Síntoma

Cuando intente toodo una acción durante la implementación, es posible que reciba un **RequestDisallowedByPolicy** error que impide la acción de hello realizarse. Hola te mostramos un ejemplo de error de hello:

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>Solución de problemas

tooretrieve obtener más información acerca de la directiva de Hola que bloquea la implementación, use Hola siguiendo uno de los métodos de hello:

### <a name="method-1"></a>Método 1

En PowerShell, proporcionar ese identificador de directiva como hello **identificador** detalles del parámetro tooretrieve acerca de la directiva de Hola que bloquea la implementación.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>Método 2 

En Azure CLI 2.0, proporcione el nombre de Hola de definición de directiva de hello: 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>Solución

Para la seguridad o el cumplimiento, el departamento de TI imponer una directiva de recursos que prohíba la creación de direcciones IP públicas, grupos de seguridad de red, rutas definidas por el usuario o tablas de enrutamiento. En el ejemplo de Hola Hola de mensaje de error que se describe en la sección "Síntomas" Hola, se denomina directiva de hello **regionPolicyDefinition**, pero podría ser diferente.
tooresolve este problema, trabajar con las directivas de recursos de TI departamento tooreview hello y determinar cómo tooperform Hola solicitado la acción de acuerdo con esas directivas.


Para obtener más información, vea Hola siguientes artículos:

- [Información general sobre las directivas de recursos](resource-manager-policy.md)
- [Errores comunes de implementación: RequestDisallowedByPolicy](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


