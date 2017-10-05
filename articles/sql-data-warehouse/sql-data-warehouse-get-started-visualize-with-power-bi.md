---
title: "Visualización de datos de Almacenamiento de datos SQL con Power BI | Microsoft Azure"
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
ms.openlocfilehash: a41393730143b14e91318a61858d989fff3786c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="e6e17-103">Visualización de datos con Power BI</span><span class="sxs-lookup"><span data-stu-id="e6e17-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6e17-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="e6e17-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="e6e17-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e6e17-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="e6e17-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e6e17-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="e6e17-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="e6e17-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="e6e17-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="e6e17-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="e6e17-109">Este tutorial muestra cómo usar Power BI para conectar con Almacenamiento de datos SQL y crear unas visualizaciones básicas.</span><span class="sxs-lookup"><span data-stu-id="e6e17-109">This tutorial shows you how to use Power BI to connect to SQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e6e17-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e6e17-110">Prerequisites</span></span>
<span data-ttu-id="e6e17-111">Para seguir paso a paso este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="e6e17-111">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="e6e17-112">Una instancia de Almacenamiento de datos SQL cargada previamente con la base de datos de AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="e6e17-112">A SQL Data Warehouse pre-loaded with the AdventureWorksDW database.</span></span> <span data-ttu-id="e6e17-113">Para aprovisionarla, consulte [Creación de una instancia de SQL Data Warehouse][Create a SQL Data Warehouse] y seleccione la opción para cargar los datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e6e17-113">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="e6e17-114">Si ya tiene un almacenamiento de datos pero no tiene datos de ejemplo, puede [cargar manualmente los datos de ejemplo][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="e6e17-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-to-your-database"></a><span data-ttu-id="e6e17-115">1. Conectarse a la base de datos</span><span class="sxs-lookup"><span data-stu-id="e6e17-115">1. Connect to your database</span></span>
<span data-ttu-id="e6e17-116">Para abrir Power BI y conectarse a la base de datos AdventureWorksDW:</span><span class="sxs-lookup"><span data-stu-id="e6e17-116">To open Power BI and connect to your AdventureWorksDW database:</span></span>

