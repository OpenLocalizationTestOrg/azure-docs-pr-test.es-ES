---
title: "aaaAzure aplicación administrada crear funciones de definición de interfaz de usuario | Documentos de Microsoft"
description: Describe Hola funciones toouse al construir las definiciones de interfaz de usuario para las aplicaciones administradas de Azure
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a>Elementos CreateUiDefinition
Este artículo describe el esquema de Hola y las propiedades de todos los elementos compatibles de un CreateUiDefinition. Use estos elementos al [crear una aplicación administrada de Azure](managed-application-publishing.md). esquema de Hello para la mayoría de los elementos es como sigue:

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| Propiedad | Obligatorio | Description |
| -------- | -------- | ----------- |
| name | Sí | Un tooreference de identificador interno de una instancia concreta de un elemento. Hola uso más común del nombre de elemento de hello es en `outputs`, donde los valores de salida de hello de hello especifican elementos son asignadas toohello parámetros de plantilla de Hola. También se puede usar valor de salida de hello toobind de un elemento toohello `defaultValue` de otro elemento. |
| type | Sí | Hola toorender de control de interfaz de usuario para el elemento de saludo. Para ver una lista de los tipos admitidos, consulte [Elementos](#elements). |
| label | Sí | Hola muestran el texto del elemento de saludo. Algunos tipos de elementos contienen varias etiquetas, por lo que el valor de hello podría ser un objeto que contiene varias cadenas. |
| defaultValue | No | valor predeterminado de Hola de elemento de saludo. Algunos tipos de elemento admiten valores predeterminados compleja, por lo que el valor de hello podría ser un objeto. |
| toolTip | No | Hola toodisplay de texto de información sobre herramientas de Hola de elemento de saludo. Similar demasiado`label`, algunos elementos de compatibilidad con varias cadenas de información sobre herramientas. Se pueden insertar vínculos en línea con la sintaxis de Markdown.
| constraints | No | Una o varias propiedades que son utilizados toocustomize Hola el comportamiento de la validación del elemento de Hola. propiedades de Hello admitida para las restricciones varían según el tipo de elemento. Algunos tipos de elemento no admite la personalización del comportamiento de la validación de hello y, por tanto, no tienen ninguna propiedad de restricciones. |
| options | No | Propiedades adicionales que personalizan el comportamiento de Hola de elemento de Hola. Similar demasiado`constraints`, propiedades de hello compatibles varían según el tipo de elemento. |
| visible | No | Indica si se muestra el elemento de saludo. Si `true`, elemento de Hola y los elementos secundarios correspondientes se muestran. valor predeterminado de Hello es `true`. Use [funciones lógicas](managed-application-createuidefinition-functions.md#logical-functions) toodynamically controlar el valor de esta propiedad.

## <a name="elements"></a>Elementos

Hola documentación para cada elemento contiene un ejemplo de interfaz de usuario, esquema, comentarios en el comportamiento de Hola de elemento de hello (normalmente sobre la validación y personalización compatibles) y salida de ejemplo.

- [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
- [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>Pasos siguientes
* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).
* Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).
