---
title: "elemento de interfaz de usuario de lista desplegable de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Common.DropDown para administrar aplicaciones de Azure
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="95c6a-103">Elemento de interfaz de usuario Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="95c6a-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="95c6a-104">Control de selección con una lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="95c6a-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="95c6a-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="95c6a-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="95c6a-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="95c6a-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="95c6a-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="95c6a-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="95c6a-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="95c6a-109">Remarks</span></span>
- <span data-ttu-id="95c6a-110">etiqueta de Hola para `constraints.allowedValues` es Hola texto para mostrar de un elemento y su valor es el valor de salida de hello de elemento de hello cuando se selecciona.</span><span class="sxs-lookup"><span data-stu-id="95c6a-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="95c6a-111">Si se especifica, valor predeterminado de hello debe ser una etiqueta presente en `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="95c6a-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="95c6a-112">Si no se especifica, Hola el primer elemento de `constraints.allowedValues` está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="95c6a-112">If not specified, hello first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="95c6a-113">es el valor predeterminado de Hello **null**.</span><span class="sxs-lookup"><span data-stu-id="95c6a-113">hello default value is **null**.</span></span>
- <span data-ttu-id="95c6a-114">`constraints.allowedValues` debe contener al menos un dígito.</span><span class="sxs-lookup"><span data-stu-id="95c6a-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="95c6a-115">Este elemento no es compatible con hello `constraints.required` propiedad.</span><span class="sxs-lookup"><span data-stu-id="95c6a-115">This element doesn't support hello `constraints.required` property.</span></span> <span data-ttu-id="95c6a-116">tooemulate este comportamiento, agregue un elemento con una etiqueta y el valor de `""` (cadena vacía) demasiado`constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="95c6a-116">tooemulate this behavior, add an item with a label and value of `""` (empty string) too`constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="95c6a-117">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="95c6a-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="95c6a-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95c6a-118">Next steps</span></span>
* <span data-ttu-id="95c6a-119">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95c6a-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="95c6a-120">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95c6a-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="95c6a-121">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="95c6a-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
