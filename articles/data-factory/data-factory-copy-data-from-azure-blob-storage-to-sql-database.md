---
title: datos de aaaCopy de almacenamiento de blobs tooSQL base de datos - Azure | Documentos de Microsoft
description: "Este tutorial muestra cómo toouse actividad de copia de una factoría de datos de Azure de canalización de datos de toocopy de base de datos de tooSQL de almacenamiento de blobs."
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
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a><span data-ttu-id="e65e2-104">Tutorial: Copiar los datos de almacenamiento de blobs tooSQL con factoría de datos de la base de datos</span><span class="sxs-lookup"><span data-stu-id="e65e2-104">Tutorial: Copy data from Blob Storage tooSQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e65e2-105">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e65e2-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="e65e2-106">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="e65e2-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="e65e2-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e65e2-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="e65e2-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e65e2-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="e65e2-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e65e2-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="e65e2-110">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e65e2-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="e65e2-111">API DE REST</span><span class="sxs-lookup"><span data-stu-id="e65e2-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="e65e2-112">API de .NET</span><span class="sxs-lookup"><span data-stu-id="e65e2-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="e65e2-113">En este tutorial, creará una factoría de datos con datos toocopy de canalización de la base de datos de tooSQL de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="e65e2-113">In this tutorial, you create a data factory with a pipeline toocopy data from Blob storage tooSQL database.</span></span>

