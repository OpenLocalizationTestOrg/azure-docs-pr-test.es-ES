---
title: "aaaHow tooview relacionados con recursos de datos en el catálogo de datos de Azure | Documentos de Microsoft"
description: "Este artículo explica cómo tooview relacionados con recursos de datos de un recurso de datos seleccionado en el catálogo de datos."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="aaeb5-103">¿Cómo tooview relacionados con recursos de datos en el catálogo de datos?</span><span class="sxs-lookup"><span data-stu-id="aaeb5-103">How tooview related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="aaeb5-104">Catálogo de datos de Azure permite tooview datos activos relacionados tooa seleccionado datos activos y ver las relaciones entre ellos.</span><span class="sxs-lookup"><span data-stu-id="aaeb5-104">Azure Data Catalog allows you tooview data assets related tooa selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="aaeb5-105">Orígenes de datos admitidos</span><span class="sxs-lookup"><span data-stu-id="aaeb5-105">Supported data sources</span></span> 
<span data-ttu-id="aaeb5-106">Al registrar los activos de datos desde Hola siguientes orígenes de datos, el catálogo de datos registra automáticamente metadatos acerca de las relaciones de combinación entre los recursos de datos de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="aaeb5-106">When you register data assets from hello following data sources, Azure Data Catalog automatically registers metadata about join relationships between hello selected data assets.</span></span> 

- <span data-ttu-id="aaeb5-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="aaeb5-107">SQL Server</span></span>
- <span data-ttu-id="aaeb5-108">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="aaeb5-108">Azure SQL Database</span></span>
- <span data-ttu-id="aaeb5-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="aaeb5-109">MySQL</span></span>
- <span data-ttu-id="aaeb5-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="aaeb5-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="aaeb5-111">Visualización de los recursos de datos relacionados</span><span class="sxs-lookup"><span data-stu-id="aaeb5-111">View related data assets</span></span>
<span data-ttu-id="aaeb5-112">tooview activos de datos que son el conjunto de datos relacionadas tooa seleccionado, utilice hello **relaciones** pestaña tal como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="aaeb5-112">tooview data assets that are related tooa selected dataset, use hello **Relationships** tab as shown in hello following image:</span></span> 

![Azure Data Catalog: visualización de los recursos de datos relacionados](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="aaeb5-114">En este ejemplo, hay dos relaciones para hello seleccionado **ProductSubcategory** datos activos:</span><span class="sxs-lookup"><span data-stu-id="aaeb5-114">In this example, there are two relationships for hello selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="aaeb5-115">ProductSubcategoryID columna de tabla de productos de hello tiene una relación de clave externa con ProductSubcategoryID columna de tabla ProductSubcategory de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="aaeb5-115">ProductSubcategoryID column of hello Product table has a foreign key relationship with ProductSubcategoryID column of hello selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="aaeb5-116">ProductCategoryID columna de tabla ProductSubCategory de hello tiene una relación de clave externa con ProductCategoryID columna de tabla ProductCategory de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="aaeb5-116">ProductCategoryID column of hello ProductSubCategory table has a foreign key relationship with ProductCategoryID column of hello selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="aaeb5-117">Observe la dirección de Hola de flecha de hello en la vista de árbol de relaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="aaeb5-117">Notice hello direction of hello arrow in hello relationships tree view.</span></span>  

<span data-ttu-id="aaeb5-118">toosee más detalles, como el nombre completo de Hola de columna de hello, mueva Hola mouse y verá un toohello similar emergente después de la imagen:</span><span class="sxs-lookup"><span data-stu-id="aaeb5-118">toosee more details such as hello fully qualified name of hello column, move hello mouse over and you see a popup similar toohello following image:</span></span> 

![Azure Data Catalog: elemento emergente Relaciones](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="aaeb5-120">tooinclude relaciones entre los recursos que ya se ha registrado, vuelva a registrar esos recursos.</span><span class="sxs-lookup"><span data-stu-id="aaeb5-120">tooinclude relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaeb5-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aaeb5-121">Next steps</span></span>
- [<span data-ttu-id="aaeb5-122">¿Cómo toomanage activos de datos</span><span class="sxs-lookup"><span data-stu-id="aaeb5-122">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
