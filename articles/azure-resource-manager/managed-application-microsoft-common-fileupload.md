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
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="f7454-103">Elemento de interfaz de usuario Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="f7454-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="f7454-104">Un control que permite a un usuario toospecify uno o más archivos tooupload.</span><span class="sxs-lookup"><span data-stu-id="f7454-104">A control that allows a user toospecify one or more files tooupload.</span></span> <span data-ttu-id="f7454-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f7454-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f7454-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="f7454-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="f7454-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="f7454-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="f7454-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="f7454-109">Remarks</span></span>
- <span data-ttu-id="f7454-110">`constraints.accept`Especifica tipos de Hola de archivos que se muestran en el cuadro de diálogo de archivos del explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="f7454-110">`constraints.accept` specifies hello types of files that are shown in hello browser's file dialog.</span></span> <span data-ttu-id="f7454-111">Vea hello [especificación de HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) para los valores permitidos.</span><span class="sxs-lookup"><span data-stu-id="f7454-111">See hello [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="f7454-112">es el valor predeterminado de Hello **null**.</span><span class="sxs-lookup"><span data-stu-id="f7454-112">hello default value is **null**.</span></span>
- <span data-ttu-id="f7454-113">Si `options.multiple` se establece demasiado**true**, usuario Hola puede tooselect más de un archivo en el cuadro de diálogo de archivos del explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="f7454-113">If `options.multiple` is set too**true**, hello user is allowed tooselect more than one file in hello browser's file dialog.</span></span> <span data-ttu-id="f7454-114">es el valor predeterminado de Hello **false**.</span><span class="sxs-lookup"><span data-stu-id="f7454-114">hello default value is **false**.</span></span>
- <span data-ttu-id="f7454-115">Este elemento es compatible con la carga de archivos en dos modos en función de valor de Hola de `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="f7454-115">This element supports uploading files in two modes based on hello value of `options.uploadMode`.</span></span> <span data-ttu-id="f7454-116">Si **archivo** se especifica, el resultado de hello contiene contenido de Hola de archivo hello como un blob.</span><span class="sxs-lookup"><span data-stu-id="f7454-116">If **file** is specified, hello output contains hello contents of hello file as a blob.</span></span> <span data-ttu-id="f7454-117">Si **url** se especifica, el archivo hello es ubicación temporal tooa cargados y salida de hello contiene Hola URL de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="f7454-117">If **url** is specified, then hello file is uploaded tooa temporary location, and hello output contains hello URL of hello blob.</span></span> <span data-ttu-id="f7454-118">Los blobs temporales se eliminan después de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="f7454-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="f7454-119">es el valor predeterminado de Hello **archivo**.</span><span class="sxs-lookup"><span data-stu-id="f7454-119">hello default value is **file**.</span></span>
- <span data-ttu-id="f7454-120">Hola valo `options.openMode` determina cómo se lee el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="f7454-120">hello value of `options.openMode` determines how hello file is read.</span></span> <span data-ttu-id="f7454-121">Si el archivo hello es texto sin formato de toobe esperado, especifique **texto**; en caso contrario, especifique **binario**.</span><span class="sxs-lookup"><span data-stu-id="f7454-121">If hello file is expected toobe plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="f7454-122">es el valor predeterminado de Hello **texto**.</span><span class="sxs-lookup"><span data-stu-id="f7454-122">hello default value is **text**.</span></span>
- <span data-ttu-id="f7454-123">Si `options.uploadMode` se establece demasiado**archivo** y `options.openMode` se establece demasiado**binario**, tiene una salida de hello codificación base64.</span><span class="sxs-lookup"><span data-stu-id="f7454-123">If `options.uploadMode` is set too**file** and `options.openMode` is set too**binary**, hello output is base64-encoded.</span></span>
- <span data-ttu-id="f7454-124">`options.encoding`Especifica Hola codificación toouse al leer el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="f7454-124">`options.encoding` specifies hello encoding toouse when reading hello file.</span></span> <span data-ttu-id="f7454-125">es el valor predeterminado de Hello **UTF-8**y se usa solo cuando `options.openMode` se establece demasiado**texto**.</span><span class="sxs-lookup"><span data-stu-id="f7454-125">hello default value is **UTF-8**, and is used only when `options.openMode` is set too**text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f7454-126">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f7454-126">Sample output</span></span>
<span data-ttu-id="f7454-127">Si options.multiple es false y options.uploadMode es el archivo, el resultado incluye contenido de Hola de archivo hello como una cadena JSON:</span><span class="sxs-lookup"><span data-stu-id="f7454-127">If options.multiple is false and options.uploadMode is file, then the output contains hello contents of hello file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="f7454-128">Si es true options.multiple and'options.uploadMode es archivo, entonces la salida contiene contenido de Hola de los archivos de hello como una matriz JSON:</span><span class="sxs-lookup"><span data-stu-id="f7454-128">If options.multiple is true and\`options.uploadMode is file, then the output contains hello contents of hello files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="f7454-129">Si options.multiple es false y options.uploadMode es url, la salida incluye una dirección URL como una cadena JSON:</span><span class="sxs-lookup"><span data-stu-id="f7454-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="f7454-130">Si options.multiple es true y options.uploadMode es url, la salida incluye una lista de direcciones URL como una matriz JSON:</span><span class="sxs-lookup"><span data-stu-id="f7454-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="f7454-131">Cuando se prueba un CreateUiDefinition, algunos exploradores (por ejemplo, Google Chrome) truncan las direcciones URL generadas por hello Microsoft.Common.FileUpload elemento en la consola del explorador Hola.</span><span class="sxs-lookup"><span data-stu-id="f7454-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by hello Microsoft.Common.FileUpload element in hello browser console.</span></span> <span data-ttu-id="f7454-132">Puede que necesite tooright y haga clic en vínculos individuales toocopy hello las direcciones URL completas.</span><span class="sxs-lookup"><span data-stu-id="f7454-132">You may need tooright-click individual links toocopy hello full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f7454-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f7454-133">Next steps</span></span>
* <span data-ttu-id="f7454-134">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7454-134">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f7454-135">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7454-135">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f7454-136">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f7454-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
