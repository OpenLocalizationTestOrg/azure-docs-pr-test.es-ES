---
title: "Conexión de Excel a SQL Database | Microsoft Docs"
description: "Más información acerca de cómo conectar Microsoft Excel a Base de datos SQL de Azure en la nube. Importación de datos en Excel para la generación de informes y la exploración de datos."
services: sql-database
keywords: conectar excel a sql, importar datos en excel
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 97344d7c0be38b3092a3224074d486b5bb984176
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-excel-to-an-azure-sql-database-and-create-a-report"></a><span data-ttu-id="dab88-105">Conexión de Excel a una Base de datos SQL de Azure y creación de un informe</span><span class="sxs-lookup"><span data-stu-id="dab88-105">Connect Excel to an Azure SQL database and create a report</span></span>

<span data-ttu-id="dab88-106">Conecte Excel a una instancia de SQL Database en la nube e importe datos y cree tablas y gráficos basados en los valores de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="dab88-106">Connect Excel to a SQL database in the cloud and import data and create tables and charts based on values in the database.</span></span> <span data-ttu-id="dab88-107">En este tutorial va a configurar la conexión entre Excel y una tabla de base de datos, guardar el archivo que almacena los datos y la información de conexión de Excel y, finalmente, crear un gráfico dinámico a partir de los valores de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="dab88-107">In this tutorial you will set up the connection between Excel and a database table, save the file that stores data and the connection information for Excel, and then create a pivot chart from the database values.</span></span>

