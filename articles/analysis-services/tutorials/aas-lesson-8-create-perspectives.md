---
title: "aaa \"crear perspectivas de Azure Analysis Services tutorial lección 8 | Documentos de Microsoft\""
description: "Describe cómo toocreate perspectivas en Hola proyecto tutorial de Analysis Services de Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a>Lección 8: Creación de perspectivas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, creará una perspectiva de venta por Internet. Una perspectiva define un subconjunto visible de un modelo que ofrece puntos de vista centrados, específicos del negocio o específicos de la aplicación. Cuando un usuario conecta tooa modelo mediante una perspectiva, podrán ver sólo los objetos de modelo (tablas, columnas, medidas, jerarquías y KPI) como campos definidos en esa perspectiva. más información, consulte toolearn [perspectivas](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).
  
Hola perspectiva venta por Internet que cree en esta lección excluye el objeto de la tabla DimCustomer Hola. Cuando se crea una perspectiva que excluye ciertos objetos de vista, ese objeto sigue existiendo en el modelo de Hola. Sin embargo, no está visible en una lista de campos de cliente de generación de informes. Las columnas y las medidas calculadas, tanto si se incluyen en una perspectiva como si no, aún se pueden calcular a partir de los datos del objeto excluido.  
  
Hola de esta lección sirve toodescribe cómo toocreate perspectivas y familiarizarse con las herramientas de creación de modelos tabulares Hola. Si posteriormente amplía estas tablas adicionales de tooinclude de modelo, puede crear otras perspectivas toodefine diferentes puntos de vista del modelo de hello, por ejemplo, inventario y las ventas.  
  
Estimado toocomplete de tiempo en esta lección: **cinco minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 7: crear indicadores clave de rendimiento](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Creación de perspectivas  
  
#### <a name="toocreate-an-internet-sales-perspective"></a>toocreate una perspectiva venta por Internet  
  
1.  Haga clic en hello **modelo** menú > **perspectivas** > **crear y administrar**.  
  
2.  Hola **perspectivas** cuadro de diálogo, haga clic en **nueva perspectiva**.  
  
3.  Haga doble clic en hello **nueva perspectiva** encabezado de columna y, a continuación, cambie el nombre **venta por Internet**.  
  
4.  Seleccione Hola todas las tablas de hello *excepto* **DimCustomer**.  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    En una lección posterior, use Hola analizar en Excel característica tootest esta perspectiva. Hola lista de campos de tabla dinámica de Excel incluye cada tabla excepto la tabla DimCustomer de Hola.  

## <a name="whats-next"></a>Pasos siguientes
[Lección 9: Creación de jerarquías](../tutorials/aas-lesson-9-create-hierarchies.md)
  
  
  
  
