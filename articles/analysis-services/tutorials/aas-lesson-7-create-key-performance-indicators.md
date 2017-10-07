---
<span data-ttu-id="d4337-101">título: aaa "lección tutorial de Analysis Services de Azure 7: crear indicadores clave de rendimiento | Descripción de Microsoft Docs": describe cómo toocreate los indicadores clave de rendimiento en Hola proyecto tutorial de Analysis Services de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4337-101">title: aaa"Azure Analysis Services tutorial lesson 7: Create Key Performance Indicators | Microsoft Docs" description: Describes how toocreate Key Performance Indicators in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="d4337-102">servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''</span><span class="sxs-lookup"><span data-stu-id="d4337-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="d4337-103">MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="d4337-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="d4337-104">Lección 7: Creación de indicadores clave de rendimiento</span><span class="sxs-lookup"><span data-stu-id="d4337-104">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="d4337-105">En esta lección, creará indicadores clave de rendimiento (KPI).</span><span class="sxs-lookup"><span data-stu-id="d4337-105">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="d4337-106">Los KPI son utilizados toogauge rendimiento de un valor definido por una *Base* medida, con un *destino* valor también se define una medida o un valor absoluto.</span><span class="sxs-lookup"><span data-stu-id="d4337-106">KPIs are used toogauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="d4337-107">En aplicaciones cliente de informes, los KPI pueden proporcionar a los profesionales de negocios un toounderstand de manera rápida y sencilla un resumen de las tendencias empresariales de éxito o tooidentify.</span><span class="sxs-lookup"><span data-stu-id="d4337-107">In reporting client applications, KPIs can provide business professionals a quick and easy way toounderstand a summary of business success or tooidentify trends.</span></span> <span data-ttu-id="d4337-108">más información, consulte toolearn [KPI](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="d4337-108">toolearn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="d4337-109">Estimado toocomplete de tiempo en esta lección: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="d4337-109">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="d4337-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d4337-110">Prerequisites</span></span>  
<span data-ttu-id="d4337-111">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="d4337-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="d4337-112">Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 6: crear medidas](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="d4337-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="d4337-113">Creación de indicadores clave de rendimiento</span><span class="sxs-lookup"><span data-stu-id="d4337-113">Create Key Performance Indicators</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="d4337-114">un KPI InternetCurrentQuarterSalesPerformance toocreate</span><span class="sxs-lookup"><span data-stu-id="d4337-114">toocreate an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="d4337-115">En el Diseñador de modelos de hello, haga clic en hello **FactInternetSales** tabla.</span><span class="sxs-lookup"><span data-stu-id="d4337-115">In hello model designer, click hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="d4337-116">En la cuadrícula de medidas de hello, haga clic en una celda vacía.</span><span class="sxs-lookup"><span data-stu-id="d4337-116">In hello measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="d4337-117">En la barra de fórmulas de hello, encima de la tabla hello, escriba Hola siguiente fórmula:</span><span class="sxs-lookup"><span data-stu-id="d4337-117">In hello formula bar, above hello table, type hello following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="d4337-118">Esta medida actúa como medida Base Hola Hola KPI.</span><span class="sxs-lookup"><span data-stu-id="d4337-118">This measure serves as hello Base measure for hello KPI.</span></span>  
  
4.  <span data-ttu-id="d4337-119">Haga clic en **InternetCurrentQuarterSalesPerformance** > **Crear KPI**.</span><span class="sxs-lookup"><span data-stu-id="d4337-119">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="d4337-120">En el cuadro de diálogo del indicador clave de rendimiento (KPI) de hello en **destino** seleccione **valor absoluto**y, a continuación, escriba **1.1**.</span><span class="sxs-lookup"><span data-stu-id="d4337-120">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="d4337-121">En el campo de control deslizante (baja) izquierdo hello, escriba **1**y, a continuación, en el control deslizante de hello derecha (alto), escriba **1.07**.</span><span class="sxs-lookup"><span data-stu-id="d4337-121">In hello left (low) slider field, type **1**, and then in hello right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="d4337-122">En **Seleccionar estilo de icono**, Hola rombo (rojo), triángulo (amarillo), círculo tipo de icono (verde).</span><span class="sxs-lookup"><span data-stu-id="d4337-122">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="d4337-124">Hola aviso expandible **descripciones** etiqueta debajo de los estilos de icono disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="d4337-124">Notice hello expandable **Descriptions** label below hello available icon styles.</span></span> <span data-ttu-id="d4337-125">Usar descripciones para saludo diversos toomake de elementos KPI ellos más fáciles de identificar en las aplicaciones cliente.</span><span class="sxs-lookup"><span data-stu-id="d4337-125">Use descriptions for hello various KPI elements toomake them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="d4337-126">Haga clic en **Aceptar** toocomplete Hola KPI.</span><span class="sxs-lookup"><span data-stu-id="d4337-126">Click **OK** toocomplete hello KPI.</span></span>  
  
    <span data-ttu-id="d4337-127">En la cuadrícula de medidas de hello, tenga en cuenta Hola icono siguiente toohello **InternetCurrentQuarterSalesPerformance** medida.</span><span class="sxs-lookup"><span data-stu-id="d4337-127">In hello measure grid, notice hello icon next toohello **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="d4337-128">Este icono indica que esta medida sirve como un valor base para un KPI.</span><span class="sxs-lookup"><span data-stu-id="d4337-128">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="d4337-129">un KPI InternetCurrentQuarterMarginPerformance toocreate</span><span class="sxs-lookup"><span data-stu-id="d4337-129">toocreate an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="d4337-130">En la cuadrícula de medidas de Hola de hello **FactInternetSales** de tabla, haga clic en una celda vacía.</span><span class="sxs-lookup"><span data-stu-id="d4337-130">In hello measure grid for hello **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="d4337-131">En la barra de fórmulas de hello, encima de la tabla hello, escriba Hola siguiente fórmula:</span><span class="sxs-lookup"><span data-stu-id="d4337-131">In hello formula bar, above hello table, type hello following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="d4337-132">Haga clic con el botón derecho en **InternetCurrentQuarterMarginPerformance** > **Crear KPI**.</span><span class="sxs-lookup"><span data-stu-id="d4337-132">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="d4337-133">En el cuadro de diálogo del indicador clave de rendimiento (KPI) de hello en **destino** seleccione **valor absoluto**y, a continuación, escriba **1.25**.</span><span class="sxs-lookup"><span data-stu-id="d4337-133">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="d4337-134">En el campo de control deslizante (baja) izquierdo hello, deslice hasta que muestre el campo de hello **0,8**, Hola de diapositiva, a continuación, este campo de control deslizante (alto), hasta que muestre el campo de Hola y **1.03**.</span><span class="sxs-lookup"><span data-stu-id="d4337-134">In hello left (low) slider field, slide until hello field displays **0.8**, and then slide hello right (high) slider field, until hello field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="d4337-135">En **Seleccionar estilo de icono**, seleccione el rombo de hello (rojo), triángulo (amarillo), el tipo de icono de círculo (verde) y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d4337-135">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="d4337-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4337-136">What's next?</span></span>
<span data-ttu-id="d4337-137">[Lección 8: Creación de perspectivas](../tutorials/aas-lesson-8-create-perspectives.md)</span><span class="sxs-lookup"><span data-stu-id="d4337-137">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
