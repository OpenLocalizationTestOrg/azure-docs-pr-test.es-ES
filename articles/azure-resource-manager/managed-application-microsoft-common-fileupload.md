---
title: "Elemento de interfaz de usuario FileUpload de una aplicación administrada de Azure | Microsoft Docs"
description: Describe el elemento de la interfaz de usuario Microsoft.Common.FileUpload para aplicaciones administradas de Azure
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
ms.openlocfilehash: 217e9e63eb7cd198f70cee42b418867df9f1f993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="8bf7e-103">Elemento de interfaz de usuario Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="8bf7e-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="8bf7e-104">Control que permite al usuario especificar uno o varios archivos para cargar.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-104">A control that allows a user to specify one or more files to upload.</span></span> <span data-ttu-id="8bf7e-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8bf7e-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="8bf7e-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="8bf7e-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="8bf7e-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="8bf7e-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="8bf7e-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="8bf7e-109">Remarks</span></span>
- <span data-ttu-id="8bf7e-110">`constraints.accept` especifica los tipos de archivos que se muestran en el cuadro de diálogo de archivo del explorador.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-110">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span></span> <span data-ttu-id="8bf7e-111">Consulte la [especificación HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) para ver los valores permitidos.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-111">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="8bf7e-112">El valor predeterminado es **null**.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-112">The default value is **null**.</span></span>
- <span data-ttu-id="8bf7e-113">Si `options.multiple` se establece en **true**, el usuario puede seleccionar más de un archivo en el cuadro de diálogo del explorador.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-113">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span></span> <span data-ttu-id="8bf7e-114">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-114">The default value is **false**.</span></span>
- <span data-ttu-id="8bf7e-115">Este elemento permite cargar archivos de dos modos, en función del valor de `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-115">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span></span> <span data-ttu-id="8bf7e-116">Si se especifica **file**, la salida incluye el contenido del archivo como un blob.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-116">If **file** is specified, the output contains the contents of the file as a blob.</span></span> <span data-ttu-id="8bf7e-117">Si se especifica **url**, el archivo se carga en una ubicación temporal y la salida contiene la dirección URL del blob.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-117">If **url** is specified, then the file is uploaded to a temporary location, and the output contains the URL of the blob.</span></span> <span data-ttu-id="8bf7e-118">Los blobs temporales se eliminan después de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="8bf7e-119">El valor predeterminado es **file**.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-119">The default value is **file**.</span></span>
- <span data-ttu-id="8bf7e-120">El valor de `options.openMode` determina cómo se lee el archivo.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-120">The value of `options.openMode` determines how the file is read.</span></span> <span data-ttu-id="8bf7e-121">Si se espera que el archivo sea de texto sin formato, especifique **text**; en caso contrario, especifique **binary**.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-121">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="8bf7e-122">El valor predeterminado es **text**.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-122">The default value is **text**.</span></span>
- <span data-ttu-id="8bf7e-123">Si `options.uploadMode` está establecido en **file** y `options.openMode` está establecido en **binary**, la salida estará codificada en base64.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-123">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span></span>
- <span data-ttu-id="8bf7e-124">`options.encoding` especifica la codificación que se utilizará al leer el archivo.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-124">`options.encoding` specifies the encoding to use when reading the file.</span></span> <span data-ttu-id="8bf7e-125">El valor predeterminado es **UTF-8**, y se usa solo cuando `options.openMode` está establecido en **text**.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-125">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="8bf7e-126">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8bf7e-126">Sample output</span></span>
<span data-ttu-id="8bf7e-127">Si options.multiple es false y options.uploadMode es file, la salida incluye el contenido del archivo como una cadena JSON:</span><span class="sxs-lookup"><span data-stu-id="8bf7e-127">If options.multiple is false and options.uploadMode is file, then the output contains the contents of the file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="8bf7e-128">Si options.multiple es true y options.uploadMode es file, la salida incluye el contenido del archivo como una matriz JSON:</span><span class="sxs-lookup"><span data-stu-id="8bf7e-128">If options.multiple is true and\`options.uploadMode is file, then the output contains the contents of the files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="8bf7e-129">Si options.multiple es false y options.uploadMode es url, la salida incluye una dirección URL como una cadena JSON:</span><span class="sxs-lookup"><span data-stu-id="8bf7e-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="8bf7e-130">Si options.multiple es true y options.uploadMode es url, la salida incluye una lista de direcciones URL como una matriz JSON:</span><span class="sxs-lookup"><span data-stu-id="8bf7e-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="8bf7e-131">Cuando se prueba una definición CreateUiDefinition, algunos exploradores (como Google Chrome) truncan las direcciones URL generadas por el elemento Microsoft.Common.FileUpload en la consola del explorador.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span></span> <span data-ttu-id="8bf7e-132">Puede que tenga que hacer clic en cada vínculo individual para copiar las direcciones URL completas.</span><span class="sxs-lookup"><span data-stu-id="8bf7e-132">You may need to right-click individual links to copy the full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8bf7e-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8bf7e-133">Next steps</span></span>
* <span data-ttu-id="8bf7e-134">Para una introducción a las aplicaciones administradas, consulte la [introducción a las aplicaciones administradas de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8bf7e-134">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8bf7e-135">Para ver una introducción sobre la creación de definiciones de interfaz de usuario, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8bf7e-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="8bf7e-136">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="8bf7e-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
