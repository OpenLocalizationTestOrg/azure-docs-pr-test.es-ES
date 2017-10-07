---
title: "elemento de interfaz de usuario de FileUpload de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Common.FileUpload para administrar aplicaciones de Azure
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
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Elemento de interfaz de usuario Microsoft.Common.FileUpload
Un control que permite a un usuario toospecify uno o más archivos tooupload. Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Ejemplo de interfaz de usuario
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a>Comentarios
- `constraints.accept`Especifica tipos de Hola de archivos que se muestran en el cuadro de diálogo de archivos del explorador de Hola. Vea hello [especificación de HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) para los valores permitidos. es el valor predeterminado de Hello **null**.
- Si `options.multiple` se establece demasiado**true**, usuario Hola puede tooselect más de un archivo en el cuadro de diálogo de archivos del explorador de Hola. es el valor predeterminado de Hello **false**.
- Este elemento es compatible con la carga de archivos en dos modos en función de valor de Hola de `options.uploadMode`. Si **archivo** se especifica, el resultado de hello contiene contenido de Hola de archivo hello como un blob. Si **url** se especifica, el archivo hello es ubicación temporal tooa cargados y salida de hello contiene Hola URL de blob de Hola. Los blobs temporales se eliminan después de 24 horas. es el valor predeterminado de Hello **archivo**.
- Hola valo `options.openMode` determina cómo se lee el archivo hello. Si el archivo hello es texto sin formato de toobe esperado, especifique **texto**; en caso contrario, especifique **binario**. es el valor predeterminado de Hello **texto**.
- Si `options.uploadMode` se establece demasiado**archivo** y `options.openMode` se establece demasiado**binario**, tiene una salida de hello codificación base64.
- `options.encoding`Especifica Hola codificación toouse al leer el archivo hello. es el valor predeterminado de Hello **UTF-8**y se usa solo cuando `options.openMode` se establece demasiado**texto**.

## <a name="sample-output"></a>Salida de ejemplo
Si options.multiple es false y options.uploadMode es el archivo, el resultado incluye contenido de Hola de archivo hello como una cadena JSON:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Si es true options.multiple and'options.uploadMode es archivo, entonces la salida contiene contenido de Hola de los archivos de hello como una matriz JSON:

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

Si options.multiple es false y options.uploadMode es url, la salida incluye una dirección URL como una cadena JSON:

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

Si options.multiple es true y options.uploadMode es url, la salida incluye una lista de direcciones URL como una matriz JSON:
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

Cuando se prueba un CreateUiDefinition, algunos exploradores (por ejemplo, Google Chrome) truncan las direcciones URL generadas por hello Microsoft.Common.FileUpload elemento en la consola del explorador Hola. Puede que necesite tooright y haga clic en vínculos individuales toocopy hello las direcciones URL completas.


## <a name="next-steps"></a>Pasos siguientes
* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).
* Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).
