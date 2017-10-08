---
title: "elemento de interfaz de usuario de PasswordBox de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Common.PasswordBox para administrar aplicaciones de Azure
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
ms.openlocfilehash: bcb1f54c0bee464075ed732ead9aa3f88697f49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="cb495-103">Elemento de interfaz de usuario Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="cb495-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="cb495-104">Un control que puede ser usado tooprovide y confirme una contraseña.</span><span class="sxs-lookup"><span data-stu-id="cb495-104">A control that can be used tooprovide and confirm a password.</span></span> <span data-ttu-id="cb495-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="cb495-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="cb495-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="cb495-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="cb495-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="cb495-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="cb495-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="cb495-109">Remarks</span></span>
- <span data-ttu-id="cb495-110">Este elemento no es compatible con hello `defaultValue` propiedad.</span><span class="sxs-lookup"><span data-stu-id="cb495-110">This element doesn't support hello `defaultValue` property.</span></span>
- <span data-ttu-id="cb495-111">Para más detalles sobre la implementación de `constraints`, consulte [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="cb495-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="cb495-112">Si `options.hideConfirmation` se establece demasiado**true**, Hola segundo cuadro de texto Confirmar contraseña del usuario de hello está oculto.</span><span class="sxs-lookup"><span data-stu-id="cb495-112">If `options.hideConfirmation` is set too**true**, hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="cb495-113">es el valor predeterminado de Hello **false**.</span><span class="sxs-lookup"><span data-stu-id="cb495-113">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="cb495-114">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="cb495-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="cb495-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb495-115">Next steps</span></span>
* <span data-ttu-id="cb495-116">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cb495-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="cb495-117">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cb495-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="cb495-118">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="cb495-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
