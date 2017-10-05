---
title: Copia de datos de Blob Storage en SQL Database - Azure | Microsoft Docs
description: "En este tutorial se muestra cómo usar la actividad de copia en una canalización de Data Factory de Azure para copiar datos de Almacenamiento de blobs en Base de datos SQL de Azure."
keywords: blob SQL, Almacenamiento de blobs, copia de datos
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 730140d15f4dec7ddc1280c2e4da1d247902fe4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a><span data-ttu-id="dcd22-104">Tutorial: Copia de datos de Blob Storage en SQL Database mediante Data Factory</span><span class="sxs-lookup"><span data-stu-id="dcd22-104">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dcd22-105">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dcd22-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="dcd22-106">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="dcd22-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="dcd22-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dcd22-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="dcd22-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dcd22-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="dcd22-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcd22-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="dcd22-110">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dcd22-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="dcd22-111">API DE REST</span><span class="sxs-lookup"><span data-stu-id="dcd22-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="dcd22-112">API de .NET</span><span class="sxs-lookup"><span data-stu-id="dcd22-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="dcd22-113">En este tutorial, creará una factoría de datos con una canalización para copiar datos de Almacenamiento de blobs en Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="dcd22-113">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span></span>

<span data-ttu-id="dcd22-114">La actividad de copia realiza el movimiento de datos en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd22-114">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="dcd22-115">Funciona con un servicio disponible de forma global que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="dcd22-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="dcd22-116">Consulte el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md) para obtener más información sobre la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="dcd22-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="dcd22-117">Para información general más detallada sobre el servicio Data Factory, consulte el artículo [Introducción al servicio Data Factory de Azure](data-factory-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="dcd22-117">For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="dcd22-118">Requisitos previos para el tutorial</span><span class="sxs-lookup"><span data-stu-id="dcd22-118">Prerequisites for the tutorial</span></span>
<span data-ttu-id="dcd22-119">Antes de comenzar este tutorial, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="dcd22-119">Before you begin this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="dcd22-120">**Suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-120">**Azure subscription**.</span></span>  <span data-ttu-id="dcd22-121">Si no tiene una suscripción, puede crear una cuenta de prueba gratuita en tan solo un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="dcd22-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="dcd22-122">Consulte el artículo [Evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/) para obtener información.</span><span class="sxs-lookup"><span data-stu-id="dcd22-122">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="dcd22-123">**Cuenta de almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-123">**Azure Storage Account**.</span></span> <span data-ttu-id="dcd22-124">Almacenamiento de blobs se usará como un almacén de datos de **origen** en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="dcd22-124">You use the blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="dcd22-125">Si no tiene una cuenta de Almacenamiento de Azure, consulte la sección [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) para ver los pasos para su creación.</span><span class="sxs-lookup"><span data-stu-id="dcd22-125">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="dcd22-126">**Base de datos de SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-126">**Azure SQL Database**.</span></span> <span data-ttu-id="dcd22-127">Usará una base de datos SQL de Azure como un almacén de datos de **destino** en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="dcd22-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="dcd22-128">Si no dispone de una base de datos SQL de Azure que pueda usar en el tutorial, vea [Cómo crear y configurar una base de datos de SQL de Azure](../sql-database/sql-database-get-started.md) para crear una.</span><span class="sxs-lookup"><span data-stu-id="dcd22-128">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.</span></span>
* <span data-ttu-id="dcd22-129">**SQL Server 2012/2014 o Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="dcd22-130">Usará SQL Server Management Studio o Visual Studio para crear una base de datos de ejemplo y ver los datos de resultados de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="dcd22-130">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="dcd22-131">Obtención del nombre y la clave de la cuenta de Almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="dcd22-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="dcd22-132">Para realizar este tutorial necesitará el nombre de cuenta y la clave de cuenta de su cuenta de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd22-132">You need the account name and account key of your Azure storage account to do this tutorial.</span></span> <span data-ttu-id="dcd22-133">Anote el **nombre de cuenta** y la **clave de cuenta** para su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dcd22-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="dcd22-134">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dcd22-134">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="dcd22-135">Haga clic en **Más servicios** en el menú de la izquierda y seleccione **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-135">Click **More services** on the left menu and select **Storage Accounts**.</span></span>

    ![Examinar: Cuentas de almacenamiento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="dcd22-137">En la hoja **Cuentas de almacenamiento**, seleccione la **cuenta de almacenamiento de Azure** que desea usar en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="dcd22-137">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span></span>
4. <span data-ttu-id="dcd22-138">Seleccione **Claves de acceso** en **CONFIGURACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="dcd22-139">Haga clic en el botón **copiar** (imagen) que se encuentra junto al cuadro de texto **Nombre de cuenta de almacenamiento** y guárdelo y péguelo en algún lugar (por ejemplo: en un archivo de texto).</span><span class="sxs-lookup"><span data-stu-id="dcd22-139">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="dcd22-140">Repita el paso anterior para copiar o anotar la **clave 1**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-140">Repeat the previous step to copy or note down the **key1**.</span></span>

    ![Clave de acceso de almacenamiento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="dcd22-142">Haga clic en **X**para cerrar todas las hojas.</span><span class="sxs-lookup"><span data-stu-id="dcd22-142">Close all the blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="dcd22-143">Recopilación de nombres de usuario, bases de datos y servidores SQL Server</span><span class="sxs-lookup"><span data-stu-id="dcd22-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="dcd22-144">Necesitará los nombres de servidor SQL de Azure, la base de datos y el usuario para realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="dcd22-144">You need the names of Azure SQL server, database, and user to do this tutorial.</span></span> <span data-ttu-id="dcd22-145">Anote los nombres del **servidor**, la **base de datos** y el **usuario** de su instancia de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="dcd22-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="dcd22-146">En **Azure Portal**, haga clic en **Más servicios** a la izquierda y seleccione **Bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-146">In the **Azure portal**, click **More services** on the left and select **SQL databases**.</span></span>
2. <span data-ttu-id="dcd22-147">En la **hoja de bases de datos SQL**, seleccione la **base de datos** que desea usar en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="dcd22-147">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span></span> <span data-ttu-id="dcd22-148">Anote el **nombre de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-148">Note down the **database name**.</span></span>  
3. <span data-ttu-id="dcd22-149">En la hoja **SQL Database**, haga clic en **Propiedades** en **CONFIGURACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-149">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="dcd22-150">Anote los valores de **NOMBRE DEL SERVIDOR** e **INICIO DE SESIÓN DE ADMINISTRADOR DE SERVIDOR**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-150">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="dcd22-151">Haga clic en **X**para cerrar todas las hojas.</span><span class="sxs-lookup"><span data-stu-id="dcd22-151">Close all the blades by clicking **X**.</span></span>

## <a name="allow-azure-services-to-access-sql-server"></a><span data-ttu-id="dcd22-152">Procedimiento para permitir que los servicios de Azure accedan a SQL Server</span><span class="sxs-lookup"><span data-stu-id="dcd22-152">Allow Azure services to access SQL server</span></span>
<span data-ttu-id="dcd22-153">Asegúrese de que la configuración **Permitir el acceso a los servicios de Azure** está **ACTIVADA** para el servidor de SQL de Azure para que el servicio Data Factory pueda acceder al servidor de SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd22-153">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="dcd22-154">Para comprobar y activar esta configuración, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="dcd22-154">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="dcd22-155">Haga clic en el concentrador **Más servicios** a la izquierda y haga clic en **Servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-155">Click **More services** hub on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="dcd22-156">Seleccione el servidor y haga clic en **Firewall** en **CONFIGURACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="dcd22-157">En la hoja **Configuración de firewall**, haga clic en **ACTIVADA** para **Permitir el acceso a los servicios de Azure**.</span><span class="sxs-lookup"><span data-stu-id="dcd22-157">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
4. <span data-ttu-id="dcd22-158">Haga clic en **X**para cerrar todas las hojas.</span><span class="sxs-lookup"><span data-stu-id="dcd22-158">Close all the blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="dcd22-159">Preparación del Almacenamiento de blobs y Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="dcd22-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="dcd22-160">Ahora, prepare su almacenamiento de blobs de Azure y base de datos SQL de Azure para el tutorial realizando los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="dcd22-160">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span></span>  

1. <span data-ttu-id="dcd22-161">Inicie el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="dcd22-161">Launch Notepad.</span></span> <span data-ttu-id="dcd22-162">Copie el texto siguiente y guárdelo como **emp.txt** en la carpeta **C:\ADFGetStarted** de su disco duro.</span><span class="sxs-lookup"><span data-stu-id="dcd22-162">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="dcd22-163">Use herramientas como el [Explorador de Azure Storage](http://storageexplorer.com/) para crear el contenedor **adftutorial** y cargar el archivo **emp.txt** en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="dcd22-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>

    ![Explorador de almacenamiento de Azure](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="dcd22-166">Use el siguiente script de SQL para crear la tabla **emp** en su Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd22-166">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    <span data-ttu-id="dcd22-167">**Si tiene SQL Server 2012/2014 instalado en el equipo**: siga las instrucciones de [Administración de Azure SQL Database con el uso de SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) para conectarse al servidor SQL de Azure y ejecutar el script de SQL.</span><span class="sxs-lookup"><span data-stu-id="dcd22-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span></span> <span data-ttu-id="dcd22-168">En este artículo se usa el [Portal de Azure clásico](http://manage.windowsazure.com) en lugar de [Azure Portal](https://portal.azure.com) para configurar el firewall para un servidor SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd22-168">This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="dcd22-169">Si el cliente no tiene permiso para acceder al servidor SQL de Azure, tendrá que configurar el firewall de su servidor SQL de Azure para permitir el acceso desde su máquina (dirección IP).</span><span class="sxs-lookup"><span data-stu-id="dcd22-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="dcd22-170">Consulte [este artículo](../sql-database/sql-database-configure-firewall-settings.md) para conocer los pasos que deben darse para configurar el firewall de un servidor SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd22-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="dcd22-171">Crear una factoría de datos</span><span class="sxs-lookup"><span data-stu-id="dcd22-171">Create a data factory</span></span>
<span data-ttu-id="dcd22-172">Ha completado los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="dcd22-172">You have completed the prerequisites.</span></span> <span data-ttu-id="dcd22-173">Puede crear una factoría de datos de una de las siguientes formas.</span><span class="sxs-lookup"><span data-stu-id="dcd22-173">You can create a data factory using one of the following ways.</span></span> <span data-ttu-id="dcd22-174">Haga clic en una de las opciones de la lista desplegable de la parte superior o en los vínculos siguientes para realizar el tutorial.</span><span class="sxs-lookup"><span data-stu-id="dcd22-174">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span></span>     

* [<span data-ttu-id="dcd22-175">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="dcd22-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="dcd22-176">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dcd22-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="dcd22-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dcd22-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="dcd22-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcd22-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="dcd22-179">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dcd22-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="dcd22-180">API DE REST</span><span class="sxs-lookup"><span data-stu-id="dcd22-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="dcd22-181">API de .NET</span><span class="sxs-lookup"><span data-stu-id="dcd22-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="dcd22-182">La canalización de datos de este tutorial copia datos de un almacén de datos de origen a un almacén de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="dcd22-182">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="dcd22-183">No transforma los datos de entrada para generar datos de salida.</span><span class="sxs-lookup"><span data-stu-id="dcd22-183">It does not transform input data to produce output data.</span></span> <span data-ttu-id="dcd22-184">Para ver un tutorial acerca de cómo transformar datos mediante Azure Data Factory, consulte [Tutorial: Compilación de la primera canalización para procesar datos mediante el clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="dcd22-184">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="dcd22-185">Puede encadenar dos actividades (ejecutar una después de otra) haciendo que el conjunto de datos de salida de una actividad sea el conjunto de datos de entrada de la otra actividad.</span><span class="sxs-lookup"><span data-stu-id="dcd22-185">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="dcd22-186">Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="dcd22-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
