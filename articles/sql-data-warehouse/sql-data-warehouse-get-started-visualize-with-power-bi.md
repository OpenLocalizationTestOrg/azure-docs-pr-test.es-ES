---
title: aaaVisualize datos de almacenamiento de datos de SQL con Microsoft Azure de Power BI
description: "Visualización de datos de Almacenamiento de datos SQL con Power BI"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="f4338-103">Visualización de datos con Power BI</span><span class="sxs-lookup"><span data-stu-id="f4338-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4338-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="f4338-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="f4338-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f4338-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="f4338-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4338-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="f4338-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="f4338-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="f4338-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="f4338-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="f4338-109">Este tutorial muestra cómo toouse Power BI tooconnect tooSQL almacenamiento de datos y crear unas visualizaciones básicas.</span><span class="sxs-lookup"><span data-stu-id="f4338-109">This tutorial shows you how toouse Power BI tooconnect tooSQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f4338-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f4338-110">Prerequisites</span></span>
<span data-ttu-id="f4338-111">toostep a través de este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="f4338-111">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="f4338-112">Un almacén de datos de SQL previamente cargados con base de datos de hello AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="f4338-112">A SQL Data Warehouse pre-loaded with hello AdventureWorksDW database.</span></span> <span data-ttu-id="f4338-113">tooprovision, vea [crear un almacén de datos de SQL] [ Create a SQL Data Warehouse] y elegir los datos de ejemplo de Hola tooload.</span><span class="sxs-lookup"><span data-stu-id="f4338-113">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="f4338-114">Si ya tiene un almacenamiento de datos pero no tiene datos de ejemplo, puede [cargar manualmente los datos de ejemplo][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="f4338-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-tooyour-database"></a><span data-ttu-id="f4338-115">1. Conectar la base de datos de tooyour</span><span class="sxs-lookup"><span data-stu-id="f4338-115">1. Connect tooyour database</span></span>
<span data-ttu-id="f4338-116">tooopen Power BI y conectar la base de datos de AdventureWorksDW tooyour:</span><span class="sxs-lookup"><span data-stu-id="f4338-116">tooopen Power BI and connect tooyour AdventureWorksDW database:</span></span>

1. <span data-ttu-id="f4338-117">Inicio de sesión en hello [portal de Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="f4338-117">Sign into hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="f4338-118">Haga clic en **Bases de datos SQL** y elija su base de datos de Almacenamiento de datos SQL de AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="f4338-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Buscar la base de datos][1]
3. <span data-ttu-id="f4338-120">Haga clic en el botón 'Abrir en Power BI' hello.</span><span class="sxs-lookup"><span data-stu-id="f4338-120">Click hello 'Open in Power BI' button.</span></span>
   
    ![Botón Power BI][2]
4. <span data-ttu-id="f4338-122">Ahora debería ver la página de conexión de almacenamiento de datos SQL de hello mostrar la dirección web de base de datos.</span><span class="sxs-lookup"><span data-stu-id="f4338-122">You should now see hello SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="f4338-123">Haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="f4338-123">Click next.</span></span>
   
    ![Conexión de Power BI][3]
5. <span data-ttu-id="f4338-125">Escriba el nombre de usuario de Azure SQL server y la contraseña y será la base de datos de almacenamiento de datos SQL de tooyour conectados de forma continua.</span><span class="sxs-lookup"><span data-stu-id="f4338-125">Enter your Azure SQL server username and password and you will be fully connected tooyour SQL Data Warehouse database.</span></span>
   
    ![Inicio de sesión de Power BI][4]
6. <span data-ttu-id="f4338-127">Una vez que han iniciado sesión en Power BI, haga clic en conjunto de datos de hello AdventureWorksDW en hoja izquierdo Hola.</span><span class="sxs-lookup"><span data-stu-id="f4338-127">Once you have signed into Power BI, click hello AdventureWorksDW dataset on hello left blade.</span></span> <span data-ttu-id="f4338-128">Se abrirá la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4338-128">This will open hello database.</span></span>
   
    ![Apertura de AdventureWorksDW en Power BI][5]

## <a name="2-create-a-report"></a><span data-ttu-id="f4338-130">2. Creación de un informe</span><span class="sxs-lookup"><span data-stu-id="f4338-130">2. Create a report</span></span>
<span data-ttu-id="f4338-131">Se está ahora listo toouse Power BI tooanalyze los datos de ejemplo AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="f4338-131">You are now ready toouse Power BI tooanalyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="f4338-132">análisis de hello tooperform, AdventureWorksDW tiene una vista denominada AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="f4338-132">tooperform hello analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="f4338-133">Esta vista contiene algunas de las métricas clave de Hola para análisis de ventas de Hola de empresa de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4338-133">This view contains a few of hello key metrics for analyzing hello sales of hello company.</span></span>

1. <span data-ttu-id="f4338-134">toocreate un mapa del importe de ventas según el código de toopostal, en el panel de la derecha de campos de hello, haga clic en hello AggregateSales vista tooexpand se.</span><span class="sxs-lookup"><span data-stu-id="f4338-134">toocreate a map of sales amount according toopostal code, in hello right-hand fields pane, click hello AggregateSales view tooexpand it.</span></span> <span data-ttu-id="f4338-135">Haga clic en tooselect de hello PostalCode y SalesAmount columnas ellos.</span><span class="sxs-lookup"><span data-stu-id="f4338-135">Click hello PostalCode and SalesAmount columns tooselect them.</span></span>
   
    ![Selección de AggregateSales en Power BI][6]
   
    <span data-ttu-id="f4338-137">Power BI reconoce automáticamente estos datos como geográficos y los coloca en un mapa.</span><span class="sxs-lookup"><span data-stu-id="f4338-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Mapa Power BI][7]
2. <span data-ttu-id="f4338-139">Este paso crea un gráfico de barras que muestra la cantidad de ventas por los ingresos del cliente.</span><span class="sxs-lookup"><span data-stu-id="f4338-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="f4338-140">toocreate este toohello vaya expandido AggregateSales vista.</span><span class="sxs-lookup"><span data-stu-id="f4338-140">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="f4338-141">Haga clic en el campo SalesAmount Hola.</span><span class="sxs-lookup"><span data-stu-id="f4338-141">Click hello SalesAmount field.</span></span> <span data-ttu-id="f4338-142">Arrastre hacia la izquierda Hola ingresos de los clientes campo toohello y colóquelo en el eje.</span><span class="sxs-lookup"><span data-stu-id="f4338-142">Drag hello Customer Income field toohello left and drop it into Axis.</span></span>
   
    ![Selección del eje en Power BI][8]
   
    <span data-ttu-id="f4338-144">Gráfico de barras de Hola se mueve sobre Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="f4338-144">We moved hello bar chart over hello left.</span></span>
   
    ![Barra Power BI][9]
3. <span data-ttu-id="f4338-146">Este paso crea un gráfico de líneas que muestra el importe de ventas por fecha de pedido.</span><span class="sxs-lookup"><span data-stu-id="f4338-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="f4338-147">toocreate este toohello vaya expandido AggregateSales vista.</span><span class="sxs-lookup"><span data-stu-id="f4338-147">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="f4338-148">Haga clic en SalesAmount y OrderDate.</span><span class="sxs-lookup"><span data-stu-id="f4338-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="f4338-149">En la columna de visualizaciones de hello haga clic en el icono de gráfico de líneas de hello; Esto es primer icono de hello en la segunda línea de hello en visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="f4338-149">In hello Visualizations column click hello Line Chart icon; this is hello first icon in hello second line under visualizations.</span></span>
   
    ![Selección del gráfico de líneas de Power BI][10]
   
    <span data-ttu-id="f4338-151">Ahora tiene un informe que muestra tres diferentes visualizaciones de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4338-151">You now have a report that shows three different visualizations of hello data.</span></span>
   
    ![LíneaPower BI][11]

<span data-ttu-id="f4338-153">Para guardar el progreso en cualquier momento, haga clic en **Archivo** y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f4338-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4338-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4338-154">Next steps</span></span>
<span data-ttu-id="f4338-155">Ahora que hemos dado algunos toowarm tiempo con datos de ejemplo de Hola, vea cómo demasiado[desarrollar][develop], [cargar][load], o [ migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="f4338-155">Now that we've given you some time toowarm up with hello sample data, see how too[develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="f4338-156">O eche un vistazo a hello [sitio Web de Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="f4338-156">Or take a look at hello [Power BI website][Power BI website].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
