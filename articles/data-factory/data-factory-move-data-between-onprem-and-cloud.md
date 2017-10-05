---
title: 'Movimiento de datos: Data Management Gateway | Microsoft Docs'
description: "Configuración de una puerta de enlace para mover datos entre una infraestructura local y la nube. Uso de Data Management Gateway en Azure Data Factory para mover los datos."
keywords: "puerta de enlace de datos, integración de datos, mover datos, credenciales de puerta de enlace"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 565091e24a8c0009793e2e2365fb95013cad5028
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-between-on-premises-sources-and-the-cloud-with-data-management-gateway"></a><span data-ttu-id="805cf-105">Movimiento de datos entre orígenes locales y la nube con Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="805cf-105">Move data between on-premises sources and the cloud with Data Management Gateway</span></span>
<span data-ttu-id="805cf-106">Este artículo proporciona información general sobre la integración de los almacenes de datos locales y los almacenes de datos en la nube mediante Data Factory.</span><span class="sxs-lookup"><span data-stu-id="805cf-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="805cf-107">Este artículo se basa en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md) y otros artículos de conceptos básicos de Data Factory: [conjuntos de datos](data-factory-create-datasets.md) y [canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="805cf-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="805cf-108">Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="805cf-108">Data Management Gateway</span></span>
<span data-ttu-id="805cf-109">Debe instalar Data Management Gateway en su equipo local para habilitar el movimiento de datos a o desde un almacén de datos local.</span><span class="sxs-lookup"><span data-stu-id="805cf-109">You must install Data Management Gateway on your on-premises machine to enable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="805cf-110">La puerta de enlace puede instalarse en el mismo equipo que el almacén de datos o en un equipo diferente, siempre que la puerta de enlace pueda conectarse al almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-110">The gateway can be installed on the same machine as the data store or on a different machine as long as the gateway can connect to the data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="805cf-111">Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para más detalles sobre Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="805cf-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="805cf-112">El siguiente tutorial muestra cómo crear una factoría de datos con una canalización que mueve los datos de una base de datos de **SQL Server** local a Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="805cf-112">The following walkthrough shows you how to create a data factory with a pipeline that moves data from an on-premises **SQL Server** database to an Azure blob storage.</span></span> <span data-ttu-id="805cf-113">Como parte del tutorial, instalará y configurará la puerta de enlace de administración de datos en su máquina.</span><span class="sxs-lookup"><span data-stu-id="805cf-113">As part of the walkthrough, you install and configure the Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-to-cloud"></a><span data-ttu-id="805cf-114">Tutorial: copiar datos locales a la nube</span><span class="sxs-lookup"><span data-stu-id="805cf-114">Walkthrough: copy on-premises data to cloud</span></span>
<span data-ttu-id="805cf-115">En este tutorial realizará los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="805cf-115">In this walkthrough you do the following steps:</span></span> 

1. <span data-ttu-id="805cf-116">Creación de una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-116">Create a data factory.</span></span>
2. <span data-ttu-id="805cf-117">Creación de una instancia de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="805cf-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="805cf-118">Creación de servicios vinculados para los almacenes de datos de origen y receptor.</span><span class="sxs-lookup"><span data-stu-id="805cf-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="805cf-119">Creación de conjuntos de datos que representen los datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="805cf-119">Create datasets to represent input and output data.</span></span>
5. <span data-ttu-id="805cf-120">Creación de una canalización con una actividad de copia para mover los datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-120">Create a pipeline with a copy activity to move the data.</span></span>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="805cf-121">Requisitos previos para el tutorial</span><span class="sxs-lookup"><span data-stu-id="805cf-121">Prerequisites for the tutorial</span></span>
<span data-ttu-id="805cf-122">Antes de comenzar este tutorial, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="805cf-122">Before you begin this walkthrough, you must have the following prerequisites:</span></span>

