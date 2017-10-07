---
title: datos de aaaMove - Data Management Gateway | Documentos de Microsoft
description: Configurar una puerta de enlace de datos toomove datos entre hello y local en la nube. Utilice Data Management Gateway en toomove Data Factory de Azure los datos.
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
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a><span data-ttu-id="06bf7-105">Mover datos entre orígenes locales y en la nube Hola con Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="06bf7-105">Move data between on-premises sources and hello cloud with Data Management Gateway</span></span>
<span data-ttu-id="06bf7-106">Este artículo proporciona información general sobre la integración de los almacenes de datos locales y los almacenes de datos en la nube mediante Data Factory.</span><span class="sxs-lookup"><span data-stu-id="06bf7-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="06bf7-107">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo y otros artículos de conceptos de núcleo de generador de datos: [conjuntos de datos](data-factory-create-datasets.md) y [canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="06bf7-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="06bf7-108">Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="06bf7-108">Data Management Gateway</span></span>
<span data-ttu-id="06bf7-109">Debe instalar Data Management Gateway en su tooenable de máquina local mover datos desde un almacén de datos local.</span><span class="sxs-lookup"><span data-stu-id="06bf7-109">You must install Data Management Gateway on your on-premises machine tooenable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="06bf7-110">puerta de enlace de Hello puede instalarse en hello que mismo equipo como almacén de datos de Hola o en un equipo diferente como puerta de enlace de hello puede conectar el almacén de datos de toohello.</span><span class="sxs-lookup"><span data-stu-id="06bf7-110">hello gateway can be installed on hello same machine as hello data store or on a different machine as long as hello gateway can connect toohello data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06bf7-111">Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para más detalles sobre Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="06bf7-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="06bf7-112">Hello en el tutorial siguiente muestra cómo una factoría de datos con una canalización que mueve los datos de una implementación local de toocreate **SQL Server** tooan almacenamiento de blobs de Azure de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="06bf7-112">hello following walkthrough shows you how toocreate a data factory with a pipeline that moves data from an on-premises **SQL Server** database tooan Azure blob storage.</span></span> <span data-ttu-id="06bf7-113">Como parte del tutorial de hello, instalar y configurar Hola Data Management Gateway en su equipo.</span><span class="sxs-lookup"><span data-stu-id="06bf7-113">As part of hello walkthrough, you install and configure hello Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-toocloud"></a><span data-ttu-id="06bf7-114">Tutorial: copiar toocloud de datos local</span><span class="sxs-lookup"><span data-stu-id="06bf7-114">Walkthrough: copy on-premises data toocloud</span></span>
<span data-ttu-id="06bf7-115">En este tutorial Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="06bf7-115">In this walkthrough you do hello following steps:</span></span> 

