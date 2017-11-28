---
title: "aaaCapture datos desde los centros de eventos en el almacén de Azure Data Lake | Documentos de Microsoft"
description: "Datos de toocapture de almacén de Azure Data Lake de uso de los centros de eventos"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a><span data-ttu-id="d4cec-103">Datos de toocapture de almacén de Azure Data Lake de uso de los centros de eventos</span><span class="sxs-lookup"><span data-stu-id="d4cec-103">Use Azure Data Lake Store toocapture data from Event Hubs</span></span>

<span data-ttu-id="d4cec-104">Obtenga información acerca de cómo toouse datos de almacén de Azure Data Lake toocapture recibido por centros de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4cec-104">Learn how toouse Azure Data Lake Store toocapture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4cec-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d4cec-105">Prerequisites</span></span>

* <span data-ttu-id="d4cec-106">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-106">**An Azure subscription**.</span></span> <span data-ttu-id="d4cec-107">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4cec-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="d4cec-108">**Una cuenta de Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="d4cec-109">Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d4cec-109">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="d4cec-110">**Un espacio de nombres de Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="d4cec-111">Para obtener instrucciones, consulte [Creación de un espacio de nombres de Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="d4cec-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="d4cec-112">Asegurarse de que cuenta de almacén de Data Lake hello y espacio de nombres de los centros de eventos de Hola Hola misma suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4cec-112">Make sure hello Data Lake Store account and hello Event Hubs namespace are in hello same Azure subscription.</span></span>


## <a name="assign-permissions-tooevent-hubs"></a><span data-ttu-id="d4cec-113">Asignar permisos de los centros de tooEvent</span><span class="sxs-lookup"><span data-stu-id="d4cec-113">Assign permissions tooEvent Hubs</span></span>

<span data-ttu-id="d4cec-114">En esta sección, creará una carpeta dentro de la cuenta de hello donde desea toocapture Hola datos desde los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="d4cec-114">In this section, you create a folder within hello account where you want toocapture hello data from Event Hubs.</span></span> <span data-ttu-id="d4cec-115">También asigna permisos tooEvent concentradores para que pueden escribir datos en una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d4cec-115">You also assign permissions tooEvent Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="d4cec-116">Abrir cuenta de almacén de Data Lake Hola donde desea que los datos de toocapture los centros de eventos y, a continuación, haga clic en **Explorador de datos**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-116">Open hello Data Lake Store account where you want toocapture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="d4cec-117">![Explorador de datos de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Explorador de datos de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d4cec-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="d4cec-118">Haga clic en **nueva carpeta** y, a continuación, escriba un nombre para la carpeta donde desea que los datos de hello toocapture.</span><span class="sxs-lookup"><span data-stu-id="d4cec-118">Click **New Folder** and then enter a name for folder where you want toocapture hello data.</span></span>

    <span data-ttu-id="d4cec-119">![Crear una carpeta en Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Crear una carpeta en Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d4cec-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="d4cec-120">Asignar permisos en la raíz de Hola de hello almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d4cec-120">Assign permissions at hello root of hello Data Lake Store.</span></span> 

    <span data-ttu-id="d4cec-121">a.</span><span class="sxs-lookup"><span data-stu-id="d4cec-121">a.</span></span> <span data-ttu-id="d4cec-122">Haga clic en **Explorador de datos**, seleccione raíz Hola Hola cuenta de almacén de Data Lake y, a continuación, haga clic en **acceso**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-122">Click **Data Explorer**, select hello root of hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="d4cec-123">![Asignar permisos a la raíz de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Asignar permisos a la raíz de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d4cec-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="d4cec-124">b.</span><span class="sxs-lookup"><span data-stu-id="d4cec-124">b.</span></span> <span data-ttu-id="d4cec-125">En **Acceso**, haga clic en **Agregar**, en **Seleccionar usuario o grupo** y después busque `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="d4cec-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="d4cec-126">![Asignar permisos a la raíz de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Asignar permisos a la raíz de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d4cec-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="d4cec-127">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-127">Click **Select**.</span></span>

    <span data-ttu-id="d4cec-128">c.</span><span class="sxs-lookup"><span data-stu-id="d4cec-128">c.</span></span> <span data-ttu-id="d4cec-129">En **Asignar permisos**, haga clic en **Seleccionar permisos**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="d4cec-130">Establecer **permisos** demasiado**Execute**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-130">Set **Permissions** too**Execute**.</span></span> <span data-ttu-id="d4cec-131">Establecer **agregar a** demasiado**esta carpeta y todos los elementos secundarios**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-131">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="d4cec-132">Establecer **agregar como** demasiado**una entrada de permiso de acceso y una entrada de permiso predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-132">Set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="d4cec-133">![Asignar permisos a la raíz de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Asignar permisos a la raíz de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d4cec-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="d4cec-134">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-134">Click **OK**.</span></span>

4. <span data-ttu-id="d4cec-135">Asignar permisos para las carpetas de hello en la cuenta de almacén de Data Lake donde desea toocapture datos.</span><span class="sxs-lookup"><span data-stu-id="d4cec-135">Assign permissions for hello folder under Data Lake Store account where you want toocapture data.</span></span>

    <span data-ttu-id="d4cec-136">a.</span><span class="sxs-lookup"><span data-stu-id="d4cec-136">a.</span></span> <span data-ttu-id="d4cec-137">Haga clic en **Explorador de datos**, seleccione la carpeta de Hola Hola cuenta de almacén de Data Lake y, a continuación, haga clic en **acceso**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-137">Click **Data Explorer**, select hello folder in hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="d4cec-138">![Asignar permisos a la carpeta de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Asignar permisos a la carpeta de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d4cec-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="d4cec-139">b.</span><span class="sxs-lookup"><span data-stu-id="d4cec-139">b.</span></span> <span data-ttu-id="d4cec-140">En **Acceso**, haga clic en **Agregar**, en **Seleccionar usuario o grupo** y después busque `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="d4cec-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="d4cec-141">![Asignar permisos a la carpeta de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Asignar permisos a la carpeta de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d4cec-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="d4cec-142">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-142">Click **Select**.</span></span>

    <span data-ttu-id="d4cec-143">c.</span><span class="sxs-lookup"><span data-stu-id="d4cec-143">c.</span></span> <span data-ttu-id="d4cec-144">En **Asignar permisos**, haga clic en **Seleccionar permisos**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="d4cec-145">Establecer **permisos** demasiado**lectura, escritura,** y **Execute**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-145">Set **Permissions** too**Read, Write,** and **Execute**.</span></span> <span data-ttu-id="d4cec-146">Establecer **agregar a** demasiado**esta carpeta y todos los elementos secundarios**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-146">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="d4cec-147">Por último, establezca **agregar como** demasiado**una entrada de permiso de acceso y una entrada de permiso predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-147">Finally, set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="d4cec-148">![Asignar permisos a la carpeta de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Asignar permisos a la carpeta de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d4cec-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="d4cec-149">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a><span data-ttu-id="d4cec-150">Configurar almacén de los centros de eventos toocapture data tooData Lake</span><span class="sxs-lookup"><span data-stu-id="d4cec-150">Configure Event Hubs toocapture data tooData Lake Store</span></span>

<span data-ttu-id="d4cec-151">En esta sección, creará un centro de eventos en un espacio de nombres de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d4cec-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="d4cec-152">También configurará Hola concentrador de eventos toocapture datos tooan cuenta de almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d4cec-152">You also configure hello Event Hub toocapture data tooan Azure Data Lake Store account.</span></span> <span data-ttu-id="d4cec-153">En esta sección, se da por supuesto que ya ha creado un espacio de nombres de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d4cec-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="d4cec-154">De hello **Introducción** de espacio de nombres de los centros de eventos de hello, haga clic en **+ concentrador de eventos**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-154">From hello **Overview** pane of hello Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="d4cec-155">![Crear centro de eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Crear centro de eventos")</span><span class="sxs-lookup"><span data-stu-id="d4cec-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="d4cec-156">Proporcione la siguiente Hola valores tooconfigure centros de eventos toocapture datos tooData Lake almacén.</span><span class="sxs-lookup"><span data-stu-id="d4cec-156">Provide hello following values tooconfigure Event Hubs toocapture data tooData Lake Store.</span></span>

    <span data-ttu-id="d4cec-157">![Crear centro de eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Crear centro de eventos")</span><span class="sxs-lookup"><span data-stu-id="d4cec-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="d4cec-158">a.</span><span class="sxs-lookup"><span data-stu-id="d4cec-158">a.</span></span> <span data-ttu-id="d4cec-159">Proporcione un nombre para hello concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="d4cec-159">Provide a name for hello Event Hub.</span></span>
    
    <span data-ttu-id="d4cec-160">b.</span><span class="sxs-lookup"><span data-stu-id="d4cec-160">b.</span></span> <span data-ttu-id="d4cec-161">Para este tutorial, establezca **recuento de particiones** y **retención de mensajes** valores predeterminados de toohello.</span><span class="sxs-lookup"><span data-stu-id="d4cec-161">For this tutorial, set **Partition Count** and **Message Retention** toohello default values.</span></span>
    
    <span data-ttu-id="d4cec-162">c.</span><span class="sxs-lookup"><span data-stu-id="d4cec-162">c.</span></span> <span data-ttu-id="d4cec-163">Establecer **capturar** demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-163">Set **Capture** too**On**.</span></span> <span data-ttu-id="d4cec-164">Conjunto hello **período de tiempo** (con qué frecuencia toocapture) y **ventana de tamaño** (toocapture de tamaño de datos).</span><span class="sxs-lookup"><span data-stu-id="d4cec-164">Set hello **Time Window** (how frequently toocapture) and **Size Window** (data size toocapture).</span></span> 
    
    <span data-ttu-id="d4cec-165">d.</span><span class="sxs-lookup"><span data-stu-id="d4cec-165">d.</span></span> <span data-ttu-id="d4cec-166">Para **proveedor capturar**, seleccione **almacén de Azure Data Lake** y seleccione Hola Hola almacén de Data Lake que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d4cec-166">For **Capture Provider**, select **Azure Data Lake Store** and hello select hello Data Lake Store you created earlier.</span></span> <span data-ttu-id="d4cec-167">Para **ruta de acceso de datos Lake**, escriba el nombre de Hola de carpeta de Hola que creó en hello cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d4cec-167">For **Data Lake Path**, enter hello name of hello folder you created in hello Data Lake Store account.</span></span> <span data-ttu-id="d4cec-168">Solo se necesita carpeta de toohello de tooprovide Hola ruta de acceso relativa.</span><span class="sxs-lookup"><span data-stu-id="d4cec-168">You only need tooprovide hello relative path toohello folder.</span></span>

    <span data-ttu-id="d4cec-169">e.</span><span class="sxs-lookup"><span data-stu-id="d4cec-169">e.</span></span> <span data-ttu-id="d4cec-170">Deje hello **formatos de nombre de archivo de ejemplo captura** valor predeterminado de toohello.</span><span class="sxs-lookup"><span data-stu-id="d4cec-170">Leave hello **Sample capture file name formats** toohello default value.</span></span> <span data-ttu-id="d4cec-171">Esta opción rige la estructura de carpetas de Hola que se crea en la carpeta de captura de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4cec-171">This option governs hello folder structure that is created under hello capture folder.</span></span>

    <span data-ttu-id="d4cec-172">f.</span><span class="sxs-lookup"><span data-stu-id="d4cec-172">f.</span></span> <span data-ttu-id="d4cec-173">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d4cec-173">Click **Create**.</span></span>

## <a name="test-hello-setup"></a><span data-ttu-id="d4cec-174">Programa de instalación de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="d4cec-174">Test hello setup</span></span>

<span data-ttu-id="d4cec-175">Ahora puede probar la solución de hello enviando datos toohello concentrador de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4cec-175">You can now test hello solution by sending data toohello Azure Event Hub.</span></span> <span data-ttu-id="d4cec-176">Siga las instrucciones de hello en [enviar eventos centros de eventos de tooAzure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="d4cec-176">Follow hello instructions at [Send events tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="d4cec-177">Una vez que empezar a enviar datos de hello, verá datos Hola reflejados en el almacén de Data Lake con la estructura de carpetas de Hola que especificó.</span><span class="sxs-lookup"><span data-stu-id="d4cec-177">Once you start sending hello data, you see hello data reflected in Data Lake Store using hello folder structure you specified.</span></span> <span data-ttu-id="d4cec-178">Por ejemplo, verá una estructura de carpetas tal y como se muestra en la siguiente captura de pantalla, en el almacén de Data Lake de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4cec-178">For example, you see a folder structure, as shown in hello following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="d4cec-179">![Datos de ejemplo del centro de eventos en Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Datos de ejemplo del centro de eventos en Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d4cec-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="d4cec-180">Incluso si no tiene mensajes que entran en los centros de eventos, los concentradores de eventos escribe archivos vacíos con solo a los encabezados hello en hello cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d4cec-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just hello headers into hello Data Lake Store account.</span></span> <span data-ttu-id="d4cec-181">Hello archivos se escriben en hello mismo intervalo de tiempo que haya especificado durante la creación de centros de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4cec-181">hello files are written at hello same time interval that you provided while creating hello Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="d4cec-182">Análisis de datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="d4cec-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="d4cec-183">Una vez en el almacén de Data Lake datos hello, puede ejecutar trabajos analíticos tooprocess y delicadas datos Hola.</span><span class="sxs-lookup"><span data-stu-id="d4cec-183">Once hello data is in Data Lake Store, you can run analytical jobs tooprocess and crunch hello data.</span></span> <span data-ttu-id="d4cec-184">Vea [USQL Avro ejemplo](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) acerca de cómo toodo este mediante el análisis de Data Lake de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4cec-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how toodo this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="d4cec-185">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d4cec-185">See also</span></span>
* [<span data-ttu-id="d4cec-186">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="d4cec-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="d4cec-187">Copiar los datos de almacén de Blobs de Azure almacenamiento Lake tooData</span><span class="sxs-lookup"><span data-stu-id="d4cec-187">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
