---
title: "elemento de interfaz de usuario de CredentialsCombo de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Compute.CredentialsCombo para administrar aplicaciones de Azure
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a>Elemento de interfaz de usuario Microsoft.Compute.CredentialsCombo
Grupo de controles con validación integrada para las contraseñas de Windows y Linux, y las claves públicas de SSH. Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Ejemplo de interfaz de usuario
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a>Esquema
Si `osPlatform` es **Windows**, hello esquema siguiente se utiliza:
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

Si `osPlatform` es **Linux**, hello esquema siguiente se utiliza:
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a>Comentarios
- `osPlatform` debe especificarse y puede ser **Windows** o **Linux**.
- Si `constraints.required` se establece demasiado**true**, a continuación, Hola contraseña o cuadros de texto de la clave pública SSH deben contener valores toovalidate correctamente. es el valor predeterminado de Hello **true**.
- Si `options.hideConfirmation` se establece demasiado**true**, a continuación, se oculta el segundo cuadro de texto hello para confirmar la contraseña del usuario de Hola. es el valor predeterminado de Hello **false**.
- Si `options.hidePassword` se establece demasiado**true**, a continuación, la autenticación de contraseña de hello opción toouse está oculto. Se puede utilizar solo cuando `osPlatform` es **Linux**. El valor predeterminado es **false**.
- Las restricciones adicionales en hello permiten contraseñas pueden implementarse mediante hello `customPasswordRegex` propiedad. Hola cadena en `customValidationMessage` se muestra cuando una contraseña se produce un error de validación personalizada. Hello valor predeterminado para ambas propiedades es **null**.

## <a name="sample-output"></a>Salida de ejemplo
Si `osPlatform` es **Windows**, o una contraseña en lugar de una clave pública SSH proporcionado por el usuario de hello, hello se espera resultado siguiente:

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

Si una clave pública SSH había proporcionado por el usuario de hello, a continuación, hello se espera resultado siguiente:
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a>Pasos siguientes
* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).
* Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).
