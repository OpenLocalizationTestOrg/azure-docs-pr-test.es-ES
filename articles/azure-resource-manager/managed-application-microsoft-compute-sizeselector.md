---
title: "Elemento de interfaz de usuario SizeSelector de una aplicación administrada de Azure | Microsoft Docs"
description: Describe el elemento de la interfaz de usuario Microsoft.Compute.SizeSelector para aplicaciones administradas de Azure
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
ms.openlocfilehash: e54962f73028ada258a7faef271d66f0fbcef649
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="76110-103">Elemento de interfaz de usuario Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="76110-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="76110-104">Control para seleccionar un tamaño para una o varias instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76110-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="76110-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="76110-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="76110-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="76110-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="76110-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="76110-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="76110-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="76110-109">Remarks</span></span>
- <span data-ttu-id="76110-110">`recommendedSizes` debe contener al menos un tamaño.</span><span class="sxs-lookup"><span data-stu-id="76110-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="76110-111">El primer tamaño recomendado se utiliza como valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="76110-111">The first recommended size is used as the default.</span></span>
- <span data-ttu-id="76110-112">Si no hay un tamaño recomendado en la ubicación seleccionada, el tamaño se omite automáticamente.</span><span class="sxs-lookup"><span data-stu-id="76110-112">If a recommended size is not available in the selected location, the size is automatically skipped.</span></span> <span data-ttu-id="76110-113">En su lugar, se utiliza el siguiente tamaño recomendado.</span><span class="sxs-lookup"><span data-stu-id="76110-113">Instead, the next recommended size is used.</span></span>
- <span data-ttu-id="76110-114">Los tipos no especificados en `constraints.allowedSizes` se ocultan, mientras que los tipos no especificados en `constraints.excludedSizes` se muestran.</span><span class="sxs-lookup"><span data-stu-id="76110-114">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="76110-115">Tanto `constraints.allowedSizes` como `constraints.excludedSizes` son opcionales, pero no se pueden usar simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="76110-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="76110-116">Para determinar la lista de los tamaños disponibles, consulte la [lista de tamaños de máquina virtual disponibles para una suscripción](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="76110-116">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="76110-117">`osPlatform` debe especificarse y puede ser **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="76110-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="76110-118">Se usa para determinar los costos de hardware de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="76110-118">It's used to determine the hardware costs of the virtual machines.</span></span>
- <span data-ttu-id="76110-119">`imageReference` se omite para las imágenes propias, pero se proporciona para las imágenes de terceros.</span><span class="sxs-lookup"><span data-stu-id="76110-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="76110-120">Se usa para determinar los costos de software de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="76110-120">It's used to determine the software costs of the virtual machines.</span></span>
- <span data-ttu-id="76110-121">`count` se usa para establecer el multiplicador apropiado para el elemento.</span><span class="sxs-lookup"><span data-stu-id="76110-121">`count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="76110-122">Admite un valor estático, como **2**, o un valor dinámico de otro elemento, como `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="76110-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="76110-123">El valor predeterminado es **1**.</span><span class="sxs-lookup"><span data-stu-id="76110-123">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="76110-124">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="76110-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="76110-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76110-125">Next steps</span></span>
* <span data-ttu-id="76110-126">Para una introducción a las aplicaciones administradas, consulte la [introducción a las aplicaciones administradas de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76110-126">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="76110-127">Para ver una introducción sobre la creación de definiciones de interfaz de usuario, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76110-127">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="76110-128">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="76110-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
