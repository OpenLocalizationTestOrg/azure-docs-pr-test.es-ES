---
title: 'Carga de datos en Azure SQL Data Warehouse: Data Factory | Microsoft Docs'
description: En este tutorial se cargan datos en Azure SQL Data Warehouse mediante Data Factory de Azure y se utiliza una base de datos de SQL Server como origen de datos.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 12a35213e07ff16bdc1c27be106792bcc032ac80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="0a2f0-103">Carga de datos en SQL Data Warehouse con Data Factory</span><span class="sxs-lookup"><span data-stu-id="0a2f0-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="0a2f0-104">Puede usar Azure Data Factory para cargar datos en Azure SQL Data Warehouse desde cualquiera de los [almacenes de datos de origen compatibles](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0a2f0-104">You can use Azure Data Factory to load data into Azure SQL Data Warehouse from any of the [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="0a2f0-105">Por ejemplo, puede cargar datos desde una base de datos SQL de Azure o una base de datos de Oracle en una instancia de SQL Data Warehouse mediante Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="0a2f0-106">El tutorial de este artículo muestra cómo cargar datos desde una base de datos de SQL Server local en una instancia de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-106">Tutorial in this article shows you how to load data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="0a2f0-107">**Tiempo estimado**: una vez que haya cumplido los requisitos previos, tardará en completar este tutorial aproximadamente entre 10 y 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-107">**Time estimate**: This tutorial takes about 10-15 minutes to complete once the prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a2f0-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0a2f0-108">Prerequisites</span></span>

- <span data-ttu-id="0a2f0-109">Necesita una **base de datos de SQL Server** con tablas que contienen los datos que se copiarán en la instancia de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-109">You need a **SQL Server database** with tables that contain the data to be copied over to the SQL data warehouse.</span></span>  

- <span data-ttu-id="0a2f0-110">Necesita una instancia en línea de **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="0a2f0-111">Si no dispone de un almacén de datos, aprenda a [crear una instancia de Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="0a2f0-111">If you do not already have a data warehouse, learn how to [Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="0a2f0-112">Debe tener una **cuenta de Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="0a2f0-113">Si todavía no tiene una cuenta de almacenamiento, obtenga información sobre cómo [crear una](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0a2f0-113">If you do not already have a storage account, learn how to [Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="0a2f0-114">El rendimiento mejora si la cuenta de almacenamiento y el almacenamiento de datos se encuentran en la misma región de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-114">For best performance, locate the storage account and the data warehouse in the same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="0a2f0-115">Configuración de una factoría de datos</span><span class="sxs-lookup"><span data-stu-id="0a2f0-115">Configure a data factory</span></span>
1. <span data-ttu-id="0a2f0-116">Inicie sesión en el [Portal de Azure][].</span><span class="sxs-lookup"><span data-stu-id="0a2f0-116">Log in to the [Azure portal][].</span></span>
2. <span data-ttu-id="0a2f0-117">Localice el almacenamiento de datos y haga clic en él para abrirlo.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-117">Locate your data warehouse and click to open it.</span></span>
3. <span data-ttu-id="0a2f0-118">En la hoja principal, haga clic en **Cargar datos** > **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-118">In the main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Inicio del Asistente para cargar datos](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="0a2f0-120">Si no tiene una factoría de datos en la suscripción de Azure, verá un cuadro de diálogo **Nueva factoría de datos** en una pestaña independiente del explorador.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of the browser.</span></span> <span data-ttu-id="0a2f0-121">Rellene la información solicitada y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-121">Fill in the requested information, and click **Create**.</span></span> <span data-ttu-id="0a2f0-122">Una vez que se crea la factoría de datos, el cuadro de diálogo **Nueva factoría de datos** se cierra y aparece el cuadro de diálogo **Seleccionar factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-122">After the data factory is created, the **New Data Factory** dialog box closes, and you see the **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="0a2f0-123">Si ya tiene una o varias factorías de datos en la suscripción de Azure, verá el cuadro de diálogo **Seleccionar factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-123">If you have one or more data factories already in the Azure subscription, you see the **Select Data Factory** dialog box.</span></span> <span data-ttu-id="0a2f0-124">En este cuadro de diálogo, puede elegir una factoría de datos existente o hacer clic en **Crear la nueva factoría de datos** para crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** to create a new one.</span></span>

    ![Configurar Data Factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="0a2f0-126">En el cuadro de diálogo **Select Data Factory** (Seleccione la factoría de datos), la opción **Cargar datos** está activada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-126">In the **Select Data Factory** dialog box, the **Load data** option is selected by default.</span></span> <span data-ttu-id="0a2f0-127">Haga clic en **Siguiente** para empezar a crear una tarea de carga de datos.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-127">Click **Next** to start creating a data loading task.</span></span>

## <a name="configure-the-data-factory-properties"></a><span data-ttu-id="0a2f0-128">Configuración de las propiedades de la factoría de datos</span><span class="sxs-lookup"><span data-stu-id="0a2f0-128">Configure the data factory properties</span></span>
<span data-ttu-id="0a2f0-129">Ahora que ha creado una factoría de datos, el siguiente paso consiste en configurar la programación de carga de datos.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-129">Now that you have created a data factory, the next step is to configure the data loading schedule.</span></span>

1. <span data-ttu-id="0a2f0-130">En **Nombre de la tarea**, escriba **DWLoadData-fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="0a2f0-131">Use la opción predeterminada **Ejecutar una vez ahora** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-131">Use the default **Run once now** option, click **Next**.</span></span>

    ![Configuración de la programación de carga](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-the-source-data-store-and-gateway"></a><span data-ttu-id="0a2f0-133">Configuración de la puerta de enlace y el almacén de datos de origen</span><span class="sxs-lookup"><span data-stu-id="0a2f0-133">Configure the source data store and gateway</span></span>
<span data-ttu-id="0a2f0-134">Ahora, indicaremos a Data Factory la base de datos de SQL Server local desde la que se van a cargar los datos.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-134">Now you tell Data Factory about the on-premises SQL Server database from which you want to load data.</span></span>

1. <span data-ttu-id="0a2f0-135">Elija **SQL Server** en el catálogo de almacenes de datos compatibles y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-135">Choose **SQL Server** from the supported source data store catalog, and click **Next**.</span></span>

    ![Selección del origen de SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="0a2f0-137">Se mostrará el cuadro de diálogo **Specify the on-premises SQL Server database** (Especifique la base de datos de SQL Server local).</span><span class="sxs-lookup"><span data-stu-id="0a2f0-137">A **Specify the on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="0a2f0-138">El primer campo **Nombre de conexión** se rellena automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-138">The first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="0a2f0-139">En el segundo campo se pregunta el nombre de la **puerta de enlace**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-139">The second field asks for the name of the **Gateway**.</span></span> <span data-ttu-id="0a2f0-140">Si usa una factoría de datos existente que ya tiene una puerta de enlace, puede reutilizar esta puerta de enlace. Para ello, selecciónela en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-140">If you are using an existing data factory that already has a gateway, you can reuse the gateway by selecting it from the drop-down list.</span></span> <span data-ttu-id="0a2f0-141">Haga clic en el vínculo **Crear puerta de enlace** para crear una puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-141">Click the **Create Gateway** link to create a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="0a2f0-142">Si el almacén de datos de origen es local o se encuentra en una máquina virtual de Azure IaaS, se requiere una instancia de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-142">If the source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="0a2f0-143">Una puerta de enlace tiene una relación de 1 a 1 con una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="0a2f0-144">No se puede usar desde otra factoría de datos, pero sí se puede usar para varias tareas de carga de datos con la misma factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in the same data factory.</span></span> <span data-ttu-id="0a2f0-145">Una puerta de enlace se puede usar para conectarse con varios almacenes de datos cuando se ejecutan tareas de carga de datos.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-145">A gateway can be used to connect to multiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="0a2f0-146">Para información más detallada sobre la puerta de enlace, consulte el artículo [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="0a2f0-146">For detailed information about the gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="0a2f0-147">Se mostrará el cuadro de diálogo **Crear puerta de enlace**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="0a2f0-148">En Nombre, escriba **GatewayForDWLoading**y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="0a2f0-149">Se mostrará el cuadro de diálogo **Configure Gateway** (Configurar puerta de enlace).</span><span class="sxs-lookup"><span data-stu-id="0a2f0-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="0a2f0-150">Haga clic en **Iniciar la configuración rápida en este equipo** para descargar, instalar y registrar automáticamente la puerta de enlace de administración de datos en la máquina actual.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-150">Click **Launch express setup on this computer** to automatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="0a2f0-151">El progreso se muestra en una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-151">The progress is shown in a pop-up window.</span></span> <span data-ttu-id="0a2f0-152">Si la máquina no se puede conectar con el almacén de datos, puede [descargar e instalar manualmente la puerta de enlace](https://www.microsoft.com/download/details.aspx?id=39717) en una máquina que se puede conectar con el almacén de datos y, luego, usar la clave para registrarse.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-152">If the machine cannot connect to the data store, you can manually [download and install the gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect to the data store, and then use the key to register.</span></span>
    > [!NOTE]
    > <span data-ttu-id="0a2f0-153">La configuración rápida funciona de forma nativa con Microsoft Edge e Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-153">The express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="0a2f0-154">Si usa Google Chrome, instale primero la extensión de ClickOnce desde Chrome Web Store.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-154">If you are using Google Chrome, first install the ClickOnce extension from Chrome web store.</span></span>

    ![Inicio de la configuración rápida](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="0a2f0-156">Espere a que termine de configurarse la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-156">Wait for the gateway setup to complete.</span></span> <span data-ttu-id="0a2f0-157">Cuando la puerta de enlace se haya registrado correctamente y esté en línea, se cerrará la ventana emergente y se mostrará la nueva puerta de enlace en el campo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-157">Once the gateway is successfully registered and is online, the pop-up window closes and the new gateway appears in the gateway field.</span></span> <span data-ttu-id="0a2f0-158">A continuación, rellene el resto de los campos necesarios como se indica y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-158">Then fill in the rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="0a2f0-159">**Nombre del servidor**: el nombre del servidor SQL local.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-159">**Server name**: Name of the on-premises SQL Server.</span></span>
    - <span data-ttu-id="0a2f0-160">**Nombre de la base de datos**: la base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="0a2f0-161">**Cifrado de credenciales**: use el valor predeterminado "Por el navegador web".</span><span class="sxs-lookup"><span data-stu-id="0a2f0-161">**Credential encryption**: Use the default "By web browser".</span></span>
    - <span data-ttu-id="0a2f0-162">**Tipo de autenticación**: elija el tipo de autenticación que usa.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-162">**Authentication type**: Choose the type of authentication you are using.</span></span>
    - <span data-ttu-id="0a2f0-163">**Nombre de usuario** y **contraseña**: escriba el nombre de usuario y la contraseña de un usuario que tenga permisos para copiar los datos.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-163">**User name** and **password**: Enter the user name and password for a user who has permission to copy the data.</span></span>

    ![Inicio de la configuración rápida](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="0a2f0-165">El siguiente paso consiste en elegir las tablas desde las que se copiarán los datos.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-165">The next step is to choose the tables from which to copy the data.</span></span> <span data-ttu-id="0a2f0-166">Puede filtrar las tablas usando palabras clave.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-166">You can filter the tables by using keywords.</span></span> <span data-ttu-id="0a2f0-167">Además, puede obtener una vista previa del esquema de datos y tablas en el panel inferior.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-167">And you can preview the data and table schema in the bottom panel.</span></span> <span data-ttu-id="0a2f0-168">Después de finalizar la selección, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-168">After you finish your selection, click **Next**.</span></span>

    ![Selección de tablas](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-the-destination-your-sql-data-warehouse"></a><span data-ttu-id="0a2f0-170">Configuración de la instancia de SQL Data Warehouse de destino</span><span class="sxs-lookup"><span data-stu-id="0a2f0-170">Configure the destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="0a2f0-171">Ahora indique a Data Factory la información de destino.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-171">Now you tell Data Factory about the destination information.</span></span>

1. <span data-ttu-id="0a2f0-172">La información de conexión de SQL Data Warehouse se rellenará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="0a2f0-173">Escriba la contraseña del nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="0a2f0-173">Enter the password for the user name.</span></span> <span data-ttu-id="0a2f0-174">y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-174">and click **Next**.</span></span>

    ![Configuración del destino](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="0a2f0-176">Se muestra una asignación de tabla inteligente que asigna las tablas de origen y de destino basándose en nombres de tablas.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-176">An intelligent table mapping appears that maps source to destination tables based on table names.</span></span> <span data-ttu-id="0a2f0-177">Si la tabla no existe en el destino, ADF creará de manera predeterminada una con el mismo nombre (esto se aplica a SQL Server o Azure SQL Database como origen).</span><span class="sxs-lookup"><span data-stu-id="0a2f0-177">If the table does not exist in the destination, by default ADF will create one with the same name (this applies to SQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="0a2f0-178">También puede optar por la asignación a una tabla existente.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-178">You can also choose to map to an existing table.</span></span> <span data-ttu-id="0a2f0-179">Revise la información y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-179">Review and click **Next**.</span></span>

    ![Asignación de tablas](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="0a2f0-181">Revise la asignación de esquemas y busque mensajes de error o advertencia.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-181">Review the schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="0a2f0-182">La asignación inteligente se basa en el nombre de las columnas.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="0a2f0-183">Si hay una conversión de tipos de datos no compatibles entre las columnas de origen y de destino, verá un mensaje de error junto a la tabla correspondiente.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-183">If there is an unsupported data type conversion between the source and destination column, you see an error message alongside the corresponding table.</span></span> <span data-ttu-id="0a2f0-184">Si opta por permitir que Data Factory cree automáticamente las tablas, puede producirse la conversión de tipos de datos adecuada en caso de que haga falta corregir la incompatibilidad entre los almacenes de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-184">If you choose to let Data Factory auto create the tables, proper data type conversion may happen if needed to fix the incompatibility between source and destination stores.</span></span>

    ![Esquema de asignación](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="0a2f0-186">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-186">Click **Next**.</span></span>

## <a name="configure-the-performance-settings"></a><span data-ttu-id="0a2f0-187">Configuración de las opciones de rendimiento</span><span class="sxs-lookup"><span data-stu-id="0a2f0-187">Configure the performance settings</span></span>
<span data-ttu-id="0a2f0-188">En las opciones de rendimiento, configure una cuenta de Azure Storage para usarla con el fin de almacenar provisionalmente los datos antes de que se carguen en SQL Data Warehouse con buen rendimiento con [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="0a2f0-188">In the Performance configurations, you configure an Azure storage account used for staging the data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="0a2f0-189">Una vez que se realiza la copia, los datos provisionales en almacenamiento se limpiarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-189">After the copy is done, the interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="0a2f0-190">Seleccione una cuenta de Azure Storage y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Configuración del blob de almacenamiento provisional](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-the-pipeline"></a><span data-ttu-id="0a2f0-192">Revisión de la información de resumen e implementación de la canalización</span><span class="sxs-lookup"><span data-stu-id="0a2f0-192">Review summary information and deploy the pipeline</span></span>

<span data-ttu-id="0a2f0-193">Revise la configuración y haga clic en el botón **Finalizar** para implementar la canalización.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-193">Review the configuration and click **Finish** button to deploy the pipeline.</span></span>

![Implementación de la factoría de datos](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="0a2f0-195">Supervisión del progreso de carga de datos</span><span class="sxs-lookup"><span data-stu-id="0a2f0-195">Monitor data loading progress</span></span>

<span data-ttu-id="0a2f0-196">Puede ver el progreso de la implementación y los resultados en la página **Implementación**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-196">You can see the deployment progress and results in the **Deployment** page.</span></span>

1. <span data-ttu-id="0a2f0-197">Una vez que se realice la implementación, haga clic en el vínculo que indica **Haga clic aquí para supervisar canalización de copia** para supervisar el progreso de la carga.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-197">Once the deployment is done, click the link that says **Click here to monitor copy pipeline** to monitor data loading progress.</span></span>

    ![Supervisión de la canalización](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="0a2f0-199">La canalización de carga de datos **DWLoadData-fromSQLServer** recién creada se selecciona de forma automática en el **Explorador de recursos**.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-199">The newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from the left-hand **Resource Explorer**.</span></span>

    ![Visualización de la canalización](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="0a2f0-201">Haga clic en la canalización que se encuentra en el panel del medio para ver el estado detallado de cada tabla que se asigna a una actividad.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-201">Click into the pipeline in the middle panel to see the detailed status for each table that maps to an Activity.</span></span>

    ![Visualización de la actividad de tabla](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="0a2f0-203">Haga clic en una actividad y vea los detalles de carga de datos en el panel derecho, entre ellos, el tamaño de los datos, las filas, el rendimiento, etc.</span><span class="sxs-lookup"><span data-stu-id="0a2f0-203">Further click into an activity and you see the data loading details in the right panel including data size, rows, throughput, etc.</span></span>

    ![Visualización de la información de actividad de tabla](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="0a2f0-205">Para iniciar esta vista de supervisión más adelante, vaya a su instancia de SQL Data Warehouse, haga clic en **Cargar datos > Data Factory de Azure**, seleccione la fábrica y elija **Monitor existing loading tasks** (Supervisar tareas de carga existentes).</span><span class="sxs-lookup"><span data-stu-id="0a2f0-205">To launch this monitoring view later, go to your SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a2f0-206">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a2f0-206">Next steps</span></span>

<span data-ttu-id="0a2f0-207">Para migrar la base de datos a SQL Data Warehouse, consulte el artículo de [introducción a la migración](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="0a2f0-207">To migrate your database to SQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="0a2f0-208">Para más información sobre Azure Data Factory y sus funcionalidades de movimientos de datos, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0a2f0-208">To learn more about Azure Data Factory and its data movement capabilities, see the following articles:</span></span>

- [<span data-ttu-id="0a2f0-209">Introducción al servicio Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="0a2f0-209">Introduction to Azure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="0a2f0-210">Movimiento de datos con la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="0a2f0-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="0a2f0-211">Movimiento de datos hacia y desde Azure SQL Data Warehouse mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0a2f0-211">Move data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="0a2f0-212">Para explorar los datos en SQL Data Warehouse, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0a2f0-212">To explore your data in SQL Data Warehouse, see the following articles:</span></span>

- [<span data-ttu-id="0a2f0-213">Conexión a SQL Data Warehouse con Visual Studio y SSDT</span><span class="sxs-lookup"><span data-stu-id="0a2f0-213">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="0a2f0-214">[Datos visuales con Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="0a2f0-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[Portal de Azure]: https://portal.azure.com
