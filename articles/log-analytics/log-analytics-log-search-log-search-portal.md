---
title: "portal de la búsqueda de registro aaaUsing hello en análisis de registros de Azure | Documentos de Microsoft"
description: "Este artículo incluye un tutorial que describe cómo toocreate búsquedas de registro y analizar los datos almacenados en el área de trabajo de análisis de registros mediante el portal de la búsqueda de registro de hello.  tutorial de Hello incluye ejecutan algunas consultas sencillas tooreturn diferentes tipos de datos y analizar los resultados."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a><span data-ttu-id="37c47-104">Crear búsquedas de registros de análisis de registros de Azure mediante el portal de la búsqueda de registro de hello</span><span class="sxs-lookup"><span data-stu-id="37c47-104">Create log searches in Azure Log Analytics using hello Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="37c47-105">Este artículo describe portal de búsqueda de registros de hello en análisis de registros de Azure mediante el lenguaje de consulta nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-105">This article describes hello Log Search portal in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="37c47-106">Puede obtener más información sobre el nuevo lenguaje de Hola y obtener Hola procedimiento tooupgrade el área de trabajo en [actualizar la búsqueda de registros de toonew de área de trabajo de análisis de registros de Azure](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="37c47-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="37c47-107">Si el área de trabajo no se ha actualizado toohello nuevo lenguaje de consulta, se debe hacer referencia demasiado[buscar datos mediante búsquedas de registros de análisis de registros](log-analytics-log-searches.md) para obtener información sobre la versión actual de Hola de portal de la búsqueda de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="37c47-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="37c47-108">Este artículo incluye un tutorial que describe cómo toocreate búsquedas de registro y analizar los datos almacenados en el área de trabajo de análisis de registros mediante el portal de la búsqueda de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="37c47-108">This article includes a tutorial that describes how toocreate log searches and analyze data stored in your Log Analytics workspace using hello Log Search portal.</span></span>  <span data-ttu-id="37c47-109">tutorial de Hello incluye ejecutan algunas consultas sencillas tooreturn diferentes tipos de datos y analizar los resultados.</span><span class="sxs-lookup"><span data-stu-id="37c47-109">hello tutorial includes running some simple queries tooreturn different types of data and analyzing results.</span></span>  <span data-ttu-id="37c47-110">Se centra en características de portal de la búsqueda de registros de Hola para modificar la consulta de hello en lugar de modificarlo directamente.</span><span class="sxs-lookup"><span data-stu-id="37c47-110">It focuses on features in hello Log Search portal for modifying hello query rather than modifying it directly.</span></span>  <span data-ttu-id="37c47-111">Para obtener más información acerca de cómo modificar directamente consultas hello, vea hello [referencia del lenguaje de consulta](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="37c47-111">For details on directly editing hello query, see hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="37c47-112">toocreate realiza una búsqueda en portal de análisis avanzado de hello en lugar de portal de la búsqueda de registro de hello, consulte [Getting Started with Hola Portal de análisis](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="37c47-112">toocreate searches in hello Advanced Analytics portal instead of hello Log Search portal, see [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="37c47-113">Ambos portales usar hello misma consulta lenguaje tooaccess Hola mismos datos en el área de trabajo de análisis de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-113">Both portals use hello same query language tooaccess hello same data in hello Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37c47-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="37c47-114">Prerequisites</span></span>
<span data-ttu-id="37c47-115">Este tutorial se da por supuesto que ya tiene un área de trabajo de análisis de registros con al menos un origen conectado que genera los datos de hello consultas tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="37c47-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for hello queries tooanalyze.</span></span>  

