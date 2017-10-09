---
title: "elemento de interfaz de usuario de UserNameTextBox de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Compute.UserNameTextBox para administrar aplicaciones de Azure
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a>Elemento de interfaz de usuario Microsoft.Compute.UserNameTextBox
Control de cuadro de texto con validación integrada para nombres de usuario de Windows y Linux. Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Ejemplo de interfaz de usuario
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a>Comentarios
- Si `constraints.required` se establece demasiado**true**, cuadro de texto hello debe contener un valor toovalidate correctamente. es el valor predeterminado de Hello **true**.
- `osPlatform` debe especificarse y puede ser **Windows** o **Linux**.
- `constraints.regex` es un patrón de expresión regular de JavaScript. Si se especifica, a continuación, valor del cuadro de texto hello debe coincidir con hello patrón toovalidate correctamente. El valor predeterminado es **null**.
- `constraints.validationMessage`es una cadena toodisplay al valor del cuadro de texto hello no supera la validación de hello especificado por `constraints.regex`. Si no se especifica, Hola se utilizan mensajes de validación integradas del cuadro de texto. es el valor predeterminado de Hello **null**.
- Este elemento tiene validación integrada que se basa en el valor de hello especificado para `osPlatform`. validación integradas Hola puede usarse junto con una expresión regular personalizada.
Si un valor para `constraints.regex` se especifica, ambos Hola integrados y se activan las validaciones personalizadas.

## <a name="sample-output"></a>Salida de ejemplo
```json
"tabrezm"
```

## <a name="next-steps"></a>Pasos siguientes
* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).
* Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).
