---
title: aaaUse Power BI con almacenamiento de datos SQL | Documentos de Microsoft
description: Sugerencias para usar Power BI con Almacenamiento de datos SQL de Azure para el desarrollo de soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="03e7d-103">Uso de Power BI con Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="03e7d-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="03e7d-104">Al igual que con la base de datos de SQL Azure, en la conexión directa de SQL datos de almacenamiento permite aplicación lógica del usuario tooleverage eficaz junto con capacidades de análisis de Hola de Power BI.</span><span class="sxs-lookup"><span data-stu-id="03e7d-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user tooleverage powerful logical pushdown alongside hello analytical capabilities of Power BI.</span></span>  <span data-ttu-id="03e7d-105">Con conexión directa, las consultas se envían tooyour back-almacenamiento de datos de SQL Azure en tiempo real como explorar datos Hola.</span><span class="sxs-lookup"><span data-stu-id="03e7d-105">With Direct Connect, queries are sent back tooyour Azure SQL Data Warehouse in real time as you explore hello data.</span></span>  <span data-ttu-id="03e7d-106">Esto, combinado con una escala de hello del almacén de datos de SQL, permite a los usuarios de informes dinámicos toocreate en minutos con terabytes de datos.</span><span class="sxs-lookup"><span data-stu-id="03e7d-106">This, combined with hello scale of SQL Data Warehouse, enables users toocreate dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="03e7d-107">Además, la introducción de Hola de hello abierto en el botón de Power BI permite a los usuarios toodirectly conectar Power BI tootheir almacenamiento de datos SQL sin recopilar información de otras partes de Azure.</span><span class="sxs-lookup"><span data-stu-id="03e7d-107">In addition, hello introduction of hello Open in Power BI button allows users toodirectly connect Power BI tootheir SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="03e7d-108">Cuando use Conexión directa, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="03e7d-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="03e7d-109">Especifique el nombre del servidor de acceso completa de hello cuando se conecte (consulte a continuación para obtener más detalles)</span><span class="sxs-lookup"><span data-stu-id="03e7d-109">Specify hello fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="03e7d-110">Garantizar las reglas de firewall se configuran la base de datos de Hola demasiado "permitan el acceso tooAzure services".</span><span class="sxs-lookup"><span data-stu-id="03e7d-110">Ensure firewall rules for hello database are configured too"Allow access tooAzure services".</span></span>
* <span data-ttu-id="03e7d-111">Cada acción, como seleccionar una columna o agregar un filtro directamente consultará el almacenamiento de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="03e7d-111">Every action such as selecting a column or adding a filter will  directly query hello data warehouse</span></span>
* <span data-ttu-id="03e7d-112">Iconos se actualizan aproximadamente cada 15 minutos (no es necesario actualización toobe programado)</span><span class="sxs-lookup"><span data-stu-id="03e7d-112">Tiles are refreshed approximately every 15 minutes (refresh does not need toobe scheduled)</span></span>
* <span data-ttu-id="03e7d-113">La sección de Preguntas y respuestas no está disponible para los conjuntos de datos de Conexión directa.</span><span class="sxs-lookup"><span data-stu-id="03e7d-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="03e7d-114">Los cambios de esquema no se seleccionan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="03e7d-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="03e7d-115">Todas las consultas de conexión directa agotarán el tiempo de espera al cabo de 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="03e7d-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="03e7d-116">Estas restricciones y notas pueden cambiar mientras seguimos tooimprove Hola experiencias.</span><span class="sxs-lookup"><span data-stu-id="03e7d-116">These restrictions and notes may change as we continue tooimprove hello experiences.</span></span> <span data-ttu-id="03e7d-117">Hola tooconnect de pasos se detallan a continuación.</span><span class="sxs-lookup"><span data-stu-id="03e7d-117">hello steps tooconnect are detailed below.</span></span>  

