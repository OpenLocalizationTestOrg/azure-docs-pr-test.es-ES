---
title: "Conexión a Azure SQL Data Warehouse: VSTS | Microsoft Docs"
description: Consultas en Almacenamiento de datos SQL con Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 1e44c6c3c47034a892753c69c5ef22a5eac18c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="07751-103">Conexión a SQL Data Warehouse con Visual Studio y SSDT</span><span class="sxs-lookup"><span data-stu-id="07751-103">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07751-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="07751-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="07751-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="07751-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="07751-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07751-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="07751-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="07751-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="07751-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="07751-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="07751-109">Utilice Visual Studio para realizar consultas en Almacenamiento de datos SQL de Azure en unos minutos.</span><span class="sxs-lookup"><span data-stu-id="07751-109">Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="07751-110">Este método usa la extensión SQL Server Data Tools (SSDT) de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07751-110">This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="07751-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="07751-111">Prerequisites</span></span>
<span data-ttu-id="07751-112">Para utilizar este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="07751-112">To use this tutorial, you need:</span></span>

* <span data-ttu-id="07751-113">Una cuenta de SQL Data Warehouse existente.</span><span class="sxs-lookup"><span data-stu-id="07751-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="07751-114">Para crearla, consulte [Creación de una instancia de SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="07751-114">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="07751-115">SSDT para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07751-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="07751-116">Si tiene Visual Studio, probablemente ya tenga este componente.</span><span class="sxs-lookup"><span data-stu-id="07751-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="07751-117">Para ver opciones e instrucciones de instalación, consulte [Instalación de Visual Studio 2015 y SSDT para SQL Data Warehouse][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="07751-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="07751-118">El nombre del servidor SQL completo.</span><span class="sxs-lookup"><span data-stu-id="07751-118">The fully qualified SQL server name.</span></span> <span data-ttu-id="07751-119">Para encontrarlo, consulte [Conexión a Azure SQL Data Warehouse][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="07751-119">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="07751-120">1. Conexión a la instancia de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="07751-120">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="07751-121">Abra Visual Studio 2013 o 2015</span><span class="sxs-lookup"><span data-stu-id="07751-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="07751-122">Abra el Explorador de objetos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="07751-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="07751-123">Para ello, seleccione **Ver** > **Explorador de objetos de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="07751-123">To do this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![Explorador de objetos de SQL Server][1]
3. <span data-ttu-id="07751-125">Haga clic en el botón **Agregar SQL Server** .</span><span class="sxs-lookup"><span data-stu-id="07751-125">Click the **Add SQL Server** icon.</span></span>
   
    ![Agregar SQL Server][2]
4. <span data-ttu-id="07751-127">Rellene los campos en la ventana Conectar al servidor.</span><span class="sxs-lookup"><span data-stu-id="07751-127">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Conectar al servidor][3]
   
   * <span data-ttu-id="07751-129">**Nombre del servidor**.</span><span class="sxs-lookup"><span data-stu-id="07751-129">**Server name**.</span></span> <span data-ttu-id="07751-130">Escriba el **nombre del servidor** definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="07751-130">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="07751-131">**Autenticación**.</span><span class="sxs-lookup"><span data-stu-id="07751-131">**Authentication**.</span></span> <span data-ttu-id="07751-132">Seleccione **Autenticación de SQL Server** o **Autenticación integrada de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07751-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="07751-133">**Nombre de usuario** y **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="07751-133">**User Name** and **Password**.</span></span> <span data-ttu-id="07751-134">Escriba el nombre de usuario y la contraseña si la autenticación de SQL Server se seleccionó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="07751-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="07751-135">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="07751-135">Click **Connect**.</span></span>
5. <span data-ttu-id="07751-136">Para explorar, expanda su Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="07751-136">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="07751-137">Puede ver las bases de datos asociadas al servidor.</span><span class="sxs-lookup"><span data-stu-id="07751-137">You can view the databases associated with the server.</span></span> <span data-ttu-id="07751-138">Expanda AdventureWorksDW para ver las tablas de la base de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="07751-138">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![Explorar AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="07751-140">2. Ejecución de una consulta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="07751-140">2. Run a sample query</span></span>
<span data-ttu-id="07751-141">Ahora que se ha establecido una conexión a la base de datos, pasemos a escribir una consulta.</span><span class="sxs-lookup"><span data-stu-id="07751-141">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="07751-142">Haga clic con el botón derecho en la base de datos en el Explorador de objetos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="07751-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="07751-143">Seleccione **Nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="07751-143">Select **New Query**.</span></span> <span data-ttu-id="07751-144">Se abre una nueva ventana de consulta.</span><span class="sxs-lookup"><span data-stu-id="07751-144">A new query window opens.</span></span>
   
    ![Nueva consulta][5]
3. <span data-ttu-id="07751-146">Copie esta consulta TSQL en la ventana de consulta:</span><span class="sxs-lookup"><span data-stu-id="07751-146">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="07751-147">Ejecute la consulta.</span><span class="sxs-lookup"><span data-stu-id="07751-147">Run the query.</span></span> <span data-ttu-id="07751-148">Para hacerlo, haga clic en la flecha verde o use la combinación de teclas `CTRL`+`SHIFT`+`E`.</span><span class="sxs-lookup"><span data-stu-id="07751-148">To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Ejecutar consulta][6]
5. <span data-ttu-id="07751-150">Consulte los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="07751-150">Look at the query results.</span></span> <span data-ttu-id="07751-151">En este ejemplo, la tabla FactInternetSales tiene 60398 filas.</span><span class="sxs-lookup"><span data-stu-id="07751-151">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Resultados de la consulta][7]

## <a name="next-steps"></a><span data-ttu-id="07751-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="07751-153">Next steps</span></span>
<span data-ttu-id="07751-154">Ahora que puede conectarse y realizar consultas, pruebe a [visualizar los datos con PowerBI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="07751-154">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="07751-155">Para configurar un entorno para la autenticación de Azure Active Directory, consulte [Autenticación en Azure SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="07751-155">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
