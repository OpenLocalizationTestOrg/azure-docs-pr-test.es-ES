---
title: "elemento de interfaz de usuario de grupo Opciones de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Common.OptionsGroup para administrar aplicaciones de Azure
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a>Elemento de interfaz de usuario Microsoft.Common.OptionsGroup
Control de selección con una fila de opciones disponibles. Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Ejemplo de interfaz de usuario
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a>Comentarios
- etiqueta de Hola para `constraints.allowedValues` es Hola texto para mostrar de un elemento y su valor es el valor de salida de hello de elemento de hello cuando se selecciona.
- Si se especifica, valor predeterminado de hello debe ser una etiqueta presente en `constraints.allowedValues`. Si no se especifica, Hola el primer elemento de `constraints.allowedValues` está activada de forma predeterminada. es el valor predeterminado de Hello **null**.
- `constraints.allowedValues` debe contener al menos un dígito.
- Este elemento no es compatible con hello `constraints.required` propiedad; un elemento debe ser toovalidate seleccionado correctamente.

## <a name="sample-output"></a>Salida de ejemplo
```json
"Bar"
```

## <a name="next-steps"></a>Pasos siguientes
* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).
* Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).
