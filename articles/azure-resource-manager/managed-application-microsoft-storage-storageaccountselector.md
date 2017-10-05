---
title: Elemento de interfaz de usuario StorageAccountSelector de aplicaciones administradas de Azure | Microsoft Docs
description: Describe el elemento de la interfaz de usuario Microsoft.Storage.StorageAccountSelector para aplicaciones administradas de Azure
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
ms.openlocfilehash: 15e69c0deb4bce64b7413b557eb69db5165bde73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="038a9-103">Elemento de interfaz de usuario Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="038a9-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="038a9-104">Un control para seleccionar una cuenta de almacenamiento nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="038a9-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="038a9-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="038a9-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="038a9-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="038a9-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="038a9-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="038a9-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="038a9-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="038a9-109">Remarks</span></span>
- <span data-ttu-id="038a9-110">Si se especifica, se valida automáticamente la unicidad de `defaultValue.name`.</span><span class="sxs-lookup"><span data-stu-id="038a9-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="038a9-111">Si el nombre de cuenta de almacenamiento no es único, el usuario debe especificar otro nombre diferente o elegir una cuenta de almacenamiento existente.</span><span class="sxs-lookup"><span data-stu-id="038a9-111">If the storage account name is not unique, the user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="038a9-112">El valor predeterminado de `defaultValue.type` es **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="038a9-112">The default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="038a9-113">Los tipos no especificados en `constraints.allowedTypes` está oculto, mientras que los tipos no especificado en `constraints.excludedTypes` se muestran.</span><span class="sxs-lookup"><span data-stu-id="038a9-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="038a9-114">Tanto `constraints.allowedTypes` como `constraints.excludedTypes` son opcionales, pero no se pueden usar simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="038a9-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="038a9-115">Si el valor de `options.hideExisting` es **true**, el usuario no puede elegir una cuenta de almacenamiento existente.</span><span class="sxs-lookup"><span data-stu-id="038a9-115">If `options.hideExisting` is **true**, the user can't choose an existing storage account.</span></span> <span data-ttu-id="038a9-116">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="038a9-116">The default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="038a9-117">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="038a9-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="038a9-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="038a9-118">Next steps</span></span>
* <span data-ttu-id="038a9-119">Para una introducción a las aplicaciones administradas, consulte la [introducción a las aplicaciones administradas de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="038a9-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="038a9-120">Para ver una introducción sobre la creación de definiciones de interfaz de usuario, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="038a9-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="038a9-121">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="038a9-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
