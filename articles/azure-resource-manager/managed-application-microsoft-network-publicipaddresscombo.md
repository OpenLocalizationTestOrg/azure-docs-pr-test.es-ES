---
title: "elemento de interfaz de usuario de PublicIpAddressCombo de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Network.PublicIpAddressCombo para administrar aplicaciones de Azure
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a>Elemento de interfaz de usuario Microsoft.Network.PublicIpAddressCombo
Grupo de controles para seleccionar una dirección IP pública nueva o existente. Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Ejemplo de interfaz de usuario
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- Si el usuario de hello selecciona 'None' para la dirección IP pública, cuadro de texto de etiqueta de nombre de dominio de hello está oculto.
- Si el usuario de hello selecciona una dirección IP pública existente, cuadro de texto de etiqueta de nombre de dominio de hello está deshabilitada. Su valor es la etiqueta de nombre de dominio de Hola de dirección IP de hello seleccionado.
- Hola automáticamente en función de la ubicación de hello selecciona las actualizaciones de sufijo (por ejemplo, westus.cloudapp.azure.com) de nombres de dominio.

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a>Comentarios
- Si `constraints.required.domainNameLabel` se establece demasiado**true**, usuario de hello debe proporcionar una etiqueta de nombre de dominio al crear una nueva dirección IP pública. Las direcciones IP públicas existentes sin una etiqueta no están disponibles para la selección.
- Si `options.hideNone` se establece demasiado**true**, Hola, a continuación, la opción tooselect **ninguno** para la dirección IP pública Hola dirección está oculto. es el valor predeterminado de Hello **false**.
- Si `options.hideDomainNameLabel` se establece demasiado**true**, a continuación, se oculta el cuadro de texto de hello para la etiqueta de nombre de dominio. es el valor predeterminado de Hello **false**.
- Si `options.hideExisting` es true, el usuario hello no es capaz de toochoose una dirección IP pública existente. es el valor predeterminado de Hello **false**.

## <a name="sample-output"></a>Salida de ejemplo
Si el usuario de hello no selecciona ninguna dirección IP pública, hello se espera resultado siguiente:
```json
{
  "newOrExistingOrNone": "none"
}
```

Si el usuario de hello selecciona una dirección IP nueva o existente, hello se espera resultado siguiente:
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- Cuando se especifica `options.hideNone`, `newOrExistingOrNone` siempre devuelve **none**.
- Cuando se especifica `options.hideDomainNameLabel`, `domainNameLabel` no se declara.

## <a name="next-steps"></a>Pasos siguientes
* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).
* Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).
