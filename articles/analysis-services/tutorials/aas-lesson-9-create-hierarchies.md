---
<span data-ttu-id="29cf8-101">título: aaa "lección tutorial de Analysis Services de Azure 9: crear jerarquías | Descripción de Microsoft Docs": servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''</span><span class="sxs-lookup"><span data-stu-id="29cf8-101">title: aaa"Azure Analysis Services tutorial lesson 9: Create hierarchies | Microsoft Docs" description: services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="29cf8-102">MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="29cf8-102">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="29cf8-103">Lección 9: Creación de jerarquías</span><span class="sxs-lookup"><span data-stu-id="29cf8-103">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="29cf8-104">En esta lección, creará jerarquías.</span><span class="sxs-lookup"><span data-stu-id="29cf8-104">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="29cf8-105">Las jerarquías son grupos de columnas dispuestas en niveles; por ejemplo, una jerarquía geografía puede tener subniveles de país, estado, provincia y ciudad.</span><span class="sxs-lookup"><span data-stu-id="29cf8-105">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="29cf8-106">Jerarquías pueden aparecer por separado de otras columnas en una lista de campos de aplicación de cliente informes, facilitando de cliente a los usuarios toonavigate e incluya en un informe.</span><span class="sxs-lookup"><span data-stu-id="29cf8-106">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users toonavigate and include in a report.</span></span> <span data-ttu-id="29cf8-107">más información, consulte toolearn [jerarquías](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="29cf8-107">toolearn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="29cf8-108">las jerarquías de toocreate, use el Diseñador de modelo de Hola de *vista de diagrama*.</span><span class="sxs-lookup"><span data-stu-id="29cf8-108">toocreate hierarchies, use hello model designer in *Diagram View*.</span></span> <span data-ttu-id="29cf8-109">La creación y la administración de jerarquías no se admiten en vista de datos.</span><span class="sxs-lookup"><span data-stu-id="29cf8-109">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="29cf8-110">Estimado toocomplete de tiempo en esta lección: **20 minutos**</span><span class="sxs-lookup"><span data-stu-id="29cf8-110">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="29cf8-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="29cf8-111">Prerequisites</span></span>  
<span data-ttu-id="29cf8-112">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="29cf8-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="29cf8-113">Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 8: crear perspectivas](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="29cf8-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="29cf8-114">Creación de jerarquías</span><span class="sxs-lookup"><span data-stu-id="29cf8-114">Create hierarchies</span></span>  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a><span data-ttu-id="29cf8-115">una jerarquía de categorías en la tabla DimProduct de hello toocreate</span><span class="sxs-lookup"><span data-stu-id="29cf8-115">toocreate a Category hierarchy in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="29cf8-116">En el Diseñador de modelos de hello (vista de diagrama), haga clic en hello **DimProduct** tabla > **crear jerarquía**.</span><span class="sxs-lookup"><span data-stu-id="29cf8-116">In hello model designer (diagram view), right-click hello **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="29cf8-117">Aparece una nueva jerarquía final Hola de ventana de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="29cf8-117">A new hierarchy appears at hello bottom of hello table window.</span></span> <span data-ttu-id="29cf8-118">Cambiar el nombre de la jerarquía de hello **categoría**.</span><span class="sxs-lookup"><span data-stu-id="29cf8-118">Rename hello hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="29cf8-119">Haga clic y arrastre hello **ProductCategoryName** toohello de columna nuevo **categoría** jerarquía.</span><span class="sxs-lookup"><span data-stu-id="29cf8-119">Click and drag hello **ProductCategoryName** column toohello new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="29cf8-120">Hola **categoría** jerarquía, contextual hello **ProductCategoryName** > **cambiar el nombre de**y, a continuación, escriba **categoría**.</span><span class="sxs-lookup"><span data-stu-id="29cf8-120">In hello **Category** hierarchy, right-click hello **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="29cf8-121">Cambiar el nombre de una columna en una jerarquía no cambiar el nombre de esa columna en tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="29cf8-121">Renaming a column in a hierarchy does not rename that column in hello table.</span></span> <span data-ttu-id="29cf8-122">Una columna de una jerarquía es simplemente una representación de la columna de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="29cf8-122">A column in a hierarchy is just a representation of hello column in hello table.</span></span>  
  
4.  <span data-ttu-id="29cf8-123">Haga clic y arrastre hello **ProductSubcategoryName** columna toohello **categoría** jerarquía.</span><span class="sxs-lookup"><span data-stu-id="29cf8-123">Click and drag hello **ProductSubcategoryName** column toohello **Category** hierarchy.</span></span> <span data-ttu-id="29cf8-124">Cambie su nombre por **Subcategoría**.</span><span class="sxs-lookup"><span data-stu-id="29cf8-124">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="29cf8-125">Menú contextual hello **ModelName** columna > **agregar toohierarchy**y, a continuación, seleccione **categoría**.</span><span class="sxs-lookup"><span data-stu-id="29cf8-125">Right-click hello **ModelName** column > **Add toohierarchy**, and then select **Category**.</span></span> <span data-ttu-id="29cf8-126">Cambie su nombre por **Modelo**.</span><span class="sxs-lookup"><span data-stu-id="29cf8-126">Rename it **Model**.</span></span>

6.  <span data-ttu-id="29cf8-127">Por último, agregue **EnglishProductName** toohello jerarquía de categorías.</span><span class="sxs-lookup"><span data-stu-id="29cf8-127">Finally, add **EnglishProductName** toohello Category hierarchy.</span></span> <span data-ttu-id="29cf8-128">Cambie su nombre por **Producto**.</span><span class="sxs-lookup"><span data-stu-id="29cf8-128">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a><span data-ttu-id="29cf8-130">jerarquías de toocreate en la tabla DimDate de Hola</span><span class="sxs-lookup"><span data-stu-id="29cf8-130">toocreate hierarchies in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="29cf8-131">Hola **DimDate** de tabla, cree una jerarquía denominada **calendario**.</span><span class="sxs-lookup"><span data-stu-id="29cf8-131">In hello **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="29cf8-132">Agregue Hola siguiendo en orden de columnas:</span><span class="sxs-lookup"><span data-stu-id="29cf8-132">Add hello following columns in-order:</span></span>

    *  <span data-ttu-id="29cf8-133">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="29cf8-133">CalendarYear</span></span>
    *  <span data-ttu-id="29cf8-134">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="29cf8-134">CalendarSemester</span></span>
    *  <span data-ttu-id="29cf8-135">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="29cf8-135">CalendarQuarter</span></span>
    *  <span data-ttu-id="29cf8-136">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="29cf8-136">MonthCalendar</span></span>
    *  <span data-ttu-id="29cf8-137">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="29cf8-137">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="29cf8-138">Hola **DimDate** de tabla, cree un **Fiscal** jerarquía.</span><span class="sxs-lookup"><span data-stu-id="29cf8-138">In hello **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="29cf8-139">Hola siguiendo en orden de columnas se incluyen:</span><span class="sxs-lookup"><span data-stu-id="29cf8-139">Include hello following columns in-order:</span></span>  
  
    *  <span data-ttu-id="29cf8-140">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="29cf8-140">FiscalYear</span></span>
    *  <span data-ttu-id="29cf8-141">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="29cf8-141">FiscalSemester</span></span>
    *  <span data-ttu-id="29cf8-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="29cf8-142">FiscalQuarter</span></span>
    *  <span data-ttu-id="29cf8-143">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="29cf8-143">MonthCalendar</span></span>
    *  <span data-ttu-id="29cf8-144">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="29cf8-144">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="29cf8-145">Por último, en hello **DimDate** de tabla, cree un **ProductionCalendar** jerarquía.</span><span class="sxs-lookup"><span data-stu-id="29cf8-145">Finally, in hello **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="29cf8-146">Hola siguiendo en orden de columnas se incluyen:</span><span class="sxs-lookup"><span data-stu-id="29cf8-146">Include hello following columns in-order:</span></span>  
    *  <span data-ttu-id="29cf8-147">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="29cf8-147">CalendarYear</span></span>
    *  <span data-ttu-id="29cf8-148">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="29cf8-148">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="29cf8-149">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="29cf8-149">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="29cf8-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29cf8-150">What's next?</span></span>
<span data-ttu-id="29cf8-151">[Lección 10: Creación de particiones](../tutorials/aas-lesson-10-create-partitions.md)</span><span class="sxs-lookup"><span data-stu-id="29cf8-151">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
