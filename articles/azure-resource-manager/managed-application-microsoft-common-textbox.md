---
title: "elemento de interfaz de usuario de cuadro de texto de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Common.TextBox para administrar aplicaciones de Azure
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="0cf0c-103">Elemento de interfaz de usuario Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="0cf0c-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="0cf0c-104">Un control que puede ser utilizado tooedit texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-104">A control that can be used tooedit unformatted text.</span></span> <span data-ttu-id="0cf0c-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="0cf0c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="0cf0c-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="0cf0c-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="0cf0c-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="0cf0c-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="0cf0c-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="0cf0c-109">Remarks</span></span>
- <span data-ttu-id="0cf0c-110">Si `constraints.required` se establece demasiado**true**, cuadro de texto hello debe contener un valor toovalidate correctamente.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="0cf0c-111">es el valor predeterminado de Hello **false**.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-111">hello default value is **false**.</span></span>
- <span data-ttu-id="0cf0c-112">`constraints.regex` es un patrón de expresión regular de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="0cf0c-113">Si se especifica, a continuación, valor del cuadro de texto hello debe coincidir con hello patrón toovalidate correctamente.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-113">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="0cf0c-114">El valor predeterminado es **null**.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-114">The default value is **null**.</span></span>
- <span data-ttu-id="0cf0c-115">`constraints.validationMessage`es una cadena toodisplay al valor del cuadro de texto hello no puede validarse.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-115">`constraints.validationMessage` is a string toodisplay when hello text box's value fails validation.</span></span> <span data-ttu-id="0cf0c-116">Si no se especifica, Hola se utilizan mensajes de validación integradas del cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-116">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="0cf0c-117">es el valor predeterminado de Hello **null**.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-117">hello default value is **null**.</span></span>
- <span data-ttu-id="0cf0c-118">Es posible toospecify un valor para `constraints.regex` cuando `constraints.required` se establece demasiado**false**.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-118">It's possible toospecify a value for `constraints.regex` when `constraints.required` is set too**false**.</span></span> <span data-ttu-id="0cf0c-119">En este escenario, un valor no es necesario para toovalidate de cuadro de texto hello correctamente.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-119">In this scenario, a value is not required for hello text box toovalidate successfully.</span></span> <span data-ttu-id="0cf0c-120">Si se especifica uno, debe coincidir con el patrón de expresión regular de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cf0c-120">If one is specified, it must match hello regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="0cf0c-121">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0cf0c-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="0cf0c-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0cf0c-122">Next steps</span></span>
* <span data-ttu-id="0cf0c-123">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cf0c-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="0cf0c-124">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cf0c-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="0cf0c-125">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="0cf0c-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
