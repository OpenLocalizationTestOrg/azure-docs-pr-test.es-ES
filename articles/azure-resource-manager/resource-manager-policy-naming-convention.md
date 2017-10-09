---
title: las directivas de recursos de aaaAzure para las convenciones de nomenclatura | Documentos de Microsoft
description: Describe las directivas de Azure Resource Manager para convenciones de nomenclatura de recursos.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a>Aplicación de directivas de recursos para nombres y texto
En este tema se muestra varios [las directivas de recursos](resource-manager-policy.md) puede aplicar las convenciones de nomenclatura y texto de tooestablish. Estas directivas garantizan la coherencia para valores de etiquetas y nombres de recursos. 

## <a name="set-naming-convention-with-wildcard"></a>Establecimiento de la convención de nomenclatura con caracteres comodín
Hello en el ejemplo siguiente se muestra uso de Hola de carácter comodín, que es compatible con hello **como** condición. Hello condición indica que si hello nombre coincide con patrón mencionados hello (namePrefix\*nameSuffix), a continuación, denegar la solicitud de hello:

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a>Establecimiento de la convención de nomenclatura con patrones

toospecify que los nombres de recursos coinciden con un patrón, use Hola coincide con la condición. en el ejemplo siguiente se Hello requiere nombres toostart con `contoso` y contener seis letras adicionales:

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a>Establecimiento del patrón de fecha para el valor de etiqueta

toorequire un patrón de fecha de dos dígitos, guión, tres letras, guión y cuatro dígitos, use:

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>Pasos siguientes
* Después de definir una regla de directiva (como se muestra en hello anteriores ejemplos), se necesita la definición de la directiva de toocreate hello y se asigna tooa ámbito. Hola ámbito puede ser una suscripción, el grupo de recursos o el recurso. directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md). directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md). 
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