<span data-ttu-id="e65e2-114">Hola actividad de copia realiza el movimiento de datos de hello en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="e65e2-114">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="e65e2-115">Funciona con un servicio disponible de forma global que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="e65e2-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="e65e2-116">Vea [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo para obtener más información acerca de la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="e65e2-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="e65e2-117">Para obtener una descripción detallada del programa Hola a servicio de factoría de datos, vea hello [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="e65e2-117">For a detailed overview of hello Data Factory service, see hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="e65e2-118">Requisitos previos para el tutorial de Hola</span><span class="sxs-lookup"><span data-stu-id="e65e2-118">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="e65e2-119">Antes de comenzar este tutorial, debe tener Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="e65e2-119">Before you begin this tutorial, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="e65e2-120">**Suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-120">**Azure subscription**.</span></span>  <span data-ttu-id="e65e2-121">Si no tiene una suscripción, puede crear una cuenta de prueba gratuita en tan solo un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="e65e2-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e65e2-122">Vea hello [gratuita](http://azure.microsoft.com/pricing/free-trial/) artículo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e65e2-122">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="e65e2-123">**Cuenta de almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-123">**Azure Storage Account**.</span></span> <span data-ttu-id="e65e2-124">Usar el almacenamiento de blobs de Hola como un **origen** almacén de datos en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e65e2-124">You use hello blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="e65e2-125">Si no tiene una cuenta de almacenamiento de Azure, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo para toocreate pasos uno.</span><span class="sxs-lookup"><span data-stu-id="e65e2-125">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="e65e2-126">**Base de datos de SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-126">**Azure SQL Database**.</span></span> <span data-ttu-id="e65e2-127">Usará una base de datos SQL de Azure como un almacén de datos de **destino** en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e65e2-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="e65e2-128">Si no dispone de una base de datos de SQL Azure que puede usar en el tutorial de hello, vea [cómo toocreate y configurar una base de datos de SQL Azure](../sql-database/sql-database-get-started.md) toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="e65e2-128">If you don't have an Azure SQL database that you can use in hello tutorial, See [How toocreate and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate one.</span></span>
* <span data-ttu-id="e65e2-129">**SQL Server 2012/2014 o Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="e65e2-130">Usar SQL Server Management Studio o Visual Studio toocreate una base de datos de ejemplo y los datos de resultado de hello tooview en base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e65e2-130">You use SQL Server Management Studio or Visual Studio toocreate a sample database and tooview hello result data in hello database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="e65e2-131">Obtención del nombre y la clave de la cuenta de Almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="e65e2-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="e65e2-132">Necesita cuenta Hola nombre y clave de cuenta de su almacenamiento de Azure cuenta toodo este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e65e2-132">You need hello account name and account key of your Azure storage account toodo this tutorial.</span></span> <span data-ttu-id="e65e2-133">Anote el **nombre de cuenta** y la **clave de cuenta** para su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e65e2-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="e65e2-134">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e65e2-134">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e65e2-135">Haga clic en **más servicios** en hello dejado de menú y seleccione **cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-135">Click **More services** on hello left menu and select **Storage Accounts**.</span></span>

    ![Examinar: Cuentas de almacenamiento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="e65e2-137">Hola **cuentas de almacenamiento** hoja, seleccione hello **cuenta de almacenamiento de Azure** que desea toouse en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e65e2-137">In hello **Storage Accounts** blade, select hello **Azure storage account** that you want toouse in this tutorial.</span></span>
4. <span data-ttu-id="e65e2-138">Seleccione **Claves de acceso** en **CONFIGURACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="e65e2-139">Haga clic en **copia** (imagen) aparece al lado demasiado**nombre de la cuenta de almacenamiento** texto cuadro y guardar y pegar, en algún lugar (por ejemplo: en un archivo de texto).</span><span class="sxs-lookup"><span data-stu-id="e65e2-139">Click **copy** (image) button next too**Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="e65e2-140">Repetir Hola anterior paso toocopy o anote hello **key1**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-140">Repeat hello previous step toocopy or note down hello **key1**.</span></span>

    ![Clave de acceso de almacenamiento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="e65e2-142">Haga clic en Cerrar todos los módulos de hello **X**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-142">Close all hello blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="e65e2-143">Recopilación de nombres de usuario, bases de datos y servidores SQL Server</span><span class="sxs-lookup"><span data-stu-id="e65e2-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="e65e2-144">Necesita nombres Hola del servidor SQL Azure, base de datos y toodo de usuario de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e65e2-144">You need hello names of Azure SQL server, database, and user toodo this tutorial.</span></span> <span data-ttu-id="e65e2-145">Anote los nombres del **servidor**, la **base de datos** y el **usuario** de su instancia de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e65e2-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="e65e2-146">Hola **portal de Azure**, haga clic en **más servicios** en hello izquierdo y seleccione **bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-146">In hello **Azure portal**, click **More services** on hello left and select **SQL databases**.</span></span>
2. <span data-ttu-id="e65e2-147">Hola **hoja de bases de datos de SQL**, seleccione hello **base de datos** que desea toouse en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e65e2-147">In hello **SQL databases blade**, select hello **database** that you want toouse in this tutorial.</span></span> <span data-ttu-id="e65e2-148">Tome nota de hello **nombre de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-148">Note down hello **database name**.</span></span>  
3. <span data-ttu-id="e65e2-149">Hola **base de datos SQL** hoja, haga clic en **propiedades** en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-149">In hello **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="e65e2-150">Tome nota de los valores de hello para **nombre del servidor** y **inicio de sesión de administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-150">Note down hello values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="e65e2-151">Haga clic en Cerrar todos los módulos de hello **X**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-151">Close all hello blades by clicking **X**.</span></span>

## <a name="allow-azure-services-tooaccess-sql-server"></a><span data-ttu-id="e65e2-152">Permitir a los servicios de Azure tooaccess SQL server</span><span class="sxs-lookup"><span data-stu-id="e65e2-152">Allow Azure services tooaccess SQL server</span></span>
<span data-ttu-id="e65e2-153">Asegúrese de que **permitir acceso a servicios de tooAzure** configuración girada **ON** para el servidor de SQL Azure para ese servicio Data Factory Hola pueda acceder a su servidor de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e65e2-153">Ensure that **Allow access tooAzure services** setting turned **ON** for your Azure SQL server so that hello Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="e65e2-154">Hola tooverify y activar esta configuración, lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e65e2-154">tooverify and turn on this setting, do hello following steps:</span></span>

1. <span data-ttu-id="e65e2-155">Haga clic en **más servicios** concentrador Hola izquierda y haga clic en **servidores SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-155">Click **More services** hub on hello left and click **SQL servers**.</span></span>
2. <span data-ttu-id="e65e2-156">Seleccione el servidor y haga clic en **Firewall** en **CONFIGURACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="e65e2-157">Hola **configuración del Firewall** hoja, haga clic en **ON** para **permitir acceso a servicios de tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-157">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
4. <span data-ttu-id="e65e2-158">Haga clic en Cerrar todos los módulos de hello **X**.</span><span class="sxs-lookup"><span data-stu-id="e65e2-158">Close all hello blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="e65e2-159">Preparación del Almacenamiento de blobs y Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="e65e2-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="e65e2-160">Ahora, prepare el almacenamiento de blobs de Azure y base de datos SQL de Azure para tutorial Hola realizando Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e65e2-160">Now, prepare your Azure blob storage and Azure SQL database for hello tutorial by performing hello following steps:</span></span>  

1. <span data-ttu-id="e65e2-161">Inicie el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="e65e2-161">Launch Notepad.</span></span> <span data-ttu-id="e65e2-162">Copie Hola después de texto y guárdelo como **emp.txt** demasiado**C:\ADFGetStarted** carpeta en el disco duro.</span><span class="sxs-lookup"><span data-stu-id="e65e2-162">Copy hello following text and save it as **emp.txt** too**C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="e65e2-163">Usar herramientas como [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** Hola de contenedor y tooupload **emp.txt** contenedor toohello de archivos.</span><span class="sxs-lookup"><span data-stu-id="e65e2-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** container and tooupload hello **emp.txt** file toohello container.</span></span>

    ![Explorador de almacenamiento de Azure](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="e65e2-166">Hola de uso después de hello de toocreate de script SQL **emp** tabla en la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e65e2-166">Use hello following SQL script toocreate hello **emp** table in your Azure SQL Database.</span></span>  

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

    <span data-ttu-id="e65e2-167">**Si tiene instalado en el equipo SQL Server 2012/2014:** siga las instrucciones de [administración de Azure SQL Database utilizando SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server y ejecute hello secuencia de comandos SQL.</span><span class="sxs-lookup"><span data-stu-id="e65e2-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server and run hello SQL script.</span></span> <span data-ttu-id="e65e2-168">En este artículo usa hello [portal de Azure clásico](http://manage.windowsazure.com), no Hola [nuevo portal de Azure](https://portal.azure.com), firewall de tooconfigure para un servidor de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e65e2-168">This article uses hello [classic Azure portal](http://manage.windowsazure.com), not hello [new Azure portal](https://portal.azure.com), tooconfigure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="e65e2-169">Si el cliente no está permitido a tooaccess Hola servidor SQL de Azure, necesita tooconfigure firewall para el acceso de tooallow de servidor de SQL Azure desde el equipo (dirección IP).</span><span class="sxs-lookup"><span data-stu-id="e65e2-169">If your client is not allowed tooaccess hello Azure SQL server, you need tooconfigure firewall for your Azure SQL server tooallow access from your machine (IP Address).</span></span> <span data-ttu-id="e65e2-170">Vea [este artículo](../sql-database/sql-database-configure-firewall-settings.md) para firewall de hello tooconfigure de pasos para el servidor de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e65e2-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps tooconfigure hello firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="e65e2-171">Crear una factoría de datos</span><span class="sxs-lookup"><span data-stu-id="e65e2-171">Create a data factory</span></span>
<span data-ttu-id="e65e2-172">Ha completado los requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e65e2-172">You have completed hello prerequisites.</span></span> <span data-ttu-id="e65e2-173">Puede crear una factoría de datos mediante uno de hello siguientes formas.</span><span class="sxs-lookup"><span data-stu-id="e65e2-173">You can create a data factory using one of hello following ways.</span></span> <span data-ttu-id="e65e2-174">Haga clic en una de las opciones de hello en la lista desplegable de hello en parte superior de Hola u Hola sigue vínculos tooperform Hola tutorial.</span><span class="sxs-lookup"><span data-stu-id="e65e2-174">Click one of hello options in hello drop-down list at hello top or hello following links tooperform hello tutorial.</span></span>     

* [<span data-ttu-id="e65e2-175">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="e65e2-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="e65e2-176">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e65e2-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="e65e2-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e65e2-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="e65e2-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e65e2-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="e65e2-179">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e65e2-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="e65e2-180">API DE REST</span><span class="sxs-lookup"><span data-stu-id="e65e2-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="e65e2-181">API de .NET</span><span class="sxs-lookup"><span data-stu-id="e65e2-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="e65e2-182">canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa.</span><span class="sxs-lookup"><span data-stu-id="e65e2-182">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="e65e2-183">No transforma datos de salida de tooproduce de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e65e2-183">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="e65e2-184">Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar los datos primera canalización tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="e65e2-184">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="e65e2-185">Se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="e65e2-185">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="e65e2-186">Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="e65e2-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
