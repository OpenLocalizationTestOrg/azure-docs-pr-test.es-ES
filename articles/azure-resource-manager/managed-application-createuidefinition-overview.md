---
title: "aaaUnderstand Crear definición de interfaz de usuario para las aplicaciones administradas de Azure | Documentos de Microsoft"
description: "Describe cómo toocreate las definiciones de interfaz de usuario para las aplicaciones administradas de Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="86e73-103">Introducción a CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="86e73-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="86e73-104">Este documento presentan conceptos básicos de Hola de un CreateUiDefinition, que se utiliza la interfaz de usuario de Hola Hola toogenerate portal Azure para crear una aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="86e73-104">This document introduces hello core concepts of a CreateUiDefinition, which is used by hello Azure portal toogenerate hello user interface for creating a managed application.</span></span>

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

<span data-ttu-id="86e73-105">CreateUiDefinition siempre contiene tres propiedades:</span><span class="sxs-lookup"><span data-stu-id="86e73-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="86e73-106">handler</span><span class="sxs-lookup"><span data-stu-id="86e73-106">handler</span></span>
* <span data-ttu-id="86e73-107">versión</span><span class="sxs-lookup"><span data-stu-id="86e73-107">version</span></span>
* <span data-ttu-id="86e73-108">parameters</span><span class="sxs-lookup"><span data-stu-id="86e73-108">parameters</span></span>