- <span data-ttu-id="37c47-116">Si no tiene un área de trabajo, puede crear uno mediante el procedimiento de hello en [empezar a trabajar con un área de trabajo de análisis de registros](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="37c47-116">If you don't have a workspace, you can create a free one using hello procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="37c47-117">Conecte uno menos [el agente de Windows](log-analytics-windows-agents.md) o un [agente Linux](log-analytics-linux-agents.md) toohello área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="37c47-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) toohello workspace.</span></span>  

## <a name="open-hello-log-search-portal"></a><span data-ttu-id="37c47-118">Portal de la búsqueda de registro de hello abierto</span><span class="sxs-lookup"><span data-stu-id="37c47-118">Open hello Log Search portal</span></span>
<span data-ttu-id="37c47-119">Empiece por abrir el portal de la búsqueda de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-119">Start by opening hello Log Search portal.</span></span>  <span data-ttu-id="37c47-120">Puede acceder a ella de hello portal de Azure o portal de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-120">You can access it in either hello Azure portal or hello OMS portal.</span></span>

1. <span data-ttu-id="37c47-121">Hola abrir portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="37c47-121">Open hello Azure portal.</span></span>
2. <span data-ttu-id="37c47-122">Desplácese tooLog análisis y seleccione el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="37c47-122">Navigate tooLog Analytics and select your workspace.</span></span>
3. <span data-ttu-id="37c47-123">Seleccionar una opción **Log Search** toostay Hola portal o inicie Hola OMS portal de Azure seleccionando **Portal de OMS** y, a continuación, haga clic en botón de búsqueda de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-123">Either select **Log Search** toostay in hello Azure portal or launch hello OMS portal by selecting **OMS Portal** and then clicking hello Log Search button.</span></span>

![Botón Log Search (Búsqueda de registros)](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="37c47-125">Creación de una búsqueda simple</span><span class="sxs-lookup"><span data-stu-id="37c47-125">Create a simple search</span></span>
<span data-ttu-id="37c47-126">tooretrieve de manera más rápida de Hello algunos toowork de datos con es una consulta simple que devuelve todos los registros en la tabla.</span><span class="sxs-lookup"><span data-stu-id="37c47-126">hello quickest way tooretrieve some data toowork with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="37c47-127">Si dispone de todas las ventanas o los clientes de Linux conectados tooyour área de trabajo, tendrá que datos de Hola o eventos (Windows) o una tabla de Syslog (Linux).</span><span class="sxs-lookup"><span data-stu-id="37c47-127">If you have any Windows or Linux clients connected tooyour workspace, then you'll have data in either hello Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="37c47-128">Escriba un hello las siguientes consultas en el cuadro de búsqueda de Hola y haga clic en el botón de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-128">Type one hello following queries in hello search box and click hello search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="37c47-129">Se devuelven los datos en la vista de lista predeterminada de Hola y puede ver el número total de registros se han devuelto.</span><span class="sxs-lookup"><span data-stu-id="37c47-129">Data is returned in hello default list view, and you can see how many total records were returned.</span></span>

![Consulta sencilla](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="37c47-131">Solo hello primera algunas propiedades de cada registro se muestran.</span><span class="sxs-lookup"><span data-stu-id="37c47-131">Only hello first few properties of each record are displayed.</span></span>  <span data-ttu-id="37c47-132">Haga clic en **mostrar más** toodisplay todas las propiedades de un registro concreto.</span><span class="sxs-lookup"><span data-stu-id="37c47-132">Click **show more** toodisplay all properties for a particular record.</span></span>

![Detalles del registro](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a><span data-ttu-id="37c47-134">Establecer el ámbito de la hora de Hola</span><span class="sxs-lookup"><span data-stu-id="37c47-134">Set hello time scope</span></span>
<span data-ttu-id="37c47-135">Cada registro recopilado por el análisis de registro tiene una **TimeGenerated** propiedad que contiene Hola fecha y hora en que se creó ese registro Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains hello date and time that hello record was created.</span></span>  <span data-ttu-id="37c47-136">Una consulta en el portal de la búsqueda de registro de hello solo devuelve los registros con un **TimeGenerated** ámbito Hola tiempo que se muestra en la parte izquierda de la pantalla de bienvenida de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-136">A query in hello Log Search portal only returns records with a **TimeGenerated** within hello time scope that's displayed on hello left side of hello screen.</span></span>  

<span data-ttu-id="37c47-137">Puede cambiar filtro de tiempo de hello mediante la selección de la lista desplegable de Hola o modificando el control deslizante de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-137">You can change hello time filter either by selecting hello dropdown or by modifying hello slider.</span></span>  <span data-ttu-id="37c47-138">control deslizante de Hello muestra un gráfico de barras que muestra hello relativa número de registros para cada segmento de tiempo de intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="37c47-138">hello slider displays a bar graph that shows hello relative number of records for each time segment within hello range.</span></span>  <span data-ttu-id="37c47-139">Este segmento variará según el intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="37c47-139">This segment will vary depending on hello range.</span></span>

<span data-ttu-id="37c47-140">ámbito de tiempo predeterminado de Hello es **1 día**.</span><span class="sxs-lookup"><span data-stu-id="37c47-140">hello default time scope is **1 day**.</span></span>  <span data-ttu-id="37c47-141">Cambie este valor demasiado**7 días**, y debe aumentar el número total de Hola de registros.</span><span class="sxs-lookup"><span data-stu-id="37c47-141">Change this value too**7 days**, and hello total number of records should increase.</span></span>

![Ámbito de tiempo y fecha](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a><span data-ttu-id="37c47-143">Filtrar los resultados de consulta de Hola</span><span class="sxs-lookup"><span data-stu-id="37c47-143">Filter results of hello query</span></span>
<span data-ttu-id="37c47-144">En hello lado izquierdo de la pantalla de bienvenida es el panel de filtro de Hola que permite tooadd filtrado de la consulta toohello sin modificarlo directamente.</span><span class="sxs-lookup"><span data-stu-id="37c47-144">On hello left side of hello screen is hello filter pane which allows you tooadd filtering toohello query without modifying it directly.</span></span>  <span data-ttu-id="37c47-145">Varias propiedades de registros de hello devueltos se muestran con sus valores superiores diez con su número de registros.</span><span class="sxs-lookup"><span data-stu-id="37c47-145">Several properties of hello records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="37c47-146">Si está trabajando con **eventos**, seleccione Hola casilla de verificación junto a demasiado**Error** en **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="37c47-146">If you're working with **Event**, select hello checkbox next too**Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="37c47-147">Si está trabajando con **Syslog**, seleccione Hola casilla de verificación junto a demasiado**err** en **SEVERITYLEVEL**.</span><span class="sxs-lookup"><span data-stu-id="37c47-147">If you're working with **Syslog**, select hello checkbox next too**err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="37c47-148">Esto cambia la consulta de hello tooone de hello después toolimit Hola provoca eventos tooerror.</span><span class="sxs-lookup"><span data-stu-id="37c47-148">This changes hello query tooone of hello following toolimit hello results tooerror events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtrar](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="37c47-150">Panel de filtro de agregar propiedades toohello seleccionando **agregar toofilters** desde el menú de la propiedad de hello en uno de los registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-150">Add properties toohello filter pane by selecting **Add toofilters** from hello property menu on one of hello records.</span></span>

![Agregar menús toofilter](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="37c47-152">Puede establecer Hola mismo filtro seleccionando **filtro** desde el menú de la propiedad de Hola para un registro con el valor de hello desea toofilter.</span><span class="sxs-lookup"><span data-stu-id="37c47-152">You can set hello same filter by selecting **Filter** from hello property menu for a record with hello value you want toofilter.</span></span>  

<span data-ttu-id="37c47-153">Solo tiene hello **filtro** opción de propiedades con su nombre en azul.</span><span class="sxs-lookup"><span data-stu-id="37c47-153">You only have hello **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="37c47-154">Se trata de campos que permiten *búsquedas* que se indexan para las condiciones de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="37c47-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="37c47-155">Campos en gris son *permite realizar búsquedas de texto libre* los campos que solo tienen hello **mostrar referencias** opción.</span><span class="sxs-lookup"><span data-stu-id="37c47-155">Fields in grey are *free text searchable* fields which only have hello **Show references** option.</span></span>  <span data-ttu-id="37c47-156">Esta opción devuelve los registros que contienen ese valor en cualquier propiedad.</span><span class="sxs-lookup"><span data-stu-id="37c47-156">This option returns records that have that value in any property.</span></span>

![Menú Filtrar](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="37c47-158">Puede agrupar los resultados de hello en una sola propiedad seleccionando hello **Agrupar por** opción en el menú del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="37c47-158">You can group hello results on a single property by selecting hello **Group by** option in hello record menu.</span></span>  <span data-ttu-id="37c47-159">Esto agregará una [resumir](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) consulta tooyour de operador que muestra los resultados de hello en un gráfico.</span><span class="sxs-lookup"><span data-stu-id="37c47-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query that displays hello results in a chart.</span></span>  <span data-ttu-id="37c47-160">Puede agrupar por más de una propiedad, pero debe generar consulta de hello tooedit directamente.</span><span class="sxs-lookup"><span data-stu-id="37c47-160">You can group on more than one property, but you would need tooedit hello query directly.</span></span>  <span data-ttu-id="37c47-161">Siguiente Hola Hola del menú Registro Hola seleccione **equipo** propiedad y seleccione **Group by 'Computer'**.</span><span class="sxs-lookup"><span data-stu-id="37c47-161">Select hello record menu next hello hello **Computer** property and select **Group by 'Computer'**.</span></span>  

![Agrupar por equipo](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="37c47-163">Trabajo con resultados</span><span class="sxs-lookup"><span data-stu-id="37c47-163">Work with results</span></span>
<span data-ttu-id="37c47-164">portal de la búsqueda de registro de Hello tiene una variedad de características para trabajar con hello los resultados de una consulta.</span><span class="sxs-lookup"><span data-stu-id="37c47-164">hello Log Search portal has a variety of features for working with hello results of a query.</span></span>  <span data-ttu-id="37c47-165">Puede ordenar, filtrar y agrupar datos de resultados de tooanalyze Hola sin modificar la consulta real Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-165">You can sort, filter, and group results tooanalyze hello data without modifying hello actual query.</span></span>  <span data-ttu-id="37c47-166">Los resultados de una consulta no se ordenan de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="37c47-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="37c47-167">tooview Hola datos en forma de tabla que proporciona opciones adicionales para filtrar y ordenar, haga clic en **tabla**.</span><span class="sxs-lookup"><span data-stu-id="37c47-167">tooview hello data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Vista Tabla](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="37c47-169">Haga clic en la flecha de Hola por un detalles de hello tooview registros para ese registro.</span><span class="sxs-lookup"><span data-stu-id="37c47-169">Click hello arrow by a record tooview hello details for that record.</span></span>

![Ordenar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="37c47-171">Ordene cualquier campo haciendo clic en el encabezado de la columna.</span><span class="sxs-lookup"><span data-stu-id="37c47-171">Sort on any field by clicking on its column header.</span></span>

![Ordenar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="37c47-173">Filtrar los resultados de hello en un valor específico en la columna de hello haciendo clic en el botón de filtro de Hola y proporcionar una condición de filtro.</span><span class="sxs-lookup"><span data-stu-id="37c47-173">Filter hello results on a specific value in hello column by clicking hello filter button and providing a filter condition.</span></span>

![Filtrar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="37c47-175">Agrupar en una columna arrastrando su parte superior toohello de encabezado de columna de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-175">Group on a column by dragging its column header toohello top of hello results.</span></span>  <span data-ttu-id="37c47-176">Puede agrupar por varios campos, arrastre la parte superior toohello de varias columnas.</span><span class="sxs-lookup"><span data-stu-id="37c47-176">You can group on multiple fields by dragging multiple columns toohello top.</span></span>

![Agrupar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="37c47-178">Trabajo con datos de rendimiento</span><span class="sxs-lookup"><span data-stu-id="37c47-178">Work with performance data</span></span>
<span data-ttu-id="37c47-179">Los datos de rendimiento para los agentes de Windows y Linux se almacenan en el área de trabajo de análisis de registros de Hola Hola **rendimiento** tabla.</span><span class="sxs-lookup"><span data-stu-id="37c47-179">Performance data for both Windows and Linux agents is stored in hello Log Analytics workspace in hello **Perf** table.</span></span>  <span data-ttu-id="37c47-180">Los registros de rendimiento tienen la misma apariencia que cualquier otro registro y puede escribir una consulta sencilla que devuelva todos los datos de rendimiento igual que se hace con los eventos.</span><span class="sxs-lookup"><span data-stu-id="37c47-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Datos de rendimiento](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="37c47-182">La devolución de millones de registros para todos los objetos y contadores de rendimiento no resulta muy útil.</span><span class="sxs-lookup"><span data-stu-id="37c47-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="37c47-183">Puede usar Hola mismos métodos usados por encima de los datos de hello toofilter o simplemente escriba Hola siguiente consultar directamente en el cuadro de búsqueda de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="37c47-183">You can use hello same methods you used above toofilter hello data or just type hello following query directly into hello log search box.</span></span>  <span data-ttu-id="37c47-184">Esta devolverá únicamente los registros de utilización del procesador para los equipos con Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="37c47-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Utilización del procesador](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="37c47-186">Esto limita el contador de hello datos tooa determinado, pero aún no lo coloque en un formulario que es especialmente útil.</span><span class="sxs-lookup"><span data-stu-id="37c47-186">This limits hello data tooa particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="37c47-187">Puede mostrar los datos de hello en un gráfico de líneas, pero primero debe toogroup por equipo y TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="37c47-187">You can display hello data in a line chart, but first need toogroup it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="37c47-188">toogroup por varios campos, es necesario tener toomodify Hola query directamente, por lo que modificar Hola consulta toohello.</span><span class="sxs-lookup"><span data-stu-id="37c47-188">toogroup on multiple fields, you need toomodify hello query directly, so modify hello query toohello following.</span></span>  <span data-ttu-id="37c47-189">Esto utiliza hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) función hello **CounterValue** propiedad toocalculate Hola promedio durante cada hora.</span><span class="sxs-lookup"><span data-stu-id="37c47-189">This uses hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on hello **CounterValue** property toocalculate hello average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Gráfico con datos de rendimiento](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="37c47-191">Ahora que los datos de hello convenientemente están agrupados, puede mostrar en un gráfico visual agregando hello [representar](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operador.</span><span class="sxs-lookup"><span data-stu-id="37c47-191">Now that hello data is suitably grouped, you can display it in a visual chart by adding hello [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Gráfico de líneas](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="37c47-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37c47-193">Next steps</span></span>

- <span data-ttu-id="37c47-194">Obtener más información sobre el lenguaje de consulta de análisis de registros de hello en [Getting Started with Hola Portal de análisis](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="37c47-194">Learn more about hello Log Analytics query language at [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="37c47-195">Ver un tutorial con hello [portal Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587) que le permite toorun Hola mismo las consultas y acceso Hola mismos datos que el portal de la búsqueda de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="37c47-195">Walk through a tutorial using hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you toorun hello same queries and access hello same data as hello Log Search portal.</span></span>
