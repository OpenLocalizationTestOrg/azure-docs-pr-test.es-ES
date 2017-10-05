---
title: Elemento de interfaz de usuario MultiStorageAccountCombo de aplicaciones administradas de Azure | Microsoft Docs
description: Describe el elemento de la interfaz de usuario Microsoft.Storage.MultiStorageAccountCombo para aplicaciones administradas de Azure
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
ms.openlocfilehash: 27843b116d949899e4eae65f342324f77ebca70b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="dfd8e-103">Elemento de la interfaz de usuario Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="dfd8e-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="dfd8e-104">Un grupo de controles para crear varias cuentas de almacenamiento con nombres que comienzan con un prefijo común.</span><span class="sxs-lookup"><span data-stu-id="dfd8e-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="dfd8e-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="dfd8e-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="dfd8e-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="dfd8e-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="dfd8e-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="dfd8e-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="dfd8e-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="dfd8e-109">Remarks</span></span>
- <span data-ttu-id="dfd8e-110">El valor de `defaultValue.prefix` se concatena con uno o varios números enteros para generar la secuencia de nombres de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dfd8e-110">The value for `defaultValue.prefix` is concatenated with one or more integers to generate the sequence of storage account names.</span></span> <span data-ttu-id="dfd8e-111">Por ejemplo, si `defaultValue.prefix` es **foobar** y `count` es **2**, se generan los nombres de cuenta de almacenamiento **foobar1** y **foobar2**.</span><span class="sxs-lookup"><span data-stu-id="dfd8e-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="dfd8e-112">La unicidad de los nombres de cuenta de almacenamiento generados se valida automáticamente.</span><span class="sxs-lookup"><span data-stu-id="dfd8e-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="dfd8e-113">Los nombres de cuenta de almacenamiento se generan lexicográficamente en función de `count`.</span><span class="sxs-lookup"><span data-stu-id="dfd8e-113">The storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="dfd8e-114">Por ejemplo, si `count` es 10, los nombres de cuenta de almacenamiento terminan en enteros de 2 dígitos (01, 02, 03, etc.).</span><span class="sxs-lookup"><span data-stu-id="dfd8e-114">For example, if `count` is 10, then the storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="dfd8e-115">El valor predeterminado de `defaultValue.prefix` es **null**, mientras que el de `defaultValue.type` es **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="dfd8e-115">The default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="dfd8e-116">Los tipos no especificados en `constraints.allowedTypes` está oculto, mientras que los tipos no especificado en `constraints.excludedTypes` se muestran.</span><span class="sxs-lookup"><span data-stu-id="dfd8e-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="dfd8e-117">Tanto `constraints.allowedTypes` como `constraints.excludedTypes` son opcionales, pero no se pueden usar simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="dfd8e-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="dfd8e-118">Además de para generar nombres de cuenta de almacenamiento, `count` se usa para establecer el multiplicador apropiado para el elemento.</span><span class="sxs-lookup"><span data-stu-id="dfd8e-118">In addition to generating storage account names, `count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="dfd8e-119">Admite un valor estático, como **2**, o un valor dinámico de otro elemento, como `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="dfd8e-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="dfd8e-120">El valor predeterminado es **1**.</span><span class="sxs-lookup"><span data-stu-id="dfd8e-120">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="dfd8e-121">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="dfd8e-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="dfd8e-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dfd8e-122">Next steps</span></span>
* <span data-ttu-id="dfd8e-123">Para una introducción a las aplicaciones administradas, consulte la [introducción a las aplicaciones administradas de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dfd8e-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="dfd8e-124">Para ver una introducción sobre la creación de definiciones de interfaz de usuario, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dfd8e-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="dfd8e-125">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="dfd8e-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
