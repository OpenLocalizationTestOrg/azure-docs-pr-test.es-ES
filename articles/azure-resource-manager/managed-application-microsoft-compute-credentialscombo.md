---
title: "elemento de interfaz de usuario de CredentialsCombo de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Compute.CredentialsCombo para administrar aplicaciones de Azure
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="5ccdf-103">Elemento de interfaz de usuario Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="5ccdf-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="5ccdf-104">Grupo de controles con validación integrada para las contraseñas de Windows y Linux, y las claves públicas de SSH.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="5ccdf-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5ccdf-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5ccdf-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="5ccdf-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="5ccdf-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="5ccdf-108">Schema</span></span>
<span data-ttu-id="5ccdf-109">Si `osPlatform` es **Windows**, hello esquema siguiente se utiliza:</span><span class="sxs-lookup"><span data-stu-id="5ccdf-109">If `osPlatform` is **Windows**, then hello following schema is used:</span></span>
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="5ccdf-110">Si `osPlatform` es **Linux**, hello esquema siguiente se utiliza:</span><span class="sxs-lookup"><span data-stu-id="5ccdf-110">If `osPlatform` is **Linux**, then hello following schema is used:</span></span>
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="5ccdf-111">Comentarios</span><span class="sxs-lookup"><span data-stu-id="5ccdf-111">Remarks</span></span>
- <span data-ttu-id="5ccdf-112">`osPlatform` debe especificarse y puede ser **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="5ccdf-113">Si `constraints.required` se establece demasiado**true**, a continuación, Hola contraseña o cuadros de texto de la clave pública SSH deben contener valores toovalidate correctamente.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-113">If `constraints.required` is set too**true**, then hello password or SSH public key text boxes must contain values toovalidate successfully.</span></span> <span data-ttu-id="5ccdf-114">es el valor predeterminado de Hello **true**.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-114">hello default value is **true**.</span></span>
- <span data-ttu-id="5ccdf-115">Si `options.hideConfirmation` se establece demasiado**true**, a continuación, se oculta el segundo cuadro de texto hello para confirmar la contraseña del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-115">If `options.hideConfirmation` is set too**true**, then hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="5ccdf-116">es el valor predeterminado de Hello **false**.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-116">hello default value is **false**.</span></span>
- <span data-ttu-id="5ccdf-117">Si `options.hidePassword` se establece demasiado**true**, a continuación, la autenticación de contraseña de hello opción toouse está oculto.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-117">If `options.hidePassword` is set too**true**, then hello option toouse password authentication is hidden.</span></span> <span data-ttu-id="5ccdf-118">Se puede utilizar solo cuando `osPlatform` es **Linux**.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="5ccdf-119">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-119">The default value is **false**.</span></span>
- <span data-ttu-id="5ccdf-120">Las restricciones adicionales en hello permiten contraseñas pueden implementarse mediante hello `customPasswordRegex` propiedad.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-120">Additional constraints on hello allowed passwords can be implemented by using hello `customPasswordRegex` property.</span></span> <span data-ttu-id="5ccdf-121">Hola cadena en `customValidationMessage` se muestra cuando una contraseña se produce un error de validación personalizada.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-121">hello string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="5ccdf-122">Hello valor predeterminado para ambas propiedades es **null**.</span><span class="sxs-lookup"><span data-stu-id="5ccdf-122">hello default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5ccdf-123">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5ccdf-123">Sample output</span></span>
<span data-ttu-id="5ccdf-124">Si `osPlatform` es **Windows**, o una contraseña en lugar de una clave pública SSH proporcionado por el usuario de hello, hello se espera resultado siguiente:</span><span class="sxs-lookup"><span data-stu-id="5ccdf-124">If `osPlatform` is **Windows**, or hello user provided a password instead of an SSH public key, then hello following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="5ccdf-125">Si una clave pública SSH había proporcionado por el usuario de hello, a continuación, hello se espera resultado siguiente:</span><span class="sxs-lookup"><span data-stu-id="5ccdf-125">If hello user provided an SSH public key, then hello following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="5ccdf-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5ccdf-126">Next steps</span></span>
* <span data-ttu-id="5ccdf-127">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ccdf-127">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5ccdf-128">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ccdf-128">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5ccdf-129">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="5ccdf-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