1. <span data-ttu-id="e6e17-117">Inicie sesión en [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="e6e17-117">Sign into the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="e6e17-118">Haga clic en **Bases de datos SQL** y elija su base de datos de Almacenamiento de datos SQL de AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="e6e17-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Buscar la base de datos][1]
3. <span data-ttu-id="e6e17-120">Haga clic en el botón "Abrir en Power BI".</span><span class="sxs-lookup"><span data-stu-id="e6e17-120">Click the 'Open in Power BI' button.</span></span>
   
    ![Botón Power BI][2]
4. <span data-ttu-id="e6e17-122">Deberá ver la página de conexión de Almacenamiento de datos SQL que muestra la dirección web de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="e6e17-122">You should now see the SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="e6e17-123">Haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="e6e17-123">Click next.</span></span>
   
    ![Conexión de Power BI][3]
5. <span data-ttu-id="e6e17-125">Escriba el nombre de usuario y la contraseña de Azure SQL Server y se conectará completamente a la base de datos de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="e6e17-125">Enter your Azure SQL server username and password and you will be fully connected to your SQL Data Warehouse database.</span></span>
   
    ![Inicio de sesión de Power BI][4]
6. <span data-ttu-id="e6e17-127">Una vez que haya iniciado sesión en Power BI, haga clic en el conjunto de datos AdventureWorksDW en la hoja izquierda.</span><span class="sxs-lookup"><span data-stu-id="e6e17-127">Once you have signed into Power BI, click the AdventureWorksDW dataset on the left blade.</span></span> <span data-ttu-id="e6e17-128">Se abrirá la base de datos.</span><span class="sxs-lookup"><span data-stu-id="e6e17-128">This will open the database.</span></span>
   
    ![Apertura de AdventureWorksDW en Power BI][5]

## <a name="2-create-a-report"></a><span data-ttu-id="e6e17-130">2. Creación de un informe</span><span class="sxs-lookup"><span data-stu-id="e6e17-130">2. Create a report</span></span>
<span data-ttu-id="e6e17-131">Ahora está listo para usar Power BI para analizar los datos de ejemplo AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="e6e17-131">You are now ready to use Power BI to analyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="e6e17-132">Para realizar el análisis, AdventureWorksDW tiene una vista denominada AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="e6e17-132">To perform the analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="e6e17-133">Esta vista contiene algunas de las métricas clave para analizar las ventas de la empresa.</span><span class="sxs-lookup"><span data-stu-id="e6e17-133">This view contains a few of the key metrics for analyzing the sales of the company.</span></span>

1. <span data-ttu-id="e6e17-134">Para crear una asignación del importe de ventas según el código postal, en los campos de la derecha, haga clic en la vista AggregateSales para expandirla.</span><span class="sxs-lookup"><span data-stu-id="e6e17-134">To create a map of sales amount according to postal code, in the right-hand fields pane, click the AggregateSales view to expand it.</span></span> <span data-ttu-id="e6e17-135">A continuación, haga clic en las columnas PostalCode y SalesAmount para seleccionarlas.</span><span class="sxs-lookup"><span data-stu-id="e6e17-135">Click the PostalCode and SalesAmount columns to select them.</span></span>
   
    ![Selección de AggregateSales en Power BI][6]
   
    <span data-ttu-id="e6e17-137">Power BI reconoce automáticamente estos datos como geográficos y los coloca en un mapa.</span><span class="sxs-lookup"><span data-stu-id="e6e17-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Mapa Power BI][7]
2. <span data-ttu-id="e6e17-139">Este paso crea un gráfico de barras que muestra la cantidad de ventas por los ingresos del cliente.</span><span class="sxs-lookup"><span data-stu-id="e6e17-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="e6e17-140">Para crear esto, vaya a la vista expandida de AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="e6e17-140">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="e6e17-141">Haga clic en el campo SalesAmount.</span><span class="sxs-lookup"><span data-stu-id="e6e17-141">Click the SalesAmount field.</span></span> <span data-ttu-id="e6e17-142">Arrastre el campo de ingresos de los clientes hacia la izquierda y colóquelo en el eje.</span><span class="sxs-lookup"><span data-stu-id="e6e17-142">Drag the Customer Income field to the left and drop it into Axis.</span></span>
   
    ![Selección del eje en Power BI][8]
   
    <span data-ttu-id="e6e17-144">Pasamos el gráfico de barras a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="e6e17-144">We moved the bar chart over the left.</span></span>
   
    ![Barra Power BI][9]
3. <span data-ttu-id="e6e17-146">Este paso crea un gráfico de líneas que muestra el importe de ventas por fecha de pedido.</span><span class="sxs-lookup"><span data-stu-id="e6e17-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="e6e17-147">Para crear esto, vaya a la vista expandida de AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="e6e17-147">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="e6e17-148">Haga clic en SalesAmount y OrderDate.</span><span class="sxs-lookup"><span data-stu-id="e6e17-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="e6e17-149">En la columna de visualizaciones, haga clic en el icono de gráfico de líneas, que es el primer icono en la segunda línea bajo las visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="e6e17-149">In the Visualizations column click the Line Chart icon; this is the first icon in the second line under visualizations.</span></span>
   
    ![Selección del gráfico de líneas de Power BI][10]
   
    <span data-ttu-id="e6e17-151">Ahora tiene un informe que muestra tres visualizaciones de los datos diferentes.</span><span class="sxs-lookup"><span data-stu-id="e6e17-151">You now have a report that shows three different visualizations of the data.</span></span>
   
    ![LíneaPower BI][11]

<span data-ttu-id="e6e17-153">Para guardar el progreso en cualquier momento, haga clic en **Archivo** y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e6e17-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6e17-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e6e17-154">Next steps</span></span>
<span data-ttu-id="e6e17-155">Ahora que le hemos dado algún tiempo para preparar los datos de ejemplo, consulte cómo puede [desarrollar][develop], [cargar][load] o [migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="e6e17-155">Now that we've given you some time to warm up with the sample data, see how to [develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="e6e17-156">También puede visitar la [página web de Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="e6e17-156">Or take a look at the [Power BI website][Power BI website].</span></span>

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
[connecting to SQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
