---
title: "Elemento de interfaz de usuario PasswordBox de una aplicación administrada de Azure | Microsoft Docs"
description: Describe el elemento de la interfaz de usuario Microsoft.Common.PasswordBox para aplicaciones administradas de Azure
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
ms.openlocfilehash: 196a4b8f77145f83e46b4b23e148bb3a9dffc1b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="5b997-103">Elemento de interfaz de usuario Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="5b997-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="5b997-104">Control que puede usarse para proporcionar una contraseña y confirmarla.</span><span class="sxs-lookup"><span data-stu-id="5b997-104">A control that can be used to provide and confirm a password.</span></span> <span data-ttu-id="5b997-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5b997-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5b997-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="5b997-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="5b997-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="5b997-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="5b997-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="5b997-109">Remarks</span></span>
- <span data-ttu-id="5b997-110">Este elemento no admite la propiedad `defaultValue`.</span><span class="sxs-lookup"><span data-stu-id="5b997-110">This element doesn't support the `defaultValue` property.</span></span>
- <span data-ttu-id="5b997-111">Para más detalles sobre la implementación de `constraints`, consulte [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="5b997-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="5b997-112">Si `options.hideConfirmation` está establecido en **true**, se oculta el segundo cuadro de texto para confirmar la contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="5b997-112">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="5b997-113">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="5b997-113">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5b997-114">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5b997-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="5b997-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b997-115">Next steps</span></span>
* <span data-ttu-id="5b997-116">Para una introducción a las aplicaciones administradas, consulte la [introducción a las aplicaciones administradas de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b997-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5b997-117">Para ver una introducción sobre la creación de definiciones de interfaz de usuario, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b997-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5b997-118">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="5b997-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
