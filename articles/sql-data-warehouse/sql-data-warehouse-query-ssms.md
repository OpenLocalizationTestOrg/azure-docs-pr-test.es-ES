---
title: aaaConnect tooAzure almacenamiento de datos de SQL - SSMS | Documentos de Microsoft
description: Usar SQL Server Management Studio (SSMS) tooconnect tooand consulta de almacenamiento de datos de SQL Azure.
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="4d20b-103">Conectar tooSQL almacenamiento de datos con SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="4d20b-103">Connect tooSQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d20b-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="4d20b-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="4d20b-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4d20b-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="4d20b-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d20b-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="4d20b-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="4d20b-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="4d20b-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="4d20b-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="4d20b-109">Usar SQL Server Management Studio (SSMS) tooconnect tooand consulta de almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4d20b-109">Use SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4d20b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4d20b-110">Prerequisites</span></span>
<span data-ttu-id="4d20b-111">toouse este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="4d20b-111">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="4d20b-112">Una cuenta de SQL Data Warehouse existente.</span><span class="sxs-lookup"><span data-stu-id="4d20b-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="4d20b-113">toocreate uno, vea [crear un almacén de datos de SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="4d20b-113">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="4d20b-114">SQL Server Management Studio (SSMS) instalado.</span><span class="sxs-lookup"><span data-stu-id="4d20b-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="4d20b-115">[Instale SSMS][Install SSMS] de forma gratuita si aún no lo tiene.</span><span class="sxs-lookup"><span data-stu-id="4d20b-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="4d20b-116">Hola completo nombre de SQL server.</span><span class="sxs-lookup"><span data-stu-id="4d20b-116">hello fully qualified SQL server name.</span></span> <span data-ttu-id="4d20b-117">toofind, vea [conectar tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="4d20b-117">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="4d20b-118">1. Conectar tooyour almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="4d20b-118">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="4d20b-119">Abra SSMS.</span><span class="sxs-lookup"><span data-stu-id="4d20b-119">Open SSMS.</span></span>
2. <span data-ttu-id="4d20b-120">Abra el Explorador de objetos.</span><span class="sxs-lookup"><span data-stu-id="4d20b-120">Open Object Explorer.</span></span> <span data-ttu-id="4d20b-121">toodo, seleccione **archivo** > **conectar Explorador de objetos**.</span><span class="sxs-lookup"><span data-stu-id="4d20b-121">toodo this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![Explorador de objetos de SQL Server][1]
3. <span data-ttu-id="4d20b-123">Rellene los campos de hello en ventana de hello conectar tooServer.</span><span class="sxs-lookup"><span data-stu-id="4d20b-123">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Conectar tooServer][2]
   
   * <span data-ttu-id="4d20b-125">**Nombre del servidor**.</span><span class="sxs-lookup"><span data-stu-id="4d20b-125">**Server name**.</span></span> <span data-ttu-id="4d20b-126">Escriba hello **nombre del servidor** ha identificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4d20b-126">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="4d20b-127">**Autenticación**.</span><span class="sxs-lookup"><span data-stu-id="4d20b-127">**Authentication**.</span></span> <span data-ttu-id="4d20b-128">Seleccione **Autenticación de SQL Server** o **Autenticación integrada de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d20b-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="4d20b-129">**Nombre de usuario** y **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4d20b-129">**User Name** and **Password**.</span></span> <span data-ttu-id="4d20b-130">Escriba el nombre de usuario y la contraseña si la autenticación de SQL Server se seleccionó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4d20b-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="4d20b-131">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="4d20b-131">Click **Connect**.</span></span>
4. <span data-ttu-id="4d20b-132">tooexplore, expanda el servidor de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4d20b-132">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="4d20b-133">Puede ver bases de datos de hello asociadas con el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d20b-133">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="4d20b-134">Expandir AdventureWorksDW toosee Hola tablas en la base de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4d20b-134">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Explorar AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="4d20b-136">2. Ejecución de una consulta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4d20b-136">2. Run a sample query</span></span>
<span data-ttu-id="4d20b-137">Ahora que ha sido establecida tooyour base de datos de una conexión, vamos a escribir una consulta.</span><span class="sxs-lookup"><span data-stu-id="4d20b-137">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="4d20b-138">Haga clic con el botón derecho en la base de datos en el Explorador de objetos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4d20b-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="4d20b-139">Seleccione **Nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="4d20b-139">Select **New Query**.</span></span> <span data-ttu-id="4d20b-140">Se abre una nueva ventana de consulta.</span><span class="sxs-lookup"><span data-stu-id="4d20b-140">A new query window opens.</span></span>
   
    ![Nueva consulta][4]
3. <span data-ttu-id="4d20b-142">Copie esta consulta TSQL en la ventana de consulta de hello:</span><span class="sxs-lookup"><span data-stu-id="4d20b-142">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="4d20b-143">Ejecutar consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="4d20b-143">Run hello query.</span></span> <span data-ttu-id="4d20b-144">toodo, haga clic en `Execute` o use Hola después de método abreviado: `F5`.</span><span class="sxs-lookup"><span data-stu-id="4d20b-144">toodo this, click `Execute` or use hello following shortcut: `F5`.</span></span>
   
    ![Ejecutar consulta][5]
5. <span data-ttu-id="4d20b-146">Buscar en los resultados de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d20b-146">Look at hello query results.</span></span> <span data-ttu-id="4d20b-147">En este ejemplo, la tabla FactInternetSales de hello tiene 60398 filas.</span><span class="sxs-lookup"><span data-stu-id="4d20b-147">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Resultados de la consulta][6]

## <a name="next-steps"></a><span data-ttu-id="4d20b-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4d20b-149">Next steps</span></span>
<span data-ttu-id="4d20b-150">Ahora que puede conectarse y consultar, intente [visualizar datos Hola con Power BI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="4d20b-150">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="4d20b-151">tooconfigure su entorno para la autenticación de Azure Active Directory, vea [autenticar tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="4d20b-151">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
