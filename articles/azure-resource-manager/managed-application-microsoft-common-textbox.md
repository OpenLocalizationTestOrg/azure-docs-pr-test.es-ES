---
title: "elemento de interfaz de usuario de cuadro de texto de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Common.TextBox para administrar aplicaciones de Azure
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a>Elemento de interfaz de usuario Microsoft.Common.TextBox
Un control que puede ser utilizado tooedit texto sin formato. Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Ejemplo de interfaz de usuario
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a>Comentarios
- Si `constraints.required` se establece demasiado**true**, cuadro de texto hello debe contener un valor toovalidate correctamente. es el valor predeterminado de Hello **false**.
- `constraints.regex` es un patrón de expresión regular de JavaScript. Si se especifica, a continuación, valor del cuadro de texto hello debe coincidir con hello patrón toovalidate correctamente. El valor predeterminado es **null**.
- `constraints.validationMessage`es una cadena toodisplay al valor del cuadro de texto hello no puede validarse. Si no se especifica, Hola se utilizan mensajes de validación integradas del cuadro de texto. es el valor predeterminado de Hello **null**.
- Es posible toospecify un valor para `constraints.regex` cuando `constraints.required` se establece demasiado**false**. En este escenario, un valor no es necesario para toovalidate de cuadro de texto hello correctamente. Si se especifica uno, debe coincidir con el patrón de expresión regular de Hola.

## <a name="sample-output"></a>Salida de ejemplo

```json
"foobar"
```

## <a name="next-steps"></a>Pasos siguientes
* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).
* Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).
