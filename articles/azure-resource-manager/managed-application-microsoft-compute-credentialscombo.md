---
title: "Elemento de interfaz de usuario CredentialsCombo de una aplicación administrada de Azure | Microsoft Docs"
description: Describe el elemento de la interfaz de usuario Microsoft.Compute.CredentialsCombo para aplicaciones administradas de Azure
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
ms.openlocfilehash: 254f383ee6f7cb9f7051fa135d85319a22c3c369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="1d4b7-103">Elemento de interfaz de usuario Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="1d4b7-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="1d4b7-104">Grupo de controles con validación integrada para las contraseñas de Windows y Linux, y las claves públicas de SSH.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="1d4b7-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b7-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="1d4b7-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="1d4b7-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="1d4b7-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="1d4b7-108">Schema</span></span>
<span data-ttu-id="1d4b7-109">Si `osPlatform` es **Windows**, se utiliza el siguiente esquema:</span><span class="sxs-lookup"><span data-stu-id="1d4b7-109">If `osPlatform` is **Windows**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="1d4b7-110">Si `osPlatform` es **Linux**, se utiliza el siguiente esquema:</span><span class="sxs-lookup"><span data-stu-id="1d4b7-110">If `osPlatform` is **Linux**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="1d4b7-111">Comentarios</span><span class="sxs-lookup"><span data-stu-id="1d4b7-111">Remarks</span></span>
- <span data-ttu-id="1d4b7-112">`osPlatform` debe especificarse y puede ser **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="1d4b7-113">Si `constraints.required` está establecido en **true**, los cuadros de texto de clave pública SSH o contraseña deben contener valores para que la validación sea correcta.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-113">If `constraints.required` is set to **true**, then the password or SSH public key text boxes must contain values to validate successfully.</span></span> <span data-ttu-id="1d4b7-114">El valor predeterminado es **true**.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-114">The default value is **true**.</span></span>
- <span data-ttu-id="1d4b7-115">Si `options.hideConfirmation` está establecido en **true**, se oculta el segundo cuadro de texto para confirmar la contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-115">If `options.hideConfirmation` is set to **true**, then the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="1d4b7-116">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-116">The default value is **false**.</span></span>
- <span data-ttu-id="1d4b7-117">Si `options.hidePassword` está establecido en **true**, se oculta la opción para utilizar la autenticación de contraseña.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-117">If `options.hidePassword` is set to **true**, then the option to use password authentication is hidden.</span></span> <span data-ttu-id="1d4b7-118">Se puede utilizar solo cuando `osPlatform` es **Linux**.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="1d4b7-119">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-119">The default value is **false**.</span></span>
- <span data-ttu-id="1d4b7-120">Se pueden implementar restricciones adicionales en las contraseñas permitidas con la propiedad `customPasswordRegex`.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-120">Additional constraints on the allowed passwords can be implemented by using the `customPasswordRegex` property.</span></span> <span data-ttu-id="1d4b7-121">La cadena de `customValidationMessage` se muestra cuando se produce un error de validación personalizada en una contraseña.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-121">The string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="1d4b7-122">El valor predeterminado para ambas propiedades es **null**.</span><span class="sxs-lookup"><span data-stu-id="1d4b7-122">The default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="1d4b7-123">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1d4b7-123">Sample output</span></span>
<span data-ttu-id="1d4b7-124">Si `osPlatform` es **Windows**, o el usuario proporcionó una contraseña en lugar de una clave pública SSH, se espera la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="1d4b7-124">If `osPlatform` is **Windows**, or the user provided a password instead of an SSH public key, then the following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="1d4b7-125">Si el usuario proporcionó una clave pública SSH, se espera la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="1d4b7-125">If the user provided an SSH public key, then the following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="1d4b7-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d4b7-126">Next steps</span></span>
* <span data-ttu-id="1d4b7-127">Para una introducción a las aplicaciones administradas, consulte la [introducción a las aplicaciones administradas de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b7-127">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="1d4b7-128">Para ver una introducción sobre la creación de definiciones de interfaz de usuario, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b7-128">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="1d4b7-129">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="1d4b7-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
