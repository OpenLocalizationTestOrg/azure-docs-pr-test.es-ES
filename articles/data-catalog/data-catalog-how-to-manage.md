---
title: "aaaManage activos de datos en el catálogo de datos de Azure | Documentos de Microsoft"
description: "artículo de Hello destaca cómo toocontrol visibilidad y la propiedad de activos de datos registran en el catálogo de datos."
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
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="8e0fe-103">Administración de recursos de datos en Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="8e0fe-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="8e0fe-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="8e0fe-104">Introduction</span></span>
<span data-ttu-id="8e0fe-105">Catálogo de datos de Azure está diseñado para la detección de origen de datos, por lo que puede detectar fácilmente y comprender los orígenes de datos de hello necesita tooperform análisis y tomar decisiones.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand hello data sources you need tooperform analysis and make decisions.</span></span> <span data-ttu-id="8e0fe-106">Estas capacidades de detección tener mayor impacto de hello cuando usted y otros usuarios pueden buscar y comprender la gama más amplia de Hola de orígenes de datos disponibles.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-106">These discovery capabilities make hello biggest impact when you and other users can find and understand hello broadest range of available data sources.</span></span> <span data-ttu-id="8e0fe-107">Con estos elementos en mente, comportamiento predeterminado de hello del catálogo de datos es para todos los datos registrados orígenes toobe visible tooand reconocible por todos los usuarios del catálogo.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-107">With these elements in mind, hello default behavior of Data Catalog is for all registered data sources toobe visible tooand discoverable by all catalog users.</span></span>

<span data-ttu-id="8e0fe-108">El catálogo de datos no le otorga acceso a los datos de toohello propio.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-108">Data Catalog does not give you access toohello data itself.</span></span> <span data-ttu-id="8e0fe-109">Acceso a datos se controla mediante el propietario de Hola Hola del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-109">Data access is controlled by hello owner of hello data source.</span></span> <span data-ttu-id="8e0fe-110">Con el catálogo de datos, puede detectar los orígenes de datos y ver los metadatos de Hola que son orígenes de toohello relacionados que están registrados en el catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-110">With Data Catalog, you can discover data sources and view hello metadata that's related toohello sources that are registered in hello catalog.</span></span>

<span data-ttu-id="8e0fe-111">Puede haber casos, sin embargo, en los orígenes de datos solo deberían resultar toospecific visible a los usuarios o toomembers de grupos específicos.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-111">There might be situations, however, where data sources should only be visible toospecific users, or toomembers of specific groups.</span></span> <span data-ttu-id="8e0fe-112">En estos escenarios, los usuarios pueden tomar posesión de los activos de datos registrado en el catálogo de hello y, a continuación, controlar la visibilidad de Hola de activos de Hola que poseen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-112">In such scenarios, users can take ownership of registered data assets within hello catalog and then control hello visibility of hello assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="8e0fe-113">funcionalidad de Hello descrita en este artículo solo está disponible en hello edición estándar de catálogo de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-113">hello functionality described in this article is available only in hello Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="8e0fe-114">Hello edición gratuita no proporciona funciones para la propiedad y para restringir la visibilidad de recurso de datos.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-114">hello Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="8e0fe-115">Administración de la propiedad de los recursos de datos</span><span class="sxs-lookup"><span data-stu-id="8e0fe-115">Manage ownership of data assets</span></span>
<span data-ttu-id="8e0fe-116">De forma predeterminada, los activos de datos que están registrados en Data Catalog no tienen propietario.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="8e0fe-117">Cualquier usuario con permiso tooaccess Hola del catálogo puede detectar y anotar estos activos.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-117">Any user with permission tooaccess hello catalog can discover and annotate these assets.</span></span> <span data-ttu-id="8e0fe-118">Los usuarios pueden tomar posesión de activos de datos no poseído y, a continuación, limitar la visibilidad de Hola de activos de Hola que poseen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-118">Users can take ownership of unowned data assets and then limit hello visibility of hello assets they own.</span></span>

