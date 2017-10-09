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
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a>¿Cómo tooview relacionados con recursos de datos en el catálogo de datos?
Catálogo de datos de Azure permite tooview datos activos relacionados tooa seleccionado datos activos y ver las relaciones entre ellos. 

## <a name="supported-data-sources"></a>Orígenes de datos admitidos 
Al registrar los activos de datos desde Hola siguientes orígenes de datos, el catálogo de datos registra automáticamente metadatos acerca de las relaciones de combinación entre los recursos de datos de hello seleccionado. 

- SQL Server
- Base de datos SQL de Azure
- MySQL
- Oracle

## <a name="view-related-data-assets"></a>Visualización de los recursos de datos relacionados
tooview activos de datos que son el conjunto de datos relacionadas tooa seleccionado, utilice hello **relaciones** pestaña tal como se muestra en hello después de imagen: 

![Azure Data Catalog: visualización de los recursos de datos relacionados](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

En este ejemplo, hay dos relaciones para hello seleccionado **ProductSubcategory** datos activos: 

- ProductSubcategoryID columna de tabla de productos de hello tiene una relación de clave externa con ProductSubcategoryID columna de tabla ProductSubcategory de hello seleccionado. 
- ProductCategoryID columna de tabla ProductSubCategory de hello tiene una relación de clave externa con ProductCategoryID columna de tabla ProductCategory de hello seleccionado.

> [!NOTE]
> Observe la dirección de Hola de flecha de hello en la vista de árbol de relaciones de Hola.  

toosee más detalles, como el nombre completo de Hola de columna de hello, mueva Hola mouse y verá un toohello similar emergente después de la imagen: 

![Azure Data Catalog: elemento emergente Relaciones](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

tooinclude relaciones entre los recursos que ya se ha registrado, vuelva a registrar esos recursos.

## <a name="next-steps"></a>Pasos siguientes
- [¿Cómo toomanage activos de datos](data-catalog-how-to-manage.md)
