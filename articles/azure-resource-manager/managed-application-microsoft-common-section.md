---
title: "elemento de interfaz de usuario de sección de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Common.Section para administrar aplicaciones de Azure
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
ms.openlocfilehash: d20b365b12fab66177e1a12db2ebbeefe507212e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="ff38e-103">Elemento de interfaz de usuario Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="ff38e-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="ff38e-104">Control que agrupa uno o varios elementos en un encabezado.</span><span class="sxs-lookup"><span data-stu-id="ff38e-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="ff38e-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ff38e-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="ff38e-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="ff38e-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="ff38e-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="ff38e-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="ff38e-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="ff38e-109">Remarks</span></span>
- <span data-ttu-id="ff38e-110">`elements` debe contener al menos un elemento, y puede contener todos los tipos de elementos excepto `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="ff38e-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="ff38e-111">Este elemento no es compatible con hello `toolTip` propiedad.</span><span class="sxs-lookup"><span data-stu-id="ff38e-111">This element doesn't support hello `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="ff38e-112">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ff38e-112">Sample output</span></span>
<span data-ttu-id="ff38e-113">valores de elementos de salida de hello tooaccess `elements`, usar hello [basics()](managed-application-createuidefinition-functions.md#basics) o [steps()](managed-application-createuidefinition-functions.md#steps) funciones y la notación de puntos:</span><span class="sxs-lookup"><span data-stu-id="ff38e-113">tooaccess hello output values of elements in `elements`, use hello [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="ff38e-114">Los elementos del tipo `Microsoft.Common.Section` no tienen valores de salida por sí mismos.</span><span class="sxs-lookup"><span data-stu-id="ff38e-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff38e-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ff38e-115">Next steps</span></span>
* <span data-ttu-id="ff38e-116">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff38e-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="ff38e-117">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff38e-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="ff38e-118">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="ff38e-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
