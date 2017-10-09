---
title: "datos de aaaLoad en almacenamiento de datos de SQL Azure: factoría de datos | Documentos de Microsoft"
description: Este tutorial carga datos en almacenamiento de datos de SQL Azure mediante Data Factory de Azure y utiliza una base de datos de SQL Server como origen de datos de Hola.
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
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="65f4b-103">Carga de datos en SQL Data Warehouse con Data Factory</span><span class="sxs-lookup"><span data-stu-id="65f4b-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="65f4b-104">Puede usar datos de tooload de Data Factory de Azure en almacenamiento de datos de SQL Azure desde cualquiera de hello [admite almacenes de datos de origen](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="65f4b-104">You can use Azure Data Factory tooload data into Azure SQL Data Warehouse from any of hello [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="65f4b-105">Por ejemplo, puede cargar datos desde una base de datos SQL de Azure o una base de datos de Oracle en una instancia de SQL Data Warehouse mediante Data Factory.</span><span class="sxs-lookup"><span data-stu-id="65f4b-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="65f4b-106">Tutorial en este artículo muestra cómo tooload datos desde un servidor local de SQL base de datos en un almacén de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="65f4b-106">Tutorial in this article shows you how tooload data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="65f4b-107">**Estimación del tiempo**: este tutorial tarda aproximadamente 10-15 minutos toocomplete una vez que se cumplen los requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-107">**Time estimate**: This tutorial takes about 10-15 minutes toocomplete once hello prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65f4b-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="65f4b-108">Prerequisites</span></span>

- <span data-ttu-id="65f4b-109">Necesita un **base de datos de SQL Server** con tablas que contienen datos de hello toobe copió toohello almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="65f4b-109">You need a **SQL Server database** with tables that contain hello data toobe copied over toohello SQL data warehouse.</span></span>  

