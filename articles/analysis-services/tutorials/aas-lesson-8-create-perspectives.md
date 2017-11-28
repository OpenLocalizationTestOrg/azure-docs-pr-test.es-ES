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
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="0e0fc-103">Lección 8: Creación de perspectivas</span><span class="sxs-lookup"><span data-stu-id="0e0fc-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="0e0fc-104">En esta lección, creará una perspectiva de venta por Internet.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="0e0fc-105">Una perspectiva define un subconjunto visible de un modelo que ofrece puntos de vista centrados, específicos del negocio o específicos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="0e0fc-106">Cuando un usuario conecta tooa modelo mediante una perspectiva, podrán ver sólo los objetos de modelo (tablas, columnas, medidas, jerarquías y KPI) como campos definidos en esa perspectiva.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-106">When a user connects tooa model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="0e0fc-107">más información, consulte toolearn [perspectivas](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="0e0fc-107">toolearn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="0e0fc-108">Hola perspectiva venta por Internet que cree en esta lección excluye el objeto de la tabla DimCustomer Hola.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-108">hello Internet Sales perspective you create in this lesson excludes hello DimCustomer table object.</span></span> <span data-ttu-id="0e0fc-109">Cuando se crea una perspectiva que excluye ciertos objetos de vista, ese objeto sigue existiendo en el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-109">When you create a perspective that excludes certain objects from view, that object still exists in hello model.</span></span> <span data-ttu-id="0e0fc-110">Sin embargo, no está visible en una lista de campos de cliente de generación de informes.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="0e0fc-111">Las columnas y las medidas calculadas, tanto si se incluyen en una perspectiva como si no, aún se pueden calcular a partir de los datos del objeto excluido.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="0e0fc-112">Hola de esta lección sirve toodescribe cómo toocreate perspectivas y familiarizarse con las herramientas de creación de modelos tabulares Hola.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-112">hello purpose of this lesson is toodescribe how toocreate perspectives and become familiar with hello tabular model authoring tools.</span></span> <span data-ttu-id="0e0fc-113">Si posteriormente amplía estas tablas adicionales de tooinclude de modelo, puede crear otras perspectivas toodefine diferentes puntos de vista del modelo de hello, por ejemplo, inventario y las ventas.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-113">If you later expand this model tooinclude additional tables, you can create additional perspectives toodefine different viewpoints of hello model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="0e0fc-114">Estimado toocomplete de tiempo en esta lección: **cinco minutos**</span><span class="sxs-lookup"><span data-stu-id="0e0fc-114">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="0e0fc-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0e0fc-115">Prerequisites</span></span>  
<span data-ttu-id="0e0fc-116">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="0e0fc-117">Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 7: crear indicadores clave de rendimiento](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="0e0fc-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="0e0fc-118">Creación de perspectivas</span><span class="sxs-lookup"><span data-stu-id="0e0fc-118">Create perspectives</span></span>  
  
#### <a name="toocreate-an-internet-sales-perspective"></a><span data-ttu-id="0e0fc-119">toocreate una perspectiva venta por Internet</span><span class="sxs-lookup"><span data-stu-id="0e0fc-119">toocreate an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="0e0fc-120">Haga clic en hello **modelo** menú > **perspectivas** > **crear y administrar**.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-120">Click hello **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="0e0fc-121">Hola **perspectivas** cuadro de diálogo, haga clic en **nueva perspectiva**.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-121">In hello **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="0e0fc-122">Haga doble clic en hello **nueva perspectiva** encabezado de columna y, a continuación, cambie el nombre **venta por Internet**.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-122">Double-click hello **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="0e0fc-123">Seleccione Hola todas las tablas de hello *excepto* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-123">Select hello all hello tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="0e0fc-125">En una lección posterior, use Hola analizar en Excel característica tootest esta perspectiva.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-125">In a later lesson, you use hello Analyze in Excel feature tootest this perspective.</span></span> <span data-ttu-id="0e0fc-126">Hola lista de campos de tabla dinámica de Excel incluye cada tabla excepto la tabla DimCustomer de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e0fc-126">hello Excel PivotTable Fields List includes each table except hello DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="0e0fc-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e0fc-127">What's next?</span></span>
<span data-ttu-id="0e0fc-128">[Lección 9: Creación de jerarquías](../tutorials/aas-lesson-9-create-hierarchies.md)</span><span class="sxs-lookup"><span data-stu-id="0e0fc-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
