---
title: "Elemento de interfaz de usuario VirtualNetworkCombo de una aplicación administrada de Azure | Microsoft Docs"
description: Describe el elemento de la interfaz de usuario Microsoft.Network.VirtualNetworkCombo para aplicaciones administradas de Azure
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
ms.openlocfilehash: 8bb255b76ac5c3de570fa569a1cfb3ee953f9687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="58218-103">Elemento de la interfaz de usuario Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="58218-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="58218-104">Un grupo de controles para seleccionar una red virtual nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="58218-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="58218-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="58218-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="58218-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="58218-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="58218-108">En la estructura de alambre superior, el usuario ha seleccionado una nueva red virtual, por lo que puede personalizar el nombre y el prefijo de dirección de cada subred.</span><span class="sxs-lookup"><span data-stu-id="58218-108">In the top wireframe, the user has picked a new virtual network, so the user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="58218-109">En este caso, la configuración de subredes es opcional.</span><span class="sxs-lookup"><span data-stu-id="58218-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="58218-110">En la estructura de alambre inferior, el usuario ha seleccionado una red virtual existente, por lo que debe asignar cada subred que requiere la plantilla de implementación a una subred existente.</span><span class="sxs-lookup"><span data-stu-id="58218-110">In the bottom wireframe, the user has picked an existing virtual network, so the user must map each subnet the deployment template requires to an existing subnet.</span></span> <span data-ttu-id="58218-111">En este caso, la configuración de subredes es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="58218-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="58218-112">Esquema</span><span class="sxs-lookup"><span data-stu-id="58218-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="58218-113">Comentarios</span><span class="sxs-lookup"><span data-stu-id="58218-113">Remarks</span></span>
- <span data-ttu-id="58218-114">Si se ha especificado, el primer prefijo de dirección que no se superponga del tamaño `defaultValue.addressPrefixSize` se determina automáticamente en función de las redes virtuales existentes en la suscripción del usuario.</span><span class="sxs-lookup"><span data-stu-id="58218-114">If specified, the first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in the user's subscription.</span></span>
- <span data-ttu-id="58218-115">El valor predeterminado de `defaultValue.name` y `defaultValue.addressPrefixSize` es **null**.</span><span class="sxs-lookup"><span data-stu-id="58218-115">The default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="58218-116">`constraints.minAddressPrefixSize` debe especificarse.</span><span class="sxs-lookup"><span data-stu-id="58218-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="58218-117">Las redes virtuales existentes con un espacio de direcciones menor que el valor especificado no se pueden seleccionar.</span><span class="sxs-lookup"><span data-stu-id="58218-117">Any existing virtual networks with an address space smaller than the specified value are unavailable for selection.</span></span>
- <span data-ttu-id="58218-118">`subnets` debe especificarse y `constraints.minAddressPrefixSize` debe especificarse para cada subred.</span><span class="sxs-lookup"><span data-stu-id="58218-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="58218-119">Al crear una nueva red virtual, el prefijo de dirección de cada subred se calcula automáticamente basándose en el prefijo de dirección de la red virtual y en los respectivos `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="58218-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on the virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="58218-120">Si se usa una red virtual existente, las subredes menores que la `constraints.minAddressPrefixSize` respectiva no están disponibles para la selección.</span><span class="sxs-lookup"><span data-stu-id="58218-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="58218-121">Además, si se especifica, las subredes que no contienen al menos `minAddressCount` direcciones disponibles no se podrán seleccionar.</span><span class="sxs-lookup"><span data-stu-id="58218-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="58218-122">El valor predeterminado es **0**.</span><span class="sxs-lookup"><span data-stu-id="58218-122">The default value is **0**.</span></span> <span data-ttu-id="58218-123">Para asegurarse de que las direcciones disponibles son contiguas, especifique **true** en `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="58218-123">To ensure that the available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="58218-124">El valor predeterminado es **true**.</span><span class="sxs-lookup"><span data-stu-id="58218-124">The default value is **true**.</span></span>
- <span data-ttu-id="58218-125">No se admite la creación de subredes en una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="58218-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="58218-126">Si el valor de `options.hideExisting` es **true**, el usuario no puede elegir una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="58218-126">If `options.hideExisting` is **true**, the user can't choose an existing virtual network.</span></span> <span data-ttu-id="58218-127">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="58218-127">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="58218-128">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="58218-128">Sample output</span></span>
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="58218-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="58218-129">Next steps</span></span>
* <span data-ttu-id="58218-130">Para una introducción a las aplicaciones administradas, consulte la [introducción a las aplicaciones administradas de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58218-130">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="58218-131">Para ver una introducción sobre la creación de definiciones de interfaz de usuario, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58218-131">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="58218-132">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="58218-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
