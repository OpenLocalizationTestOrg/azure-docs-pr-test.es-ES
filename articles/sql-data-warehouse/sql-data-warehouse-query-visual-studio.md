---
title: aaaConnect tooAzure almacenamiento de datos de SQL - VSTS | Documentos de Microsoft
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
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="41a82-103">Conectar tooSQL almacenamiento de datos con Visual Studio como SSDT</span><span class="sxs-lookup"><span data-stu-id="41a82-103">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41a82-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="41a82-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="41a82-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="41a82-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="41a82-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="41a82-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="41a82-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="41a82-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="41a82-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="41a82-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="41a82-109">Use Visual Studio tooquery almacenamiento de datos de SQL Azure en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="41a82-109">Use Visual Studio tooquery Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="41a82-110">Este método usa la extensión de SQL Server Data Tools (SSDT) de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41a82-110">This method uses hello SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="41a82-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="41a82-111">Prerequisites</span></span>
<span data-ttu-id="41a82-112">toouse este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="41a82-112">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="41a82-113">Una cuenta de SQL Data Warehouse existente.</span><span class="sxs-lookup"><span data-stu-id="41a82-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="41a82-114">toocreate uno, vea [crear un almacén de datos de SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="41a82-114">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="41a82-115">SSDT para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41a82-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="41a82-116">Si tiene Visual Studio, probablemente ya tenga este componente.</span><span class="sxs-lookup"><span data-stu-id="41a82-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="41a82-117">Para ver opciones e instrucciones de instalación, consulte [Instalación de Visual Studio 2015 y SSDT para SQL Data Warehouse][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="41a82-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="41a82-118">Hola completo nombre de SQL server.</span><span class="sxs-lookup"><span data-stu-id="41a82-118">hello fully qualified SQL server name.</span></span> <span data-ttu-id="41a82-119">toofind, vea [conectar tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="41a82-119">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="41a82-120">1. Conectar tooyour almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="41a82-120">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="41a82-121">Abra Visual Studio 2013 o 2015</span><span class="sxs-lookup"><span data-stu-id="41a82-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="41a82-122">Abra el Explorador de objetos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41a82-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="41a82-123">toodo, seleccione **vista** > **Explorador de objetos de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="41a82-123">toodo this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![Explorador de objetos de SQL Server][1]
3. <span data-ttu-id="41a82-125">Haga clic en hello **agregar SQL Server** icono.</span><span class="sxs-lookup"><span data-stu-id="41a82-125">Click hello **Add SQL Server** icon.</span></span>
   
    ![Agregar SQL Server][2]
4. <span data-ttu-id="41a82-127">Rellene los campos de hello en ventana de hello conectar tooServer.</span><span class="sxs-lookup"><span data-stu-id="41a82-127">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Conectar tooServer][3]
   
   * <span data-ttu-id="41a82-129">**Nombre del servidor**.</span><span class="sxs-lookup"><span data-stu-id="41a82-129">**Server name**.</span></span> <span data-ttu-id="41a82-130">Escriba hello **nombre del servidor** ha identificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="41a82-130">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="41a82-131">**Autenticación**.</span><span class="sxs-lookup"><span data-stu-id="41a82-131">**Authentication**.</span></span> <span data-ttu-id="41a82-132">Seleccione **Autenticación de SQL Server** o **Autenticación integrada de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41a82-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="41a82-133">**Nombre de usuario** y **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="41a82-133">**User Name** and **Password**.</span></span> <span data-ttu-id="41a82-134">Escriba el nombre de usuario y la contraseña si la autenticación de SQL Server se seleccionó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="41a82-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="41a82-135">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="41a82-135">Click **Connect**.</span></span>
5. <span data-ttu-id="41a82-136">tooexplore, expanda el servidor de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="41a82-136">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="41a82-137">Puede ver bases de datos de hello asociadas con el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a82-137">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="41a82-138">Expandir AdventureWorksDW toosee Hola tablas en la base de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="41a82-138">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Explorar AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="41a82-140">2. Ejecución de una consulta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="41a82-140">2. Run a sample query</span></span>
<span data-ttu-id="41a82-141">Ahora que ha sido establecida tooyour base de datos de una conexión, vamos a escribir una consulta.</span><span class="sxs-lookup"><span data-stu-id="41a82-141">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="41a82-142">Haga clic con el botón derecho en la base de datos en el Explorador de objetos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41a82-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="41a82-143">Seleccione **Nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="41a82-143">Select **New Query**.</span></span> <span data-ttu-id="41a82-144">Se abre una nueva ventana de consulta.</span><span class="sxs-lookup"><span data-stu-id="41a82-144">A new query window opens.</span></span>
   
    ![Nueva consulta][5]
3. <span data-ttu-id="41a82-146">Copie esta consulta TSQL en la ventana de consulta de hello:</span><span class="sxs-lookup"><span data-stu-id="41a82-146">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="41a82-147">Ejecutar consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="41a82-147">Run hello query.</span></span> <span data-ttu-id="41a82-148">toodo esto, haga clic en la flecha verde de Hola o usar hello siguiendo el método abreviado: `CTRL` + `SHIFT` + `E`.</span><span class="sxs-lookup"><span data-stu-id="41a82-148">toodo this, click hello green arrow or use hello following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Ejecutar consulta][6]
5. <span data-ttu-id="41a82-150">Buscar en los resultados de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a82-150">Look at hello query results.</span></span> <span data-ttu-id="41a82-151">En este ejemplo, la tabla FactInternetSales de hello tiene 60398 filas.</span><span class="sxs-lookup"><span data-stu-id="41a82-151">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Resultados de la consulta][7]

## <a name="next-steps"></a><span data-ttu-id="41a82-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="41a82-153">Next steps</span></span>
<span data-ttu-id="41a82-154">Ahora que puede conectarse y consultar, intente [visualizar datos Hola con Power BI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="41a82-154">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="41a82-155">tooconfigure su entorno para la autenticación de Azure Active Directory, vea [autenticar tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="41a82-155">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

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
