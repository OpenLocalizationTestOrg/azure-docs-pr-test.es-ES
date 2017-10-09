---
title: "elemento de interfaz de usuario de VirtualNetworkCombo de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Network.VirtualNetworkCombo para administrar aplicaciones de Azure
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="8273d-103">Elemento de la interfaz de usuario Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="8273d-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="8273d-104">Un grupo de controles para seleccionar una red virtual nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="8273d-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="8273d-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8273d-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="8273d-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="8273d-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="8273d-108">En tramas de alambres superior hello, usuario Hola detectado una nueva red virtual, por lo que el usuario de hello puede personalizar el prefijo de nombre y la dirección de cada subred.</span><span class="sxs-lookup"><span data-stu-id="8273d-108">In hello top wireframe, hello user has picked a new virtual network, so hello user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="8273d-109">En este caso, la configuración de subredes es opcional.</span><span class="sxs-lookup"><span data-stu-id="8273d-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="8273d-110">En tramas de alambres Hola inferior, usuario Hola se ha seleccionado una red virtual existente, por lo que debe asignar el usuario de hello cada plantilla de implementación de subred Hola requiere tooan subred.</span><span class="sxs-lookup"><span data-stu-id="8273d-110">In hello bottom wireframe, hello user has picked an existing virtual network, so hello user must map each subnet hello deployment template requires tooan existing subnet.</span></span> <span data-ttu-id="8273d-111">En este caso, la configuración de subredes es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="8273d-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="8273d-112">Esquema</span><span class="sxs-lookup"><span data-stu-id="8273d-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="8273d-113">Comentarios</span><span class="sxs-lookup"><span data-stu-id="8273d-113">Remarks</span></span>
- <span data-ttu-id="8273d-114">Si se especifica, Hola primer prefijo de dirección no superpuestos de tamaño `defaultValue.addressPrefixSize` se determina automáticamente según las redes virtuales existentes en la suscripción del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="8273d-114">If specified, hello first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in hello user's subscription.</span></span>
- <span data-ttu-id="8273d-115">Hola valor predeterminado de `defaultValue.name` y `defaultValue.addressPrefixSize` es **null**.</span><span class="sxs-lookup"><span data-stu-id="8273d-115">hello default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="8273d-116">`constraints.minAddressPrefixSize` debe especificarse.</span><span class="sxs-lookup"><span data-stu-id="8273d-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="8273d-117">Cualquier red virtual existente con un espacio de direcciones más pequeño que lo hello valor especificado no están disponibles para la selección.</span><span class="sxs-lookup"><span data-stu-id="8273d-117">Any existing virtual networks with an address space smaller than hello specified value are unavailable for selection.</span></span>
- <span data-ttu-id="8273d-118">`subnets` debe especificarse y `constraints.minAddressPrefixSize` debe especificarse para cada subred.</span><span class="sxs-lookup"><span data-stu-id="8273d-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="8273d-119">Al crear una nueva red virtual, prefijo de dirección de cada subred se calcula automáticamente basándose en prefijo de dirección de la red virtual de Hola y los respectivos `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="8273d-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on hello virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="8273d-120">Si se usa una red virtual existente, las subredes menores que la `constraints.minAddressPrefixSize` respectiva no están disponibles para la selección.</span><span class="sxs-lookup"><span data-stu-id="8273d-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="8273d-121">Además, si se especifica, las subredes que no contienen al menos `minAddressCount` direcciones disponibles no se podrán seleccionar.</span><span class="sxs-lookup"><span data-stu-id="8273d-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="8273d-122">es el valor predeterminado de Hello **0**.</span><span class="sxs-lookup"><span data-stu-id="8273d-122">hello default value is **0**.</span></span> <span data-ttu-id="8273d-123">tooensure que Hola direcciones disponibles son contiguas, especifique **true** para `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="8273d-123">tooensure that hello available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="8273d-124">es el valor predeterminado de Hello **true**.</span><span class="sxs-lookup"><span data-stu-id="8273d-124">hello default value is **true**.</span></span>
- <span data-ttu-id="8273d-125">No se admite la creación de subredes en una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="8273d-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="8273d-126">Si `options.hideExisting` es **true**, usuario de hello no puede elegir una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="8273d-126">If `options.hideExisting` is **true**, hello user can't choose an existing virtual network.</span></span> <span data-ttu-id="8273d-127">es el valor predeterminado de Hello **false**.</span><span class="sxs-lookup"><span data-stu-id="8273d-127">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="8273d-128">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8273d-128">Sample output</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="8273d-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8273d-129">Next steps</span></span>
* <span data-ttu-id="8273d-130">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8273d-130">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8273d-131">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8273d-131">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="8273d-132">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="8273d-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
