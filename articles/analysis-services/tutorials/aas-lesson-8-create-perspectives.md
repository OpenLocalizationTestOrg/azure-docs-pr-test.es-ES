---
title: "Lección 8 del tutorial de Azure Analysis Services: Creación de perspectivas | Microsoft Docs"
description: "Se describe cómo crear perspectivas en el proyecto del tutorial de Analysis Services de Azure."
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
ms.openlocfilehash: 491500909b0de0360afae45e172e85999d764fe0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="ac9d8-103">Lección 8: Creación de perspectivas</span><span class="sxs-lookup"><span data-stu-id="ac9d8-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="ac9d8-104">En esta lección, creará una perspectiva de venta por Internet.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="ac9d8-105">Una perspectiva define un subconjunto visible de un modelo que ofrece puntos de vista centrados, específicos del negocio o específicos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="ac9d8-106">Cuando un usuario se conecta a un modelo mediante una perspectiva, solo ve esos objetos de modelo (tablas, columnas, medidas, jerarquías y KPI) como campos definidos en esa perspectiva.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-106">When a user connects to a model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="ac9d8-107">Para más información, consulte [Perspectivas](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="ac9d8-107">To learn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="ac9d8-108">La perspectiva Venta por Internet que creará en esta lección excluye el objeto de tabla DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-108">The Internet Sales perspective you create in this lesson excludes the DimCustomer table object.</span></span> <span data-ttu-id="ac9d8-109">Cuando se crea una perspectiva que excluye ciertos objetos de la vista, ese objeto todavía existe en el modelo.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-109">When you create a perspective that excludes certain objects from view, that object still exists in the model.</span></span> <span data-ttu-id="ac9d8-110">Sin embargo, no está visible en una lista de campos de cliente de generación de informes.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="ac9d8-111">Las columnas y las medidas calculadas, tanto si se incluyen en una perspectiva como si no, aún se pueden calcular a partir de los datos del objeto excluido.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="ac9d8-112">Esta lección tiene como objetivo describir cómo se crean las perspectivas, así como familiarizarse con las herramientas de creación de modelos tabulares.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-112">The purpose of this lesson is to describe how to create perspectives and become familiar with the tabular model authoring tools.</span></span> <span data-ttu-id="ac9d8-113">Si más tarde amplía este modelo para incluir tablas adicionales, puede crear otras perspectivas para definir puntos de vista diferentes del modelo, por ejemplo, Inventario y Ventas.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-113">If you later expand this model to include additional tables, you can create additional perspectives to define different viewpoints of the model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="ac9d8-114">Tiempo estimado para completar esta lección: **cinco minutos**</span><span class="sxs-lookup"><span data-stu-id="ac9d8-114">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ac9d8-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ac9d8-115">Prerequisites</span></span>  
<span data-ttu-id="ac9d8-116">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="ac9d8-117">Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 7: Creación de indicadores clave de rendimiento](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="ac9d8-117">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="ac9d8-118">Creación de perspectivas</span><span class="sxs-lookup"><span data-stu-id="ac9d8-118">Create perspectives</span></span>  
  
#### <a name="to-create-an-internet-sales-perspective"></a><span data-ttu-id="ac9d8-119">Para crear una perspectiva Venta por Internet, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ac9d8-119">To create an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="ac9d8-120">Haga clic en el menú **Modelo** > **Perspectivas** > **Crear y administrar**.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-120">Click the **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="ac9d8-121">En el cuadro de diálogo **Perspectivas**, haga clic en **Nueva perspectiva**.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-121">In the **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="ac9d8-122">Haga doble clic en el encabezado de columna **Nueva perspectiva** y llámelo **Venta por Internet**.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-122">Double-click the **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="ac9d8-123">Seleccione todas las tablas *excepto* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-123">Select the all the tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="ac9d8-125">En una lección posterior, usará la característica Analizar en Excel para probar esta perspectiva.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-125">In a later lesson, you use the Analyze in Excel feature to test this perspective.</span></span> <span data-ttu-id="ac9d8-126">La lista de campos de tabla dinámica de Excel incluye todas las tablas, excepto DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="ac9d8-126">The Excel PivotTable Fields List includes each table except the DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="ac9d8-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac9d8-127">What's next?</span></span>
<span data-ttu-id="ac9d8-128">[Lección 9: Creación de jerarquías](../tutorials/aas-lesson-9-create-hierarchies.md)</span><span class="sxs-lookup"><span data-stu-id="ac9d8-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
