---
title: "elemento de interfaz de usuario de SizeSelector de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Compute.SizeSelector para administrar aplicaciones de Azure
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="4a832-103">Elemento de interfaz de usuario Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="4a832-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="4a832-104">Control para seleccionar un tamaño para una o varias instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4a832-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="4a832-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="4a832-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="4a832-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="4a832-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="4a832-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="4a832-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="4a832-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="4a832-109">Remarks</span></span>
- <span data-ttu-id="4a832-110">`recommendedSizes` debe contener al menos un tamaño.</span><span class="sxs-lookup"><span data-stu-id="4a832-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="4a832-111">Hola primero recomienda tamaño se utiliza como valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a832-111">hello first recommended size is used as hello default.</span></span>
- <span data-ttu-id="4a832-112">Si no hay un tamaño recomendado en lugar de hello seleccionado, tamaño de Hola se omitirá automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4a832-112">If a recommended size is not available in hello selected location, hello size is automatically skipped.</span></span> <span data-ttu-id="4a832-113">En su lugar, hello tamaño recomendado siguiente se utiliza.</span><span class="sxs-lookup"><span data-stu-id="4a832-113">Instead, hello next recommended size is used.</span></span>
- <span data-ttu-id="4a832-114">Cualquier tamaño no se especifica en hello `constraints.allowedSizes` está oculto y de cualquier tamaño no se especifica en `constraints.excludedSizes` se muestra.</span><span class="sxs-lookup"><span data-stu-id="4a832-114">Any size not specified in hello `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="4a832-115">Tanto `constraints.allowedSizes` como `constraints.excludedSizes` son opcionales, pero no se pueden usar simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="4a832-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="4a832-116">lista de Hola de los tamaños disponibles se puede determinar mediante una llamada a [lista de tamaños de máquina virtual disponible para una suscripción](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="4a832-116">hello list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="4a832-117">`osPlatform` debe especificarse y puede ser **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="4a832-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="4a832-118">Ha utilizado toodetermine los costos de hardware de Hola de máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a832-118">It's used toodetermine hello hardware costs of hello virtual machines.</span></span>
- <span data-ttu-id="4a832-119">`imageReference` se omite para las imágenes propias, pero se proporciona para las imágenes de terceros.</span><span class="sxs-lookup"><span data-stu-id="4a832-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="4a832-120">Ha utilizado los costes de software de toodetermine Hola de máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a832-120">It's used toodetermine hello software costs of hello virtual machines.</span></span>
- <span data-ttu-id="4a832-121">`count`es tooset usado Hola multiplicador apropiado para el elemento de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a832-121">`count` is used tooset hello appropriate multiplier for hello element.</span></span> <span data-ttu-id="4a832-122">Admite un valor estático, como **2**, o un valor dinámico de otro elemento, como `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="4a832-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="4a832-123">es el valor predeterminado de Hello **1**.</span><span class="sxs-lookup"><span data-stu-id="4a832-123">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="4a832-124">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4a832-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="4a832-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a832-125">Next steps</span></span>
* <span data-ttu-id="4a832-126">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4a832-126">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="4a832-127">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4a832-127">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="4a832-128">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="4a832-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
