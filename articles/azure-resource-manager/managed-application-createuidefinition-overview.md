---
title: "Información sobre la creación de definiciones de interfaz de usuario para aplicaciones administradas de Azure | Microsoft Docs"
description: "Describe cómo crear definiciones de interfaz de usuario para aplicaciones administradas de Azure"
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
ms.openlocfilehash: 176b891538f85c5638a2321561c3d8bd377d245b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="b9950-103">Introducción a CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="b9950-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="b9950-104">Este documento presenta los conceptos básicos de CreateUiDefinition, que Azure Portal utiliza para generar la interfaz de usuario para crear una aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="b9950-104">This document introduces the core concepts of a CreateUiDefinition, which is used by the Azure portal to generate the user interface for creating a managed application.</span></span>

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

<span data-ttu-id="b9950-105">CreateUiDefinition siempre contiene tres propiedades:</span><span class="sxs-lookup"><span data-stu-id="b9950-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="b9950-106">handler</span><span class="sxs-lookup"><span data-stu-id="b9950-106">handler</span></span>
* <span data-ttu-id="b9950-107">versión</span><span class="sxs-lookup"><span data-stu-id="b9950-107">version</span></span>
* <span data-ttu-id="b9950-108">parameters</span><span class="sxs-lookup"><span data-stu-id="b9950-108">parameters</span></span>

