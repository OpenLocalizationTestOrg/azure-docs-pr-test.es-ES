---
title: "Elemento de interfaz de usuario TextBox de una aplicación administrada de Azure | Microsoft Docs"
description: Describe el elemento de la interfaz de usuario Microsoft.Common.TextBox para aplicaciones administradas de Azure
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
ms.openlocfilehash: 5a0ac5b811812c8c03f7f63aae12b8699d248ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="b89c5-103">Elemento de interfaz de usuario Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="b89c5-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="b89c5-104">Control que puede usarse para editar texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="b89c5-104">A control that can be used to edit unformatted text.</span></span> <span data-ttu-id="b89c5-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="b89c5-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="b89c5-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="b89c5-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="b89c5-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="b89c5-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="b89c5-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="b89c5-109">Remarks</span></span>
- <span data-ttu-id="b89c5-110">Si `constraints.required` está establecido en **true**, el cuadro de texto debe contener un valor para que la validación sea correcta.</span><span class="sxs-lookup"><span data-stu-id="b89c5-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="b89c5-111">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="b89c5-111">The default value is **false**.</span></span>
- <span data-ttu-id="b89c5-112">`constraints.regex` es un patrón de expresión regular de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b89c5-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="b89c5-113">Si se especifica, el valor del cuadro de texto debe coincidir con el patrón para que la validación sea correcta.</span><span class="sxs-lookup"><span data-stu-id="b89c5-113">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="b89c5-114">El valor predeterminado es **null**.</span><span class="sxs-lookup"><span data-stu-id="b89c5-114">The default value is **null**.</span></span>
- <span data-ttu-id="b89c5-115">`constraints.validationMessage` es una cadena que se muestra cuando el valor del cuadro de texto produce un error de validación.</span><span class="sxs-lookup"><span data-stu-id="b89c5-115">`constraints.validationMessage` is a string to display when the text box's value fails validation.</span></span> <span data-ttu-id="b89c5-116">Si no se especifica, se utilizan los mensajes de validación integrados del cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="b89c5-116">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="b89c5-117">El valor predeterminado es **null**.</span><span class="sxs-lookup"><span data-stu-id="b89c5-117">The default value is **null**.</span></span>
- <span data-ttu-id="b89c5-118">Es posible especificar un valor para `constraints.regex` cuando `constraints.required` está establecido en **false**.</span><span class="sxs-lookup"><span data-stu-id="b89c5-118">It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**.</span></span> <span data-ttu-id="b89c5-119">En este escenario, no se requiere un valor para que la validación del cuadro de texto sea correcta.</span><span class="sxs-lookup"><span data-stu-id="b89c5-119">In this scenario, a value is not required for the text box to validate successfully.</span></span> <span data-ttu-id="b89c5-120">Si se especifica uno, debe coincidir con el patrón de expresión regular.</span><span class="sxs-lookup"><span data-stu-id="b89c5-120">If one is specified, it must match the regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="b89c5-121">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b89c5-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="b89c5-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b89c5-122">Next steps</span></span>
* <span data-ttu-id="b89c5-123">Para una introducción a las aplicaciones administradas, consulte la [introducción a las aplicaciones administradas de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b89c5-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="b89c5-124">Para ver una introducción sobre la creación de definiciones de interfaz de usuario, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b89c5-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="b89c5-125">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="b89c5-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
