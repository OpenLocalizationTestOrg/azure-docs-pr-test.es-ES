---
title: "Elemento de interfaz de usuario Section de una aplicación administrada de Azure | Microsoft Docs"
description: Describe el elemento de la interfaz de usuario Microsoft.Common.Section para aplicaciones administradas de Azure
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
ms.openlocfilehash: 34c0f2f88e6af5a0f822ec116e7e2334e4e29e8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="6dd6a-103">Elemento de interfaz de usuario Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="6dd6a-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="6dd6a-104">Control que agrupa uno o varios elementos en un encabezado.</span><span class="sxs-lookup"><span data-stu-id="6dd6a-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="6dd6a-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="6dd6a-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6dd6a-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="6dd6a-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="6dd6a-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="6dd6a-108">Schema</span></span>
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Some section",
  "elements": [
    {
      "name": "element1",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 1"
    },
    {
      "name": "element2",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="6dd6a-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="6dd6a-109">Remarks</span></span>
- <span data-ttu-id="6dd6a-110">`elements` debe contener al menos un elemento, y puede contener todos los tipos de elementos excepto `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="6dd6a-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="6dd6a-111">Este elemento no admite la propiedad `toolTip`.</span><span class="sxs-lookup"><span data-stu-id="6dd6a-111">This element doesn't support the `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6dd6a-112">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6dd6a-112">Sample output</span></span>
<span data-ttu-id="6dd6a-113">Para obtener acceso a los valores de salida de los elementos en `elements`, use las funciones [basics()](managed-application-createuidefinition-functions.md#basics) o [steps()](managed-application-createuidefinition-functions.md#steps) y la notación de puntos:</span><span class="sxs-lookup"><span data-stu-id="6dd6a-113">To access the output values of elements in `elements`, use the [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="6dd6a-114">Los elementos del tipo `Microsoft.Common.Section` no tienen valores de salida por sí mismos.</span><span class="sxs-lookup"><span data-stu-id="6dd6a-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dd6a-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6dd6a-115">Next steps</span></span>
* <span data-ttu-id="6dd6a-116">Para una introducción a las aplicaciones administradas, consulte la [introducción a las aplicaciones administradas de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6dd6a-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6dd6a-117">Para ver una introducción sobre la creación de definiciones de interfaz de usuario, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6dd6a-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="6dd6a-118">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6dd6a-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
