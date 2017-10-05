---
title: "Azure Event Hubs Capture se habilita a través del portal | Microsoft Docs"
description: Habilite la funcionalidad de captura de Event Hubs mediante Azure Portal.
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a><span data-ttu-id="50446-103">Habilitación de la funcionalidad de captura de Event Hubs mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="50446-103">Enable Event Hubs Capture using the Azure portal</span></span>

<span data-ttu-id="50446-104">Puede configurar la funcionalidad de captura en el momento de creación del centro de eventos mediante [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="50446-104">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="50446-105">O bien puede capturar los datos de un contenedor de Azure [Blob Storage](https://azure.microsoft.com/services/storage/blobs/) o de una cuenta de [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="50446-105">You can either capture the data to an Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or to an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-to-an-azure-storage-account"></a><span data-ttu-id="50446-106">Captura de datos en una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="50446-106">Capture data to an Azure Storage account</span></span>  

<span data-ttu-id="50446-107">Cuando se crea un centro de eventos, puede habilitar la captura, haga clic en el **en** botón en el **crear centro de eventos** portal hoja.</span><span class="sxs-lookup"><span data-stu-id="50446-107">When you create an event hub, you can enable Capture by clicking the **On** button in the **Create Event Hub** portal blade.</span></span> <span data-ttu-id="50446-108">Después, para especificar una cuenta de almacenamiento y un contenedor, haga clic en **Azure Storage** en el cuadro **Capture Provider** (Proveedor de Capture).</span><span class="sxs-lookup"><span data-stu-id="50446-108">You then specify a Storage Account and container by clicking **Azure Storage** in the **Capture Provider** box.</span></span> <span data-ttu-id="50446-109">Dado que la captura de Event Hubs utiliza la autenticación de servicio a servicio con el almacenamiento, no es necesario especificar una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="50446-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need to specify a storage connection string.</span></span> <span data-ttu-id="50446-110">El selector de recursos selecciona automáticamente el identificador URI del recurso para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="50446-110">The resource picker selects the resource URI for your storage account automatically.</span></span> <span data-ttu-id="50446-111">Si se usa Azure Resource Manager, es preciso suministrar explícitamente dicho identificador URI como una cadena.</span><span class="sxs-lookup"><span data-stu-id="50446-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="50446-112">La ventana de tiempo predeterminada es cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="50446-112">The default time window is 5 minutes.</span></span> <span data-ttu-id="50446-113">El valor mínimo es 1 y el máximo 15.</span><span class="sxs-lookup"><span data-stu-id="50446-113">The minimum value is 1, the maximum 15.</span></span> <span data-ttu-id="50446-114">La ventana **Tamaño** tiene un intervalo de 10-500 MB.</span><span class="sxs-lookup"><span data-stu-id="50446-114">The **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a><span data-ttu-id="50446-115">Captura de datos en una cuenta de Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="50446-115">Capture data to an Azure Data Lake Store account</span></span>

<span data-ttu-id="50446-116">Para capturar datos en Azure Data Lake Store, cree una cuenta de Data Lake Store y un centro de eventos:</span><span class="sxs-lookup"><span data-stu-id="50446-116">To capture data to Azure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="50446-117">Creación de una cuenta de Azure Data Lake Store y de carpetas</span><span class="sxs-lookup"><span data-stu-id="50446-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="50446-118">Cree una cuenta de Data Lake Store siguiendo las instrucciones que se describen en [Introducción al uso de Azure Portal por parte de Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="50446-118">Create a Data Lake Store account, following the instructions in [Get started with Azure Data Lake Store using the Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="50446-119">Cree una carpeta en esta cuenta, siguiendo las instrucciones de la sección [Creación de carpetas en una cuenta de Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).</span><span class="sxs-lookup"><span data-stu-id="50446-119">Create a folder under this account, following the instructions in the [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="50446-120">En la hoja de la cuenta de almacén de Data Lake, haga clic en **Explorador de datos**.</span><span class="sxs-lookup"><span data-stu-id="50446-120">In the Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="50446-121">Haga clic en **Acceder**.</span><span class="sxs-lookup"><span data-stu-id="50446-121">Click **Access**.</span></span>
5. <span data-ttu-id="50446-122">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="50446-122">Click **Add**.</span></span>
6. <span data-ttu-id="50446-123">En el tipo de cuadro **Busque por nombre o correo electrónico**, escriba **Microsoft.EventHubs** y, después, seleccione esta opción.</span><span class="sxs-lookup"><span data-stu-id="50446-123">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="50446-124">Se muestra la pestaña **Permisos**.</span><span class="sxs-lookup"><span data-stu-id="50446-124">The **Permissions** tab appears.</span></span> <span data-ttu-id="50446-125">Establezca los permisos tal como se muestra en la ilustración siguiente:</span><span class="sxs-lookup"><span data-stu-id="50446-125">Set the permissions as shown in the following figure:</span></span>

    ![][6]

8. <span data-ttu-id="50446-126">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="50446-126">Click **OK**.</span></span>
9. <span data-ttu-id="50446-127">Ahora, cree una carpeta en la carpeta raíz buscando la carpeta de destino y haciendo clic en el nombre de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="50446-127">Now, create a folder in the root folder by browsing to the target folder and clicking on the folder name.</span></span>
10. <span data-ttu-id="50446-128">Haga clic en **Acceder**.</span><span class="sxs-lookup"><span data-stu-id="50446-128">Click **Access**.</span></span>
11. <span data-ttu-id="50446-129">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="50446-129">Click **Add**.</span></span>
12. <span data-ttu-id="50446-130">En el tipo de cuadro **Busque por nombre o correo electrónico**, escriba **Microsoft.EventHubs** y, después, seleccione esta opción.</span><span class="sxs-lookup"><span data-stu-id="50446-130">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="50446-131">Se vuelve a mostrar la pestaña **Permisos**.</span><span class="sxs-lookup"><span data-stu-id="50446-131">The **Permissions** tab appears again.</span></span> <span data-ttu-id="50446-132">Establezca los permisos tal como se muestra en la ilustración siguiente:</span><span class="sxs-lookup"><span data-stu-id="50446-132">Set the permissions as shown in the following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="50446-133">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="50446-133">Create an event hub</span></span>

1. <span data-ttu-id="50446-134">Tenga en cuenta que el centro de eventos debe estar en la misma suscripción de Azure que la instancia de Azure Data Lake Store que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="50446-134">Note that the event hub must be in the same Azure subscription as the Azure Data Lake Store you just created.</span></span> <span data-ttu-id="50446-135">Crear el concentrador de eventos, haga clic en el **en** situado bajo **capturar** en el **crear centro de eventos** portal hoja.</span><span class="sxs-lookup"><span data-stu-id="50446-135">Create the event hub, clicking the **On** button under **Capture** in the **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="50446-136">En el **crear centro de eventos** portal hoja, seleccione **almacén de Azure Data Lake** desde el **proveedor capturar** cuadro.</span><span class="sxs-lookup"><span data-stu-id="50446-136">In the **Create Event Hub** portal blade, select **Azure Data Lake Store** from the **Capture Provider** box.</span></span>
3. <span data-ttu-id="50446-137">En **Seleccione Data Lake Store**, especifique la cuenta de Data Lake Store que creó anteriormente y en **Data Lake Path** (Ruta de acceso de Data Lake), escriba la ruta de acceso a la carpeta de datos que ha creado.</span><span class="sxs-lookup"><span data-stu-id="50446-137">In **Select Data Lake Store**, specify the Data Lake Store account you created previously, and in the **Data Lake Path** field, enter the path to the data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="50446-138">Adición o configuración de Capture en un centro de eventos existente</span><span class="sxs-lookup"><span data-stu-id="50446-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="50446-139">Se puede configurar Capture en los centros de eventos existentes que se encuentran en los espacios de nombres de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="50446-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="50446-140">Para habilitar Capture en un centro de eventos existente o para cambiar la configuración Capture, haga clic en el espacio de nombres para cargar la hoja **Essentials** y, después, haga clic en el centro de eventos para el que desea habilitar o cambiar la configuración de Capture.</span><span class="sxs-lookup"><span data-stu-id="50446-140">To enable Capture on an existing event hub, or to change your Capture settings, click the namespace to load the **Essentials** blade, then click the event hub for which you want to enable or change the Capture setting.</span></span> <span data-ttu-id="50446-141">Por último, haga clic en el **propiedades** sección de la hoja abierta y, a continuación, edite la configuración de captura, como se muestra en las ilustraciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="50446-141">Finally, click the **Properties** section of the open blade and then edit the Capture settings, as shown in the following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="50446-142">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="50446-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="50446-143">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="50446-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="50446-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="50446-144">Next steps</span></span>

<span data-ttu-id="50446-145">La Event Hubs Capture también se puede configurar a través de las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="50446-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="50446-146">Para más información, consulte [Habilitar Capture mediante la plantilla de Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="50446-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
