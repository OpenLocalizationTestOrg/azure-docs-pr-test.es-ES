---
title: "Lección 3 del tutorial de Azure Analysis Services: Marcar como tabla de fechas |Microsoft Docs"
description: "Se describe cómo marcar una tabla de fechas en el proyecto del tutorial de Azure Analysis Services."
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
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: c62f2726fef5219155a08b70c61162c914600d1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-3-mark-as-date-table"></a><span data-ttu-id="9e811-103">Lección 3: Marcar como tabla de fechas</span><span class="sxs-lookup"><span data-stu-id="9e811-103">Lesson 3: Mark as Date Table</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="9e811-104">En la lección 2: Obtención de datos, importó una tabla de dimensiones denominada DimDate.</span><span class="sxs-lookup"><span data-stu-id="9e811-104">In Lesson 2: Get data, you imported a dimension table named DimDate.</span></span> <span data-ttu-id="9e811-105">Mientras que en su modelo esta tabla se denomina DimDate, también se conoce como *tabla de fechas* porque contiene datos de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="9e811-105">While in your model this table is named DimDate, it can also be known as a *Date table*, in that it contains date and time data.</span></span>  
  
<span data-ttu-id="9e811-106">Cada vez que se usan funciones de inteligencia de tiempo de DAX, igual que hará cuando cree medidas un poco más tarde, debe especificar propiedades que incluyan una *tabla de fechas* y un identificador único de *columna de fecha* en esa tabla.</span><span class="sxs-lookup"><span data-stu-id="9e811-106">Whenever you use DAX time-intelligence functions, like when you create measures later, you must specify properties which include a *Date table* and a unique identifier *Date column* in that table.</span></span>
  
<span data-ttu-id="9e811-107">En esta lección, marcará la tabla DimDate como la *tabla de fechas* y la columna de fecha (de la tabla de fechas) como la *columna de fecha* (identificador único).</span><span class="sxs-lookup"><span data-stu-id="9e811-107">In this lesson, you mark the DimDate table as the *Date table* and the Date column (in the Date table) as the *Date column* (unique identifier).</span></span>  

<span data-ttu-id="9e811-108">Antes de marcar la tabla de fechas y la columna de fecha, es hora de realizar algunas tareas para que su modelo sea más fácil de comprender.</span><span class="sxs-lookup"><span data-stu-id="9e811-108">Before you mark the date table and date column, it's a good time to do a little housekeeping to make your model easier to understand.</span></span> <span data-ttu-id="9e811-109">Observe en la tabla DimDate una columna llamada **FullDateAlternateKey**.</span><span class="sxs-lookup"><span data-stu-id="9e811-109">Notice in the DimDate table a column named **FullDateAlternateKey**.</span></span> <span data-ttu-id="9e811-110">Esta columna contiene una fila por cada día de cada año de calendario incluido en la tabla.</span><span class="sxs-lookup"><span data-stu-id="9e811-110">This column contains one row for every day in each calendar year included in the table.</span></span> <span data-ttu-id="9e811-111">Esta columna se usa mucho en las fórmulas de medida y los informes.</span><span class="sxs-lookup"><span data-stu-id="9e811-111">You use this column a lot in measure formulas and in reports.</span></span> <span data-ttu-id="9e811-112">Sin embargo, FullDateAlternateKey no es realmente un buen identificador en esta columna.</span><span class="sxs-lookup"><span data-stu-id="9e811-112">But, FullDateAlternateKey isn't really a good identifier for this column.</span></span> <span data-ttu-id="9e811-113">Cambie el nombre por **Date**, para que sea más fácil identificarlo e incluirlo en fórmulas.</span><span class="sxs-lookup"><span data-stu-id="9e811-113">You rename it to **Date**, making it easier to identify and include in formulas.</span></span> <span data-ttu-id="9e811-114">Siempre que sea posible, es una buena idea cambiar el nombre de los objetos, como tablas y columnas, para que sean más fáciles de identificar en SSDT y en aplicaciones cliente de generación de informes como Power BI y Excel.</span><span class="sxs-lookup"><span data-stu-id="9e811-114">Whenever possible, it's a good idea to rename objects like tables and columns to make them easier to identify in SSDT and client reporting applications like Power BI and Excel.</span></span> 
  
<span data-ttu-id="9e811-115">Tiempo estimado para completar esta lección: **tres minutos**</span><span class="sxs-lookup"><span data-stu-id="9e811-115">Estimated time to complete this lesson: **Three minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="9e811-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9e811-116">Prerequisites</span></span>  
<span data-ttu-id="9e811-117">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="9e811-117">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="9e811-118">Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 2: Obtención de datos](../tutorials/aas-lesson-2-get-data.md).</span><span class="sxs-lookup"><span data-stu-id="9e811-118">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 2: Get data](../tutorials/aas-lesson-2-get-data.md).</span></span> 

### <a name="to-rename-the-fulldatealternatekey-column"></a><span data-ttu-id="9e811-119">Para cambiar el nombre de la columna FullDateAlternateKey, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9e811-119">To rename the FullDateAlternateKey column</span></span>

1.  <span data-ttu-id="9e811-120">En el diseñador de modelos, haga clic en la tabla **DimDate**.</span><span class="sxs-lookup"><span data-stu-id="9e811-120">In the model designer, click the **DimDate** table.</span></span>

2.  <span data-ttu-id="9e811-121">Haga doble clic en el encabezado de la columna **FullDateAlternateKey** y luego cambie su nombre por **Date**.</span><span class="sxs-lookup"><span data-stu-id="9e811-121">Double-click the header for the **FullDateAlternateKey** column, and then rename it to **Date**.</span></span>

  
### <a name="to-set-mark-as-date-table"></a><span data-ttu-id="9e811-122">Para establecer Marcar como tabla de fechas, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9e811-122">To set Mark as Date Table</span></span>  
  
1.  <span data-ttu-id="9e811-123">Seleccione la columna **Date** y, luego, en la ventana **Propiedades**, en **Tipo de datos**, asegúrese de que esté seleccionado **Fecha**.</span><span class="sxs-lookup"><span data-stu-id="9e811-123">Select the **Date** column, and then in the **Properties** window, under **Data Type**, make sure  **Date** is selected.</span></span>  
  
2.  <span data-ttu-id="9e811-124">Haga clic en el menú **Tabla**, haga clic en **Fecha** y luego en **Marcar como tabla de fechas**.</span><span class="sxs-lookup"><span data-stu-id="9e811-124">Click the **Table** menu, then click **Date**, and then click **Mark as Date Table**.</span></span>  
  
3.  <span data-ttu-id="9e811-125">En el cuadro de diálogo **Marcar como tabla de fechas**, en el cuadro de lista **Fecha**, seleccione la columna **Date** como identificador único.</span><span class="sxs-lookup"><span data-stu-id="9e811-125">In the **Mark as Date Table** dialog box, in the **Date** listbox, select the **Date** column as the unique identifier.</span></span> <span data-ttu-id="9e811-126">Normalmente se selecciona de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9e811-126">It's usually selected by default.</span></span> <span data-ttu-id="9e811-127">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9e811-127">Click **OK**.</span></span> 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a><span data-ttu-id="9e811-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9e811-129">What's next?</span></span>
<span data-ttu-id="9e811-130">[Lección 4: Creación de relaciones](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="9e811-130">[Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span>
  
