---
title: "Visualización de recursos de datos relacionados en Azure Data Catalog | Microsoft Docs"
description: "En este artículo se explica cómo ver los recursos de datos relacionados de un recurso de datos seleccionado en Azure Data Catalog."
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
ms.openlocfilehash: d45f2cabe712a7982f99a9d280fed4494fc4d377
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-view-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="c5e85-103">¿Cómo ver los recursos de datos relacionados en Azure Data Catalog?</span><span class="sxs-lookup"><span data-stu-id="c5e85-103">How to view related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="c5e85-104">Azure Data Catalog permite ver los recursos de datos relacionados con un recurso de datos seleccionado, así como ver las relaciones entre ellos.</span><span class="sxs-lookup"><span data-stu-id="c5e85-104">Azure Data Catalog allows you to view data assets related to a selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="c5e85-105">Orígenes de datos admitidos</span><span class="sxs-lookup"><span data-stu-id="c5e85-105">Supported data sources</span></span> 
<span data-ttu-id="c5e85-106">Al registrar los recursos de datos de los siguientes orígenes de datos, Azure Data Catalog registra automáticamente los metadatos sobre las relaciones de combinación entre los recursos de datos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="c5e85-106">When you register data assets from the following data sources, Azure Data Catalog automatically registers metadata about join relationships between the selected data assets.</span></span> 

- <span data-ttu-id="c5e85-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="c5e85-107">SQL Server</span></span>
- <span data-ttu-id="c5e85-108">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="c5e85-108">Azure SQL Database</span></span>
- <span data-ttu-id="c5e85-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="c5e85-109">MySQL</span></span>
- <span data-ttu-id="c5e85-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="c5e85-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="c5e85-111">Visualización de los recursos de datos relacionados</span><span class="sxs-lookup"><span data-stu-id="c5e85-111">View related data assets</span></span>
<span data-ttu-id="c5e85-112">Para ver los recursos de datos que están relacionados con un conjunto de datos seleccionado, utilice la pestaña **Relaciones**, tal como se muestra en la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="c5e85-112">To view data assets that are related to a selected dataset, use the **Relationships** tab as shown in the following image:</span></span> 

![Azure Data Catalog: visualización de los recursos de datos relacionados](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="c5e85-114">En este ejemplo, hay dos relaciones para el recurso de datos **ProductSubcategory** seleccionado:</span><span class="sxs-lookup"><span data-stu-id="c5e85-114">In this example, there are two relationships for the selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="c5e85-115">La columna ProductSubcategoryID de la tabla Product tiene una relación de clave externa con la columna ProductSubcategoryID de la tabla ProductSubcategory seleccionada.</span><span class="sxs-lookup"><span data-stu-id="c5e85-115">ProductSubcategoryID column of the Product table has a foreign key relationship with ProductSubcategoryID column of the selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="c5e85-116">La columna ProductCategoryID de la tabla ProductSubCategory tiene una relación de clave externa con la columna ProductCategoryID de la tabla ProductCategory seleccionada.</span><span class="sxs-lookup"><span data-stu-id="c5e85-116">ProductCategoryID column of the ProductSubCategory table has a foreign key relationship with ProductCategoryID column of the selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="c5e85-117">Tenga en cuenta la dirección de la flecha en la vista de árbol de relaciones.</span><span class="sxs-lookup"><span data-stu-id="c5e85-117">Notice the direction of the arrow in the relationships tree view.</span></span>  

<span data-ttu-id="c5e85-118">Para ver más detalles, como el nombre completo de la columna, mueva el mouse sobre él para ver un menú emergente similar al de la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="c5e85-118">To see more details such as the fully qualified name of the column, move the mouse over and you see a popup similar to the following image:</span></span> 

![Azure Data Catalog: elemento emergente Relaciones](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="c5e85-120">Para incluir las relaciones entre los recursos que ya se han registrado, vuelva a registrar esos recursos.</span><span class="sxs-lookup"><span data-stu-id="c5e85-120">To include relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5e85-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5e85-121">Next steps</span></span>
- [<span data-ttu-id="c5e85-122">Cómo administrar recursos de datos</span><span class="sxs-lookup"><span data-stu-id="c5e85-122">How to manage data assets</span></span>](data-catalog-how-to-manage.md)