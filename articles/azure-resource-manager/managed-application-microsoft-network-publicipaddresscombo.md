---
title: "elemento de interfaz de usuario de PublicIpAddressCombo de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Network.PublicIpAddressCombo para administrar aplicaciones de Azure
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="e0b9b-103">Elemento de interfaz de usuario Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="e0b9b-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="e0b9b-104">Grupo de controles para seleccionar una dirección IP pública nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="e0b9b-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e0b9b-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="e0b9b-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="e0b9b-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="e0b9b-108">Si el usuario de hello selecciona 'None' para la dirección IP pública, cuadro de texto de etiqueta de nombre de dominio de hello está oculto.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-108">If hello user selects 'None' for public IP address, hello domain name label text box is hidden.</span></span>
- <span data-ttu-id="e0b9b-109">Si el usuario de hello selecciona una dirección IP pública existente, cuadro de texto de etiqueta de nombre de dominio de hello está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-109">If hello user selects an existing public IP address, hello domain name label text box is disabled.</span></span> <span data-ttu-id="e0b9b-110">Su valor es la etiqueta de nombre de dominio de Hola de dirección IP de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-110">Its value is hello domain name label of hello selected IP address.</span></span>
- <span data-ttu-id="e0b9b-111">Hola automáticamente en función de la ubicación de hello selecciona las actualizaciones de sufijo (por ejemplo, westus.cloudapp.azure.com) de nombres de dominio.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-111">hello domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on hello selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="e0b9b-112">Esquema</span><span class="sxs-lookup"><span data-stu-id="e0b9b-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="e0b9b-113">Comentarios</span><span class="sxs-lookup"><span data-stu-id="e0b9b-113">Remarks</span></span>
- <span data-ttu-id="e0b9b-114">Si `constraints.required.domainNameLabel` se establece demasiado**true**, usuario de hello debe proporcionar una etiqueta de nombre de dominio al crear una nueva dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-114">If `constraints.required.domainNameLabel` is set too**true**, hello user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="e0b9b-115">Las direcciones IP públicas existentes sin una etiqueta no están disponibles para la selección.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="e0b9b-116">Si `options.hideNone` se establece demasiado**true**, Hola, a continuación, la opción tooselect **ninguno** para la dirección IP pública Hola dirección está oculto.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-116">If `options.hideNone` is set too**true**, then hello option tooselect **None** for hello public IP address is hidden.</span></span> <span data-ttu-id="e0b9b-117">es el valor predeterminado de Hello **false**.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-117">hello default value is **false**.</span></span>
- <span data-ttu-id="e0b9b-118">Si `options.hideDomainNameLabel` se establece demasiado**true**, a continuación, se oculta el cuadro de texto de hello para la etiqueta de nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-118">If `options.hideDomainNameLabel` is set too**true**, then hello text box for domain name label is hidden.</span></span> <span data-ttu-id="e0b9b-119">es el valor predeterminado de Hello **false**.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-119">hello default value is **false**.</span></span>
- <span data-ttu-id="e0b9b-120">Si `options.hideExisting` es true, el usuario hello no es capaz de toochoose una dirección IP pública existente.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-120">If `options.hideExisting` is true, then hello user is not able toochoose an existing public IP address.</span></span> <span data-ttu-id="e0b9b-121">es el valor predeterminado de Hello **false**.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-121">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="e0b9b-122">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e0b9b-122">Sample output</span></span>
<span data-ttu-id="e0b9b-123">Si el usuario de hello no selecciona ninguna dirección IP pública, hello se espera resultado siguiente:</span><span class="sxs-lookup"><span data-stu-id="e0b9b-123">If hello user selects no public IP address, hello following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="e0b9b-124">Si el usuario de hello selecciona una dirección IP nueva o existente, hello se espera resultado siguiente:</span><span class="sxs-lookup"><span data-stu-id="e0b9b-124">If hello user selects a new or existing IP address, hello following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="e0b9b-125">Cuando se especifica `options.hideNone`, `newOrExistingOrNone` siempre devuelve **none**.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="e0b9b-126">Cuando se especifica `options.hideDomainNameLabel`, `domainNameLabel` no se declara.</span><span class="sxs-lookup"><span data-stu-id="e0b9b-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0b9b-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e0b9b-127">Next steps</span></span>
* <span data-ttu-id="e0b9b-128">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0b9b-128">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="e0b9b-129">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0b9b-129">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="e0b9b-130">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="e0b9b-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
