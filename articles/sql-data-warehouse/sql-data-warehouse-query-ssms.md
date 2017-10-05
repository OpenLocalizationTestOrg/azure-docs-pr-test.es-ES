---
title: "Conexión a Azure SQL Data Warehouse: SSMS | Microsoft Docs"
description: Use SQL Server Management Studio (SSMS) para conectarse a y realizar consultas en Azure SQL Data Warehouse.
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
ms.openlocfilehash: 207fb9fd861c66039fbde89681aed3df3a2f4021
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="a1752-103">Conexión a SQL Data Warehouse con SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="a1752-103">Connect to SQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1752-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="a1752-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="a1752-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a1752-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="a1752-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a1752-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="a1752-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="a1752-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="a1752-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="a1752-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="a1752-109">Use SQL Server Management Studio (SSMS) para conectarse a y realizar consultas en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a1752-109">Use SQL Server Management Studio (SSMS) to connect to and query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a1752-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a1752-110">Prerequisites</span></span>
<span data-ttu-id="a1752-111">Para utilizar este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="a1752-111">To use this tutorial, you need:</span></span>

* <span data-ttu-id="a1752-112">Una cuenta de SQL Data Warehouse existente.</span><span class="sxs-lookup"><span data-stu-id="a1752-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="a1752-113">Para crearla, consulte [Creación de una instancia de SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a1752-113">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="a1752-114">SQL Server Management Studio (SSMS) instalado.</span><span class="sxs-lookup"><span data-stu-id="a1752-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="a1752-115">[Instale SSMS][Install SSMS] de forma gratuita si aún no lo tiene.</span><span class="sxs-lookup"><span data-stu-id="a1752-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="a1752-116">El nombre del servidor SQL completo.</span><span class="sxs-lookup"><span data-stu-id="a1752-116">The fully qualified SQL server name.</span></span> <span data-ttu-id="a1752-117">Para encontrarlo, consulte [Conexión a Azure SQL Data Warehouse][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a1752-117">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="a1752-118">1. Conexión a la instancia de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="a1752-118">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="a1752-119">Abra SSMS.</span><span class="sxs-lookup"><span data-stu-id="a1752-119">Open SSMS.</span></span>
2. <span data-ttu-id="a1752-120">Abra el Explorador de objetos.</span><span class="sxs-lookup"><span data-stu-id="a1752-120">Open Object Explorer.</span></span> <span data-ttu-id="a1752-121">Para ello, seleccione **Archivo** > **Conectar Explorador de objetos**.</span><span class="sxs-lookup"><span data-stu-id="a1752-121">To do this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![Explorador de objetos de SQL Server][1]
3. <span data-ttu-id="a1752-123">Rellene los campos en la ventana Conectar al servidor.</span><span class="sxs-lookup"><span data-stu-id="a1752-123">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Conectar al servidor][2]
   
   * <span data-ttu-id="a1752-125">**Nombre del servidor**.</span><span class="sxs-lookup"><span data-stu-id="a1752-125">**Server name**.</span></span> <span data-ttu-id="a1752-126">Escriba el **nombre del servidor** definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a1752-126">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="a1752-127">**Autenticación**.</span><span class="sxs-lookup"><span data-stu-id="a1752-127">**Authentication**.</span></span> <span data-ttu-id="a1752-128">Seleccione **Autenticación de SQL Server** o **Autenticación integrada de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1752-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="a1752-129">**Nombre de usuario** y **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a1752-129">**User Name** and **Password**.</span></span> <span data-ttu-id="a1752-130">Escriba el nombre de usuario y la contraseña si la autenticación de SQL Server se seleccionó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a1752-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="a1752-131">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="a1752-131">Click **Connect**.</span></span>
4. <span data-ttu-id="a1752-132">Para explorar, expanda su Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a1752-132">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="a1752-133">Puede ver las bases de datos asociadas al servidor.</span><span class="sxs-lookup"><span data-stu-id="a1752-133">You can view the databases associated with the server.</span></span> <span data-ttu-id="a1752-134">Expanda AdventureWorksDW para ver las tablas de la base de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a1752-134">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![Explorar AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="a1752-136">2. Ejecución de una consulta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a1752-136">2. Run a sample query</span></span>
<span data-ttu-id="a1752-137">Ahora que se ha establecido una conexión a la base de datos, pasemos a escribir una consulta.</span><span class="sxs-lookup"><span data-stu-id="a1752-137">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="a1752-138">Haga clic con el botón derecho en la base de datos en el Explorador de objetos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a1752-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="a1752-139">Seleccione **Nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="a1752-139">Select **New Query**.</span></span> <span data-ttu-id="a1752-140">Se abre una nueva ventana de consulta.</span><span class="sxs-lookup"><span data-stu-id="a1752-140">A new query window opens.</span></span>
   
    ![Nueva consulta][4]
3. <span data-ttu-id="a1752-142">Copie esta consulta TSQL en la ventana de consulta:</span><span class="sxs-lookup"><span data-stu-id="a1752-142">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="a1752-143">Ejecute la consulta.</span><span class="sxs-lookup"><span data-stu-id="a1752-143">Run the query.</span></span> <span data-ttu-id="a1752-144">Para hacerlo, haga clic en `Execute` o use la combinación de teclas `F5`.</span><span class="sxs-lookup"><span data-stu-id="a1752-144">To do this, click `Execute` or use the following shortcut: `F5`.</span></span>
   
    ![Ejecutar consulta][5]
5. <span data-ttu-id="a1752-146">Consulte los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="a1752-146">Look at the query results.</span></span> <span data-ttu-id="a1752-147">En este ejemplo, la tabla FactInternetSales tiene 60398 filas.</span><span class="sxs-lookup"><span data-stu-id="a1752-147">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Resultados de la consulta][6]

## <a name="next-steps"></a><span data-ttu-id="a1752-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1752-149">Next steps</span></span>
<span data-ttu-id="a1752-150">Ahora que puede conectarse y realizar consultas, pruebe a [visualizar los datos con PowerBI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="a1752-150">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="a1752-151">Para configurar un entorno para la autenticación de Azure Active Directory, consulte [Autenticación en Azure SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a1752-151">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

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
