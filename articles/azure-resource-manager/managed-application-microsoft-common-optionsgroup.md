---
title: "elemento de interfaz de usuario de grupo Opciones de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Common.OptionsGroup para administrar aplicaciones de Azure
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
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="4879f-103">Elemento de interfaz de usuario Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="4879f-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="4879f-104">Control de selección con una fila de opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="4879f-104">A selection control with a row of available options.</span></span> <span data-ttu-id="4879f-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="4879f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="4879f-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="4879f-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="4879f-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="4879f-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="4879f-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="4879f-109">Remarks</span></span>
- <span data-ttu-id="4879f-110">etiqueta de Hola para `constraints.allowedValues` es Hola texto para mostrar de un elemento y su valor es el valor de salida de hello de elemento de hello cuando se selecciona.</span><span class="sxs-lookup"><span data-stu-id="4879f-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="4879f-111">Si se especifica, valor predeterminado de hello debe ser una etiqueta presente en `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="4879f-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="4879f-112">Si no se especifica, Hola el primer elemento de `constraints.allowedValues` está activada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4879f-112">If not specified, hello first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="4879f-113">es el valor predeterminado de Hello **null**.</span><span class="sxs-lookup"><span data-stu-id="4879f-113">hello default value is **null**.</span></span>
- <span data-ttu-id="4879f-114">`constraints.allowedValues` debe contener al menos un dígito.</span><span class="sxs-lookup"><span data-stu-id="4879f-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="4879f-115">Este elemento no es compatible con hello `constraints.required` propiedad; un elemento debe ser toovalidate seleccionado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4879f-115">This element doesn't support hello `constraints.required` property; an item must be selected toovalidate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="4879f-116">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4879f-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="4879f-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4879f-117">Next steps</span></span>
* <span data-ttu-id="4879f-118">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4879f-118">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="4879f-119">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4879f-119">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="4879f-120">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="4879f-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