<span data-ttu-id="8e0fe-119">Cuando es propiedad de un recurso de datos en el catálogo de datos, solo los usuarios que estén autorizados a los propietarios de hello pueden detectar asset hello y ver sus metadatos, y sólo los propietarios de hello pueden eliminar el recurso de Hola desde el catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-119">When a data asset in Data Catalog is owned, only users who are authorized by hello owners can discover hello asset and view its metadata, and only hello owners can delete hello asset from hello catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="8e0fe-120">Propiedad de catálogo de datos afecta a solo los metadatos de Hola que se almacenan en el catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-120">Ownership in Data Catalog affects only hello metadata that's stored in hello catalog.</span></span> <span data-ttu-id="8e0fe-121">Propiedad no confiere ningún permiso en el origen de datos subyacente de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-121">Ownership does not confer any permissions on hello underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="8e0fe-122">Toma de posesión</span><span class="sxs-lookup"><span data-stu-id="8e0fe-122">Take ownership</span></span>
<span data-ttu-id="8e0fe-123">Los usuarios pueden tomar posesión de activos de datos seleccionando hello **Take Ownership** opción en el portal del catálogo de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-123">Users can take ownership of data assets by selecting hello **Take Ownership** option in hello Data Catalog portal.</span></span> <span data-ttu-id="8e0fe-124">No hay permisos especiales son tootake requiere la propiedad de un recurso de datos no poseído.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-124">No special permissions are required tootake ownership of an unowned data asset.</span></span> <span data-ttu-id="8e0fe-125">Cualquier usuario puede tomar posesión de un recurso de datos sin propietario.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="8e0fe-126">Adición de propietarios y copropietarios</span><span class="sxs-lookup"><span data-stu-id="8e0fe-126">Add owners and co-owners</span></span>
<span data-ttu-id="8e0fe-127">Si un recurso de datos ya tiene propietario, los demás usuarios simplemente no podrán tomar posesión del mismo.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="8e0fe-128">Un propietario ya existente debe agregarles como copropietarios.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="8e0fe-129">Cualquier propietario puede agregar más usuarios o grupos de seguridad como copropietarios.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="8e0fe-130">Es al menos dos usuarios como propietarios de un toohave de prácticas recomendada para cualquier propiedad de recurso de datos.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-130">It is a best practice toohave at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="8e0fe-131">Eliminación de propietarios</span><span class="sxs-lookup"><span data-stu-id="8e0fe-131">Remove owners</span></span>
<span data-ttu-id="8e0fe-132">Al igual que un propietario de recursos puede agregar copropietarios, cualquier propietario de recursos puede quitar a un copropietario.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="8e0fe-133">Un propietario del recurso que se quita de él o su propio como un propietario no podrá administrar activos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-133">An asset owner who removes him or herself as an owner can no longer manage hello asset.</span></span> <span data-ttu-id="8e0fe-134">Si el propietario del recurso de hello quita le o su propio como un propietario y no hay ningún otros los copropietarios, asset Hola revierte tooan no poseído estado.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-134">If hello asset owner removes him or herself as an owner and there are no other co-owners, hello asset reverts tooan unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="8e0fe-135">Control de la visibilidad</span><span class="sxs-lookup"><span data-stu-id="8e0fe-135">Control visibility</span></span>
<span data-ttu-id="8e0fe-136">Los propietarios del recurso de datos pueden controlar la visibilidad de Hola Hola de activos de datos que poseen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-136">Data-asset owners can control hello visibility of hello data assets they own.</span></span> <span data-ttu-id="8e0fe-137">visibilidad de toorestrict como valor predeterminado de hello, donde Hola a todos los usuarios pueden detectar el catálogo de datos y ver datos activos, el propietario del recurso de hello puede alternar configuración de visibilidad de Hola de **todos** demasiado**propietarios y usuarios de estas** en Propiedades de Hola de activos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-137">toorestrict visibility as hello default, where all Data Catalog users can discover and view hello data asset, hello asset owner can toggle hello visibility setting from **Everyone** too**Owners & These Users** in hello properties for hello asset.</span></span> <span data-ttu-id="8e0fe-138">Los propietarios pueden después agregar usuarios y grupos de seguridad específicos.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="8e0fe-139">Siempre que sea posible, deben asignarse permisos de propiedad y la visibilidad de activos toosecurity grupos y no tooindividual a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-139">Whenever possible, asset ownership and visibility permissions should be assigned toosecurity groups and not tooindividual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="8e0fe-140">Administradores del Catálogo</span><span class="sxs-lookup"><span data-stu-id="8e0fe-140">Catalog administrators</span></span>
<span data-ttu-id="8e0fe-141">Los administradores del catálogo de datos son implícitamente los copropietarios de todos los activos en el catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-141">Data Catalog administrators are implicitly co-owners of all assets in hello catalog.</span></span> <span data-ttu-id="8e0fe-142">Los propietarios de activos no pueden quitar la visibilidad de los administradores y los administradores pueden administrar la visibilidad de todos los activos de datos en el catálogo de Hola y propiedad.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in hello catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="8e0fe-143">Resumen</span><span class="sxs-lookup"><span data-stu-id="8e0fe-143">Summary</span></span>
<span data-ttu-id="8e0fe-144">Hola catálogo de datos crowdsourcing modelo toometadata y los datos activos detección permite que todos los catálogos a los usuarios toocontribute y detectar.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-144">hello Data Catalog crowdsourcing model toometadata and data asset discovery allows all catalog users toocontribute and discover.</span></span> <span data-ttu-id="8e0fe-145">Hola edición estándar de catálogo de datos está diseñado para la propiedad y la administración de visibilidad de hello toolimit y el uso de activos de datos específicos.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-145">hello Standard Edition of Data Catalog is designed for ownership and management toolimit hello visibility and use of specific data assets.</span></span>
