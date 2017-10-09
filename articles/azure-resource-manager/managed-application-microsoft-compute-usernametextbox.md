---
title: "elemento de interfaz de usuario de UserNameTextBox de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Compute.UserNameTextBox para administrar aplicaciones de Azure
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="d49e7-103">Elemento de interfaz de usuario Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="d49e7-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="d49e7-104">Control de cuadro de texto con validación integrada para nombres de usuario de Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="d49e7-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="d49e7-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="d49e7-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d49e7-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="d49e7-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="d49e7-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="d49e7-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="d49e7-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="d49e7-109">Remarks</span></span>
- <span data-ttu-id="d49e7-110">Si `constraints.required` se establece demasiado**true**, cuadro de texto hello debe contener un valor toovalidate correctamente.</span><span class="sxs-lookup"><span data-stu-id="d49e7-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="d49e7-111">es el valor predeterminado de Hello **true**.</span><span class="sxs-lookup"><span data-stu-id="d49e7-111">hello default value is **true**.</span></span>
- <span data-ttu-id="d49e7-112">`osPlatform` debe especificarse y puede ser **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="d49e7-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="d49e7-113">`constraints.regex` es un patrón de expresión regular de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d49e7-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="d49e7-114">Si se especifica, a continuación, valor del cuadro de texto hello debe coincidir con hello patrón toovalidate correctamente.</span><span class="sxs-lookup"><span data-stu-id="d49e7-114">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="d49e7-115">El valor predeterminado es **null**.</span><span class="sxs-lookup"><span data-stu-id="d49e7-115">The default value is **null**.</span></span>
- <span data-ttu-id="d49e7-116">`constraints.validationMessage`es una cadena toodisplay al valor del cuadro de texto hello no supera la validación de hello especificado por `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="d49e7-116">`constraints.validationMessage` is a string toodisplay when hello text box's value fails hello validation specified by `constraints.regex`.</span></span> <span data-ttu-id="d49e7-117">Si no se especifica, Hola se utilizan mensajes de validación integradas del cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="d49e7-117">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="d49e7-118">es el valor predeterminado de Hello **null**.</span><span class="sxs-lookup"><span data-stu-id="d49e7-118">hello default value is **null**.</span></span>
- <span data-ttu-id="d49e7-119">Este elemento tiene validación integrada que se basa en el valor de hello especificado para `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="d49e7-119">This element has built-in validation that is based on hello value specified for `osPlatform`.</span></span> <span data-ttu-id="d49e7-120">validación integradas Hola puede usarse junto con una expresión regular personalizada.</span><span class="sxs-lookup"><span data-stu-id="d49e7-120">hello built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="d49e7-121">Si un valor para `constraints.regex` se especifica, ambos Hola integrados y se activan las validaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="d49e7-121">If a value for `constraints.regex` is specified, then both hello built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="d49e7-122">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d49e7-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="d49e7-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d49e7-123">Next steps</span></span>
* <span data-ttu-id="d49e7-124">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d49e7-124">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d49e7-125">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d49e7-125">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="d49e7-126">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="d49e7-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