<span data-ttu-id="b9950-109">Para las aplicaciones administradas, handler siempre debería ser `Microsoft.Compute.MultiVm`, y la versión más reciente admitida es `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="b9950-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and the latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="b9950-110">El esquema de la propiedad parameters depende de la combinación de los valores de handler y version especificados.</span><span class="sxs-lookup"><span data-stu-id="b9950-110">The schema of the parameters property depends on the combination of the specified handler and version.</span></span> <span data-ttu-id="b9950-111">Para las aplicaciones administradas, las propiedades admitidas son `basics`, `steps` y `outputs`.</span><span class="sxs-lookup"><span data-stu-id="b9950-111">For managed applications, the supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="b9950-112">Las propiedades basics y steps contienen los _elementos_, como cuadros de texto y listas desplegables, que se mostrarán en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b9950-112">The basics and steps properties contain the _elements_ - like textboxes and dropdowns - to be displayed in the Azure portal.</span></span> <span data-ttu-id="b9950-113">La propiedad outputs se utiliza para asignar los valores de salida de los elementos especificados a los parámetros de la plantilla de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b9950-113">The outputs property is used to map the output values of the specified elements to the parameters of the Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="b9950-114">Se recomienda incluir `$schema`, aunque es opcional.</span><span class="sxs-lookup"><span data-stu-id="b9950-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="b9950-115">Si se especifica, el valor de `version` debe coincidir con la versión en el identificador URI de `$schema`.</span><span class="sxs-lookup"><span data-stu-id="b9950-115">If specified, the value for `version` must match the version within the `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="b9950-116">Aspectos básicos</span><span class="sxs-lookup"><span data-stu-id="b9950-116">Basics</span></span>
<span data-ttu-id="b9950-117">El paso basics siempre es el primero del asistente que se genera cuando Azure Portal analiza una instancia de CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="b9950-117">The Basics step is always the first step of the wizard generated when the Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="b9950-118">Además de mostrar los elementos especificados en `basics`, el portal inserta elementos para que los usuarios elijan la suscripción, el grupo de recursos y la ubicación de la implementación.</span><span class="sxs-lookup"><span data-stu-id="b9950-118">In addition to displaying the elements specified in `basics`, the portal injects elements for users to choose the subscription, resource group, and location for the deployment.</span></span> <span data-ttu-id="b9950-119">Por lo general, los elementos que consultan los parámetros de toda la implementación, como el nombre de un clúster o las credenciales del administrador, deben ir en este paso.</span><span class="sxs-lookup"><span data-stu-id="b9950-119">Generally, elements that query for deployment-wide parameters, like the name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="b9950-120">Si el comportamiento de un elemento depende de la suscripción, el grupo de recursos o la ubicación del usuario, ese elemento no puede utilizarse en basics.</span><span class="sxs-lookup"><span data-stu-id="b9950-120">If an element's behavior depends on the user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="b9950-121">Por ejemplo, **Microsoft.Compute.SizeSelector** depende de suscripción del usuario y la ubicación para determinar la lista de los tamaños disponibles.</span><span class="sxs-lookup"><span data-stu-id="b9950-121">For example, **Microsoft.Compute.SizeSelector** depends on the user's subscription and location to determine the list of available sizes.</span></span> <span data-ttu-id="b9950-122">Por lo tanto, **Microsoft.Compute.SizeSelector** solo puede utilizarse en steps.</span><span class="sxs-lookup"><span data-stu-id="b9950-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="b9950-123">Por lo general, solo los elementos del espacio de nombres **Microsoft.Common** pueden usarse en basics.</span><span class="sxs-lookup"><span data-stu-id="b9950-123">Generally, only elements in the **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="b9950-124">Sin embargo, sí se permiten algunos elementos de otros espacios de nombres (como **Microsoft.Compute.Credentials**) que no dependen del contexto del usuario.</span><span class="sxs-lookup"><span data-stu-id="b9950-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on the user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="b9950-125">Pasos</span><span class="sxs-lookup"><span data-stu-id="b9950-125">Steps</span></span>
<span data-ttu-id="b9950-126">La propiedad steps puede contener cero o más pasos adicionales que se mostrarán después de basics, cada uno de los cuales contiene uno o más elementos.</span><span class="sxs-lookup"><span data-stu-id="b9950-126">The steps property can contain zero or more additional steps to display after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="b9950-127">Considere la posibilidad de agregar pasos por rol o nivel de aplicación que se está implementando.</span><span class="sxs-lookup"><span data-stu-id="b9950-127">Consider adding steps per role or tier of the application being deployed.</span></span> <span data-ttu-id="b9950-128">Por ejemplo, agregue un paso para las entradas de los nodos principales y un paso para los nodos de trabajo de un clúster.</span><span class="sxs-lookup"><span data-stu-id="b9950-128">For example, add a step for inputs for the master nodes, and a step for the worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="b9950-129">Salidas</span><span class="sxs-lookup"><span data-stu-id="b9950-129">Outputs</span></span>
<span data-ttu-id="b9950-130">Azure Portal usa la propiedad `outputs` para asignar elementos de `basics` y `steps` a los parámetros de la plantilla de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b9950-130">The Azure portal uses the `outputs` property to map elements from `basics` and `steps` to the parameters of the Azure Resource Manager deployment template.</span></span> <span data-ttu-id="b9950-131">Las claves de este diccionario son los nombres de los parámetros de plantilla, y los valores son propiedades de los objetos de salida de los elementos a los que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="b9950-131">The keys of this dictionary are the names of the template parameters, and the values are properties of the output objects from the referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="b9950-132">Functions</span><span class="sxs-lookup"><span data-stu-id="b9950-132">Functions</span></span>
<span data-ttu-id="b9950-133">Similar a las [funciones de plantilla](resource-group-template-functions.md) de Azure Resource Manager (tanto en la sintaxis como en la funcionalidad), CreateUiDefinition proporciona funciones para trabajar con las entradas y salidas de los elementos, así como características tales como los condicionales.</span><span class="sxs-lookup"><span data-stu-id="b9950-133">Similar to [template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9950-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b9950-134">Next steps</span></span>
<span data-ttu-id="b9950-135">El esquema de CreateUiDefinition en sí es simple.</span><span class="sxs-lookup"><span data-stu-id="b9950-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="b9950-136">Su profundidad real se debe a todos los elementos y funciones admitidos, que se describen con detalle en los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="b9950-136">The real depth of it comes from all the supported elements and functions, which the following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="b9950-137">Elementos</span><span class="sxs-lookup"><span data-stu-id="b9950-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="b9950-138">Funciones</span><span class="sxs-lookup"><span data-stu-id="b9950-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="b9950-139">Hay disponible un esquema JSON actual para CreateUiDefinition aquí: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="b9950-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="b9950-140">Las versiones posteriores estarán disponibles en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="b9950-140">Later versions will be available at the same location.</span></span> <span data-ttu-id="b9950-141">Reemplace la parte `0.1.2-preview` de la dirección URL y el valor de `version` por el identificador de versión que va a utilizar.</span><span class="sxs-lookup"><span data-stu-id="b9950-141">Replace the `0.1.2-preview` portion of the URL and the `version` value with the version identifier you intend to use.</span></span> <span data-ttu-id="b9950-142">Los identificadores de versión actualmente admitidos son `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview` y `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="b9950-142">The currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>