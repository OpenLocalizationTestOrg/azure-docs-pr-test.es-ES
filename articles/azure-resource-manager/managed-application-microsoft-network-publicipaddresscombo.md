---
title: "Elemento de interfaz de usuario PublicIpAddressCombo de una aplicación administrada de Azure | Microsoft Docs"
description: Describe el elemento de la interfaz de usuario Microsoft.Network.PublicIpAddressCombo para aplicaciones administradas de Azure
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
ms.openlocfilehash: 2eb773f5f0cf389fc39bc3a0f5fbf9ac726d1949
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="d82ab-103">Elemento de interfaz de usuario Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="d82ab-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="d82ab-104">Grupo de controles para seleccionar una dirección IP pública nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="d82ab-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="d82ab-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="d82ab-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d82ab-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="d82ab-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="d82ab-108">Si el usuario selecciona “None” para la dirección IP pública, se oculta el cuadro de texto de la etiqueta de nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="d82ab-108">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span></span>
- <span data-ttu-id="d82ab-109">Si el usuario selecciona una dirección IP pública, se deshabilita el cuadro de texto de la etiqueta de nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="d82ab-109">If the user selects an existing public IP address, the domain name label text box is disabled.</span></span> <span data-ttu-id="d82ab-110">Su valor es la etiqueta de nombre de dominio de la dirección IP seleccionada.</span><span class="sxs-lookup"><span data-stu-id="d82ab-110">Its value is the domain name label of the selected IP address.</span></span>
- <span data-ttu-id="d82ab-111">El sufijo de nombre de dominio (por ejemplo, westus.cloudapp.azure.com) se actualiza automáticamente en función de la ubicación seleccionada.</span><span class="sxs-lookup"><span data-stu-id="d82ab-111">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="d82ab-112">Esquema</span><span class="sxs-lookup"><span data-stu-id="d82ab-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="d82ab-113">Comentarios</span><span class="sxs-lookup"><span data-stu-id="d82ab-113">Remarks</span></span>
- <span data-ttu-id="d82ab-114">Si `constraints.required.domainNameLabel` está establecido en **true**, el usuario debe proporcionar una etiqueta de nombre de dominio al crear una dirección IP pública nueva.</span><span class="sxs-lookup"><span data-stu-id="d82ab-114">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="d82ab-115">Las direcciones IP públicas existentes sin una etiqueta no están disponibles para la selección.</span><span class="sxs-lookup"><span data-stu-id="d82ab-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="d82ab-116">Si `options.hideNone` está establecido en **true**, la opción para seleccionar **None** como dirección IP pública está oculta.</span><span class="sxs-lookup"><span data-stu-id="d82ab-116">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span></span> <span data-ttu-id="d82ab-117">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="d82ab-117">The default value is **false**.</span></span>
- <span data-ttu-id="d82ab-118">Si `options.hideDomainNameLabel` está establecido en **true**, se oculta el cuadro de texto de la etiqueta de nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="d82ab-118">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span></span> <span data-ttu-id="d82ab-119">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="d82ab-119">The default value is **false**.</span></span>
- <span data-ttu-id="d82ab-120">Si `options.hideExisting` es true, el usuario no puede elegir una dirección IP pública existente.</span><span class="sxs-lookup"><span data-stu-id="d82ab-120">If `options.hideExisting` is true, then the user is not able to choose an existing public IP address.</span></span> <span data-ttu-id="d82ab-121">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="d82ab-121">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="d82ab-122">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d82ab-122">Sample output</span></span>
<span data-ttu-id="d82ab-123">Si el usuario no selecciona ninguna dirección IP pública, se espera la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="d82ab-123">If the user selects no public IP address, the following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="d82ab-124">Si el usuario selecciona una dirección IP pública nueva o existente, se espera la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="d82ab-124">If the user selects a new or existing IP address, the following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="d82ab-125">Cuando se especifica `options.hideNone`, `newOrExistingOrNone` siempre devuelve **none**.</span><span class="sxs-lookup"><span data-stu-id="d82ab-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="d82ab-126">Cuando se especifica `options.hideDomainNameLabel`, `domainNameLabel` no se declara.</span><span class="sxs-lookup"><span data-stu-id="d82ab-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d82ab-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d82ab-127">Next steps</span></span>
* <span data-ttu-id="d82ab-128">Para una introducción a las aplicaciones administradas, consulte la [introducción a las aplicaciones administradas de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d82ab-128">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d82ab-129">Para ver una introducción sobre la creación de definiciones de interfaz de usuario, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d82ab-129">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="d82ab-130">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="d82ab-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