* <span data-ttu-id="805cf-123">**Suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="805cf-123">**Azure subscription**.</span></span>  <span data-ttu-id="805cf-124">Si no tiene una suscripción, puede crear una cuenta de prueba gratuita en tan solo un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="805cf-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="805cf-125">Consulte el artículo [Evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/) para obtener información.</span><span class="sxs-lookup"><span data-stu-id="805cf-125">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="805cf-126">**Cuenta de almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="805cf-126">**Azure Storage Account**.</span></span> <span data-ttu-id="805cf-127">Blob Storage se usará como un almacén de datos de **destino o receptor** en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="805cf-127">You use the blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="805cf-128">Si no tiene una cuenta de almacenamiento de Azure, consulte la sección [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) para ver los pasos para su creación.</span><span class="sxs-lookup"><span data-stu-id="805cf-128">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="805cf-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="805cf-129">**SQL Server**.</span></span> <span data-ttu-id="805cf-130">Use una base de datos de SQL Server local como almacén de datos de **origen** en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="805cf-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="805cf-131">Creación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="805cf-131">Create data factory</span></span>
<span data-ttu-id="805cf-132">En este paso, use Azure Portal para crear una instancia de Azure Data Factory denominada **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="805cf-132">In this step, you use the Azure portal to create an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="805cf-133">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="805cf-133">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="805cf-134">Haga clic en **+ NUEVO**, en **Inteligencia y análisis** y en **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="805cf-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![New->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="805cf-136">En la página **Nueva factoría de datos**, escriba el nombre **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="805cf-136">In the **New data factory** page, enter **ADFTutorialOnPremDF** for the Name.</span></span>

    ![Agregar al Panel de inicio](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="805cf-138">El nombre de la factoría de datos de Azure debe ser único global.</span><span class="sxs-lookup"><span data-stu-id="805cf-138">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="805cf-139">Si recibe el error: **El nombre de la factoría de datos "ADFTutorialOnPremDF" no está disponible**, cambie el nombre de la factoría de datos (por ejemplo, yournameADFTutorialDataFactory) e intente crearla de nuevo.</span><span class="sxs-lookup"><span data-stu-id="805cf-139">If you receive the error: **Data factory name “ADFTutorialOnPremDF” is not available**, change the name of the data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="805cf-140">Use este nombre en lugar de ADFTutorialFactory al realizar los restantes pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="805cf-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="805cf-141">El nombre de la factoría de datos se puede registrar como un nombre **DNS** en el futuro y, por consiguiente, hacerse públicamente visible.</span><span class="sxs-lookup"><span data-stu-id="805cf-141">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="805cf-142">Seleccione la **suscripción de Azure** donde desea crear la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-142">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="805cf-143">Seleccione un **grupo de recursos** existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="805cf-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="805cf-144">Para este tutorial, cree un grupo de recursos llamado: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="805cf-144">For the tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="805cf-145">Haga clic en **Crear** en la página **Nueva factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="805cf-145">Click **Create** on the **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="805cf-146">Para crear instancias de Data Factory, es preciso ser miembro del rol [Colaborador de Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) en el nivel de grupo de recursos o suscripción.</span><span class="sxs-lookup"><span data-stu-id="805cf-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="805cf-147">Una vez completada la creación, puede ver la página **Factoría de datos** que se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="805cf-147">After creation is complete, you see the **Data Factory** page as shown in the following image:</span></span>

   ![Página principal de Factoría de datos](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="805cf-149">Crear puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="805cf-149">Create gateway</span></span>
1. <span data-ttu-id="805cf-150">En la página **Factoría de datos**, haga clic en el icono **Crear e implementar** para iniciar el **Editor** de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-150">In the **Data Factory** page, click **Author and deploy** tile to launch the **Editor** for the data factory.</span></span>

    ![Mosaico Crear e implementar](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="805cf-152">En Data Factory Editor, haga clic en **... Más** en la barra de herramientas y, a continuación, haga clic en **Nueva puerta de enlace de datos**.</span><span class="sxs-lookup"><span data-stu-id="805cf-152">In the Data Factory Editor, click **... More** on the toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="805cf-153">O bien, haga clic con el botón derecho **Puertas de enlace de datos** en la vista de árbol y elija **Nueva puerta de enlace de datos**.</span><span class="sxs-lookup"><span data-stu-id="805cf-153">Alternatively, you can right-click **Data Gateways** in the tree view, and click **New data gateway**.</span></span>

   ![Nueva puerta de enlace de datos en la barra de herramientas](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="805cf-155">En la página **Crear**, escriba **adftutorialgateway** para el **nombre** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="805cf-155">In the **Create** page, enter **adftutorialgateway** for the **name**, and click **OK**.</span></span>     

    ![Página Crear puerta de enlace](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="805cf-157">En este tutorial, creará la puerta de enlace lógica con un único nodo (la máquina de Windows local).</span><span class="sxs-lookup"><span data-stu-id="805cf-157">In this walkthrough, you create the logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="805cf-158">Puede escalar horizontalmente una puerta de enlace de administración de datos mediante la asociación de varias máquinas locales con la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="805cf-158">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="805cf-159">Puede escalar verticalmente aumentando el número de trabajos de movimiento de datos que pueden ejecutarse simultáneamente en un nodo.</span><span class="sxs-lookup"><span data-stu-id="805cf-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="805cf-160">Esta característica también está disponible para una puerta de enlace lógica con un único nodo.</span><span class="sxs-lookup"><span data-stu-id="805cf-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="805cf-161">Consulte el artículo [Escalado en Data Management Gateway en Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="805cf-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="805cf-162">En la página **Configurar**, haga clic en **Instalar directamente en este equipo**.</span><span class="sxs-lookup"><span data-stu-id="805cf-162">In the **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="805cf-163">Esta acción descarga el paquete de instalación de la puerta de enlace, instala, configura y registra la puerta de enlace en el equipo.</span><span class="sxs-lookup"><span data-stu-id="805cf-163">This action downloads the installation package for the gateway, installs, configures, and registers the gateway on the computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="805cf-164">Utilice Internet Explorer o un explorador web compatible con Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="805cf-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="805cf-165">Si usa Chrome, vaya a [Chrome Web Store](https://chrome.google.com/webstore/), busque la palabra clave "ClickOnce", elija una de las extensiones de ClickOnce e instálela.</span><span class="sxs-lookup"><span data-stu-id="805cf-165">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="805cf-166">Debe hacer lo mismo para Firefox (instale un complemento).</span><span class="sxs-lookup"><span data-stu-id="805cf-166">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="805cf-167">Haga clic en el botón **Abrir menú** de la barra de herramientas (**tres líneas horizontales** en la esquina superior derecha), haga clic en **Complementos**, busque la palabra clave "ClickOnce", elija una de las extensiones de ClickOnce e instálela.</span><span class="sxs-lookup"><span data-stu-id="805cf-167">Click **Open Menu** button on the toolbar (**three horizontal lines** in the top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Puerta de enlace: página Configurar](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="805cf-169">Esta es la forma más sencilla (un clic) para descargar, instalar, configurar y registrar la puerta de enlace en un solo paso.</span><span class="sxs-lookup"><span data-stu-id="805cf-169">This way is the easiest way (one-click) to download, install, configure, and register the gateway in one single step.</span></span> <span data-ttu-id="805cf-170">Puede ver que la aplicación **Administrador de configuración de Microsoft Data Management Gateway** está instalada en el equipo.</span><span class="sxs-lookup"><span data-stu-id="805cf-170">You can see the **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="805cf-171">También puede encontrar el archivo ejecutable **ConfigManager.exe** en la carpeta: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="805cf-171">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="805cf-172">También puede descargar e instalar la puerta de enlace manualmente con los vínculos de esta página y registrarla usando la clave que se muestra en el cuadro de texto **Nueva clave**.</span><span class="sxs-lookup"><span data-stu-id="805cf-172">You can also download and install gateway manually by using the links in this page and register it using the key shown in the **NEW KEY** text box.</span></span>

    <span data-ttu-id="805cf-173">Vea el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para obtener todos los detalles sobre la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="805cf-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="805cf-174">Debe ser administrador del equipo local para instalar y configurar correctamente Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="805cf-174">You must be an administrator on the local computer to install and configure the Data Management Gateway successfully.</span></span> <span data-ttu-id="805cf-175">Puede agregar más usuarios al grupo local de Windows **Usuarios de Data Management Gateway** .</span><span class="sxs-lookup"><span data-stu-id="805cf-175">You can add additional users to the **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="805cf-176">Los miembros de este grupo pueden usar la herramienta Administrador de configuración de Data Management Gateway para configurar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="805cf-176">The members of this group can use the Data Management Gateway Configuration Manager tool to configure the gateway.</span></span>
   >
   >
5. <span data-ttu-id="805cf-177">Espere unos minutos o espere hasta que vea el siguiente mensaje de notificación:</span><span class="sxs-lookup"><span data-stu-id="805cf-177">Wait for a couple of minutes or wait until you see the following notification message:</span></span>

    ![Instalación correcta de la puerta de enlace](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="805cf-179">Inicie la aplicación **Administrador de configuración de Data Management Gateway** en el equipo.</span><span class="sxs-lookup"><span data-stu-id="805cf-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="805cf-180">En la ventana **Búsqueda**, escriba **Data Management Gateway** para tener acceso a esta utilidad.</span><span class="sxs-lookup"><span data-stu-id="805cf-180">In the **Search** window, type **Data Management Gateway** to access this utility.</span></span> <span data-ttu-id="805cf-181">También puede encontrar el archivo ejecutable **ConfigManager.exe** en la carpeta: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="805cf-181">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Administrador de configuración de puertas de enlace](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="805cf-183">Confirme que ve el mensaje `adftutorialgateway is connected to the cloud service`.</span><span class="sxs-lookup"><span data-stu-id="805cf-183">Confirm that you see `adftutorialgateway is connected to the cloud service` message.</span></span> <span data-ttu-id="805cf-184">La barra de estado de la parte inferior muestra **Conectado al servicio en la nube** junto con una **marca de verificación verde**.</span><span class="sxs-lookup"><span data-stu-id="805cf-184">The status bar the bottom displays **Connected to the cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="805cf-185">En la pestaña **Inicio**, también puede realizar las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="805cf-185">On the **Home** tab, you can also do the following operations:</span></span>

   * <span data-ttu-id="805cf-186">**Registrar** una puerta de enlace con una clave en Azure Portal mediante el botón Registrar.</span><span class="sxs-lookup"><span data-stu-id="805cf-186">**Register** a gateway with a key from the Azure portal by using the Register button.</span></span>
   * <span data-ttu-id="805cf-187">**Detener** el servicio host de Data Management Gateway que se ejecuta en la máquina de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="805cf-187">**Stop** the Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="805cf-188">**Programar las actualizaciones** que se instalarán en un momento específico del día.</span><span class="sxs-lookup"><span data-stu-id="805cf-188">**Schedule updates** to be installed at a specific time of the day.</span></span>
   * <span data-ttu-id="805cf-189">Ver cuándo se ha **actualizado por última vez** la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="805cf-189">View when the gateway was **last updated**.</span></span>
   * <span data-ttu-id="805cf-190">Especificar la hora a la que se puede instalar una actualización de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="805cf-190">Specify time at which an update to the gateway can be installed.</span></span>
8. <span data-ttu-id="805cf-191">Cambie a la pestaña **Configuración** . El certificado que se ha especificado en la sección **Certificado** se usa para cifrar o descifrar las credenciales para el almacén de datos local que especifique en el portal.</span><span class="sxs-lookup"><span data-stu-id="805cf-191">Switch to the **Settings** tab. The certificate specified in the **Certificate** section is used to encrypt/decrypt credentials for the on-premises data store that you specify on the portal.</span></span> <span data-ttu-id="805cf-192">Haga clic en **Cambiar** para usar su propio certificado en su lugar.</span><span class="sxs-lookup"><span data-stu-id="805cf-192">(optional) Click **Change** to use your own certificate instead.</span></span> <span data-ttu-id="805cf-193">De forma predeterminada, la puerta de enlace usa el certificado generado automáticamente por el servicio Data Factory.</span><span class="sxs-lookup"><span data-stu-id="805cf-193">By default, the gateway uses the certificate that is auto-generated by the Data Factory service.</span></span>

    ![Configuración del certificado de puerta de enlace](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="805cf-195">También puede realizar las siguientes acciones en la pestaña **Configuración**:</span><span class="sxs-lookup"><span data-stu-id="805cf-195">You can also do the following actions on the **Settings** tab:</span></span>

   * <span data-ttu-id="805cf-196">Consultar o exportar el certificado que usa la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="805cf-196">View or export the certificate being used by the gateway.</span></span>
   * <span data-ttu-id="805cf-197">Cambiar el punto de conexión HTTPS que usa la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="805cf-197">Change the HTTPS endpoint used by the gateway.</span></span>    
   * <span data-ttu-id="805cf-198">Establecer un proxy HTTP que usará la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="805cf-198">Set an HTTP proxy to be used by the gateway.</span></span>     
9. <span data-ttu-id="805cf-199">(Opcional) Cambie a la pestaña **Diagnósticos**, active la opción **Habilitar el registro detallado** si quiere habilitar el registro detallado que puede usar para solucionar los problemas de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="805cf-199">(optional) Switch to the **Diagnostics** tab, check the **Enable verbose logging** option if you want to enable verbose logging that you can use to troubleshoot any issues with the gateway.</span></span> <span data-ttu-id="805cf-200">La información de registro se encuentra en el **Visor de sucesos**, en el nodo **Registros de aplicaciones y servicios** -> **Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="805cf-200">The logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Ficha Diagnóstico](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="805cf-202">También puede realizar las siguientes acciones en la pestaña **Diagnósticos** :</span><span class="sxs-lookup"><span data-stu-id="805cf-202">You can also perform the following actions in the **Diagnostics** tab:</span></span>

   * <span data-ttu-id="805cf-203">Utilice la sección **Probar conexión** para probar la conexión con un origen de datos local mediante la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="805cf-203">Use **Test Connection** section to an on-premises data source using the gateway.</span></span>
   * <span data-ttu-id="805cf-204">Haga clic en **Ver registros** para ver el registro de Data Management Gateway en una ventana del Visor de eventos.</span><span class="sxs-lookup"><span data-stu-id="805cf-204">Click **View Logs** to see the Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="805cf-205">Haga clic en **Enviar registros** para cargar un archivo zip con los registros de los últimos siete días en Microsoft y facilitar así la solución de sus problemas.</span><span class="sxs-lookup"><span data-stu-id="805cf-205">Click **Send Logs** to upload a zip file with logs of last seven days to Microsoft to facilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="805cf-206">En la pestaña **Diagnóstico**, en la sección **Probar conexión**, seleccione **SqlServer** para el tipo de almacén de datos; escriba el nombre del servidor de base de datos, el nombre de la base de datos, especifique el tipo de autenticación, escriba el nombre de usuario y la contraseña, y haga clic en **Probar** para comprobar si la puerta de enlace puede conectarse a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-206">On the **Diagnostics** tab, in the **Test Connection** section, select **SqlServer** for the type of the data store, enter the name of the database server, name of the database, specify authentication type, enter user name, and password, and click **Test** to test whether the gateway can connect to the database.</span></span>
11. <span data-ttu-id="805cf-207">Cambie al explorador web y, en **Azure Portal**, haga clic en **Aceptar** en la página **Configurar** y, después, en la página **Nueva puerta de enlace de datos**.</span><span class="sxs-lookup"><span data-stu-id="805cf-207">Switch to the web browser, and in the **Azure portal**, click **OK** on the **Configure** page and then on the **New data gateway** page.</span></span>
12. <span data-ttu-id="805cf-208">Debería ver **adftutorialgateway** en **Puertas de enlace de datos** en la vista de árbol de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="805cf-208">You should see **adftutorialgateway** under **Data Gateways** in the tree view on the left.</span></span>  <span data-ttu-id="805cf-209">Si hace clic en ella, debería ver el JSON asociado.</span><span class="sxs-lookup"><span data-stu-id="805cf-209">If you click it, you should see the associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="805cf-210">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="805cf-210">Create linked services</span></span>
<span data-ttu-id="805cf-211">En este paso, creará dos servicios vinculados: **AzureStorageLinkedService** y **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="805cf-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="805cf-212">**SqlServerLinkedService** vincula una base de datos de SQL Server local, mientras que **AzureStorageLinkedService** vincula un almacén de blobs de Azure a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-212">The **SqlServerLinkedService** links an on-premises SQL Server database and the **AzureStorageLinkedService** linked service links an Azure blob store to the data factory.</span></span> <span data-ttu-id="805cf-213">Más adelante en este tutorial creará una canalización que copia datos de la base de datos de SQL Server local al almacén de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="805cf-213">You create a pipeline later in this walkthrough that copies data from the on-premises SQL Server database to the Azure blob store.</span></span>

#### <a name="add-a-linked-service-to-an-on-premises-sql-server-database"></a><span data-ttu-id="805cf-214">Adición de un servicio vinculado a una base de datos de SQL Server local</span><span class="sxs-lookup"><span data-stu-id="805cf-214">Add a linked service to an on-premises SQL Server database</span></span>
1. <span data-ttu-id="805cf-215">En el **Editor de Data Factory**, haga clic en **Nuevo almacén de datos** en la barra de herramientas y seleccione **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="805cf-215">In the **Data Factory Editor**, click **New data store** on the toolbar and select **SQL Server**.</span></span>

   ![Nuevo servicio vinculado de SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="805cf-217">En el **Editor de JSON** a la derecha, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="805cf-217">In the **JSON editor** on the right, do the following steps:</span></span>

   1. <span data-ttu-id="805cf-218">Para **gatewayName**, especifique **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="805cf-218">For the **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="805cf-219">En **connectionString**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="805cf-219">In the **connectionString**, do the following steps:</span></span>    

      1. <span data-ttu-id="805cf-220">En **servername**, escriba el nombre del servidor que hospeda la base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="805cf-220">For **servername**, enter the name of the server that hosts the SQL Server database.</span></span>
      2. <span data-ttu-id="805cf-221">En **databasename**, escriba el nombre de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-221">For **databasename**, enter the name of the database.</span></span>
      3. <span data-ttu-id="805cf-222">Haga clic en el botón **Cifrar** de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="805cf-222">Click **Encrypt** button on the toolbar.</span></span> <span data-ttu-id="805cf-223">Verá la aplicación Administrador de credenciales.</span><span class="sxs-lookup"><span data-stu-id="805cf-223">You see the Credentials Manager application.</span></span>

         ![Aplicación Administrador de credenciales](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="805cf-225">En el cuadro de diálogo **Establecer credenciales**, escriba el tipo de autenticación, el nombre de usuario y la contraseña, y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="805cf-225">In the **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="805cf-226">Si la conexión es correcta, se almacenan las credenciales cifradas en el código JSON y se cierra el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="805cf-226">If the connection is successful, the encrypted credentials are stored in the JSON and the dialog box closes.</span></span>
      5. <span data-ttu-id="805cf-227">Si no se cierra automáticamente, cierre la pestaña de explorador vacía que inició el cuadro de diálogo y regrese a la pestaña de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="805cf-227">Close the empty browser tab that launched the dialog box if it is not automatically closed and get back to the tab with the Azure portal.</span></span>

         <span data-ttu-id="805cf-228">En la máquina de la puerta de enlace, las credenciales se **cifrarán** mediante un certificado que es propiedad del servicio Data Factory.</span><span class="sxs-lookup"><span data-stu-id="805cf-228">On the gateway machine, these credentials are **encrypted** by using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="805cf-229">Si prefiere usar el certificado asociado a la puerta de enlace de administración de datos, consulte [Configuración de credenciales y seguridad](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="805cf-229">If you want to use the certificate that is associated with the Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="805cf-230">Haga clic en **Implementar** en la barra de comandos para implementar el servicio vinculado de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="805cf-230">Click **Deploy** on the command bar to deploy the SQL Server linked service.</span></span> <span data-ttu-id="805cf-231">Verá el servicio vinculado en la vista de árbol.</span><span class="sxs-lookup"><span data-stu-id="805cf-231">You should see the linked service in the tree view.</span></span>

      ![Servicio vinculado a SQL Server en la vista de árbol](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="805cf-233">Adición de un servicio vinculado para una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="805cf-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="805cf-234">En el **Editor de Data Factory**, haga clic en **Nuevo almacén de datos** en la barra de comandos y haga clic en **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="805cf-234">In the **Data Factory Editor**, click **New data store** on the command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="805cf-235">Escriba el nombre de la cuenta de almacenamiento de Azure en **Nombre de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="805cf-235">Enter the name of your Azure storage account for the **Account name**.</span></span>
3. <span data-ttu-id="805cf-236">Escriba la clave de su cuenta de almacenamiento de Azure en **Clave de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="805cf-236">Enter the key for your Azure storage account for the **Account key**.</span></span>
4. <span data-ttu-id="805cf-237">Haga clic en **Implementar** para implementar **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="805cf-237">Click **Deploy** to deploy the **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="805cf-238">Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="805cf-238">Create datasets</span></span>
<span data-ttu-id="805cf-239">En este paso, creará conjuntos de datos de entrada y de salida que representan datos de entrada y de salida para la operación de copia (base de datos de SQL Server local => Azure Blob Storage).</span><span class="sxs-lookup"><span data-stu-id="805cf-239">In this step, you create input and output datasets that represent input and output data for the copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="805cf-240">Antes de crear los conjuntos de datos, realice estos pasos (los pasos detallados se indican después de la lista):</span><span class="sxs-lookup"><span data-stu-id="805cf-240">Before creating datasets, do the following steps (detailed steps follows the list):</span></span>

* <span data-ttu-id="805cf-241">Cree una tabla con el nombre **emp** en la base de datos de SQL Server que agregó como servicio vinculado a la factoría de datos e inserte un par de entradas de ejemplo en la tabla.</span><span class="sxs-lookup"><span data-stu-id="805cf-241">Create a table named **emp** in the SQL Server Database you added as a linked service to the data factory and insert a couple of sample entries into the table.</span></span>
* <span data-ttu-id="805cf-242">Cree un contenedor de blobs llamado **adftutorial** en la cuenta de Azure Blob Storage que agregó como un servicio vinculado a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-242">Create a blob container named **adftutorial** in the Azure blob storage account you added as a linked service to the data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-the-tutorial"></a><span data-ttu-id="805cf-243">Preparación de la instancia local de SQL Server para el tutorial</span><span class="sxs-lookup"><span data-stu-id="805cf-243">Prepare On-premises SQL Server for the tutorial</span></span>
1. <span data-ttu-id="805cf-244">En la base de datos que especificó para el servicio vinculado de SQL Server local (**SqlServerLinkedService**), use el siguiente script de SQL para crear la tabla **emp** en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-244">In the database you specified for the on-premises SQL Server linked service (**SqlServerLinkedService**), use the following SQL script to create the **emp** table in the database.</span></span>

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. <span data-ttu-id="805cf-245">Inserte algún ejemplo en la tabla:</span><span class="sxs-lookup"><span data-stu-id="805cf-245">Insert some sample into the table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="805cf-246">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="805cf-246">Create input dataset</span></span>

1. <span data-ttu-id="805cf-247">En **Data Factory Editor**, haga clic en **... Más**, haga clic en **Nuevo conjunto de datos** en la barra de comandos y seleccione **Tabla de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="805cf-247">In the **Data Factory Editor**, click **... More**, click **New dataset** on the command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="805cf-248">Reemplace el script JSON del panel derecho por el texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="805cf-248">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   <span data-ttu-id="805cf-249">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="805cf-249">Note the following points:</span></span>

   * <span data-ttu-id="805cf-250">**type** está establecido en **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="805cf-250">**type** is set to **SqlServerTable**.</span></span>
   * <span data-ttu-id="805cf-251">**tablename** está establecido en **emp**.</span><span class="sxs-lookup"><span data-stu-id="805cf-251">**tableName** is set to **emp**.</span></span>
   * <span data-ttu-id="805cf-252">**linkedServiceName** está establecido en **SqlServerLinkedService** (creó este servicio vinculado en anteriormente en este tutorial).</span><span class="sxs-lookup"><span data-stu-id="805cf-252">**linkedServiceName** is set to **SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="805cf-253">Para un conjunto de datos de entrada no generado por otra canalización en Azure Data Factory, tiene que establecer la propiedad **external** en **true**.</span><span class="sxs-lookup"><span data-stu-id="805cf-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** to **true**.</span></span> <span data-ttu-id="805cf-254">Indica que los datos de entrada se han producido fuera del servicio Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="805cf-254">It denotes the input data is produced external to the Azure Data Factory service.</span></span> <span data-ttu-id="805cf-255">Opcionalmente, puede especificar las directivas de datos externos mediante el elemento **externalData** en la sección **Policy**.</span><span class="sxs-lookup"><span data-stu-id="805cf-255">You can optionally specify any external data policies using the **externalData** element in the **Policy** section.</span></span>    

   <span data-ttu-id="805cf-256">Para más información acerca de las propiedades de JSON, consulte [Movimiento de datos hacia y desde SQL Server](data-factory-sqlserver-connector.md).</span><span class="sxs-lookup"><span data-stu-id="805cf-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="805cf-257">Haga clic en **Implementar** en la barra de comandos para implementar el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-257">Click **Deploy** on the command bar to deploy the dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="805cf-258">Creación del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="805cf-258">Create output dataset</span></span>

1. <span data-ttu-id="805cf-259">En el **Editor de Data Factory**, haga clic en **Nuevo conjunto de datos** en la barra de comandos y seleccione **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="805cf-259">In the **Data Factory Editor**, click **New dataset** on the command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="805cf-260">Reemplace el script JSON del panel derecho por el texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="805cf-260">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   <span data-ttu-id="805cf-261">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="805cf-261">Note the following points:</span></span>

   * <span data-ttu-id="805cf-262">**type** está establecido en **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="805cf-262">**type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="805cf-263">**linkedServiceName** está establecido en **AzureStorageLinkedService** (este servicio vinculado se creó en el paso 2).</span><span class="sxs-lookup"><span data-stu-id="805cf-263">**linkedServiceName** is set to **AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="805cf-264">**folderPath** está establecido en **adftutorial/outfromonpremdf**, donde outfromonpremdf es la carpeta del contenedor adftutorial.</span><span class="sxs-lookup"><span data-stu-id="805cf-264">**folderPath** is set to **adftutorial/outfromonpremdf** where outfromonpremdf is the folder in the adftutorial container.</span></span> <span data-ttu-id="805cf-265">Cree el contenedor **adftutorial** si este todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="805cf-265">Create the **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="805cf-266">**availability** está establecido en **hourly** (**frequency** está establecido en **hour** e **interval** está establecido en **1**).</span><span class="sxs-lookup"><span data-stu-id="805cf-266">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span></span>  <span data-ttu-id="805cf-267">El servicio Data Factory generará un segmento de datos de salida cada hora en la tabla **emp** de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="805cf-267">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL Database.</span></span>

   <span data-ttu-id="805cf-268">Si no especifica un valor de **fileName** para una **tabla de salida**, los archivos generados en **folderPath** se nombran con el siguiente formato: Data<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="805cf-268">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="805cf-269">Para establecer **folderPath** y **fileName** de forma dinámica según la hora de **SliceStart**, use la propiedad partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="805cf-269">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the partitionedBy property.</span></span> <span data-ttu-id="805cf-270">En el ejemplo siguiente, folderPath usa Year, Month y Day de SliceStart (hora de inicio del segmento que se está procesando) y fileName usa Hour de SliceStart.</span><span class="sxs-lookup"><span data-stu-id="805cf-270">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="805cf-271">Por ejemplo, si se está produciendo una división de 2014-10-20T08:00:00, el nombre de carpeta se establece en wikidatagateway/wikisampledataout/2014/10/20 y el nombre de archivo se establece en 08.csv.</span><span class="sxs-lookup"><span data-stu-id="805cf-271">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span></span>

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    <span data-ttu-id="805cf-272">Para más información acerca de las propiedades de JSON, consulte [Movimiento de datos hacia y desde Azure Blob Storage](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="805cf-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="805cf-273">Haga clic en **Implementar** en la barra de comandos para implementar el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-273">Click **Deploy** on the command bar to deploy the dataset.</span></span> <span data-ttu-id="805cf-274">Confirme que ve ambos conjuntos de datos en la vista de árbol.</span><span class="sxs-lookup"><span data-stu-id="805cf-274">Confirm that you see both the datasets in the tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="805cf-275">Creación de una canalización</span><span class="sxs-lookup"><span data-stu-id="805cf-275">Create pipeline</span></span>
<span data-ttu-id="805cf-276">En este paso, va a crear una **canalización** con una **actividad de copia** que usa **EmpOnPremSQLTable** como entrada y **OutputBlobTable** como salida.</span><span class="sxs-lookup"><span data-stu-id="805cf-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="805cf-277">En Data Factory Editor, haga clic en **... Más** y, luego, en **Nueva canalización**.</span><span class="sxs-lookup"><span data-stu-id="805cf-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="805cf-278">Reemplace el script JSON del panel derecho por el texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="805cf-278">Replace the JSON in the right pane with the following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL to Azure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server to blob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > <span data-ttu-id="805cf-279">Reemplace el valor de la propiedad **start** por el día actual y el valor **end** por el próximo día.</span><span class="sxs-lookup"><span data-stu-id="805cf-279">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span>
   >
   >

   <span data-ttu-id="805cf-280">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="805cf-280">Note the following points:</span></span>

   * <span data-ttu-id="805cf-281">En la sección de actividades, solo hay una actividad cuyo **type** está establecido en **Copy**.</span><span class="sxs-lookup"><span data-stu-id="805cf-281">In the activities section, there is only activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="805cf-282">La **entrada** de la actividad está establecida en **EmpOnPremSQLTable** y la **salida** de la actividad está establecida en **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="805cf-282">**Input** for the activity is set to **EmpOnPremSQLTable** and **output** for the activity is set to **OutputBlobTable**.</span></span>
   * <span data-ttu-id="805cf-283">En la sección **typeProperties**, **SqlSource** se especifica como el **tipo de origen** y **BlobSink** como el **tipo de receptor**.</span><span class="sxs-lookup"><span data-stu-id="805cf-283">In the **typeProperties** section, **SqlSource** is specified as the **source type** and **BlobSink **is specified as the **sink type**.</span></span>
   * <span data-ttu-id="805cf-284">La consulta SQL `select * from emp` está especificada para la propiedad **sqlReaderQuery** de **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="805cf-284">SQL query `select * from emp` is specified for the **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="805cf-285">Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="805cf-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="805cf-286">Por ejemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="805cf-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="805cf-287">La hora de finalización ( **end** ) es opcional, pero se utilizará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="805cf-287">The **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="805cf-288">Si no especifica ningún valor para la propiedad **end**, se calcula como "**start + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="805cf-288">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="805cf-289">Para ejecutar la canalización indefinidamente, especifique **9/9/9999** como valor de la propiedad **end**.</span><span class="sxs-lookup"><span data-stu-id="805cf-289">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span></span>

   <span data-ttu-id="805cf-290">Está definiendo la duración del procesamiento de los segmentos de datos según las propiedades de **disponibilidad** que se definieron para cada conjunto de datos de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="805cf-290">You are defining the time duration in which the data slices are processed based on the **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="805cf-291">En el ejemplo, hay 24 segmentos de datos, ya que se produce un segmento de datos a la hora.</span><span class="sxs-lookup"><span data-stu-id="805cf-291">In the example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="805cf-292">Haga clic en **Implementar** en la barra de comandos para implementar el conjunto de datos (la tabla es un conjunto de datos rectangular).</span><span class="sxs-lookup"><span data-stu-id="805cf-292">Click **Deploy** on the command bar to deploy the dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="805cf-293">Confirme que la canalización se muestra en la vista de árbol en el nodo **Canalizaciones**.</span><span class="sxs-lookup"><span data-stu-id="805cf-293">Confirm that the pipeline shows up in the tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="805cf-294">Ahora, haga clic en **X** dos veces para cerrar la página y volver a la página **Factoría de datos** de **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="805cf-294">Now, click **X** twice to close the page to get back to the **Data Factory** page for the **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="805cf-295">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="805cf-295">**Congratulations!**</span></span> <span data-ttu-id="805cf-296">Ha creado correctamente una factoría de datos de Azure, servicios vinculados, conjuntos de datos y una canalización, y ha programado la canalización.</span><span class="sxs-lookup"><span data-stu-id="805cf-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled the pipeline.</span></span>

#### <a name="view-the-data-factory-in-a-diagram-view"></a><span data-ttu-id="805cf-297">Visualización de la factoría de datos en una vista de diagrama</span><span class="sxs-lookup"><span data-stu-id="805cf-297">View the data factory in a Diagram View</span></span>
1. <span data-ttu-id="805cf-298">En **Azure Portal**, haga clic en el icono **Diagrama** en la página principal de la factoría de datos **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="805cf-298">In the **Azure portal**, click **Diagram** tile on the home page for the **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="805cf-299">:</span><span class="sxs-lookup"><span data-stu-id="805cf-299">:</span></span>

    ![Vínculo de diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="805cf-301">Debería ver un diagrama similar a la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="805cf-301">You should see the diagram similar to the following image:</span></span>

    ![Vista de diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="805cf-303">Puede acercar, alejar, acercar al 100 %, ampliar para ajustar, colocar automáticamente canalizaciones y conjuntos de datos, y mostrar información sobre el linaje (resalta elementos ascendentes y descendentes de los elementos seleccionados).</span><span class="sxs-lookup"><span data-stu-id="805cf-303">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="805cf-304">Puede hacer doble clic en un objeto (conjunto de datos o canalización de entrada o salida) para ver sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="805cf-304">You can double-click an object (input/output dataset or pipeline) to see properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="805cf-305">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="805cf-305">Monitor pipeline</span></span>
<span data-ttu-id="805cf-306">En este paso, usará Azure Portal para supervisar lo que está ocurriendo en una factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="805cf-306">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="805cf-307">También puede usar los cmdlets de PowerShell para supervisar los conjuntos de datos y las canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="805cf-307">You can also use PowerShell cmdlets to monitor datasets and pipelines.</span></span> <span data-ttu-id="805cf-308">Para obtener más información sobre la supervisión, consulte [Supervisión y administración de canalizaciones](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="805cf-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="805cf-309">En el diagrama, haga doble clic en **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="805cf-309">In the diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Segmentos EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="805cf-311">Observe que el estado de todos los segmentos de datos es **Listo** porque la duración de la canalización (hora de inicio a hora de finalización) está en el pasado.</span><span class="sxs-lookup"><span data-stu-id="805cf-311">Notice that all the data slices up are in **Ready** state because the pipeline duration (start time to end time) is in the past.</span></span> <span data-ttu-id="805cf-312">Esto ocurre también porque ha insertado los datos en la base de datos de SQL Server y están ahí todo el tiempo.</span><span class="sxs-lookup"><span data-stu-id="805cf-312">It is also because you have inserted the data in the SQL Server database and it is there all the time.</span></span> <span data-ttu-id="805cf-313">Confirme que no aparecen segmentos en la sección de **segmentos problemáticos** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="805cf-313">Confirm that no slices show up in the **Problem slices** section at the bottom.</span></span> <span data-ttu-id="805cf-314">Para ver todos los segmentos, haga clic en **Ver más** en la parte inferior de la lista de segmentos.</span><span class="sxs-lookup"><span data-stu-id="805cf-314">To view all the slices, click **See More** at the bottom of the list of slices.</span></span>
3. <span data-ttu-id="805cf-315">A continuación, en la página **Conjuntos de datos**, haga clic en **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="805cf-315">Now, In the **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Segmentos OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="805cf-317">Haga clic en cualquier segmento de datos de la lista y debería ver la página **Segmento de datos**.</span><span class="sxs-lookup"><span data-stu-id="805cf-317">Click any data slice from the list and you should see the **Data Slice** page.</span></span> <span data-ttu-id="805cf-318">Verá las ejecuciones de actividad para ese segmento.</span><span class="sxs-lookup"><span data-stu-id="805cf-318">You see activity runs for the slice.</span></span> <span data-ttu-id="805cf-319">Normalmente solo se ve una ejecución de actividad.</span><span class="sxs-lookup"><span data-stu-id="805cf-319">You see only one activity run usually.</span></span>  

    ![Hoja Segmento de datos](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="805cf-321">Si el segmento no está en el estado **Listo**, puede ver los segmentos ascendentes que no están en estado Listo y bloquean la ejecución del segmento actual en la lista **Segmentos ascendentes que no están listos**.</span><span class="sxs-lookup"><span data-stu-id="805cf-321">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="805cf-322">Haga clic en la **ejecución de la actividad** de la lista en la parte inferior para ver los **detalles de la ejecución de la actividad**.</span><span class="sxs-lookup"><span data-stu-id="805cf-322">Click the **activity run** from the list at the bottom to see **activity run details**.</span></span>

   ![Página Detalles de ejecución de actividad](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="805cf-324">Verá información como el rendimiento, la duración y la puerta de enlace que se usa para transferir los datos.</span><span class="sxs-lookup"><span data-stu-id="805cf-324">You would see information such as throughput, duration, and the gateway used to transfer the data.</span></span>
6. <span data-ttu-id="805cf-325">Haga clic en **X** para cerrar todas las páginas hasta que</span><span class="sxs-lookup"><span data-stu-id="805cf-325">Click **X** to close all the pages until you</span></span>
7. <span data-ttu-id="805cf-326">regrese a la página principal de **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="805cf-326">get back to the home page for the **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="805cf-327">(Opcional) Haga clic en **Canalizaciones**, elija **ADFTutorialOnPremDF** y obtenga detalles de los conjuntos de datos de entrada (**Consumido**) o los conjuntos de datos de salida (**Producido**).</span><span class="sxs-lookup"><span data-stu-id="805cf-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="805cf-328">Use herramientas como el [Explorador de Microsoft Storage](http://storageexplorer.com/) para comprobar que se crea un blob o archivo cada hora.</span><span class="sxs-lookup"><span data-stu-id="805cf-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to verify that a blob/file is created for each hour.</span></span>

   ![Explorador de Azure Storage](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="805cf-330">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="805cf-330">Next steps</span></span>
* <span data-ttu-id="805cf-331">Vea el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para obtener todos los detalles sobre Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="805cf-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the Data Management Gateway.</span></span>
* <span data-ttu-id="805cf-332">Consulte [Copia de datos de Azure Blob en Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) si necesita más información sobre el uso de la actividad de copia para mover datos desde un almacén de datos de origen a un almacén de datos receptor.</span><span class="sxs-lookup"><span data-stu-id="805cf-332">See [Copy data from Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to learn about how to use Copy Activity to move data from a source data store to a sink data store.</span></span>
