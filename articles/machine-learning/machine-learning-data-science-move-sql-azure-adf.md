---
title: datos de aaaMove de un tooSQL de SQL Server local Azure con Data Factory de Azure | Documentos de Microsoft
description: "Configurar una canalización ADF que se compone de dos actividades de migración de datos que juntos se mueven datos a diario entre las bases de datos locales y en la nube de Hola."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a><span data-ttu-id="0649e-103">Mover los datos de un servidor SQL local tooSQL Azure con Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="0649e-103">Move data from an on-premises SQL server tooSQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="0649e-104">Este tema muestra cómo toomove datos desde una base de datos de SQL Server local, tooa base de datos de SQL Azure a través de almacenamiento de blobs de Azure mediante Hola factoría de datos de Azure (ADF).</span><span class="sxs-lookup"><span data-stu-id="0649e-104">This topic shows how toomove data from an on-premises SQL Server Database tooa SQL Azure Database via Azure Blob Storage using hello Azure Data Factory (ADF).</span></span>

<span data-ttu-id="0649e-105">Para una tabla que resume las distintas opciones para mover datos tooan base de datos de SQL Azure, vea [mover datos tooan base de datos de SQL Azure para el aprendizaje automático de Azure](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0649e-105">For a table that summarizes various options for moving data tooan Azure SQL Database, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="0649e-106"><a name="intro"></a>Introducción: ¿Qué es ADF y cuándo debe ser toomigrate usa datos?</span><span class="sxs-lookup"><span data-stu-id="0649e-106"><a name="intro"></a>Introduction: What is ADF and when should it be used toomigrate data?</span></span>
<span data-ttu-id="0649e-107">Factoría de datos de Azure es un servicio de integración de datos en la nube totalmente administrado que organiza y automatiza el movimiento de Hola y la transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="0649e-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="0649e-108">concepto clave de Hello en el modelo ADF hello es la canalización.</span><span class="sxs-lookup"><span data-stu-id="0649e-108">hello key concept in hello ADF model is pipeline.</span></span> <span data-ttu-id="0649e-109">Una canalización es una agrupación lógica de actividades, cada uno de los cuales define Hola acciones tooperform en datos de hello incluidos en conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="0649e-109">A pipeline is a logical grouping of Activities, each of which defines hello actions tooperform on hello data contained in Datasets.</span></span> <span data-ttu-id="0649e-110">Servicios vinculados son información de hello toodefine usado necesaria para los recursos de datos de Data Factory tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="0649e-110">Linked services are used toodefine hello information needed for Data Factory tooconnect toohello data resources.</span></span>

<span data-ttu-id="0649e-111">Con ADF, servicios de procesamiento de datos existentes se pueden formular en las canalizaciones de datos que están administrados y de alta disponibilidad en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="0649e-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in hello cloud.</span></span> <span data-ttu-id="0649e-112">Estas canalizaciones de datos pueden ser tooingest programada, preparar, transformar, analizar y publicar datos y ADF administra y organiza datos complejos de Hola y dependencias de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="0649e-112">These data pipelines can be scheduled tooingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates hello complex data and processing dependencies.</span></span> <span data-ttu-id="0649e-113">Soluciones pueden estar en la nube rápidamente compilado e implementado en hello, conectar un número creciente de local y orígenes de datos en la nube.</span><span class="sxs-lookup"><span data-stu-id="0649e-113">Solutions can be quickly built and deployed in hello cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="0649e-114">Considere el uso de ADF en estos casos:</span><span class="sxs-lookup"><span data-stu-id="0649e-114">Consider using ADF:</span></span>

* <span data-ttu-id="0649e-115">Cuando datos necesidades toobe continuamente migrado en un escenario híbrido que tenga acceso a ambos locales y recursos de la nube</span><span class="sxs-lookup"><span data-stu-id="0649e-115">when data needs toobe continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="0649e-116">Cuando se lleva a cabo datos Hola o necesidades toobe modificado o tiene lógica de negocios agrega tooit al que se está migrando.</span><span class="sxs-lookup"><span data-stu-id="0649e-116">when hello data is transacted or needs toobe modified or have business logic added tooit when being migrated.</span></span>

<span data-ttu-id="0649e-117">ADF permite Hola de programación y la supervisión de trabajos mediante scripts sencillos de JSON que administran el movimiento de Hola de datos de forma periódica.</span><span class="sxs-lookup"><span data-stu-id="0649e-117">ADF allows for hello scheduling and monitoring of jobs using simple JSON scripts that manage hello movement of data on a periodic basis.</span></span> <span data-ttu-id="0649e-118">La ADF también tiene otras capacidades como la compatibilidad con operaciones complejas.</span><span class="sxs-lookup"><span data-stu-id="0649e-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="0649e-119">Para obtener más información sobre ADF, consulte documentación de hello en [factoría de datos de Azure (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="0649e-119">For more information on ADF, see hello documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="0649e-120"><a name="scenario"></a>Hola escenario</span><span class="sxs-lookup"><span data-stu-id="0649e-120"><a name="scenario"></a>hello Scenario</span></span>
<span data-ttu-id="0649e-121">Configuramos una canalización ADF que se compone de dos actividades de migración de datos.</span><span class="sxs-lookup"><span data-stu-id="0649e-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="0649e-122">Juntos se mueven datos a diario entre una base de datos SQL local y una base de datos de SQL Azure en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="0649e-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in hello cloud.</span></span> <span data-ttu-id="0649e-123">Hola dos actividades son:</span><span class="sxs-lookup"><span data-stu-id="0649e-123">hello two activities are:</span></span>

* <span data-ttu-id="0649e-124">copiar los datos de una base de datos de SQL Server local tooan cuenta de almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="0649e-124">copy data from an on-premises SQL Server database tooan Azure Blob Storage account</span></span>
* <span data-ttu-id="0649e-125">copiar datos de hello almacenamiento de blobs de Azure cuenta tooan base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0649e-125">copy data from hello Azure Blob Storage account tooan Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="0649e-126">Hola pasos que se muestran aquí se han adaptado del hello más tutorial proporcionado por el equipo ADF hello: [mover datos entre orígenes locales y en la nube con Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) hace referencia a toohello secciones relevantes de ese tema se proporcionan cuando corresponda.</span><span class="sxs-lookup"><span data-stu-id="0649e-126">hello steps shown here have been adapted from hello more detailed tutorial provided by hello ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References toohello relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="0649e-127"><a name="prereqs"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0649e-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="0649e-128">En este tutorial se asume que dispone de:</span><span class="sxs-lookup"><span data-stu-id="0649e-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="0649e-129">Una **suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="0649e-129">An **Azure subscription**.</span></span> <span data-ttu-id="0649e-130">Si no tiene una suscripción, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0649e-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0649e-131">Una **cuenta de almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="0649e-131">An **Azure storage account**.</span></span> <span data-ttu-id="0649e-132">Usar una cuenta de almacenamiento de Azure para almacenar datos de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0649e-132">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="0649e-133">Si no tiene una cuenta de almacenamiento de Azure, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo.</span><span class="sxs-lookup"><span data-stu-id="0649e-133">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="0649e-134">Una vez haya creado la cuenta de almacenamiento de hello, necesita tooobtain Hola cuenta clave usa el almacenamiento de información de tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="0649e-134">After you have created hello storage account, you need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="0649e-135">Consulte [Administración de la cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="0649e-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="0649e-136">Acceso tooan **base de datos de SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="0649e-136">Access tooan **Azure SQL Database**.</span></span> <span data-ttu-id="0649e-137">Si debe configurar una base de datos de SQL Azure, Hola tpoic [Introducción a la base de datos de SQL de Microsoft Azure ](../sql-database/sql-database-get-started.md) proporciona información acerca de cómo tooprovision una nueva instancia de una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0649e-137">If you must set up an Azure SQL Database, hello tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how tooprovision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="0649e-138">**Azure PowerShell** instalado y configurado de forma local.</span><span class="sxs-lookup"><span data-stu-id="0649e-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="0649e-139">Para obtener instrucciones, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0649e-139">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="0649e-140">Este procedimiento utiliza hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0649e-140">This procedure uses hello [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="0649e-141"><a name="upload-data"></a>Carga Hola datos tooyour SQL Server local</span><span class="sxs-lookup"><span data-stu-id="0649e-141"><a name="upload-data"></a> Upload hello data tooyour on-premises SQL Server</span></span>
<span data-ttu-id="0649e-142">Usamos hello [conjunto de datos de Nueva York Taxi](http://chriswhong.com/open-data/foil_nyc_taxi/) proceso de migración de toodemonstrate Hola.</span><span class="sxs-lookup"><span data-stu-id="0649e-142">We use hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello migration process.</span></span> <span data-ttu-id="0649e-143">Hello NYC Taxi conjunto de datos está disponible, como se indicó en esa entrada en el almacenamiento de blobs de Azure [NYC Taxi datos](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="0649e-143">hello NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="0649e-144">datos de Hello tienen dos archivos, archivo de trip_data.csv hello, que contiene detalles de ida y vuelta, y archivo de trip_far.csv hello, que contiene detalles de tarifa de Hola de pago para cada recorrido.</span><span class="sxs-lookup"><span data-stu-id="0649e-144">hello data has two files, hello trip_data.csv file, which contains trip details, and hello  trip_far.csv file, which contains details of hello fare paid for each trip.</span></span> <span data-ttu-id="0649e-145">En [Descripción del conjunto de datos de carreras de taxi de Nueva York](machine-learning-data-science-process-sql-walkthrough.md#dataset), se proporciona un ejemplo y una descripción de estos archivos.</span><span class="sxs-lookup"><span data-stu-id="0649e-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="0649e-146">Puede adaptar procedimiento Hola proporcionada aquí tooa conjunto de sus propios datos, o bien, siga los pasos de hello tal como se describe mediante el uso de hello NYC Taxi conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="0649e-146">You can either adapt hello procedure provided here tooa set of your own data or follow hello steps as described by using hello NYC Taxi dataset.</span></span> <span data-ttu-id="0649e-147">Hola tooupload NYC Taxi conjunto de datos en la base de datos de SQL Server local, siga procedimiento Hola descrito en [importar masivamente datos en la base de datos de SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="0649e-147">tooupload hello NYC Taxi dataset into your on-premises SQL Server database, follow hello procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="0649e-148">Estas instrucciones son para un servidor de SQL Server en una máquina Virtual de Azure, pero Hola procedimiento Hola para cargar toohello local de SQL Server es igual.</span><span class="sxs-lookup"><span data-stu-id="0649e-148">These instructions are for a SQL Server on an Azure Virtual Machine, but hello procedure for uploading toohello on-premises SQL Server is hello same.</span></span>

## <span data-ttu-id="0649e-149"><a name="create-adf"></a> Crear una factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="0649e-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="0649e-150">Hola instrucciones para crear un nuevo generador de datos de Azure y un grupo de recursos en hello [portal de Azure](https://portal.azure.com/) se proporcionan [crear un generador de datos de Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="0649e-150">hello instructions for creating a new Azure Data Factory and a resource group in hello [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="0649e-151">Nombre hello nueva ADF instancia *adfdsp* y grupo de recursos de nombre hello creado *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="0649e-151">Name hello new ADF instance *adfdsp* and name hello resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-hello-data-management-gateway"></a><span data-ttu-id="0649e-152">Instalar y configurar Hola Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="0649e-152">Install and configure up hello Data Management Gateway</span></span>
<span data-ttu-id="0649e-153">tooenable sus canalizaciones en un generador de datos de Azure toowork con un servidor local de SQL, deberá tooadd como una factoría de datos de toohello de servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="0649e-153">tooenable your pipelines in an Azure data factory toowork with an on-premises SQL Server, you need tooadd it as a Linked Service toohello data factory.</span></span> <span data-ttu-id="0649e-154">toocreate un servicio vinculado para un servidor local de SQL, debe:</span><span class="sxs-lookup"><span data-stu-id="0649e-154">toocreate a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="0649e-155">Descargue e instale Microsoft Data Management Gateway en el equipo local de Hola.</span><span class="sxs-lookup"><span data-stu-id="0649e-155">download and install Microsoft Data Management Gateway onto hello on-premises computer.</span></span>
* <span data-ttu-id="0649e-156">configurar el servicio de hello vinculado para puerta de enlace de hello local datos origen toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="0649e-156">configure hello linked service for hello on-premises data source toouse hello gateway.</span></span>

<span data-ttu-id="0649e-157">Hola Data Management Gateway serializa y deserializa datos de origen y el receptor de hello en equipo Hola donde estén hospedados.</span><span class="sxs-lookup"><span data-stu-id="0649e-157">hello Data Management Gateway serializes and deserializes hello source and sink data on hello computer where it is hosted.</span></span>

<span data-ttu-id="0649e-158">Para obtener instrucciones de instalación e información detallada sobre Data Management Gateway, consulte [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="0649e-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="0649e-159"><a name="adflinkedservices"></a>Crear servicios vinculados tooconnect toohello recursos de datos</span><span class="sxs-lookup"><span data-stu-id="0649e-159"><a name="adflinkedservices"></a>Create linked services tooconnect toohello data resources</span></span>
<span data-ttu-id="0649e-160">Un servicio vinculado define información de hello necesaria para el recurso de datos de Data Factory de Azure tooconnect tooa.</span><span class="sxs-lookup"><span data-stu-id="0649e-160">A linked service defines hello information needed for Azure Data Factory tooconnect tooa data resource.</span></span> <span data-ttu-id="0649e-161">procedimiento paso a paso de Hola para crear servicios vinculados se proporciona en [crear servicios vinculados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="0649e-161">hello step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="0649e-162">Tenemos tres recursos en este escenario para los que se necesitan servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="0649e-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="0649e-163">Servicio vinculado para SQL Server local</span><span class="sxs-lookup"><span data-stu-id="0649e-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="0649e-164">Servicio vinculado para el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="0649e-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="0649e-165">Servicio vinculado para la base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0649e-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="0649e-166"><a name="adf-linked-service-onprem-sql"></a>Servicio vinculado para la base de datos SQL Server local</span><span class="sxs-lookup"><span data-stu-id="0649e-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="0649e-167">toocreate Hola vinculado servicio para hello local de SQL Server:</span><span class="sxs-lookup"><span data-stu-id="0649e-167">toocreate hello linked service for hello on-premises SQL Server:</span></span>

* <span data-ttu-id="0649e-168">Haga clic en hello **almacén de datos** en la página de aterrizaje de ADF hello en el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="0649e-168">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="0649e-169">Seleccione **SQL** y escriba hello *nombre de usuario* y *contraseña* las credenciales de hello SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="0649e-169">select **SQL** and enter hello *username* and *password* credentials for hello on-premises SQL Server.</span></span> <span data-ttu-id="0649e-170">Necesita tooenter Hola servername como un **nombre de la instancia de la barra diagonal inversa completo servername (nombreDeServidor ombreDeInstancia)**.</span><span class="sxs-lookup"><span data-stu-id="0649e-170">You need tooenter hello servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="0649e-171">Hola de nombre de servicio vinculado *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="0649e-171">Name hello linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="0649e-172"><a name="adf-linked-service-blob-store"></a>Servicio vinculado de blob</span><span class="sxs-lookup"><span data-stu-id="0649e-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="0649e-173">toocreate Hola servicio vinculado para la cuenta de almacenamiento de blobs de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="0649e-173">toocreate hello linked service for hello Azure Blob Storage account:</span></span>

* <span data-ttu-id="0649e-174">Haga clic en hello **almacén de datos** en la página de aterrizaje de ADF hello en el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="0649e-174">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="0649e-175">Seleccione **Azure Storage Account**</span><span class="sxs-lookup"><span data-stu-id="0649e-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="0649e-176">Escriba el nombre de clave y el contenedor de la cuenta del almacenamiento de blobs de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="0649e-176">enter hello Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="0649e-177">Hola de nombre de servicio vinculado *adfds*.</span><span class="sxs-lookup"><span data-stu-id="0649e-177">Name hello Linked Service *adfds*.</span></span>

### <span data-ttu-id="0649e-178"><a name="adf-linked-service-azure-sql"></a>Servicio vinculado para la base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0649e-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="0649e-179">toocreate Hola servicio vinculado de hello base de datos de SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="0649e-179">toocreate hello linked service for hello Azure SQL Database:</span></span>

* <span data-ttu-id="0649e-180">Haga clic en hello **almacén de datos** en la página de aterrizaje de ADF hello en el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="0649e-180">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="0649e-181">Seleccione **SQL Azure** y escriba hello *nombre de usuario* y *contraseña* credenciales para hello base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0649e-181">select **Azure SQL** and enter hello *username* and *password* credentials for hello Azure SQL Database.</span></span> <span data-ttu-id="0649e-182">Hola *nombre de usuario* debe especificarse como  *user@servername* .</span><span class="sxs-lookup"><span data-stu-id="0649e-182">hello *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="0649e-183"><a name="adf-tables"></a>Definir y crear tablas toospecify cómo tooaccess Hola conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="0649e-183"><a name="adf-tables"></a>Define and create tables toospecify how tooaccess hello datasets</span></span>
<span data-ttu-id="0649e-184">Crear tablas que especifican estructura hello, la ubicación y la disponibilidad de los conjuntos de datos de hello con hello procedimientos basados en script.</span><span class="sxs-lookup"><span data-stu-id="0649e-184">Create tables that specify hello structure, location, and availability of hello datasets with hello following script-based procedures.</span></span> <span data-ttu-id="0649e-185">Archivos JSON son tablas de hello toodefine usado.</span><span class="sxs-lookup"><span data-stu-id="0649e-185">JSON files are used toodefine hello tables.</span></span> <span data-ttu-id="0649e-186">Para obtener más información sobre la estructura de Hola de estos archivos, consulte [conjuntos de datos](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="0649e-186">For more information on hello structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0649e-187">Debe ejecutar hello `Add-AzureAccount` cmdlet antes de ejecutar hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm de cmdlet que Hola suscripción de Azure derecha está seleccionada para la ejecución del comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="0649e-187">You should execute hello `Add-AzureAccount` cmdlet before executing hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet tooconfirm that hello right Azure subscription is selected for hello command execution.</span></span> <span data-ttu-id="0649e-188">Para obtener documentación sobre este cmdlet, consulte [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="0649e-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="0649e-189">las definiciones basadas en JSON de Hello en tablas de hello usan hello después de nombres:</span><span class="sxs-lookup"><span data-stu-id="0649e-189">hello JSON-based definitions in hello tables use hello following names:</span></span>

* <span data-ttu-id="0649e-190">Hola **nombre de la tabla** en hello local SQL server es *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="0649e-190">hello **table name** in hello on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="0649e-191">Hola **nombre del contenedor** en hello almacenamiento de blobs de Azure es cuenta *containername*</span><span class="sxs-lookup"><span data-stu-id="0649e-191">hello **container name** in hello Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="0649e-192">Se necesitan tres definiciones de tabla para esta canalización de ADF:</span><span class="sxs-lookup"><span data-stu-id="0649e-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="0649e-193">Tabla de SQL local</span><span class="sxs-lookup"><span data-stu-id="0649e-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="0649e-194">Tabla Blob </span><span class="sxs-lookup"><span data-stu-id="0649e-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="0649e-195">Tabla SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0649e-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="0649e-196">Estos procedimientos usar toodefine de PowerShell de Azure y crear hello las actividades ADF.</span><span class="sxs-lookup"><span data-stu-id="0649e-196">These procedures use Azure PowerShell toodefine and create hello ADF activities.</span></span> <span data-ttu-id="0649e-197">Pero estas tareas pueden realizarse también mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0649e-197">But these tasks can also be accomplished using hello Azure portal.</span></span> <span data-ttu-id="0649e-198">Para más información, consulte [Creación de conjuntos de datos](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="0649e-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="0649e-199"><a name="adf-table-onprem-sql"></a>Tabla de SQL local</span><span class="sxs-lookup"><span data-stu-id="0649e-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="0649e-200">definición de la tabla de Hola para hello local de SQL Server se especifica en hello el archivo JSON siguiente:</span><span class="sxs-lookup"><span data-stu-id="0649e-200">hello table definition for hello on-premises SQL Server is specified in hello following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="0649e-201">nombres de columna de Hello no se incluyeron.</span><span class="sxs-lookup"><span data-stu-id="0649e-201">hello column names were not included here.</span></span> <span data-ttu-id="0649e-202">Puede Sub-seleccionar en nombres de columna de hello incluyéndolos aquí (para obtener más información Compruebe hello [documentación de ADF](../data-factory/data-factory-data-movement-activities.md) tema.</span><span class="sxs-lookup"><span data-stu-id="0649e-202">You can sub-select on hello column names by including them here (for details check hello [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="0649e-203">Copiar la definición de JSON de Hola de tabla de hello en un archivo denominado *onpremtabledef.json* y guardar archivos conoce la ubicación de tooa (aquí supone toobe *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="0649e-203">Copy hello JSON definition of hello table into a file called *onpremtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="0649e-204">Crear tabla de hello en ADF con hello siguiente cmdlet de PowerShell de Azure:</span><span class="sxs-lookup"><span data-stu-id="0649e-204">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="0649e-205"><a name="adf-table-blob-store"></a>Tabla Blob</span><span class="sxs-lookup"><span data-stu-id="0649e-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="0649e-206">Definición de la tabla de Hola para hello de salida blob se encuentra en la siguiente hello (Esto asigna datos de hello ingerida de blob de tooAzure local):</span><span class="sxs-lookup"><span data-stu-id="0649e-206">Definition for hello table for hello output blob location is in hello following (this maps hello ingested data from on-premises tooAzure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="0649e-207">Copiar la definición de JSON de Hola de tabla de hello en un archivo denominado *bloboutputtabledef.json* y guardar archivos conoce la ubicación de tooa (aquí supone toobe *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="0649e-207">Copy hello JSON definition of hello table into a file called *bloboutputtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="0649e-208">Crear tabla de hello en ADF con hello siguiente cmdlet de PowerShell de Azure:</span><span class="sxs-lookup"><span data-stu-id="0649e-208">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="0649e-209"><a name="adf-table-azure-sq"></a>Tabla SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0649e-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="0649e-210">Definición de tabla Hola Hola salida de SQL Azure es siguiente hello (este esquema asigna datos de hello procedentes de blob de hello):</span><span class="sxs-lookup"><span data-stu-id="0649e-210">Definition for hello table for hello SQL Azure output is in hello following (this schema maps hello data coming from hello blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="0649e-211">Copiar la definición de JSON de Hola de tabla de hello en un archivo denominado *AzureSqlTable.json* y guardar archivos conoce la ubicación de tooa (aquí supone toobe *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="0649e-211">Copy hello JSON definition of hello table into a file called *AzureSqlTable.json* file and save it tooa known location (here assumed toobe *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="0649e-212">Crear tabla de hello en ADF con hello siguiente cmdlet de PowerShell de Azure:</span><span class="sxs-lookup"><span data-stu-id="0649e-212">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="0649e-213"><a name="adf-pipeline"></a>Definir y crear la canalización de Hola</span><span class="sxs-lookup"><span data-stu-id="0649e-213"><a name="adf-pipeline"></a>Define and create hello pipeline</span></span>
<span data-ttu-id="0649e-214">Especifique las actividades de Hola que pertenecen toohello de canalización y crear canalización Hola con hello procedimientos basados en script.</span><span class="sxs-lookup"><span data-stu-id="0649e-214">Specify hello activities that belong toohello pipeline and create hello pipeline with hello following script-based procedures.</span></span> <span data-ttu-id="0649e-215">Un archivo JSON es propiedades de canalización de hello toodefine usado.</span><span class="sxs-lookup"><span data-stu-id="0649e-215">A JSON file is used toodefine hello pipeline properties.</span></span>

* <span data-ttu-id="0649e-216">Hello script se da por supuesto que hello **nombre de la canalización** es *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="0649e-216">hello script assumes that hello **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="0649e-217">Tenga en cuenta que se debe establecer periodicidad Hola de hello canalización toobe ejecutado en cada día base y el uso Hola tiempo de ejecución predeterminado para el trabajo de hello (12 a.m. hora UTC).</span><span class="sxs-lookup"><span data-stu-id="0649e-217">Also note that we set hello periodicity of hello pipeline toobe executed on daily basis and use hello default execution time for hello job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="0649e-218">Hello procedimientos siguientes utilice toodefine de PowerShell de Azure y crear la canalización ADF Hola.</span><span class="sxs-lookup"><span data-stu-id="0649e-218">hello following procedures use Azure PowerShell toodefine and create hello ADF pipeline.</span></span> <span data-ttu-id="0649e-219">Sin embargo, esta tarea también se puede realizar en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0649e-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="0649e-220">Para más información, consulte [Creación de una canalización](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="0649e-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="0649e-221">Usar definiciones de tabla de Hola proporcionado anteriormente, definición de la canalización de Hola para hello que ADF se especifica como sigue:</span><span class="sxs-lookup"><span data-stu-id="0649e-221">Using hello table definitions provided previously, hello pipeline definition for hello ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="0649e-222">Copie esta definición JSON de canalización de hello en un archivo denominado *pipelinedef.json* y guardar archivos conoce la ubicación de tooa (aquí supone toobe *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="0649e-222">Copy this JSON definition of hello pipeline into a file called *pipelinedef.json* file and save it tooa known location (here assumed toobe *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="0649e-223">Crear canalización Hola de ADF con hello siguiente cmdlet de PowerShell de Azure:</span><span class="sxs-lookup"><span data-stu-id="0649e-223">Create hello pipeline in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="0649e-224">Confirmar que puede ver canalización hello en hello ADF Hola Portal clásico de Azure se mostrarán como sigue (al hacer clic en el diagrama de hello)</span><span class="sxs-lookup"><span data-stu-id="0649e-224">Confirm that you can see hello pipeline on hello ADF in hello Azure Classic Portal show up as following (when you click hello diagram)</span></span>

![Canalización de ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="0649e-226"><a name="adf-pipeline-start"></a>Iniciar Hola canalización</span><span class="sxs-lookup"><span data-stu-id="0649e-226"><a name="adf-pipeline-start"></a>Start hello Pipeline</span></span>
<span data-ttu-id="0649e-227">canalización de Hello ahora se pueden ejecutar con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0649e-227">hello pipeline can now be run using hello following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="0649e-228">Hola *startdate* y *enddate* toobe reemplazado con fechas de hello real entre los que desea Hola canalización toorun los valores de parámetro tienen.</span><span class="sxs-lookup"><span data-stu-id="0649e-228">hello *startdate* and *enddate* parameter values need toobe replaced with hello actual dates between which you want hello pipeline toorun.</span></span>

<span data-ttu-id="0649e-229">Una vez que se ejecuta la canalización de hello, debe ser capaz de toosee Hola datos aparezcan de contenedor de hello seleccionado para el blob de hello, un archivo por día.</span><span class="sxs-lookup"><span data-stu-id="0649e-229">Once hello pipeline executes, you should be able toosee hello data show up in hello container selected for hello blob, one file per day.</span></span>

<span data-ttu-id="0649e-230">Tenga en cuenta que no hemos aprovechado funcionalidad de Hola que proporciona datos ADF toopipe incrementalmente.</span><span class="sxs-lookup"><span data-stu-id="0649e-230">Note that we have not leveraged hello functionality provided by ADF toopipe data incrementally.</span></span> <span data-ttu-id="0649e-231">Para obtener más información sobre cómo toodo esta y otras funcionalidades proporcionadas por ADF, vea Hola [documentación de ADF](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="0649e-231">For more information on how toodo this and other capabilities provided by ADF, see hello [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
