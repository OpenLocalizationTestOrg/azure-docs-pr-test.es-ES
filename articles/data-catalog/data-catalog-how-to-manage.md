---
title: "Administración de recursos de datos en Azure Data Catalog | Microsoft Docs"
description: "En este artículo se resalta cómo controlar la visibilidad y la propiedad de los recursos de datos registrados en Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 8b9159b7bc4f7b2dac12d9012c6c903e75a6ac16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="b3d93-103">Administración de recursos de datos en Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="b3d93-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="b3d93-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="b3d93-104">Introduction</span></span>
<span data-ttu-id="b3d93-105">Azure Data Catalog está diseñado para la detección de orígenes de datos, lo que le permite detectar y comprender fácilmente los orígenes de datos que necesitan para realizar análisis y tomar decisiones.</span><span class="sxs-lookup"><span data-stu-id="b3d93-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand the data sources you need to perform analysis and make decisions.</span></span> <span data-ttu-id="b3d93-106">Estas funcionalidades de detección consiguen el mayor impacto cuando todos los usuarios puedan buscar y comprender la gama más amplia de orígenes de datos disponibles.</span><span class="sxs-lookup"><span data-stu-id="b3d93-106">These discovery capabilities make the biggest impact when you and other users can find and understand the broadest range of available data sources.</span></span> <span data-ttu-id="b3d93-107">Con estos elementos en mente, el comportamiento predeterminado de Data Catalog es que todos los orígenes de datos registrados sean visibles, y detectables, para todos los usuarios del catálogo.</span><span class="sxs-lookup"><span data-stu-id="b3d93-107">With these elements in mind, the default behavior of Data Catalog is for all registered data sources to be visible to and discoverable by all catalog users.</span></span>

<span data-ttu-id="b3d93-108">Data Catalog no ofrece a los usuarios acceso a los mismos datos.</span><span class="sxs-lookup"><span data-stu-id="b3d93-108">Data Catalog does not give you access to the data itself.</span></span> <span data-ttu-id="b3d93-109">El propietario del origen de datos es quien controla el acceso a los datos.</span><span class="sxs-lookup"><span data-stu-id="b3d93-109">Data access is controlled by the owner of the data source.</span></span> <span data-ttu-id="b3d93-110">Con Data Catalog se pueden detectar los orígenes de datos y ver los metadatos relacionados con los orígenes registrados en el catálogo.</span><span class="sxs-lookup"><span data-stu-id="b3d93-110">With Data Catalog, you can discover data sources and view the metadata that's related to the sources that are registered in the catalog.</span></span>

<span data-ttu-id="b3d93-111">Sin embargo, puede haber situaciones en las que los orígenes de datos solo deben ser visibles a usuarios específicos o a los miembros de grupos específicos.</span><span class="sxs-lookup"><span data-stu-id="b3d93-111">There might be situations, however, where data sources should only be visible to specific users, or to members of specific groups.</span></span> <span data-ttu-id="b3d93-112">En estos escenarios, los usuarios pueden tomar posesión de los recursos de datos registrados en el catálogo y, después, controlar la visibilidad de los recursos que poseen.</span><span class="sxs-lookup"><span data-stu-id="b3d93-112">In such scenarios, users can take ownership of registered data assets within the catalog and then control the visibility of the assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="b3d93-113">La funcionalidad descrita en este artículo solo está disponible en la edición Estándar de Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="b3d93-113">The functionality described in this article is available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="b3d93-114">La edición Gratis no ofrece funcionalidades para poseer y restringir la visibilidad de los recursos de datos.</span><span class="sxs-lookup"><span data-stu-id="b3d93-114">The Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="b3d93-115">Administración de la propiedad de los recursos de datos</span><span class="sxs-lookup"><span data-stu-id="b3d93-115">Manage ownership of data assets</span></span>
<span data-ttu-id="b3d93-116">De forma predeterminada, los activos de datos que están registrados en Data Catalog no tienen propietario.</span><span class="sxs-lookup"><span data-stu-id="b3d93-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="b3d93-117">Cualquier usuario con permiso para acceder al catálogo puede detectar y anotar estos recursos.</span><span class="sxs-lookup"><span data-stu-id="b3d93-117">Any user with permission to access the catalog can discover and annotate these assets.</span></span> <span data-ttu-id="b3d93-118">Los usuarios pueden tomar posesión de los recursos de datos sin propietario y limitar la visibilidad de los recursos que poseen.</span><span class="sxs-lookup"><span data-stu-id="b3d93-118">Users can take ownership of unowned data assets and then limit the visibility of the assets they own.</span></span>

