---
title: "elemento de interfaz de usuario de MultiStorageAccountCombo de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Storage.MultiStorageAccountCombo para administrar aplicaciones de Azure
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a>Elemento de la interfaz de usuario Microsoft.Storage.MultiStorageAccountCombo
Un grupo de controles para crear varias cuentas de almacenamiento con nombres que comienzan con un prefijo común. Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Ejemplo de interfaz de usuario
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Comentarios
- Hola valor para `defaultValue.prefix` se concatena con uno o más números enteros toogenerate hello secuencia de nombres de cuenta de almacenamiento. Por ejemplo, si `defaultValue.prefix` es **foobar** y `count` es **2**, se generan los nombres de cuenta de almacenamiento **foobar1** y **foobar2**. La unicidad de los nombres de cuenta de almacenamiento generados se valida automáticamente.
- nombres de cuenta de almacenamiento de Hola se generan según lexicográficamente `count`. Por ejemplo, si `count` es 10, a continuación, los nombres de cuenta de almacenamiento Hola terminar con enteros de 2 dígitos (01, 02, 03, etcetera.).
- Hola valor predeterminado de `defaultValue.prefix` es **null**y para `defaultValue.type` es **Premium_LRS**.
- Los tipos no especificados en `constraints.allowedTypes` está oculto, mientras que los tipos no especificado en `constraints.excludedTypes` se muestran.
Tanto `constraints.allowedTypes` como `constraints.excludedTypes` son opcionales, pero no se pueden usar simultáneamente.
- En los nombres de cuenta de almacenamiento de toogenerating adición, `count` es tooset usado el multiplicador apropiado para el elemento de saludo. Admite un valor estático, como **2**, o un valor dinámico de otro elemento, como `[steps('step1').storageAccountCount]`. es el valor predeterminado de Hello **1**.

## <a name="sample-output"></a>Salida de ejemplo
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a>Pasos siguientes
* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).
* Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).