## <a name="using-hello-open-in-power-bi-button"></a><span data-ttu-id="03e7d-118">Utilizando el botón 'Abrir en Power BI' hello</span><span class="sxs-lookup"><span data-stu-id="03e7d-118">Using hello ‘Open in Power BI’ button</span></span>
<span data-ttu-id="03e7d-119">Hola toomove de manera más sencilla entre el almacenamiento de datos SQL y Power BI es con hello abierto en el botón de Power BI.</span><span class="sxs-lookup"><span data-stu-id="03e7d-119">hello easiest way toomove between your SQL Data Warehouse and Power BI is with hello Open in Power BI button.</span></span> <span data-ttu-id="03e7d-120">Este botón permite tooseamlessly empezar a crear nuevos paneles en Power BI.</span><span class="sxs-lookup"><span data-stu-id="03e7d-120">This button allows you tooseamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="03e7d-121">tooget inició navegar por instancia de almacenamiento de datos SQL de tooyour Hola Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="03e7d-121">tooget started navigate tooyour SQL Data Warehouse instance in hello Azure Classic Portal.</span></span>
2. <span data-ttu-id="03e7d-122">Haga clic en el botón 'Abrir en Power BI' hello.</span><span class="sxs-lookup"><span data-stu-id="03e7d-122">Click hello 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="03e7d-123">Si no es capaz de toosign en directamente, o si no tiene una cuenta de Power BI, necesitará toosign en.</span><span class="sxs-lookup"><span data-stu-id="03e7d-123">If we are not able toosign you in directly, or if you do not have a Power BI account, you will need toosign-in.</span></span>  
4. <span data-ttu-id="03e7d-124">Se le dirigirá toohello página de conexión de almacenamiento de datos SQL, con información de Hola desde el almacenamiento de datos de SQL se ha rellenado previamente.</span><span class="sxs-lookup"><span data-stu-id="03e7d-124">You will be directed toohello SQL Data Warehouse connection page, with hello information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="03e7d-125">Después de escribir sus credenciales será tooyour conectados de forma continua de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="03e7d-125">After entering your credentials you will be fully connected tooyour SQL Data Warehouse.</span></span>

## <a name="connecting-through-hello-power-bi-portal"></a><span data-ttu-id="03e7d-126">Conexión a través del portal de Power BI Hola</span><span class="sxs-lookup"><span data-stu-id="03e7d-126">Connecting through hello Power BI portal</span></span>
<span data-ttu-id="03e7d-127">En suma toousing Hola abierto en el botón de Power BI a los usuarios también pueden conectar tootheir almacenamiento de datos SQL a través de hello Portal de Power BI.</span><span class="sxs-lookup"><span data-stu-id="03e7d-127">In addition toousing hello Open in Power BI button, users can also connect tootheir SQL Data Warehouse through hello Power BI Portal.</span></span>

1. <span data-ttu-id="03e7d-128">Haga clic en obtener datos en parte inferior de Hola Hola del panel de exploración.</span><span class="sxs-lookup"><span data-stu-id="03e7d-128">Click 'Get Data' at hello bottom of hello navigation pane.</span></span>
2. <span data-ttu-id="03e7d-129">Seleccione "Bases de datos".</span><span class="sxs-lookup"><span data-stu-id="03e7d-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="03e7d-130">Una vez en la página de bases de datos de hello, seleccione "Almacenamiento de datos de SQL Azure" y, a continuación, haga clic en 'Conectar'.</span><span class="sxs-lookup"><span data-stu-id="03e7d-130">Once on hello Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="03e7d-131">Escriba la información de conexión necesaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="03e7d-131">Enter hello necessary connection information.</span></span>  <span data-ttu-id="03e7d-132">El nombre del servidor y el nombre de la base de datos pueden encontrarse en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="03e7d-132">Your server name and database name can be found in hello Azure Portal.</span></span>
5. <span data-ttu-id="03e7d-133">Se le dirigirá volver toohello la página principal de Power BI y después de la conexión se realiza una nueva entrada en 'Conjuntos de datos' aparecerá con el nombre de saludo de la instancia.</span><span class="sxs-lookup"><span data-stu-id="03e7d-133">You will be directed back toohello main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with hello name of your instance.</span></span>  
6. <span data-ttu-id="03e7d-134">Puede hacer clic en hello nuevo conjunto de datos tooexplore todos Hola tablas y vistas en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="03e7d-134">You can click on hello new dataset tooexplore all of hello tables and views in your database.</span></span> <span data-ttu-id="03e7d-135">Si selecciona una columna enviará un origen de toohello espera de consulta, creará dinámicamente el objeto visual.</span><span class="sxs-lookup"><span data-stu-id="03e7d-135">Selecting a column will send a query back toohello source, dynamically creating your visual.</span></span> <span data-ttu-id="03e7d-136">Estos objetos visuales pueden guardarse en un informe nuevo y anclarse de nuevo panel tooyour.</span><span class="sxs-lookup"><span data-stu-id="03e7d-136">These visuals can be saved in a new report and pinned back tooyour dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