1. <span data-ttu-id="06bf7-116">Creación de una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="06bf7-116">Create a data factory.</span></span>
2. <span data-ttu-id="06bf7-117">Creación de una instancia de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="06bf7-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="06bf7-118">Creación de servicios vinculados para los almacenes de datos de origen y receptor.</span><span class="sxs-lookup"><span data-stu-id="06bf7-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="06bf7-119">Creación de conjuntos de datos toorepresent entrada y salida de datos.</span><span class="sxs-lookup"><span data-stu-id="06bf7-119">Create datasets toorepresent input and output data.</span></span>
5. <span data-ttu-id="06bf7-120">Crear una canalización con una copia actividad toomove Hola de datos.</span><span class="sxs-lookup"><span data-stu-id="06bf7-120">Create a pipeline with a copy activity toomove hello data.</span></span>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="06bf7-121">Requisitos previos para el tutorial de Hola</span><span class="sxs-lookup"><span data-stu-id="06bf7-121">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="06bf7-122">Antes de comenzar este tutorial, debe tener Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="06bf7-122">Before you begin this walkthrough, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="06bf7-123">**Suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-123">**Azure subscription**.</span></span>  <span data-ttu-id="06bf7-124">Si no tiene una suscripción, puede crear una cuenta de prueba gratuita en tan solo un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="06bf7-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="06bf7-125">Vea hello [gratuita](http://azure.microsoft.com/pricing/free-trial/) artículo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="06bf7-125">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="06bf7-126">**Cuenta de almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-126">**Azure Storage Account**.</span></span> <span data-ttu-id="06bf7-127">Usar el almacenamiento de blobs de Hola como un **destino/receptor** almacén de datos en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="06bf7-127">You use hello blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="06bf7-128">Si no tiene una cuenta de almacenamiento de Azure, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo para toocreate pasos uno.</span><span class="sxs-lookup"><span data-stu-id="06bf7-128">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="06bf7-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-129">**SQL Server**.</span></span> <span data-ttu-id="06bf7-130">Use una base de datos de SQL Server local como almacén de datos de **origen** en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="06bf7-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="06bf7-131">Creación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="06bf7-131">Create data factory</span></span>
<span data-ttu-id="06bf7-132">En este paso, utilice hello Azure toocreate portal una instancia de la factoría de datos de Azure denominada **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-132">In this step, you use hello Azure portal toocreate an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="06bf7-133">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06bf7-133">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="06bf7-134">Haga clic en **+ NUEVO**, en **Inteligencia y análisis** y en **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![New->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="06bf7-136">Hola **factoría de datos** escriba **ADFTutorialOnPremDF** para hello nombre.</span><span class="sxs-lookup"><span data-stu-id="06bf7-136">In hello **New data factory** page, enter **ADFTutorialOnPremDF** for hello Name.</span></span>

    ![Agregar tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="06bf7-138">nombre de Hola Hola Azure factoría de datos debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="06bf7-138">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="06bf7-139">Si recibe el error hello: **nombre de generador de datos "ADFTutorialOnPremDF" no está disponible**, cambiar nombre de Hola Hola factoría de datos (por ejemplo, yournameADFTutorialOnPremDF) y pruebe a crear de nuevo.</span><span class="sxs-lookup"><span data-stu-id="06bf7-139">If you receive hello error: **Data factory name “ADFTutorialOnPremDF” is not available**, change hello name of hello data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="06bf7-140">Use este nombre en lugar de ADFTutorialFactory al realizar los restantes pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="06bf7-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="06bf7-141">nombre de Hola Hola factoría de datos se puede registrar como un **DNS** asigne un nombre en el futuro de hello y, por tanto, se convierten en visible públicamente.</span><span class="sxs-lookup"><span data-stu-id="06bf7-141">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="06bf7-142">Seleccione hello **suscripción de Azure** donde desea Hola datos generador toobe creado.</span><span class="sxs-lookup"><span data-stu-id="06bf7-142">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="06bf7-143">Seleccione un **grupo de recursos** existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="06bf7-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="06bf7-144">Para ver tutorial Hola, cree un grupo de recursos denominado: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-144">For hello tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="06bf7-145">Haga clic en **crear** en hello **factoría de datos** página.</span><span class="sxs-lookup"><span data-stu-id="06bf7-145">Click **Create** on hello **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="06bf7-146">instancias de la factoría de datos de toocreate, debe ser miembro del programa Hola a [colaborador de la factoría de datos](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol en el nivel de grupo de recursos/suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="06bf7-147">Una vez completada la creación, vea hello **factoría de datos** página como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="06bf7-147">After creation is complete, you see hello **Data Factory** page as shown in hello following image:</span></span>

   ![Página principal de Factoría de datos](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="06bf7-149">Crear puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="06bf7-149">Create gateway</span></span>
1. <span data-ttu-id="06bf7-150">Hola **factoría de datos** página, haga clic en **autor e implementar** icono toolaunch hello **Editor** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-150">In hello **Data Factory** page, click **Author and deploy** tile toolaunch hello **Editor** for hello data factory.</span></span>

    ![Mosaico Crear e implementar](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="06bf7-152">Hola Editor de generador de datos, haga clic en **... Más** Hola barra de herramientas y, a continuación, haga clic en **nueva puerta de enlace de datos**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-152">In hello Data Factory Editor, click **... More** on hello toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="06bf7-153">Como alternativa, puede hacer clic **puertas de enlace de datos** en Hola vista de árbol y haga clic en **nueva puerta de enlace de datos**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-153">Alternatively, you can right-click **Data Gateways** in hello tree view, and click **New data gateway**.</span></span>

   ![Nueva puerta de enlace de datos en la barra de herramientas](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="06bf7-155">Hola **crear** escriba **adftutorialgateway** para hello **nombre**y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-155">In hello **Create** page, enter **adftutorialgateway** for hello **name**, and click **OK**.</span></span>     

    ![Página Crear puerta de enlace](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="06bf7-157">En este tutorial, creará puerta de enlace lógica de hello con un único nodo (máquina de Windows local).</span><span class="sxs-lookup"><span data-stu-id="06bf7-157">In this walkthrough, you create hello logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="06bf7-158">Puede escalar horizontalmente una puerta de enlace de administración de datos mediante la asociación de varios máquinas locales con puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-158">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="06bf7-159">Puede escalar verticalmente aumentando el número de trabajos de movimiento de datos que pueden ejecutarse simultáneamente en un nodo.</span><span class="sxs-lookup"><span data-stu-id="06bf7-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="06bf7-160">Esta característica también está disponible para una puerta de enlace lógica con un único nodo.</span><span class="sxs-lookup"><span data-stu-id="06bf7-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="06bf7-161">Consulte el artículo [Escalado en Data Management Gateway en Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="06bf7-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="06bf7-162">Hola **configurar** página, haga clic en **instalar directamente en este equipo**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-162">In hello **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="06bf7-163">Esta acción descarga el paquete de instalación de Hola de puerta de enlace de hello, instala, configura y registra la puerta de enlace de hello en el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-163">This action downloads hello installation package for hello gateway, installs, configures, and registers hello gateway on hello computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="06bf7-164">Utilice Internet Explorer o un explorador web compatible con Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="06bf7-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="06bf7-165">Si usas Chrome, vaya toohello [almacén web de Chrome](https://chrome.google.com/webstore/), buscar con la palabra clave "ClickOnce", elija una de las extensiones de ClickOnce hello e instalarlo.</span><span class="sxs-lookup"><span data-stu-id="06bf7-165">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="06bf7-166">Hola mismo para Firefox (complemento de instalación).</span><span class="sxs-lookup"><span data-stu-id="06bf7-166">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="06bf7-167">Haga clic en **menú Abrir** botón de barra de herramientas de hello (**tres líneas horizontales** en la esquina superior derecha de hello), haga clic en **complementos**, buscar con la palabra clave "ClickOnce", elija uno de Hola Extensiones de ClickOnce e instalarlo.</span><span class="sxs-lookup"><span data-stu-id="06bf7-167">Click **Open Menu** button on hello toolbar (**three horizontal lines** in hello top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Puerta de enlace: página Configurar](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="06bf7-169">De este modo es toodownload (un solo clic) de la manera más fácil de hello, instalar, configurar y registrar la puerta de enlace de hello en un solo paso.</span><span class="sxs-lookup"><span data-stu-id="06bf7-169">This way is hello easiest way (one-click) toodownload, install, configure, and register hello gateway in one single step.</span></span> <span data-ttu-id="06bf7-170">Puede ver hello **Administrador de configuración de Microsoft Data Management Gateway** aplicación está instalada en el equipo.</span><span class="sxs-lookup"><span data-stu-id="06bf7-170">You can see hello **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="06bf7-171">También puede encontrar Hola ejecutable **ConfigManager.exe** en la carpeta de hello: **C:\Program Files\Microsoft datos administración Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-171">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="06bf7-172">También puede descargar e instalar puerta de enlace de manualmente mediante el uso de vínculos de hello en esta página y registrarla mediante la clave de Hola que aparece en hello **nueva clave** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="06bf7-172">You can also download and install gateway manually by using hello links in this page and register it using hello key shown in hello **NEW KEY** text box.</span></span>

    <span data-ttu-id="06bf7-173">Vea [Data Management Gateway](data-factory-data-management-gateway.md) artículo para todos los detalles acerca de la puerta de enlace de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="06bf7-174">Debe ser un administrador en hello tooinstall de equipo local y configurar correctamente Hola Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="06bf7-174">You must be an administrator on hello local computer tooinstall and configure hello Data Management Gateway successfully.</span></span> <span data-ttu-id="06bf7-175">Puede agregar usuarios adicionales toohello **Data Management Gateway Users** grupo local de Windows.</span><span class="sxs-lookup"><span data-stu-id="06bf7-175">You can add additional users toohello **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="06bf7-176">los miembros de Hola de este grupo pueden utilizar la puerta de enlace de hello Administrador de configuración de Data Management Gateway herramienta tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-176">hello members of this group can use hello Data Management Gateway Configuration Manager tool tooconfigure hello gateway.</span></span>
   >
   >
5. <span data-ttu-id="06bf7-177">Espere unos minutos o espere hasta que vea Hola después el mensaje de notificación:</span><span class="sxs-lookup"><span data-stu-id="06bf7-177">Wait for a couple of minutes or wait until you see hello following notification message:</span></span>

    ![Instalación correcta de la puerta de enlace](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="06bf7-179">Inicie la aplicación **Administrador de configuración de Data Management Gateway** en el equipo.</span><span class="sxs-lookup"><span data-stu-id="06bf7-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="06bf7-180">Hola **búsqueda** ventana, escriba **Data Management Gateway** tooaccess este utilidad.</span><span class="sxs-lookup"><span data-stu-id="06bf7-180">In hello **Search** window, type **Data Management Gateway** tooaccess this utility.</span></span> <span data-ttu-id="06bf7-181">También puede encontrar Hola ejecutable **ConfigManager.exe** en la carpeta de hello: **C:\Program Files\Microsoft datos administración Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="06bf7-181">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Administrador de configuración de puertas de enlace](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="06bf7-183">Confirme que ve el mensaje `adftutorialgateway is connected toohello cloud service`.</span><span class="sxs-lookup"><span data-stu-id="06bf7-183">Confirm that you see `adftutorialgateway is connected toohello cloud service` message.</span></span> <span data-ttu-id="06bf7-184">Hola Hola inferior muestra la barra de estado **toohello servicio de nube conectado** junto con un **marca de verificación verde**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-184">hello status bar hello bottom displays **Connected toohello cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="06bf7-185">En hello **inicio** pestaña, también puede hacer Hola realizar las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="06bf7-185">On hello **Home** tab, you can also do hello following operations:</span></span>

   * <span data-ttu-id="06bf7-186">**Registrar** una puerta de enlace con una clave de hello portal de Azure con botón de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="06bf7-186">**Register** a gateway with a key from hello Azure portal by using hello Register button.</span></span>
   * <span data-ttu-id="06bf7-187">**Detener** Hola servicio de Host de Data Management Gateway ejecutando en el equipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="06bf7-187">**Stop** hello Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="06bf7-188">**Programar actualizaciones** toobe instalado en un momento determinado del día de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-188">**Schedule updates** toobe installed at a specific time of hello day.</span></span>
   * <span data-ttu-id="06bf7-189">Ver si se realizó la puerta de enlace de hello **actualizó por última vez**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-189">View when hello gateway was **last updated**.</span></span>
   * <span data-ttu-id="06bf7-190">Especifique la hora a la que se puede instalar una puerta de enlace de toohello de actualización.</span><span class="sxs-lookup"><span data-stu-id="06bf7-190">Specify time at which an update toohello gateway can be installed.</span></span>
8. <span data-ttu-id="06bf7-191">Cambiar toohello **configuración** certificado de Hola de ficha especificado en hello **certificado** sección es usado tooencrypt o descifrar credenciales para almacén de datos local de Hola que especifique en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-191">Switch toohello **Settings** tab. hello certificate specified in hello **Certificate** section is used tooencrypt/decrypt credentials for hello on-premises data store that you specify on hello portal.</span></span> <span data-ttu-id="06bf7-192">(opcional) Haga clic en **cambio** toouse su propio certificado en su lugar.</span><span class="sxs-lookup"><span data-stu-id="06bf7-192">(optional) Click **Change** toouse your own certificate instead.</span></span> <span data-ttu-id="06bf7-193">De forma predeterminada, puerta de enlace de hello utiliza certificado Hola Hola servicio factoría de datos genera automáticamente.</span><span class="sxs-lookup"><span data-stu-id="06bf7-193">By default, hello gateway uses hello certificate that is auto-generated by hello Data Factory service.</span></span>

    ![Configuración del certificado de puerta de enlace](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="06bf7-195">También puede hacer Hola siguientes acciones en hello **configuración** ficha:</span><span class="sxs-lookup"><span data-stu-id="06bf7-195">You can also do hello following actions on hello **Settings** tab:</span></span>

   * <span data-ttu-id="06bf7-196">Ver o exportar el certificado de Hola que se usa la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-196">View or export hello certificate being used by hello gateway.</span></span>
   * <span data-ttu-id="06bf7-197">Cambiar el punto de conexión HTTPS de hello usa Hola puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="06bf7-197">Change hello HTTPS endpoint used by hello gateway.</span></span>    
   * <span data-ttu-id="06bf7-198">Establecer un toobe del proxy HTTP utilizado por la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-198">Set an HTTP proxy toobe used by hello gateway.</span></span>     
9. <span data-ttu-id="06bf7-199">(opcional) Cambiar toohello **diagnósticos** ficha, compruebe hello **habilitar el registro detallado** opción si desea que tooenable el registro que puede usar cualquier problema tootroubleshoot con puerta de enlace de hello detallado.</span><span class="sxs-lookup"><span data-stu-id="06bf7-199">(optional) Switch toohello **Diagnostics** tab, check hello **Enable verbose logging** option if you want tooenable verbose logging that you can use tootroubleshoot any issues with hello gateway.</span></span> <span data-ttu-id="06bf7-200">Hello información de registro puede encontrarse en **Visor de eventos** en **registros de aplicaciones y servicios** -> **Data Management Gateway** nodo.</span><span class="sxs-lookup"><span data-stu-id="06bf7-200">hello logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Ficha Diagnóstico](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="06bf7-202">También puede realizar Hola siguientes acciones en hello **diagnósticos** ficha:</span><span class="sxs-lookup"><span data-stu-id="06bf7-202">You can also perform hello following actions in hello **Diagnostics** tab:</span></span>

   * <span data-ttu-id="06bf7-203">Use **Probar conexión** origen de datos local de la sección tooan con puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-203">Use **Test Connection** section tooan on-premises data source using hello gateway.</span></span>
   * <span data-ttu-id="06bf7-204">Haga clic en **ver registros** toosee Hola Data Management Gateway inicie sesión en una ventana del Visor de eventos.</span><span class="sxs-lookup"><span data-stu-id="06bf7-204">Click **View Logs** toosee hello Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="06bf7-205">Haga clic en **enviar registros** tooupload un archivo zip con registros de los últimos siete días tooMicrosoft toofacilitate solución de problemas de los problemas.</span><span class="sxs-lookup"><span data-stu-id="06bf7-205">Click **Send Logs** tooupload a zip file with logs of last seven days tooMicrosoft toofacilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="06bf7-206">En hello **diagnósticos** ficha Hola **Probar conexión** sección, seleccione **SqlServer** para el tipo de saludo de datos de hello, almacenar, escriba Hola nombre del servidor de base de datos de Hola, nombre del Hola de base de datos, especificar el tipo de autenticación, escriba el nombre de usuario y contraseña y haga clic en **prueba** tootest si la puerta de enlace de hello puede conectarse toohello base de datos.</span><span class="sxs-lookup"><span data-stu-id="06bf7-206">On hello **Diagnostics** tab, in hello **Test Connection** section, select **SqlServer** for hello type of hello data store, enter hello name of hello database server, name of hello database, specify authentication type, enter user name, and password, and click **Test** tootest whether hello gateway can connect toohello database.</span></span>
11. <span data-ttu-id="06bf7-207">Explorador de web toohello de conmutador y en hello **portal de Azure**, haga clic en **Aceptar** en hello **configurar** página y, a continuación, en hello **nueva puerta de enlace de datos** página.</span><span class="sxs-lookup"><span data-stu-id="06bf7-207">Switch toohello web browser, and in hello **Azure portal**, click **OK** on hello **Configure** page and then on hello **New data gateway** page.</span></span>
12. <span data-ttu-id="06bf7-208">Debería ver **adftutorialgateway** en **puertas de enlace de datos** en vista de árbol de Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="06bf7-208">You should see **adftutorialgateway** under **Data Gateways** in hello tree view on hello left.</span></span>  <span data-ttu-id="06bf7-209">Si hace clic en él, debería ver Hola asociados JSON.</span><span class="sxs-lookup"><span data-stu-id="06bf7-209">If you click it, you should see hello associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="06bf7-210">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="06bf7-210">Create linked services</span></span>
<span data-ttu-id="06bf7-211">En este paso, creará dos servicios vinculados: **AzureStorageLinkedService** y **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="06bf7-212">Hola **SqlServerLinkedService** vincula una base de datos de SQL Server local y hello **AzureStorageLinkedService** servicio vinculado vincula una factoría de datos de toohello de almacén de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="06bf7-212">hello **SqlServerLinkedService** links an on-premises SQL Server database and hello **AzureStorageLinkedService** linked service links an Azure blob store toohello data factory.</span></span> <span data-ttu-id="06bf7-213">Crear una canalización más adelante en este tutorial que copia datos de almacén de blobs de Azure de hello local SQL Server base de datos toohello.</span><span class="sxs-lookup"><span data-stu-id="06bf7-213">You create a pipeline later in this walkthrough that copies data from hello on-premises SQL Server database toohello Azure blob store.</span></span>

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a><span data-ttu-id="06bf7-214">Agregar una base de datos de SQL Server de servicio vinculado tooan local</span><span class="sxs-lookup"><span data-stu-id="06bf7-214">Add a linked service tooan on-premises SQL Server database</span></span>
1. <span data-ttu-id="06bf7-215">Hola **Editor de generador de datos**, haga clic en **nuevo almacén de datos** en la barra de herramientas de Hola y seleccione **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-215">In hello **Data Factory Editor**, click **New data store** on hello toolbar and select **SQL Server**.</span></span>

   ![Nuevo servicio vinculado de SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="06bf7-217">Hola **editor JSON** en Hola derecho Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="06bf7-217">In hello **JSON editor** on hello right, do hello following steps:</span></span>

   1. <span data-ttu-id="06bf7-218">Para hello **gatewayName**, especifique **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-218">For hello **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="06bf7-219">Hola **connectionString**, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="06bf7-219">In hello **connectionString**, do hello following steps:</span></span>    

      1. <span data-ttu-id="06bf7-220">Para **servername**, escriba Hola nombre de hello servidor que hospeda la base de datos de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-220">For **servername**, enter hello name of hello server that hosts hello SQL Server database.</span></span>
      2. <span data-ttu-id="06bf7-221">Para **databasename**, escriba Hola nombre de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-221">For **databasename**, enter hello name of hello database.</span></span>
      3. <span data-ttu-id="06bf7-222">Haga clic en **Encrypt** botón de barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-222">Click **Encrypt** button on hello toolbar.</span></span> <span data-ttu-id="06bf7-223">Consulte aplicación de administrador de credenciales de hello.</span><span class="sxs-lookup"><span data-stu-id="06bf7-223">You see hello Credentials Manager application.</span></span>

         ![Aplicación Administrador de credenciales](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="06bf7-225">Hola **establecer credenciales** cuadro de diálogo, especifique el tipo de autenticación, nombre de usuario y contraseña y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-225">In hello **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="06bf7-226">Si Hola conexión es correcta, credenciales de hello cifrado se almacenan en hello JSON y cierra el cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-226">If hello connection is successful, hello encrypted credentials are stored in hello JSON and hello dialog box closes.</span></span>
      5. <span data-ttu-id="06bf7-227">Cerrar la pestaña de explorador vacía de Hola que inicia el cuadro de diálogo de hello si no se cierra automáticamente y regresar pestaña toohello con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="06bf7-227">Close hello empty browser tab that launched hello dialog box if it is not automatically closed and get back toohello tab with hello Azure portal.</span></span>

         <span data-ttu-id="06bf7-228">En la máquina de puerta de enlace de hello, estas credenciales son **cifrados** mediante un certificado que Hola factoría de datos posee el servicio.</span><span class="sxs-lookup"><span data-stu-id="06bf7-228">On hello gateway machine, these credentials are **encrypted** by using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="06bf7-229">Si desea toouse Hola certificado asociado con hello Data Management Gateway en su lugar, consulte [establecer las credenciales de forma segura](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="06bf7-229">If you want toouse hello certificate that is associated with hello Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="06bf7-230">Haga clic en **implementar** en toodeploy Hola servicio vinculado de SQL Server de la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-230">Click **Deploy** on hello command bar toodeploy hello SQL Server linked service.</span></span> <span data-ttu-id="06bf7-231">Debería ver Hola vinculado servicio en la vista de árbol de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-231">You should see hello linked service in hello tree view.</span></span>

      ![Servicio de SQL Server vinculado en la vista de árbol de Hola](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="06bf7-233">Adición de un servicio vinculado para una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="06bf7-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="06bf7-234">Hola **Editor de generador de datos**, haga clic en **nuevo almacén de datos** Hola barra de comandos y haga clic en **almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-234">In hello **Data Factory Editor**, click **New data store** on hello command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="06bf7-235">Escriba Hola nombre de la cuenta de almacenamiento de Azure para hello **nombre de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-235">Enter hello name of your Azure storage account for hello **Account name**.</span></span>
3. <span data-ttu-id="06bf7-236">Escriba la clave de Hola de su cuenta de almacenamiento de Azure para hello **clave de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-236">Enter hello key for your Azure storage account for hello **Account key**.</span></span>
4. <span data-ttu-id="06bf7-237">Haga clic en **implementar** toodeploy hello **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-237">Click **Deploy** toodeploy hello **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="06bf7-238">Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="06bf7-238">Create datasets</span></span>
<span data-ttu-id="06bf7-239">En este paso, creará entrada y salida conjuntos de datos que representan los datos de entrada y salidas para la operación de copia de hello (base de datos de SQL Server en local = > almacenamiento de blobs de Azure).</span><span class="sxs-lookup"><span data-stu-id="06bf7-239">In this step, you create input and output datasets that represent input and output data for hello copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="06bf7-240">Antes de crear conjuntos de datos, Hola pasos (los pasos detallados a continuación de lista de hello):</span><span class="sxs-lookup"><span data-stu-id="06bf7-240">Before creating datasets, do hello following steps (detailed steps follows hello list):</span></span>

* <span data-ttu-id="06bf7-241">Crear una tabla denominada **emp** en Hola base de datos de SQL Server agrega como una factoría de datos de servicio vinculado toohello e inserte un par de entradas de ejemplo en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-241">Create a table named **emp** in hello SQL Server Database you added as a linked service toohello data factory and insert a couple of sample entries into hello table.</span></span>
* <span data-ttu-id="06bf7-242">Crear un contenedor de blobs denominado **adftutorial** en hello Azure blob agrega como una factoría de datos de servicio vinculado toohello de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="06bf7-242">Create a blob container named **adftutorial** in hello Azure blob storage account you added as a linked service toohello data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a><span data-ttu-id="06bf7-243">Preparar SQL Server en local para el tutorial de Hola</span><span class="sxs-lookup"><span data-stu-id="06bf7-243">Prepare On-premises SQL Server for hello tutorial</span></span>
1. <span data-ttu-id="06bf7-244">En base de datos de hello especificada para hello SQL Server local servicio vinculado (**SqlServerLinkedService**), usar hello después Hola de toocreate de secuencia de comandos SQL **emp** tabla de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-244">In hello database you specified for hello on-premises SQL Server linked service (**SqlServerLinkedService**), use hello following SQL script toocreate hello **emp** table in hello database.</span></span>

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
2. <span data-ttu-id="06bf7-245">Insertar algunos ejemplos en la tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="06bf7-245">Insert some sample into hello table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="06bf7-246">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="06bf7-246">Create input dataset</span></span>

1. <span data-ttu-id="06bf7-247">Hola **Editor de generador de datos**, haga clic en **... Más**, haga clic en **nuevo conjunto de datos** Hola barra de comandos y haga clic en **tabla de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-247">In hello **Data Factory Editor**, click **... More**, click **New dataset** on hello command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="06bf7-248">Reemplace Hola JSON en el panel derecho de hello con hello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="06bf7-248">Replace hello JSON in hello right pane with hello following text:</span></span>

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
   <span data-ttu-id="06bf7-249">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="06bf7-249">Note hello following points:</span></span>

   * <span data-ttu-id="06bf7-250">**tipo de** se establece demasiado**SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-250">**type** is set too**SqlServerTable**.</span></span>
   * <span data-ttu-id="06bf7-251">**tableName** se establece demasiado**emp**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-251">**tableName** is set too**emp**.</span></span>
   * <span data-ttu-id="06bf7-252">**linkedServiceName** se establece demasiado**SqlServerLinkedService** (este servicio vinculado había creado anteriormente en este tutorial.).</span><span class="sxs-lookup"><span data-stu-id="06bf7-252">**linkedServiceName** is set too**SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="06bf7-253">Para un conjunto de datos entrada que no se hayan generado por otra canalización de factoría de datos de Azure, debe establecer **externo** demasiado**true**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** too**true**.</span></span> <span data-ttu-id="06bf7-254">Indica los datos de entrada de hello están toohello externo producido servicio Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="06bf7-254">It denotes hello input data is produced external toohello Azure Data Factory service.</span></span> <span data-ttu-id="06bf7-255">Opcionalmente, puede especificar las directivas de datos externos utilizando hello **externalData** elemento Hola **directiva** sección.</span><span class="sxs-lookup"><span data-stu-id="06bf7-255">You can optionally specify any external data policies using hello **externalData** element in hello **Policy** section.</span></span>    

   <span data-ttu-id="06bf7-256">Para más información acerca de las propiedades de JSON, consulte [Movimiento de datos hacia y desde SQL Server](data-factory-sqlserver-connector.md).</span><span class="sxs-lookup"><span data-stu-id="06bf7-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="06bf7-257">Haga clic en **implementar** en el conjunto de datos de toodeploy Hola la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-257">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="06bf7-258">Creación del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="06bf7-258">Create output dataset</span></span>

1. <span data-ttu-id="06bf7-259">Hola **Editor de generador de datos**, haga clic en **nuevo conjunto de datos** Hola barra de comandos y haga clic en **almacenamiento de blobs de Azure**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-259">In hello **Data Factory Editor**, click **New dataset** on hello command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="06bf7-260">Reemplace Hola JSON en el panel derecho de hello con hello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="06bf7-260">Replace hello JSON in hello right pane with hello following text:</span></span>

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
   <span data-ttu-id="06bf7-261">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="06bf7-261">Note hello following points:</span></span>

   * <span data-ttu-id="06bf7-262">**tipo de** se establece demasiado**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-262">**type** is set too**AzureBlob**.</span></span>
   * <span data-ttu-id="06bf7-263">**linkedServiceName** se establece demasiado**AzureStorageLinkedService** (había creado este servicio vinculado en el paso 2).</span><span class="sxs-lookup"><span data-stu-id="06bf7-263">**linkedServiceName** is set too**AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="06bf7-264">**folderPath** se establece demasiado**adftutorial/outfromonpremdf** donde outfromonpremdf es la carpeta hello en el contenedor de adftutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-264">**folderPath** is set too**adftutorial/outfromonpremdf** where outfromonpremdf is hello folder in hello adftutorial container.</span></span> <span data-ttu-id="06bf7-265">Crear hello **adftutorial** contenedor si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="06bf7-265">Create hello **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="06bf7-266">Hola **disponibilidad** se establece demasiado**cada hora** (**frecuencia** establecido demasiado**hora** y **intervalo** establecido demasiado **1**).</span><span class="sxs-lookup"><span data-stu-id="06bf7-266">hello **availability** is set too**hourly** (**frequency** set too**hour** and **interval** set too**1**).</span></span>  <span data-ttu-id="06bf7-267">Hola servicio factoría de datos genera un segmento de datos de salida cada hora en hello **emp** tabla Hola base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="06bf7-267">hello Data Factory service generates an output data slice every hour in hello **emp** table in hello Azure SQL Database.</span></span>

   <span data-ttu-id="06bf7-268">Si no se especifica un **fileName** para un **tabla de salida**, archivos de hello generado en hello **folderPath** se denominan en hello siguiendo el formato: datos.<Guid>. txt (por ejemplo:: Data.0a405f8a 93ff 4c6f b3be f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="06bf7-268">If you do not specify a **fileName** for an **output table**, hello generated files in hello **folderPath** are named in hello following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="06bf7-269">tooset **folderPath** y **fileName** dinámicamente en función de hello **SliceStart** tiempo, use la propiedad de partitionedBy Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-269">tooset **folderPath** and **fileName** dynamically based on hello **SliceStart** time, use hello partitionedBy property.</span></span> <span data-ttu-id="06bf7-270">En el siguiente ejemplo de Hola folderPath usa año, mes y día de hello SliceStart (hora de inicio del segmento de hello procesando) y nombre de archivo usa hora de hello SliceStart.</span><span class="sxs-lookup"><span data-stu-id="06bf7-270">In hello following example, folderPath uses Year, Month, and Day from hello SliceStart (start time of hello slice being processed) and fileName uses Hour from hello SliceStart.</span></span> <span data-ttu-id="06bf7-271">Por ejemplo, si se está produciendo un segmento para 2014-10-20T08:00:00, Hola nombreDeCarpeta se establece toowikidatagateway/wikisampledataout/2014/10/20 y fileName hello too08.csv.</span><span class="sxs-lookup"><span data-stu-id="06bf7-271">For example, if a slice is being produced for 2014-10-20T08:00:00, hello folderName is set toowikidatagateway/wikisampledataout/2014/10/20 and hello fileName is set too08.csv.</span></span>

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

    <span data-ttu-id="06bf7-272">Para más información acerca de las propiedades de JSON, consulte [Movimiento de datos hacia y desde Azure Blob Storage](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="06bf7-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="06bf7-273">Haga clic en **implementar** en el conjunto de datos de toodeploy Hola la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-273">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span> <span data-ttu-id="06bf7-274">Confirme que ve los dos conjuntos de datos de hello en la vista de árbol de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-274">Confirm that you see both hello datasets in hello tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="06bf7-275">Creación de una canalización</span><span class="sxs-lookup"><span data-stu-id="06bf7-275">Create pipeline</span></span>
<span data-ttu-id="06bf7-276">En este paso, va a crear una **canalización** con una **actividad de copia** que usa **EmpOnPremSQLTable** como entrada y **OutputBlobTable** como salida.</span><span class="sxs-lookup"><span data-stu-id="06bf7-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="06bf7-277">En Data Factory Editor, haga clic en **... Más** y, luego, en **Nueva canalización**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="06bf7-278">Reemplace Hola JSON en el panel derecho de hello con hello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="06bf7-278">Replace hello JSON in hello right pane with hello following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
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
   > <span data-ttu-id="06bf7-279">Reemplazar el valor de Hola de hello **iniciar** propiedad con hello día actual y **final** valor con hello día siguiente.</span><span class="sxs-lookup"><span data-stu-id="06bf7-279">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span>
   >
   >

   <span data-ttu-id="06bf7-280">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="06bf7-280">Note hello following points:</span></span>

   * <span data-ttu-id="06bf7-281">En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-281">In hello activities section, there is only activity whose **type** is set too**Copy**.</span></span>
   * <span data-ttu-id="06bf7-282">**Entrada** de actividad hello se establece demasiado**EmpOnPremSQLTable** y **salida** de actividad hello se establece demasiado**OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-282">**Input** for hello activity is set too**EmpOnPremSQLTable** and **output** for hello activity is set too**OutputBlobTable**.</span></span>
   * <span data-ttu-id="06bf7-283">Hola **typeProperties** sección, **SqlSource** se especifica como hello **tipo de origen de** y ** BlobSink ** se especifica como hello **receptor tipo**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-283">In hello **typeProperties** section, **SqlSource** is specified as hello **source type** and **BlobSink **is specified as hello **sink type**.</span></span>
   * <span data-ttu-id="06bf7-284">Consulta SQL `select * from emp` se especifica para hello **sqlReaderQuery** propiedad de **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-284">SQL query `select * from emp` is specified for hello **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="06bf7-285">Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="06bf7-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="06bf7-286">Por ejemplo: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="06bf7-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="06bf7-287">Hola **final** tiempo es opcional, pero se usa en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="06bf7-287">hello **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="06bf7-288">Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="06bf7-288">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="06bf7-289">canalización de hello toorun indefinidamente, especifique **9/9/9999** como valor de Hola de hello **final** propiedad.</span><span class="sxs-lookup"><span data-stu-id="06bf7-289">toorun hello pipeline indefinitely, specify **9/9/9999** as hello value for hello **end** property.</span></span>

   <span data-ttu-id="06bf7-290">Se está definiendo Hola duración en qué Hola se procesan los segmentos de datos en función de hello **disponibilidad** propiedades que se han definido para cada conjunto de datos de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="06bf7-290">You are defining hello time duration in which hello data slices are processed based on hello **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="06bf7-291">En el ejemplo de Hola, hay 24 segmentos de datos tal y como se produce cada segmento de datos cada hora.</span><span class="sxs-lookup"><span data-stu-id="06bf7-291">In hello example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="06bf7-292">Haga clic en **implementar** en el conjunto de datos de toodeploy Hola la barra de comandos de hello (tabla es un conjunto de datos rectangular).</span><span class="sxs-lookup"><span data-stu-id="06bf7-292">Click **Deploy** on hello command bar toodeploy hello dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="06bf7-293">Confirmar esa canalización Hola se muestra en la vista de árbol de hello en **canalizaciones** nodo.</span><span class="sxs-lookup"><span data-stu-id="06bf7-293">Confirm that hello pipeline shows up in hello tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="06bf7-294">Ahora, haga clic en **X** dos veces tooclose Hola página tooget back-toohello **factoría de datos** página de hello **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-294">Now, click **X** twice tooclose hello page tooget back toohello **Data Factory** page for hello **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="06bf7-295">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="06bf7-295">**Congratulations!**</span></span> <span data-ttu-id="06bf7-296">Ha creado correctamente una factoría de datos de Azure, servicios vinculados, conjuntos de datos y una canalización y canalización Hola programada.</span><span class="sxs-lookup"><span data-stu-id="06bf7-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled hello pipeline.</span></span>

#### <a name="view-hello-data-factory-in-a-diagram-view"></a><span data-ttu-id="06bf7-297">Factoría de datos de vista hello en una vista de diagrama</span><span class="sxs-lookup"><span data-stu-id="06bf7-297">View hello data factory in a Diagram View</span></span>
1. <span data-ttu-id="06bf7-298">Hola **portal de Azure**, haga clic en **diagrama** de mosaico en la página de inicio de Hola de hello **ADFTutorialOnPremDF** factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="06bf7-298">In hello **Azure portal**, click **Diagram** tile on hello home page for hello **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="06bf7-299">:</span><span class="sxs-lookup"><span data-stu-id="06bf7-299">:</span></span>

    ![Vínculo de diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="06bf7-301">Debería ver Hola diagrama similar toohello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="06bf7-301">You should see hello diagram similar toohello following image:</span></span>

    ![Vista de diagrama](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="06bf7-303">Puede acercar, alejar, zoom too100%, toofit de zoom, automáticamente las canalizaciones de posición y conjuntos de datos y mostrar la información de linaje (resalta los elementos que preceden y siguen en la cadena de los elementos seleccionados).</span><span class="sxs-lookup"><span data-stu-id="06bf7-303">You can zoom in, zoom out, zoom too100%, zoom toofit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="06bf7-304">Hacer doble clic en un toosee las propiedades de objeto (conjunto de datos de entrada/salida o canalización) para ella.</span><span class="sxs-lookup"><span data-stu-id="06bf7-304">You can double-click an object (input/output dataset or pipeline) toosee properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="06bf7-305">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="06bf7-305">Monitor pipeline</span></span>
<span data-ttu-id="06bf7-306">En este paso, utilizará hello toomonitor portal Azure que está sucediendo en una factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="06bf7-306">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="06bf7-307">También puede utilizar las canalizaciones y conjuntos de datos de toomonitor de cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06bf7-307">You can also use PowerShell cmdlets toomonitor datasets and pipelines.</span></span> <span data-ttu-id="06bf7-308">Para obtener más información sobre la supervisión, consulte [Supervisión y administración de canalizaciones](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="06bf7-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="06bf7-309">En el diagrama de hello, haga doble clic en **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-309">In hello diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Segmentos EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="06bf7-311">Tenga en cuenta que todos los datos de hello divide los están en **listo** estado porque Hola canalización tiempo (hora de tooend de tiempo de inicio) en hello anterior.</span><span class="sxs-lookup"><span data-stu-id="06bf7-311">Notice that all hello data slices up are in **Ready** state because hello pipeline duration (start time tooend time) is in hello past.</span></span> <span data-ttu-id="06bf7-312">También es porque ha insertado datos hello en la base de datos de SQL Server de Hola y encuentra todo el tiempo Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-312">It is also because you have inserted hello data in hello SQL Server database and it is there all hello time.</span></span> <span data-ttu-id="06bf7-313">Confirme que no hay ningún segmento se mostrarán en hello **sectores problema** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-313">Confirm that no slices show up in hello **Problem slices** section at hello bottom.</span></span> <span data-ttu-id="06bf7-314">tooview todos los sectores de hello, haga clic en ejecutar **vea más** final Hola de lista de Hola de segmentos.</span><span class="sxs-lookup"><span data-stu-id="06bf7-314">tooview all hello slices, click **See More** at hello bottom of hello list of slices.</span></span>
3. <span data-ttu-id="06bf7-315">Ahora, en hello **conjuntos de datos** página, haga clic en **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-315">Now, In hello **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Segmentos OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="06bf7-317">Haga clic en cualquier segmento de datos de lista de Hola y debería ver Hola **el segmento de datos** página.</span><span class="sxs-lookup"><span data-stu-id="06bf7-317">Click any data slice from hello list and you should see hello **Data Slice** page.</span></span> <span data-ttu-id="06bf7-318">Vea la actividad se ejecuta durante el intervalo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-318">You see activity runs for hello slice.</span></span> <span data-ttu-id="06bf7-319">Normalmente solo se ve una ejecución de actividad.</span><span class="sxs-lookup"><span data-stu-id="06bf7-319">You see only one activity run usually.</span></span>  

    ![Hoja Segmento de datos](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="06bf7-321">Si el segmento de hello no está en hello **listo** estado, puede ver segmentos ascendentes de Hola que no están listos y están bloqueando el intervalo actual de Hola de ejecutarse en hello **segmentos ascendentes que no están listos** lista.</span><span class="sxs-lookup"><span data-stu-id="06bf7-321">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="06bf7-322">Haga clic en hello **actividad ejecutar** de lista de hello en hello inferior toosee **detalles de ejecución de la actividad**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-322">Click hello **activity run** from hello list at hello bottom toosee **activity run details**.</span></span>

   ![Página Detalles de ejecución de actividad](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="06bf7-324">Verá información, como el rendimiento, la duración y la puerta de enlace de hello usan datos de hello tootransfer.</span><span class="sxs-lookup"><span data-stu-id="06bf7-324">You would see information such as throughput, duration, and hello gateway used tootransfer hello data.</span></span>
6. <span data-ttu-id="06bf7-325">Haga clic en **X** tooclose todos Hola páginas hasta que</span><span class="sxs-lookup"><span data-stu-id="06bf7-325">Click **X** tooclose all hello pages until you</span></span>
7. <span data-ttu-id="06bf7-326">regresar toohello portada hello **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="06bf7-326">get back toohello home page for hello **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="06bf7-327">(Opcional) Haga clic en **Canalizaciones**, elija **ADFTutorialOnPremDF** y obtenga detalles de los conjuntos de datos de entrada (**Consumido**) o los conjuntos de datos de salida (**Producido**).</span><span class="sxs-lookup"><span data-stu-id="06bf7-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="06bf7-328">Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) tooverify que se crea un archivo de blob para cada hora.</span><span class="sxs-lookup"><span data-stu-id="06bf7-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) tooverify that a blob/file is created for each hour.</span></span>

   ![Explorador de Azure Storage](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="06bf7-330">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="06bf7-330">Next steps</span></span>
* <span data-ttu-id="06bf7-331">Vea [Data Management Gateway](data-factory-data-management-gateway.md) artículo para todos los detalles acerca de hello Data Management Gateway de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bf7-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello Data Management Gateway.</span></span>
* <span data-ttu-id="06bf7-332">Vea [copiar los datos de Blob de Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn acerca de cómo tooa almacén de datos de receptor de almacén de datos de toomove de actividad de copia de toouse desde un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="06bf7-332">See [Copy data from Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn about how toouse Copy Activity toomove data from a source data store tooa sink data store.</span></span>