<span data-ttu-id="86e73-109">Para las aplicaciones administradas, siempre debería ser el controlador `Microsoft.Compute.MultiVm`, y la versión de Hola compatible más reciente es `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="86e73-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and hello latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="86e73-110">esquema de Hola de propiedad de los parámetros de hello depende de la combinación de hello del controlador especificado de Hola y la versión.</span><span class="sxs-lookup"><span data-stu-id="86e73-110">hello schema of hello parameters property depends on hello combination of hello specified handler and version.</span></span> <span data-ttu-id="86e73-111">Para las aplicaciones administradas, son propiedades de hello admitida `basics`, `steps`, y `outputs`.</span><span class="sxs-lookup"><span data-stu-id="86e73-111">For managed applications, hello supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="86e73-112">propiedades conceptos básicos y pasos Hello contienen hello _elementos_ , como cuadros de texto y listas desplegables - toobe muestra de Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="86e73-112">hello basics and steps properties contain hello _elements_ - like textboxes and dropdowns - toobe displayed in hello Azure portal.</span></span> <span data-ttu-id="86e73-113">salidas de Hello propiedad es toomap usa valores de salida de hello de Hola elementos especificados toohello parámetros de plantilla de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86e73-113">hello outputs property is used toomap hello output values of hello specified elements toohello parameters of hello Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="86e73-114">Se recomienda incluir `$schema`, aunque es opcional.</span><span class="sxs-lookup"><span data-stu-id="86e73-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="86e73-115">Si se especifica, Hola valor para `version` debe coincidir con la versión de Hola Hola `$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="86e73-115">If specified, hello value for `version` must match hello version within hello `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="86e73-116">Aspectos básicos</span><span class="sxs-lookup"><span data-stu-id="86e73-116">Basics</span></span>
<span data-ttu-id="86e73-117">paso de conceptos básicos de Hello siempre es Hola primer paso para genera al portal de Azure Hola analiza un CreateUiDefinition con un asistente Hola.</span><span class="sxs-lookup"><span data-stu-id="86e73-117">hello Basics step is always hello first step of hello wizard generated when hello Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="86e73-118">Además se especifican los elementos de Hola de toodisplaying en `basics`, portal de hello inserta elementos de suscripción de los usuarios toochoose hello, grupo de recursos y ubicación para la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="86e73-118">In addition toodisplaying hello elements specified in `basics`, hello portal injects elements for users toochoose hello subscription, resource group, and location for hello deployment.</span></span> <span data-ttu-id="86e73-119">Por lo general, los elementos que consultan los parámetros de toda la implementación, tal como el nombre de un clúster o el Administrador de credenciales, Hola deberían ir en este paso.</span><span class="sxs-lookup"><span data-stu-id="86e73-119">Generally, elements that query for deployment-wide parameters, like hello name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="86e73-120">Si el comportamiento de un elemento depende de la suscripción del usuario de hello, el grupo de recursos o la ubicación, ese elemento no puede utilizarse en aspectos básicos.</span><span class="sxs-lookup"><span data-stu-id="86e73-120">If an element's behavior depends on hello user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="86e73-121">Por ejemplo, **Microsoft.Compute.SizeSelector** depende suscripción y ubicación toodetermine Hola lista del usuario de hello de los tamaños disponibles.</span><span class="sxs-lookup"><span data-stu-id="86e73-121">For example, **Microsoft.Compute.SizeSelector** depends on hello user's subscription and location toodetermine hello list of available sizes.</span></span> <span data-ttu-id="86e73-122">Por lo tanto, **Microsoft.Compute.SizeSelector** solo puede utilizarse en steps.</span><span class="sxs-lookup"><span data-stu-id="86e73-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="86e73-123">Por lo general, solo elementos de hello **Microsoft.Common** espacio de nombres puede usarse en aspectos básicos.</span><span class="sxs-lookup"><span data-stu-id="86e73-123">Generally, only elements in hello **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="86e73-124">Aunque algunos elementos en otros espacios de nombres (como **Microsoft.Compute.Credentials**) que no dependen de contexto del usuario de hello, todavía se permiten.</span><span class="sxs-lookup"><span data-stu-id="86e73-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on hello user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="86e73-125">Pasos</span><span class="sxs-lookup"><span data-stu-id="86e73-125">Steps</span></span>
<span data-ttu-id="86e73-126">propiedad de pasos de Hello puede contener cero o más toodisplay pasos adicionales después de conceptos básicos, cada uno de los cuales contiene uno o más elementos.</span><span class="sxs-lookup"><span data-stu-id="86e73-126">hello steps property can contain zero or more additional steps toodisplay after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="86e73-127">Considere la posibilidad de agregar pasos por rol o de la capa de aplicación Hola va a implementar.</span><span class="sxs-lookup"><span data-stu-id="86e73-127">Consider adding steps per role or tier of hello application being deployed.</span></span> <span data-ttu-id="86e73-128">Por ejemplo, agregue un paso de las entradas para los nodos maestros de Hola y un paso para nodos de trabajador de hello en un clúster.</span><span class="sxs-lookup"><span data-stu-id="86e73-128">For example, add a step for inputs for hello master nodes, and a step for hello worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="86e73-129">Salidas</span><span class="sxs-lookup"><span data-stu-id="86e73-129">Outputs</span></span>
<span data-ttu-id="86e73-130">portal de Azure Hello usa hello `outputs` elementos de propiedad toomap de `basics` y `steps` toohello parámetros de plantilla de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86e73-130">hello Azure portal uses hello `outputs` property toomap elements from `basics` and `steps` toohello parameters of hello Azure Resource Manager deployment template.</span></span> <span data-ttu-id="86e73-131">claves de Hola de este diccionario son nombres de Hola Hola de parámetros de plantilla y valores de hello son propiedades de los objetos de salida de hello de los elementos de hello al que hace referencia.</span><span class="sxs-lookup"><span data-stu-id="86e73-131">hello keys of this dictionary are hello names of hello template parameters, and hello values are properties of hello output objects from hello referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="86e73-132">Functions</span><span class="sxs-lookup"><span data-stu-id="86e73-132">Functions</span></span>
<span data-ttu-id="86e73-133">Similar demasiado[funciones de plantilla](resource-group-template-functions.md) en Azure Resource Manager (tanto en la sintaxis y las funciones), CreateUiDefinition proporciona funciones para trabajar con elementos entradas y salidas, así como características, como instrucciones condicionales.</span><span class="sxs-lookup"><span data-stu-id="86e73-133">Similar too[template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86e73-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="86e73-134">Next steps</span></span>
<span data-ttu-id="86e73-135">El esquema de CreateUiDefinition en sí es simple.</span><span class="sxs-lookup"><span data-stu-id="86e73-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="86e73-136">profundidad real de Hola de procede de todas las funciones, qué Hola siguientes documentos se describen en detalle maravillosa y elementos de hello admitida:</span><span class="sxs-lookup"><span data-stu-id="86e73-136">hello real depth of it comes from all hello supported elements and functions, which hello following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="86e73-137">Elementos</span><span class="sxs-lookup"><span data-stu-id="86e73-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="86e73-138">Funciones</span><span class="sxs-lookup"><span data-stu-id="86e73-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="86e73-139">Hay disponible un esquema JSON actual para CreateUiDefinition aquí: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="86e73-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="86e73-140">Las versiones posteriores estarán disponibles en hello misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="86e73-140">Later versions will be available at hello same location.</span></span> <span data-ttu-id="86e73-141">Reemplace hello `0.1.2-preview` parte de la dirección URL de Hola y Hola `version` valor con el identificador de la versión de Hola piensa toouse.</span><span class="sxs-lookup"><span data-stu-id="86e73-141">Replace hello `0.1.2-preview` portion of hello URL and hello `version` value with hello version identifier you intend toouse.</span></span> <span data-ttu-id="86e73-142">los identificadores de versión de Hola compatibles actualmente son `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, y `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="86e73-142">hello currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>