<span data-ttu-id="dab88-108">Antes de comenzar, necesitará una Base de datos SQL en Azure.</span><span class="sxs-lookup"><span data-stu-id="dab88-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="dab88-109">Si no tiene una, consulte [Creación de la primera Base de datos SQL de Azure](sql-database-get-started-portal.md) para tener una base de datos con datos de ejemplo en funcionamiento en unos minutos.</span><span class="sxs-lookup"><span data-stu-id="dab88-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) to get a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="dab88-110">En este artículo se importarán los datos de ejemplo en Excel de dicho artículo, pero puede seguir los pasos con sus propios datos.</span><span class="sxs-lookup"><span data-stu-id="dab88-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="dab88-111">También necesitará una copia de Excel.</span><span class="sxs-lookup"><span data-stu-id="dab88-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="dab88-112">Este artículo usa [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="dab88-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-to-a-sql-database-and-create-an-odc-file"></a><span data-ttu-id="dab88-113">Conexión de Excel a una Base de datos SQL y creación de un archivo odc</span><span class="sxs-lookup"><span data-stu-id="dab88-113">Connect Excel to a SQL database and create an odc file</span></span>
1. <span data-ttu-id="dab88-114">Para conectar Excel a Base de datos SQL, abra Excel y cree un libro nuevo o abra uno existente.</span><span class="sxs-lookup"><span data-stu-id="dab88-114">To connect Excel to SQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="dab88-115">En la barra de menús de la parte superior de la página, haga clic sucesivamente en **Datos**, **De otros orígenes** y **De SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="dab88-115">In the menu bar at the top of the page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Selección de origen de datos: conexión de Excel a Base de datos SQL.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="dab88-117">Se abre el Asistente para la conexión de datos.</span><span class="sxs-lookup"><span data-stu-id="dab88-117">The Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="dab88-118">En el cuadro de diálogo **Conectar con el servidor de la base de datos**, escriba el **nombre del servidor** de SQL Database al que quiere conectarse con el formato <*nombreDeServidor*>**.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="dab88-118">In the **Connect to Database Server** dialog box, type the SQL Database **Server name** you want to connect to in the form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="dab88-119">Por ejemplo, **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="dab88-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="dab88-120">En **Credenciales de inicio de sesión**, haga clic en **Usar el nombre de usuario y la contraseña siguientes**, escriba el **nombre de usuario** y la **contraseña** que haya configurado para el servidor de SQL Database cuando la creó y, finalmente, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dab88-120">Under **Log on credentials**, click **Use the following User Name and Password**, type the **User Name** and **Password** you set up for the SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Especificación de las credenciales del nombre del servidor y de inicio de sesión](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="dab88-122">Dependiendo de su entorno de red, es posible que no pueda conectarse o que pierda la conexión si el servidor de Base de datos SQL no permite el tráfico de la dirección IP del cliente.</span><span class="sxs-lookup"><span data-stu-id="dab88-122">Depending on your network environment, you may not be able to connect or you may lose the connection if the SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="dab88-123">Vaya al [Portal de Azure](https://portal.azure.com/), haga clic en Servidores SQL Server, haga clic en su servidor, haga clic en Firewall en Configuración y agregue la dirección IP de cliente.</span><span class="sxs-lookup"><span data-stu-id="dab88-123">Go to the [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="dab88-124">Consulte [Configuración del firewall](sql-database-configure-firewall-settings.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="dab88-124">See [How to configure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="dab88-125">En el cuadro de diálogo **Seleccionar base de datos y tabla**, seleccione en la lista la base de datos con la que desea trabajar y, después, haga clic en las tablas o vistas con las que desea trabajar (hemos elegido **vGetAllCategories**) y, finalmente, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dab88-125">In the **Select Database and Table** dialog, select the database you want to work with from the list, and then click the tables or views you want to work with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Selección de una base de datos y una tabla.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="dab88-127">Se abre el cuadro de diálogo **Guardar archivo de conexión de datos y finalizar** , donde se proporciona información sobre el archivo de conexión de base de datos de Office (*.odc) que utiliza Excel.</span><span class="sxs-lookup"><span data-stu-id="dab88-127">The **Save Data Connection File and Finish** dialog box opens, where you provide information about the Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="dab88-128">Puede dejar los valores predeterminados o personalizar sus selecciones.</span><span class="sxs-lookup"><span data-stu-id="dab88-128">You can leave the defaults or customize your selections.</span></span>
6. <span data-ttu-id="dab88-129">Puede dejar los valores predeterminados, pero tenga en cuenta el **nombre de archivo** en particular.</span><span class="sxs-lookup"><span data-stu-id="dab88-129">You can leave the defaults, but note the **File Name** in particular.</span></span> <span data-ttu-id="dab88-130">Pueden ayudarle los valores de los campos **Descripción**, **Nombre descriptivo** y **Palabras clave de búsqueda**, y otros usuarios recuerdan a lo que va a conectar y encuentran la conexión.</span><span class="sxs-lookup"><span data-stu-id="dab88-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting to and find the connection.</span></span> <span data-ttu-id="dab88-131">Haga clic en **Intentar utilizar siempre este archivo para actualizar los datos** si desea que la información de conexión se almacene en el archivo odc, para que puede actualizarse cuando se conecta a él y, después, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="dab88-131">Click **Always attempt to use this file to refresh data** if you want connection information stored in the odc file so it can update when you connect to it, and then click **Finish**.</span></span>
   
    ![Almacenamiento de un archivo odc](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="dab88-133">Aparece el cuadro de diálogo **Importar datos** .</span><span class="sxs-lookup"><span data-stu-id="dab88-133">The **Import data** dialog box appears.</span></span>

## <a name="import-the-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="dab88-134">Importación de los datos a Excel y creación de un gráfico dinámico</span><span class="sxs-lookup"><span data-stu-id="dab88-134">Import the data into Excel and create a pivot chart</span></span>
<span data-ttu-id="dab88-135">Ahora que ha establecido la conexión y ha creado el archivo con la información de conexión y de datos, va a importar los datos.</span><span class="sxs-lookup"><span data-stu-id="dab88-135">Now that you've established the connection and created the file with data and connection information, you're reading to import the data.</span></span>

1. <span data-ttu-id="dab88-136">En el cuadro de diálogo **Importar datos**, haga clic en la opción que desee para presentar los datos en la hoja de cálculo y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="dab88-136">In the **Import Data** dialog, click the option you want for presenting your data in the worksheet and then click **OK**.</span></span> <span data-ttu-id="dab88-137">Elegimos **Gráfico dinámico**.</span><span class="sxs-lookup"><span data-stu-id="dab88-137">We chose **PivotChart**.</span></span> <span data-ttu-id="dab88-138">También puede optar por crear una **nueva hoja de cálculo** o **Agregar estos datos al Modelo de datos**.</span><span class="sxs-lookup"><span data-stu-id="dab88-138">You can also choose to create a **New worksheet** or to **Add this data to a Data Model**.</span></span> <span data-ttu-id="dab88-139">Para más información sobre los modelos de datos, consulte [Crear un modelo de datos en Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="dab88-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="dab88-140">Haga clic en **Propiedades** para explorar la información sobre el archivo odc que creó en el paso anterior y elegir las opciones para actualizar los datos.</span><span class="sxs-lookup"><span data-stu-id="dab88-140">Click **Properties** to explore information about the odc file you created in the previous step and to choose options for refreshing the data.</span></span>
   
    ![Elección del formato de datos en Excel](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="dab88-142">La hoja de cálculo ahora tiene una tabla y un gráfico dinámicos vacíos.</span><span class="sxs-lookup"><span data-stu-id="dab88-142">The worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="dab88-143">En **Campos de tabla dinámica**, seleccione todas las casillas de los campos que desea ver.</span><span class="sxs-lookup"><span data-stu-id="dab88-143">Under **PivotTable Fields**, select all the check-boxes for the fields you want to view.</span></span>
   
    ![Configuración de informe de base de datos.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="dab88-145">Si quiere conectar otros libros y hojas de cálculo de Excel a la base de datos, haga clic sucesivamente en **Datos**, en **Conexiones**, en **Agregar**, elija la conexión que creó en la lista y, finalmente, haga clic en **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="dab88-145">If you want to connect other Excel workbooks and worksheets to the database, click **Data**, click **Connections**, click **Add**, choose the connection you created from the list, and then click **Open**.</span></span>
> <span data-ttu-id="dab88-146">![Apertura de una conexión desde otro libro](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="dab88-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="dab88-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dab88-147">Next steps</span></span>
* <span data-ttu-id="dab88-148">Consulte [Conexión a la Base de datos SQL con SQL Server Management Studio y realización de una consulta de T-SQL de ejemplo](sql-database-connect-query-ssms.md) para obtener más información sobre consultas y análisis avanzados.</span><span class="sxs-lookup"><span data-stu-id="dab88-148">Learn how to [Connect to SQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="dab88-149">Más información sobre las ventajas de los [grupos elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="dab88-149">Learn about the benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="dab88-150">Más información en [Crear una aplicación ASP.NET MVC con la autenticación y Base de datos SQL e implementar al Servicio de aplicaciones de Azure](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="dab88-150">Learn how to [create a web application that connects to SQL Database on the back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