- <span data-ttu-id="65f4b-110">Necesita una instancia en línea de **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="65f4b-111">Si no dispone de un almacén de datos, obtenga información acerca de cómo demasiado[para crear un almacén de datos de SQL Azure](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="65f4b-111">If you do not already have a data warehouse, learn how too[Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="65f4b-112">Debe tener una **cuenta de Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="65f4b-113">Si no dispone de una cuenta de almacenamiento, obtenga información acerca de cómo demasiado[crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="65f4b-113">If you do not already have a storage account, learn how too[Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="65f4b-114">Para mejorar el rendimiento, busque la cuenta de almacenamiento de Hola y almacenamiento de datos de Hola Hola misma región de Azure.</span><span class="sxs-lookup"><span data-stu-id="65f4b-114">For best performance, locate hello storage account and hello data warehouse in hello same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="65f4b-115">Configuración de una factoría de datos</span><span class="sxs-lookup"><span data-stu-id="65f4b-115">Configure a data factory</span></span>
1. <span data-ttu-id="65f4b-116">Inicie sesión en toohello [portal de Azure][].</span><span class="sxs-lookup"><span data-stu-id="65f4b-116">Log in toohello [Azure portal][].</span></span>
2. <span data-ttu-id="65f4b-117">Localice el almacén de datos y haga clic en tooopen se.</span><span class="sxs-lookup"><span data-stu-id="65f4b-117">Locate your data warehouse and click tooopen it.</span></span>
3. <span data-ttu-id="65f4b-118">En la hoja principal de hello, haga clic en **carga datos** > **Data Factory de Azure**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-118">In hello main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Inicio del Asistente para cargar datos](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="65f4b-120">Si no tiene una factoría de datos en su suscripción de Azure, verá un **factoría de datos** cuadro de diálogo en una pestaña independiente del explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of hello browser.</span></span> <span data-ttu-id="65f4b-121">Hola, rellene la información solicitada y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-121">Fill in hello requested information, and click **Create**.</span></span> <span data-ttu-id="65f4b-122">Después de crea la factoría de datos de hello, Hola **factoría de datos** cierra el cuadro de diálogo y ver hello **factoría de datos seleccione** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65f4b-122">After hello data factory is created, hello **New Data Factory** dialog box closes, and you see hello **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="65f4b-123">Si tiene una o varias fábricas de datos ya se encuentran en hello suscripción de Azure, vea hello **factoría de datos seleccione** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65f4b-123">If you have one or more data factories already in hello Azure subscription, you see hello **Select Data Factory** dialog box.</span></span> <span data-ttu-id="65f4b-124">En este cuadro de diálogo, puede seleccionar un generador de datos existente o haga clic en **crear nuevo generador de datos** toocreate uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="65f4b-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** toocreate a new one.</span></span>

    ![Configurar Data Factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="65f4b-126">Hola **factoría de datos seleccione** cuadro de diálogo, hello **cargar datos** opción está activada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="65f4b-126">In hello **Select Data Factory** dialog box, hello **Load data** option is selected by default.</span></span> <span data-ttu-id="65f4b-127">Haga clic en **siguiente** toostart crear una tarea de carga de datos.</span><span class="sxs-lookup"><span data-stu-id="65f4b-127">Click **Next** toostart creating a data loading task.</span></span>

## <a name="configure-hello-data-factory-properties"></a><span data-ttu-id="65f4b-128">Configurar las propiedades de generador de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="65f4b-128">Configure hello data factory properties</span></span>
<span data-ttu-id="65f4b-129">Ahora que ha creado una factoría de datos, paso siguiente hello es programación al cargar los datos tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-129">Now that you have created a data factory, hello next step is tooconfigure hello data loading schedule.</span></span>

1. <span data-ttu-id="65f4b-130">En **Nombre de la tarea**, escriba **DWLoadData-fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="65f4b-131">Usar valor predeterminado de hello **ejecutar una vez ahora** opción, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-131">Use hello default **Run once now** option, click **Next**.</span></span>

    ![Configuración de la programación de carga](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a><span data-ttu-id="65f4b-133">Configurar el almacén de datos de origen de Hola y puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="65f4b-133">Configure hello source data store and gateway</span></span>
<span data-ttu-id="65f4b-134">Ahora, saber la factoría de datos acerca de la base de datos SQL de hello local desde el que desea que los datos de tooload.</span><span class="sxs-lookup"><span data-stu-id="65f4b-134">Now you tell Data Factory about hello on-premises SQL Server database from which you want tooload data.</span></span>

1. <span data-ttu-id="65f4b-135">Elija **SQL Server** de datos de origen de hello admitida almacenar catálogo y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-135">Choose **SQL Server** from hello supported source data store catalog, and click **Next**.</span></span>

    ![Selección del origen de SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="65f4b-137">A **base de datos de SQL Server de especificar Hola local** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65f4b-137">A **Specify hello on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="65f4b-138">Hola primero **nombre de la conexión** campo está rellenado automático.</span><span class="sxs-lookup"><span data-stu-id="65f4b-138">hello first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="65f4b-139">segundo campo de Hello pide nombre Hola de hello **puerta de enlace**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-139">hello second field asks for hello name of hello **Gateway**.</span></span> <span data-ttu-id="65f4b-140">Si está utilizando un generador de datos existente que ya tiene una puerta de enlace, puede volver a usar la puerta de enlace de hello, selecciónelo en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-140">If you are using an existing data factory that already has a gateway, you can reuse hello gateway by selecting it from hello drop-down list.</span></span> <span data-ttu-id="65f4b-141">Haga clic en hello **crear puerta de enlace** vincular toocreate Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="65f4b-141">Click hello **Create Gateway** link toocreate a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="65f4b-142">Si el almacén de datos de origen de hello es local o en una máquina virtual de IaaS de Azure, se requiere una puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="65f4b-142">If hello source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="65f4b-143">Una puerta de enlace tiene una relación de 1 a 1 con una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="65f4b-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="65f4b-144">No se puede usar desde otro generador de datos, pero se puede utilizar por varias tareas con Hola de carga de datos misma factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="65f4b-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in hello same data factory.</span></span> <span data-ttu-id="65f4b-145">Una puerta de enlace puede ser usado tooconnect toomultiple los almacenes de datos cuando se ejecuta tareas de carga de datos.</span><span class="sxs-lookup"><span data-stu-id="65f4b-145">A gateway can be used tooconnect toomultiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="65f4b-146">Para obtener información detallada acerca de la puerta de enlace de hello, consulte [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="65f4b-146">For detailed information about hello gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="65f4b-147">Se mostrará el cuadro de diálogo **Crear puerta de enlace**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="65f4b-148">En Nombre, escriba **GatewayForDWLoading**y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="65f4b-149">Se mostrará el cuadro de diálogo **Configure Gateway** (Configurar puerta de enlace).</span><span class="sxs-lookup"><span data-stu-id="65f4b-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="65f4b-150">Haga clic en **iniciar el programa de instalación rápida en este equipo** tooautomatically descargar, instalar y registrar Data Management Gateway en el equipo actual.</span><span class="sxs-lookup"><span data-stu-id="65f4b-150">Click **Launch express setup on this computer** tooautomatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="65f4b-151">Hola progreso se muestra en una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="65f4b-151">hello progress is shown in a pop-up window.</span></span> <span data-ttu-id="65f4b-152">Si la máquina de hello no puede conectar el almacén de datos de toohello, puede preparar manualmente [descargar e instalar la puerta de enlace de hello](https://www.microsoft.com/download/details.aspx?id=39717) en un equipo que se puede conectar datos toohello almacenar y, a continuación, usar tooregister clave Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-152">If hello machine cannot connect toohello data store, you can manually [download and install hello gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect toohello data store, and then use hello key tooregister.</span></span>
    > [!NOTE]
    > <span data-ttu-id="65f4b-153">el programa de instalación rápida de Hello funciona de forma nativa con Microsoft Edge e Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="65f4b-153">hello express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="65f4b-154">Si está usando Google Chrome, instale primero la extensión de ClickOnce de Hola de almacén web de Chrome.</span><span class="sxs-lookup"><span data-stu-id="65f4b-154">If you are using Google Chrome, first install hello ClickOnce extension from Chrome web store.</span></span>

    ![Inicio de la configuración rápida](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="65f4b-156">Espere a que toocomplete de instalación de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-156">Wait for hello gateway setup toocomplete.</span></span> <span data-ttu-id="65f4b-157">Una vez que la puerta de enlace de Hola se ha registrado correctamente y está en línea, se cierra la ventana emergente de Hola y nueva puerta de enlace de hello aparece en el campo de la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-157">Once hello gateway is successfully registered and is online, hello pop-up window closes and hello new gateway appears in hello gateway field.</span></span> <span data-ttu-id="65f4b-158">A continuación, rellene el resto de hello campos obligatorios como se indica a continuación, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-158">Then fill in hello rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="65f4b-159">**Nombre del servidor**: nombre del programa Hola a SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="65f4b-159">**Server name**: Name of hello on-premises SQL Server.</span></span>
    - <span data-ttu-id="65f4b-160">**Nombre de la base de datos**: la base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="65f4b-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="65f4b-161">**Cifrado de credenciales**: usar valor predeterminado de hello "por el explorador web".</span><span class="sxs-lookup"><span data-stu-id="65f4b-161">**Credential encryption**: Use hello default "By web browser".</span></span>
    - <span data-ttu-id="65f4b-162">**Tipo de autenticación**: elija Hola tipo de autenticación que usa.</span><span class="sxs-lookup"><span data-stu-id="65f4b-162">**Authentication type**: Choose hello type of authentication you are using.</span></span>
    - <span data-ttu-id="65f4b-163">**Nombre de usuario** y **contraseña**: escriba Hola nombre de usuario y una contraseña para un usuario que tiene permiso toocopy Hola datos.</span><span class="sxs-lookup"><span data-stu-id="65f4b-163">**User name** and **password**: Enter hello user name and password for a user who has permission toocopy hello data.</span></span>

    ![Inicio de la configuración rápida](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="65f4b-165">Hola siguiente paso es tablas de hello toochoose de los datos de hello toocopy.</span><span class="sxs-lookup"><span data-stu-id="65f4b-165">hello next step is toochoose hello tables from which toocopy hello data.</span></span> <span data-ttu-id="65f4b-166">Puede filtrar las tablas de hello mediante palabras clave.</span><span class="sxs-lookup"><span data-stu-id="65f4b-166">You can filter hello tables by using keywords.</span></span> <span data-ttu-id="65f4b-167">Y puede obtener una vista previa de esquema de datos y tabla de hello en el panel inferior Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-167">And you can preview hello data and table schema in hello bottom panel.</span></span> <span data-ttu-id="65f4b-168">Después de finalizar la selección, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-168">After you finish your selection, click **Next**.</span></span>

    ![Selección de tablas](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a><span data-ttu-id="65f4b-170">Configurar el destino de hello, el almacenamiento de datos de SQL</span><span class="sxs-lookup"><span data-stu-id="65f4b-170">Configure hello destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="65f4b-171">Ahora se explíquenos factoría de datos de información de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-171">Now you tell Data Factory about hello destination information.</span></span>

1. <span data-ttu-id="65f4b-172">La información de conexión de SQL Data Warehouse se rellenará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="65f4b-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="65f4b-173">Escriba la contraseña de Hola Hola nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="65f4b-173">Enter hello password for hello user name.</span></span> <span data-ttu-id="65f4b-174">y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-174">and click **Next**.</span></span>

    ![Configuración del destino](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="65f4b-176">Una asignación de tabla inteligente aparece que asigna origen toodestination, basándose en los nombres de tabla.</span><span class="sxs-lookup"><span data-stu-id="65f4b-176">An intelligent table mapping appears that maps source toodestination tables based on table names.</span></span> <span data-ttu-id="65f4b-177">Si no existe la tabla de hello en el destino de hello, de forma predeterminada ADF creará uno con hello mismo nombre (Esto aplica tooSQL servidor o base de datos de SQL de Azure como origen).</span><span class="sxs-lookup"><span data-stu-id="65f4b-177">If hello table does not exist in hello destination, by default ADF will create one with hello same name (this applies tooSQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="65f4b-178">También puede elegir tabla de toomap tooan existente.</span><span class="sxs-lookup"><span data-stu-id="65f4b-178">You can also choose toomap tooan existing table.</span></span> <span data-ttu-id="65f4b-179">Revise la información y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-179">Review and click **Next**.</span></span>

    ![Asignación de tablas](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="65f4b-181">Revise la asignación de esquema de Hola y busque mensajes de error o advertencia.</span><span class="sxs-lookup"><span data-stu-id="65f4b-181">Review hello schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="65f4b-182">La asignación inteligente se basa en el nombre de las columnas.</span><span class="sxs-lookup"><span data-stu-id="65f4b-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="65f4b-183">Si se produce una conversión de tipo de datos no compatibles entre la columna de origen y destino de hello, verá un mensaje de error junto a la tabla correspondiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-183">If there is an unsupported data type conversion between hello source and destination column, you see an error message alongside hello corresponding table.</span></span> <span data-ttu-id="65f4b-184">Si elige automático de la factoría de datos de toolet crear tablas de hello, conversión de tipos de datos apropiados puede ocurrir si es necesario incompatibilidad de hello toofix entre los almacenes de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="65f4b-184">If you choose toolet Data Factory auto create hello tables, proper data type conversion may happen if needed toofix hello incompatibility between source and destination stores.</span></span>

    ![Esquema de asignación](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="65f4b-186">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-186">Click **Next**.</span></span>

## <a name="configure-hello-performance-settings"></a><span data-ttu-id="65f4b-187">Configurar opciones de rendimiento de Hola</span><span class="sxs-lookup"><span data-stu-id="65f4b-187">Configure hello performance settings</span></span>
<span data-ttu-id="65f4b-188">En configuraciones de rendimiento de hello, configure una cuenta de almacenamiento de Azure utilizada para almacenar provisionalmente los datos de hello antes de que se carga en el modo más eficaz de almacenamiento de datos SQL usando [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="65f4b-188">In hello Performance configurations, you configure an Azure storage account used for staging hello data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="65f4b-189">Después de realiza la copia de hello, datos provisionales de hello en el almacenamiento se limpiarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="65f4b-189">After hello copy is done, hello interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="65f4b-190">Seleccione una cuenta de Azure Storage y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Configuración del blob de almacenamiento provisional](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a><span data-ttu-id="65f4b-192">Revise la información de resumen e implementar la canalización de Hola</span><span class="sxs-lookup"><span data-stu-id="65f4b-192">Review summary information and deploy hello pipeline</span></span>

<span data-ttu-id="65f4b-193">Revise la configuración de Hola y haga clic en **finalizar** canalización de botón toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-193">Review hello configuration and click **Finish** button toodeploy hello pipeline.</span></span>

![Implementación de la factoría de datos](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="65f4b-195">Supervisión del progreso de carga de datos</span><span class="sxs-lookup"><span data-stu-id="65f4b-195">Monitor data loading progress</span></span>

<span data-ttu-id="65f4b-196">Puede ver el progreso de la implementación de Hola y resultados en hello **implementación** página.</span><span class="sxs-lookup"><span data-stu-id="65f4b-196">You can see hello deployment progress and results in hello **Deployment** page.</span></span>

1. <span data-ttu-id="65f4b-197">Una vez que se realice la implementación de hello, haga clic en el vínculo Hola que dice **haga clic aquí canalización de copia de toomonitor** toomonitor progreso al cargar los datos.</span><span class="sxs-lookup"><span data-stu-id="65f4b-197">Once hello deployment is done, click hello link that says **Click here toomonitor copy pipeline** toomonitor data loading progress.</span></span>

    ![Supervisión de la canalización](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="65f4b-199">Hola recién creado **DWLoadData fromSQLServer** canalización de carga de datos es automático seleccionado de hello izquierdo **Resource Explorer**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-199">hello newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from hello left-hand **Resource Explorer**.</span></span>

    ![Visualización de la canalización](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="65f4b-201">Haga clic en la canalización de hello en medio de Hola Hola de toosee panel Estado detallado de cada tabla que asigna tooan actividad.</span><span class="sxs-lookup"><span data-stu-id="65f4b-201">Click into hello pipeline in hello middle panel toosee hello detailed status for each table that maps tooan Activity.</span></span>

    ![Visualización de la actividad de tabla](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="65f4b-203">Haga clic en más de una actividad y ver detalles en el panel derecho de hello incluido el tamaño de los datos, filas, rendimiento, etcetera la carga de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="65f4b-203">Further click into an activity and you see hello data loading details in hello right panel including data size, rows, throughput, etc.</span></span>

    ![Visualización de la información de actividad de tabla](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="65f4b-205">toolaunch esta supervisión vista posterior, vaya tooyour almacenamiento de datos de SQL, haga clic en ejecutar **carga datos > Data Factory de Azure**, seleccione la fábrica y elija **supervisar existente cargar tareas**.</span><span class="sxs-lookup"><span data-stu-id="65f4b-205">toolaunch this monitoring view later, go tooyour SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65f4b-206">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65f4b-206">Next steps</span></span>

<span data-ttu-id="65f4b-207">toomigrate su tooSQL base de datos del almacén de datos, vea [información general de migración](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="65f4b-207">toomigrate your database tooSQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="65f4b-208">toolearn más información acerca de Data Factory de Azure y sus capacidades de movimiento de datos, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="65f4b-208">toolearn more about Azure Data Factory and its data movement capabilities, see hello following articles:</span></span>

- [<span data-ttu-id="65f4b-209">Introducción tooAzure factoría de datos</span><span class="sxs-lookup"><span data-stu-id="65f4b-209">Introduction tooAzure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="65f4b-210">Movimiento de datos con la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="65f4b-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="65f4b-211">Mover datos tooand de almacenamiento de datos de SQL Azure mediante Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="65f4b-211">Move data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="65f4b-212">tooexplore los datos en el almacén de datos de SQL, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="65f4b-212">tooexplore your data in SQL Data Warehouse, see hello following articles:</span></span>

- [<span data-ttu-id="65f4b-213">Conectar tooSQL almacenamiento de datos con Visual Studio como SSDT</span><span class="sxs-lookup"><span data-stu-id="65f4b-213">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="65f4b-214">[Datos visuales con Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="65f4b-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[portal de Azure]: https://portal.azure.com
