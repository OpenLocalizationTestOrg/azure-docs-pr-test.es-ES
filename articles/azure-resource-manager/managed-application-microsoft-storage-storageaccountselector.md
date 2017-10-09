---
title: "elemento de interfaz de usuario de StorageAccountSelector de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Storage.StorageAccountSelector para administrar aplicaciones de Azure
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="2450f-103">Elemento de interfaz de usuario Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="2450f-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="2450f-104">Un control para seleccionar una cuenta de almacenamiento nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="2450f-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="2450f-105">Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="2450f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="2450f-106">Ejemplo de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="2450f-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="2450f-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="2450f-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="2450f-109">Comentarios</span><span class="sxs-lookup"><span data-stu-id="2450f-109">Remarks</span></span>
- <span data-ttu-id="2450f-110">Si se especifica, se valida automáticamente la unicidad de `defaultValue.name`.</span><span class="sxs-lookup"><span data-stu-id="2450f-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="2450f-111">Si el nombre de cuenta de almacenamiento de hello no es único, usuario de hello debe especificar un nombre diferente o elija una cuenta de almacenamiento existente.</span><span class="sxs-lookup"><span data-stu-id="2450f-111">If hello storage account name is not unique, hello user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="2450f-112">Hola valor predeterminado de `defaultValue.type` es **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="2450f-112">hello default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="2450f-113">Los tipos no especificados en `constraints.allowedTypes` está oculto, mientras que los tipos no especificado en `constraints.excludedTypes` se muestran.</span><span class="sxs-lookup"><span data-stu-id="2450f-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="2450f-114">Tanto `constraints.allowedTypes` como `constraints.excludedTypes` son opcionales, pero no se pueden usar simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="2450f-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="2450f-115">Si `options.hideExisting` es **true**, usuario de hello no puede elegir una cuenta de almacenamiento existente.</span><span class="sxs-lookup"><span data-stu-id="2450f-115">If `options.hideExisting` is **true**, hello user can't choose an existing storage account.</span></span> <span data-ttu-id="2450f-116">es el valor predeterminado de Hello **false**.</span><span class="sxs-lookup"><span data-stu-id="2450f-116">hello default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="2450f-117">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2450f-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="2450f-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2450f-118">Next steps</span></span>
* <span data-ttu-id="2450f-119">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2450f-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="2450f-120">Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2450f-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="2450f-121">Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="2450f-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
