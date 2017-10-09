---
title: "elemento de interfaz de usuario de SizeSelector de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Compute.SizeSelector para administrar aplicaciones de Azure
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a>Elemento de interfaz de usuario Microsoft.Compute.SizeSelector
Control para seleccionar un tamaño para una o varias instancias de máquina virtual. Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Ejemplo de interfaz de usuario
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Comentarios
- `recommendedSizes` debe contener al menos un tamaño. Hola primero recomienda tamaño se utiliza como valor predeterminado de Hola.
- Si no hay un tamaño recomendado en lugar de hello seleccionado, tamaño de Hola se omitirá automáticamente. En su lugar, hello tamaño recomendado siguiente se utiliza.
- Cualquier tamaño no se especifica en hello `constraints.allowedSizes` está oculto y de cualquier tamaño no se especifica en `constraints.excludedSizes` se muestra.
Tanto `constraints.allowedSizes` como `constraints.excludedSizes` son opcionales, pero no se pueden usar simultáneamente. lista de Hola de los tamaños disponibles se puede determinar mediante una llamada a [lista de tamaños de máquina virtual disponible para una suscripción](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).
- `osPlatform` debe especificarse y puede ser **Windows** o **Linux**. Ha utilizado toodetermine los costos de hardware de Hola de máquinas virtuales de Hola.
- `imageReference` se omite para las imágenes propias, pero se proporciona para las imágenes de terceros. Ha utilizado los costes de software de toodetermine Hola de máquinas virtuales de Hola.
- `count`es tooset usado Hola multiplicador apropiado para el elemento de Hola. Admite un valor estático, como **2**, o un valor dinámico de otro elemento, como `[steps('step1').vmCount]`. es el valor predeterminado de Hello **1**.

## <a name="sample-output"></a>Salida de ejemplo
```json
"Standard_D1"
```

## <a name="next-steps"></a>Pasos siguientes
* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).
* Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).
