---
title: Capturar datos de Event Hubs en Azure Data Lake Store | Microsoft Docs
description: Usar Azure Data Lake Store para capturar datos de Event Hubs
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
ms.openlocfilehash: a9e69576958ae96d22a4eb03d0df429f0b307298
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-store-to-capture-data-from-event-hubs"></a><span data-ttu-id="749f3-103">Usar Azure Data Lake Store para capturar datos de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="749f3-103">Use Azure Data Lake Store to capture data from Event Hubs</span></span>

<span data-ttu-id="749f3-104">Obtenga información sobre cómo usar Azure Data Lake Store para capturar datos recibidos por Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="749f3-104">Learn how to use Azure Data Lake Store to capture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="749f3-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="749f3-105">Prerequisites</span></span>

* <span data-ttu-id="749f3-106">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="749f3-106">**An Azure subscription**.</span></span> <span data-ttu-id="749f3-107">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="749f3-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="749f3-108">**Una cuenta de Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="749f3-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="749f3-109">Para obtener instrucciones sobre cómo crear una, consulte la [introducción a Azure Data Lake Store](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="749f3-109">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="749f3-110">**Un espacio de nombres de Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="749f3-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="749f3-111">Para obtener instrucciones, consulte [Creación de un espacio de nombres de Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="749f3-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="749f3-112">Asegúrese de que la cuenta de Data Lake Store y el espacio de nombres de Event Hubs se encuentran en la misma suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="749f3-112">Make sure the Data Lake Store account and the Event Hubs namespace are in the same Azure subscription.</span></span>


## <a name="assign-permissions-to-event-hubs"></a><span data-ttu-id="749f3-113">Asignar permisos a Event Hubs</span><span class="sxs-lookup"><span data-stu-id="749f3-113">Assign permissions to Event Hubs</span></span>

<span data-ttu-id="749f3-114">En esta sección, creará una carpeta en la cuenta en que quiere capturar los datos de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="749f3-114">In this section, you create a folder within the account where you want to capture the data from Event Hubs.</span></span> <span data-ttu-id="749f3-115">También asignará permisos a Event Hubs para que pueda escribir datos en una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="749f3-115">You also assign permissions to Event Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="749f3-116">Abra la cuenta de Data Lake Store en que quiere capturar los datos de Event Hubs y después haga clic en **Explorador de datos**.</span><span class="sxs-lookup"><span data-stu-id="749f3-116">Open the Data Lake Store account where you want to capture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="749f3-117">![Explorador de datos de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Explorador de datos de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="749f3-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="749f3-118">Haga clic en **Nueva carpeta** y después escriba un nombre para la carpeta en que quiere capturar los datos.</span><span class="sxs-lookup"><span data-stu-id="749f3-118">Click **New Folder** and then enter a name for folder where you want to capture the data.</span></span>

    <span data-ttu-id="749f3-119">![Crear una carpeta en Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Crear una carpeta en Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="749f3-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="749f3-120">Asigne permisos en la raíz de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="749f3-120">Assign permissions at the root of the Data Lake Store.</span></span> 

    <span data-ttu-id="749f3-121">a.</span><span class="sxs-lookup"><span data-stu-id="749f3-121">a.</span></span> <span data-ttu-id="749f3-122">Haga clic en **Explorador de datos**, seleccione la raíz de la cuenta de Data Lake Store y después haga clic en **Acceso**.</span><span class="sxs-lookup"><span data-stu-id="749f3-122">Click **Data Explorer**, select the root of the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="749f3-123">![Asignar permisos a la raíz de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Asignar permisos a la raíz de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="749f3-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="749f3-124">b.</span><span class="sxs-lookup"><span data-stu-id="749f3-124">b.</span></span> <span data-ttu-id="749f3-125">En **Acceso**, haga clic en **Agregar**, en **Seleccionar usuario o grupo** y después busque `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="749f3-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="749f3-126">![Asignar permisos a la raíz de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Asignar permisos a la raíz de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="749f3-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="749f3-127">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="749f3-127">Click **Select**.</span></span>

    <span data-ttu-id="749f3-128">c.</span><span class="sxs-lookup"><span data-stu-id="749f3-128">c.</span></span> <span data-ttu-id="749f3-129">En **Asignar permisos**, haga clic en **Seleccionar permisos**.</span><span class="sxs-lookup"><span data-stu-id="749f3-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="749f3-130">Establezca **Permisos** en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="749f3-130">Set **Permissions** to **Execute**.</span></span> <span data-ttu-id="749f3-131">Establezca **Agregar a** en **Esta carpeta y todos los elementos secundarios**.</span><span class="sxs-lookup"><span data-stu-id="749f3-131">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="749f3-132">Establezca **Agregar como** en **Una entrada de permiso de acceso y una entrada de permiso predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="749f3-132">Set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="749f3-133">![Asignar permisos a la raíz de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Asignar permisos a la raíz de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="749f3-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="749f3-134">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="749f3-134">Click **OK**.</span></span>

4. <span data-ttu-id="749f3-135">Asigne permisos a la carpeta en la cuenta de Data Lake Store en que quiere capturar los datos.</span><span class="sxs-lookup"><span data-stu-id="749f3-135">Assign permissions for the folder under Data Lake Store account where you want to capture data.</span></span>

    <span data-ttu-id="749f3-136">a.</span><span class="sxs-lookup"><span data-stu-id="749f3-136">a.</span></span> <span data-ttu-id="749f3-137">Haga clic en **Explorador de datos**, seleccione la carpeta de la cuenta de Data Lake Store y después haga clic en **Acceso**.</span><span class="sxs-lookup"><span data-stu-id="749f3-137">Click **Data Explorer**, select the folder in the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="749f3-138">![Asignar permisos a la carpeta de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Asignar permisos a la carpeta de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="749f3-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="749f3-139">b.</span><span class="sxs-lookup"><span data-stu-id="749f3-139">b.</span></span> <span data-ttu-id="749f3-140">En **Acceso**, haga clic en **Agregar**, en **Seleccionar usuario o grupo** y después busque `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="749f3-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="749f3-141">![Asignar permisos a la carpeta de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Asignar permisos a la carpeta de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="749f3-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="749f3-142">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="749f3-142">Click **Select**.</span></span>

    <span data-ttu-id="749f3-143">c.</span><span class="sxs-lookup"><span data-stu-id="749f3-143">c.</span></span> <span data-ttu-id="749f3-144">En **Asignar permisos**, haga clic en **Seleccionar permisos**.</span><span class="sxs-lookup"><span data-stu-id="749f3-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="749f3-145">Establezca **Permisos** en **Leer, escribir** y **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="749f3-145">Set **Permissions** to **Read, Write,** and **Execute**.</span></span> <span data-ttu-id="749f3-146">Establezca **Agregar a** en **Esta carpeta y todos los elementos secundarios**.</span><span class="sxs-lookup"><span data-stu-id="749f3-146">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="749f3-147">Por último, establezca **Agregar como** en **Una entrada de permiso de acceso y una entrada de permiso predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="749f3-147">Finally, set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="749f3-148">![Asignar permisos a la carpeta de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Asignar permisos a la carpeta de Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="749f3-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="749f3-149">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="749f3-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-to-capture-data-to-data-lake-store"></a><span data-ttu-id="749f3-150">Configurar Event Hubs para capturar datos en Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="749f3-150">Configure Event Hubs to capture data to Data Lake Store</span></span>

<span data-ttu-id="749f3-151">En esta sección, creará un centro de eventos en un espacio de nombres de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="749f3-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="749f3-152">También configurará el centro de eventos para capturar los datos en una cuenta de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="749f3-152">You also configure the Event Hub to capture data to an Azure Data Lake Store account.</span></span> <span data-ttu-id="749f3-153">En esta sección, se da por supuesto que ya ha creado un espacio de nombres de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="749f3-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="749f3-154">En el panel **Introducción** del espacio de nombres de Event Hubs, haga clic en **+ Centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="749f3-154">From the **Overview** pane of the Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="749f3-155">![Crear centro de eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Crear centro de eventos")</span><span class="sxs-lookup"><span data-stu-id="749f3-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="749f3-156">Proporcione los siguientes valores para configurar Event Hubs para capturar datos en Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="749f3-156">Provide the following values to configure Event Hubs to capture data to Data Lake Store.</span></span>

    <span data-ttu-id="749f3-157">![Crear centro de eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Crear centro de eventos")</span><span class="sxs-lookup"><span data-stu-id="749f3-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="749f3-158">a.</span><span class="sxs-lookup"><span data-stu-id="749f3-158">a.</span></span> <span data-ttu-id="749f3-159">Especifique un nombre para el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="749f3-159">Provide a name for the Event Hub.</span></span>
    
    <span data-ttu-id="749f3-160">b.</span><span class="sxs-lookup"><span data-stu-id="749f3-160">b.</span></span> <span data-ttu-id="749f3-161">Para este tutorial, establezca **Recuento de particiones** y **Retención de mensajes** en los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="749f3-161">For this tutorial, set **Partition Count** and **Message Retention** to the default values.</span></span>
    
    <span data-ttu-id="749f3-162">c.</span><span class="sxs-lookup"><span data-stu-id="749f3-162">c.</span></span> <span data-ttu-id="749f3-163">Establezca **Capture** en **Activado**.</span><span class="sxs-lookup"><span data-stu-id="749f3-163">Set **Capture** to **On**.</span></span> <span data-ttu-id="749f3-164">Establezca la **Ventana de tiempo** (la frecuencia de captura) y **Ajustar tamaño de la ventana** (tamaño de los datos que se capturarán).</span><span class="sxs-lookup"><span data-stu-id="749f3-164">Set the **Time Window** (how frequently to capture) and **Size Window** (data size to capture).</span></span> 
    
    <span data-ttu-id="749f3-165">d.</span><span class="sxs-lookup"><span data-stu-id="749f3-165">d.</span></span> <span data-ttu-id="749f3-166">En **Capture Provider** (Proveedor de Capture), seleccione **Azure Data Lake Store** y después seleccione el Data Lake Store que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="749f3-166">For **Capture Provider**, select **Azure Data Lake Store** and the select the Data Lake Store you created earlier.</span></span> <span data-ttu-id="749f3-167">En **Data Lake Path** (Ruta de acceso de Data Lake), escriba el nombre de la carpeta que ha creado en la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="749f3-167">For **Data Lake Path**, enter the name of the folder you created in the Data Lake Store account.</span></span> <span data-ttu-id="749f3-168">Basta con proporcionar la ruta de acceso relativa a la carpeta.</span><span class="sxs-lookup"><span data-stu-id="749f3-168">You only need to provide the relative path to the folder.</span></span>

    <span data-ttu-id="749f3-169">e.</span><span class="sxs-lookup"><span data-stu-id="749f3-169">e.</span></span> <span data-ttu-id="749f3-170">Deje **Formatos de nombre de archivo de Capture de ejemplo** en el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="749f3-170">Leave the **Sample capture file name formats** to the default value.</span></span> <span data-ttu-id="749f3-171">Esta opción rige la estructura de carpetas que se crea en la carpeta de captura.</span><span class="sxs-lookup"><span data-stu-id="749f3-171">This option governs the folder structure that is created under the capture folder.</span></span>

    <span data-ttu-id="749f3-172">f.</span><span class="sxs-lookup"><span data-stu-id="749f3-172">f.</span></span> <span data-ttu-id="749f3-173">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="749f3-173">Click **Create**.</span></span>

## <a name="test-the-setup"></a><span data-ttu-id="749f3-174">Probar la configuración</span><span class="sxs-lookup"><span data-stu-id="749f3-174">Test the setup</span></span>

<span data-ttu-id="749f3-175">Ahora puede enviar datos a Azure Event Hubs para probar la solución.</span><span class="sxs-lookup"><span data-stu-id="749f3-175">You can now test the solution by sending data to the Azure Event Hub.</span></span> <span data-ttu-id="749f3-176">Siga las instrucciones de [Envío de eventos a Azure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="749f3-176">Follow the instructions at [Send events to Azure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="749f3-177">Cuando empiece a enviar los datos, los verá reflejados en Data Lake Store con la estructura de carpetas que ha especificado.</span><span class="sxs-lookup"><span data-stu-id="749f3-177">Once you start sending the data, you see the data reflected in Data Lake Store using the folder structure you specified.</span></span> <span data-ttu-id="749f3-178">Por ejemplo, verá una estructura de carpetas, tal y como se muestra en la siguiente captura de pantalla, en Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="749f3-178">For example, you see a folder structure, as shown in the following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="749f3-179">![Datos de ejemplo del centro de eventos en Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Datos de ejemplo del centro de eventos en Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="749f3-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="749f3-180">Incluso si no tiene mensajes que lleguen a Event Hubs, este escribe archivos vacíos solo con los encabezados en la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="749f3-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just the headers into the Data Lake Store account.</span></span> <span data-ttu-id="749f3-181">Los archivos se escriben en el mismo intervalo de tiempo que ha proporcionado al crear los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="749f3-181">The files are written at the same time interval that you provided while creating the Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="749f3-182">Análisis de datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="749f3-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="749f3-183">Una vez que los datos están en Data Lake Store, puede ejecutar trabajos analíticos para procesar y estudiar los datos.</span><span class="sxs-lookup"><span data-stu-id="749f3-183">Once the data is in Data Lake Store, you can run analytical jobs to process and crunch the data.</span></span> <span data-ttu-id="749f3-184">Vea [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) (Ejemplo de Avro de USQL) sobre cómo hacer esto con Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="749f3-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how to do this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="749f3-185">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="749f3-185">See also</span></span>
* [<span data-ttu-id="749f3-186">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="749f3-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="749f3-187">Copiar datos de los blobs de almacenamiento de Azure en el Almacén Data Lake</span><span class="sxs-lookup"><span data-stu-id="749f3-187">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