<span data-ttu-id="b3d93-119">Cuando un recurso de datos de Data Catalog tiene propietario, solo los usuarios autorizados por los propietarios pueden detectar el recurso y ver sus metadatos, y solo los propietarios pueden eliminar el recurso del catálogo.</span><span class="sxs-lookup"><span data-stu-id="b3d93-119">When a data asset in Data Catalog is owned, only users who are authorized by the owners can discover the asset and view its metadata, and only the owners can delete the asset from the catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="b3d93-120">La propiedad de Data Catalog solo afecta a los metadatos almacenados en él.</span><span class="sxs-lookup"><span data-stu-id="b3d93-120">Ownership in Data Catalog affects only the metadata that's stored in the catalog.</span></span> <span data-ttu-id="b3d93-121">La propiedad no concede ningún permiso en el origen de datos subyacente.</span><span class="sxs-lookup"><span data-stu-id="b3d93-121">Ownership does not confer any permissions on the underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="b3d93-122">Toma de posesión</span><span class="sxs-lookup"><span data-stu-id="b3d93-122">Take ownership</span></span>
<span data-ttu-id="b3d93-123">Los usuarios pueden tomar posesión de los recursos de datos mediante la selección de la opción **Tomar posesión** en Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="b3d93-123">Users can take ownership of data assets by selecting the **Take Ownership** option in the Data Catalog portal.</span></span> <span data-ttu-id="b3d93-124">No se necesitan permisos especiales para tomar posesión de un recurso de datos sin propietario.</span><span class="sxs-lookup"><span data-stu-id="b3d93-124">No special permissions are required to take ownership of an unowned data asset.</span></span> <span data-ttu-id="b3d93-125">Cualquier usuario puede tomar posesión de un recurso de datos sin propietario.</span><span class="sxs-lookup"><span data-stu-id="b3d93-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="b3d93-126">Adición de propietarios y copropietarios</span><span class="sxs-lookup"><span data-stu-id="b3d93-126">Add owners and co-owners</span></span>
<span data-ttu-id="b3d93-127">Si un recurso de datos ya tiene propietario, los demás usuarios simplemente no podrán tomar posesión del mismo.</span><span class="sxs-lookup"><span data-stu-id="b3d93-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="b3d93-128">Un propietario ya existente debe agregarles como copropietarios.</span><span class="sxs-lookup"><span data-stu-id="b3d93-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="b3d93-129">Cualquier propietario puede agregar más usuarios o grupos de seguridad como copropietarios.</span><span class="sxs-lookup"><span data-stu-id="b3d93-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="b3d93-130">Es aconsejable tener al menos dos personas como propietarios de cualquier recurso de datos con propietario.</span><span class="sxs-lookup"><span data-stu-id="b3d93-130">It is a best practice to have at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="b3d93-131">Eliminación de propietarios</span><span class="sxs-lookup"><span data-stu-id="b3d93-131">Remove owners</span></span>
<span data-ttu-id="b3d93-132">Al igual que un propietario de recursos puede agregar copropietarios, cualquier propietario de recursos puede quitar a un copropietario.</span><span class="sxs-lookup"><span data-stu-id="b3d93-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="b3d93-133">Un propietario de recursos que se quita a sí mismo como propietario, ya no podrá administrar el recurso.</span><span class="sxs-lookup"><span data-stu-id="b3d93-133">An asset owner who removes him or herself as an owner can no longer manage the asset.</span></span> <span data-ttu-id="b3d93-134">Si el propietario de recursos se quita a sí mismo como propietario y no hay ningún otro copropietario, el recurso se revertirá a un estado de sin propietario.</span><span class="sxs-lookup"><span data-stu-id="b3d93-134">If the asset owner removes him or herself as an owner and there are no other co-owners, the asset reverts to an unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="b3d93-135">Control de la visibilidad</span><span class="sxs-lookup"><span data-stu-id="b3d93-135">Control visibility</span></span>
<span data-ttu-id="b3d93-136">Los propietarios de recursos de datos pueden controlar la visibilidad de los recursos de datos que poseen.</span><span class="sxs-lookup"><span data-stu-id="b3d93-136">Data-asset owners can control the visibility of the data assets they own.</span></span> <span data-ttu-id="b3d93-137">Para restringir la visibilidad del valor predeterminado, según el cual todos los usuarios de Data Catalog pueden detectar y ver el recurso de datos, el propietario del recurso puede cambiar la configuración de visibilidad de **Todos** a **Propietarios y estos usuarios** en las propiedades del recurso.</span><span class="sxs-lookup"><span data-stu-id="b3d93-137">To restrict visibility as the default, where all Data Catalog users can discover and view the data asset, the asset owner can toggle the visibility setting from **Everyone** to **Owners & These Users** in the properties for the asset.</span></span> <span data-ttu-id="b3d93-138">Los propietarios pueden después agregar usuarios y grupos de seguridad específicos.</span><span class="sxs-lookup"><span data-stu-id="b3d93-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="b3d93-139">Siempre que sea posible, los permisos de propiedad y la visibilidad de los recursos deben asignarse a grupos de seguridad y no a usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="b3d93-139">Whenever possible, asset ownership and visibility permissions should be assigned to security groups and not to individual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="b3d93-140">Administradores del Catálogo</span><span class="sxs-lookup"><span data-stu-id="b3d93-140">Catalog administrators</span></span>
<span data-ttu-id="b3d93-141">Los administradores de Data Catalog son implícitamente copropietarios de todos los recursos del catálogo.</span><span class="sxs-lookup"><span data-stu-id="b3d93-141">Data Catalog administrators are implicitly co-owners of all assets in the catalog.</span></span> <span data-ttu-id="b3d93-142">Los propietarios de los recursos no pueden quitar la visibilidad a los administradores y estos pueden administrar la propiedad y la visibilidad de todos los recursos de datos del catálogo.</span><span class="sxs-lookup"><span data-stu-id="b3d93-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in the catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="b3d93-143">Resumen</span><span class="sxs-lookup"><span data-stu-id="b3d93-143">Summary</span></span>
<span data-ttu-id="b3d93-144">El modelo de micromecenazgo de Data Catalog para la detección de recursos de datos y metadatos permite que todos los usuarios del catálogo colaboren en él y lo detecten.</span><span class="sxs-lookup"><span data-stu-id="b3d93-144">The Data Catalog crowdsourcing model to metadata and data asset discovery allows all catalog users to contribute and discover.</span></span> <span data-ttu-id="b3d93-145">La edición Estándar de Data Catalog está diseñada para la propiedad y administración con el fin de limitar la visibilidad y el uso de los recursos de datos específicos.</span><span class="sxs-lookup"><span data-stu-id="b3d93-145">The Standard Edition of Data Catalog is designed for ownership and management to limit the visibility and use of specific data assets.</span></span>
