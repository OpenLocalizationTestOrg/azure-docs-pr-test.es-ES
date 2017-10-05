---
title: "Elemento de interfaz de usuario DropDown de una aplicación administrada de Azure | Microsoft Docs"
description: Describe el elemento de la interfaz de usuario Microsoft.Common.DropDown para aplicaciones administradas de Azure
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
ms.openlocfilehash: a769e14efbae928b811fa1f1b1c2d4fba3c7692b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="503a7-103">Elemento de interfaz de usuario Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="503a7-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="503a7-104">Control de selección con una lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="503a7-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="503a7-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="503a7-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="503a7-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="503a7-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="503a7-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="503a7-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
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

## <a name="remarks"></a><span data-ttu-id="503a7-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="503a7-109">Remarks</span></span>
- <span data-ttu-id="503a7-110">La etiqueta de `constraints.allowedValues` es el texto para mostrar de un elemento, y su valor es el valor de salida del elemento cuando se selecciona.</span><span class="sxs-lookup"><span data-stu-id="503a7-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="503a7-111">Si se especifica, el valor predeterminado debe ser una etiqueta presente en `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="503a7-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="503a7-112">Si no se especifica, se selecciona el primer elemento de `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="503a7-112">If not specified, the first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="503a7-113">El valor predeterminado es **null**.</span><span class="sxs-lookup"><span data-stu-id="503a7-113">The default value is **null**.</span></span>
- <span data-ttu-id="503a7-114">`constraints.allowedValues` debe contener al menos un dígito.</span><span class="sxs-lookup"><span data-stu-id="503a7-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="503a7-115">Este elemento no admite la propiedad `constraints.required`.</span><span class="sxs-lookup"><span data-stu-id="503a7-115">This element doesn't support the `constraints.required` property.</span></span> <span data-ttu-id="503a7-116">Para emular este comportamiento, agregue un elemento con una etiqueta y el valor `""` (cadena vacía) a `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="503a7-116">To emulate this behavior, add an item with a label and value of `""` (empty string) to `constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="503a7-117">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="503a7-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="503a7-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="503a7-118">Next steps</span></span>
* <span data-ttu-id="503a7-119">Para una introducción a las aplicaciones administradas, consulte la [introducción a las aplicaciones administradas de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="503a7-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="503a7-120">Para ver una introducción sobre la creación de definiciones de interfaz de usuario, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="503a7-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="503a7-121">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="503a7-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
