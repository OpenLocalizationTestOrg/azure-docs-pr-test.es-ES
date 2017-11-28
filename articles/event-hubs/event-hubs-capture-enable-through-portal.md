---
title: "Habilitar aaaAzure captura de los centros de eventos a través del portal | Documentos de Microsoft"
description: "Habilitar característica de captura de los centros de eventos de hello mediante Hola portal de Azure."
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
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a><span data-ttu-id="ea8ef-103">Habilitar la captura de los centros de eventos mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ea8ef-103">Enable Event Hubs Capture using hello Azure portal</span></span>

<span data-ttu-id="ea8ef-104">Puede configurar la captura en tiempo de creación de base de datos central Hola eventos con hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea8ef-104">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ea8ef-105">Puede cualquier tooan de datos de captura hello Azure [almacenamiento de blobs](https://azure.microsoft.com/services/storage/blobs/) contenedor o tooan [almacén de Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) cuenta.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-105">You can either capture hello data tooan Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-tooan-azure-storage-account"></a><span data-ttu-id="ea8ef-106">Cuenta de almacenamiento de Azure de datos tooan de captura</span><span class="sxs-lookup"><span data-stu-id="ea8ef-106">Capture data tooan Azure Storage account</span></span>  

<span data-ttu-id="ea8ef-107">Cuando se crea un centro de eventos, puede habilitar la captura, haga clic en hello **en** botón en hello **crear centro de eventos** portal hoja.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-107">When you create an event hub, you can enable Capture by clicking hello **On** button in hello **Create Event Hub** portal blade.</span></span> <span data-ttu-id="ea8ef-108">A continuación, especifique una cuenta de almacenamiento y el contenedor, haga clic en **el almacenamiento de Azure** en hello **proveedor capturar** cuadro.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-108">You then specify a Storage Account and container by clicking **Azure Storage** in hello **Capture Provider** box.</span></span> <span data-ttu-id="ea8ef-109">Como capturar de concentradores de eventos utiliza la autenticación de servicio al servicio con el almacenamiento, no es necesario toospecify una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need toospecify a storage connection string.</span></span> <span data-ttu-id="ea8ef-110">Selector de recursos de Hello seleccionará automáticamente el recurso de hello URI para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-110">hello resource picker selects hello resource URI for your storage account automatically.</span></span> <span data-ttu-id="ea8ef-111">Si se usa Azure Resource Manager, es preciso suministrar explícitamente dicho identificador URI como una cadena.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="ea8ef-112">período de tiempo de saludo predeterminado es 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-112">hello default time window is 5 minutes.</span></span> <span data-ttu-id="ea8ef-113">valor mínimo de Hello es 1, Hola máximo 15.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-113">hello minimum value is 1, hello maximum 15.</span></span> <span data-ttu-id="ea8ef-114">Hola **tamaño** ventana tiene un intervalo de 10-500 MB.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-114">hello **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a><span data-ttu-id="ea8ef-115">Cuenta de almacén de Azure Data Lake tooan de datos de captura</span><span class="sxs-lookup"><span data-stu-id="ea8ef-115">Capture data tooan Azure Data Lake Store account</span></span>

<span data-ttu-id="ea8ef-116">toocapture datos tooAzure almacén de Data Lake, cree una cuenta de almacén de Data Lake y un concentrador de eventos:</span><span class="sxs-lookup"><span data-stu-id="ea8ef-116">toocapture data tooAzure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="ea8ef-117">Creación de una cuenta de Azure Data Lake Store y de carpetas</span><span class="sxs-lookup"><span data-stu-id="ea8ef-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="ea8ef-118">Crear una cuenta de almacén de Data Lake, siga las instrucciones de hello en [empezar a trabajar con el almacén de Data Lake de Azure mediante el portal de Azure de hello](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ea8ef-118">Create a Data Lake Store account, following hello instructions in [Get started with Azure Data Lake Store using hello Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="ea8ef-119">Cree una carpeta en esta cuenta, siga las instrucciones de Hola Hola [crear carpetas en la cuenta de almacén de Azure Data Lake](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) sección.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-119">Create a folder under this account, following hello instructions in hello [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="ea8ef-120">En la hoja de la cuenta de almacén de Data Lake de hello, haga clic en **Explorador de datos**.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-120">In hello Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="ea8ef-121">Haga clic en **Acceder**.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-121">Click **Access**.</span></span>
5. <span data-ttu-id="ea8ef-122">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-122">Click **Add**.</span></span>
6. <span data-ttu-id="ea8ef-123">Hola **buscar por nombre o correo electrónico** cuadro, escriba **Microsoft.EventHubs** y, a continuación, seleccione esta opción.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-123">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="ea8ef-124">Hola **permisos** ficha aparece.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-124">hello **Permissions** tab appears.</span></span> <span data-ttu-id="ea8ef-125">Establecer permisos de hello tal y como se muestra en hello figura siguiente:</span><span class="sxs-lookup"><span data-stu-id="ea8ef-125">Set hello permissions as shown in hello following figure:</span></span>

    ![][6]

8. <span data-ttu-id="ea8ef-126">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-126">Click **OK**.</span></span>
9. <span data-ttu-id="ea8ef-127">Ahora, cree una carpeta en la carpeta raíz de hello examinando toohello la carpeta de destino y haga clic en el nombre de la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-127">Now, create a folder in hello root folder by browsing toohello target folder and clicking on hello folder name.</span></span>
10. <span data-ttu-id="ea8ef-128">Haga clic en **Acceder**.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-128">Click **Access**.</span></span>
11. <span data-ttu-id="ea8ef-129">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-129">Click **Add**.</span></span>
12. <span data-ttu-id="ea8ef-130">Hola **buscar por nombre o correo electrónico** cuadro, escriba **Microsoft.EventHubs** y, a continuación, seleccione esta opción.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-130">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="ea8ef-131">Hola **permisos** ficha aparece de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-131">hello **Permissions** tab appears again.</span></span> <span data-ttu-id="ea8ef-132">Establecer permisos de hello tal y como se muestra en hello figura siguiente:</span><span class="sxs-lookup"><span data-stu-id="ea8ef-132">Set hello permissions as shown in hello following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="ea8ef-133">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="ea8ef-133">Create an event hub</span></span>

1. <span data-ttu-id="ea8ef-134">Tenga en cuenta debe ser ese centro de eventos de Hola Hola misma suscripción de Azure como Hola almacén de Data Lake de Azure que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-134">Note that hello event hub must be in hello same Azure subscription as hello Azure Data Lake Store you just created.</span></span> <span data-ttu-id="ea8ef-135">Centro de eventos de Hola de crear, haga clic en hello **en** situado bajo **capturar** en hello **crear centro de eventos** portal hoja.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-135">Create hello event hub, clicking hello **On** button under **Capture** in hello **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="ea8ef-136">Hola **crear centro de eventos** portal hoja, seleccione **almacén de Azure Data Lake** de hello **proveedor capturar** cuadro.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-136">In hello **Create Event Hub** portal blade, select **Azure Data Lake Store** from hello **Capture Provider** box.</span></span>
3. <span data-ttu-id="ea8ef-137">En **seleccione almacén de Data Lake**, especifique la cuenta de almacén de Data Lake que creó anteriormente y Hola Hola **ruta de acceso de datos Lake** , escriba la carpeta de datos de toohello Hola ruta de acceso que ha creado.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-137">In **Select Data Lake Store**, specify hello Data Lake Store account you created previously, and in hello **Data Lake Path** field, enter hello path toohello data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="ea8ef-138">Adición o configuración de Capture en un centro de eventos existente</span><span class="sxs-lookup"><span data-stu-id="ea8ef-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="ea8ef-139">Se puede configurar Capture en los centros de eventos existentes que se encuentran en los espacios de nombres de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="ea8ef-140">tooenable capturar en un centro de eventos existente, o toochange la configuración de captura, haga clic en Hola Hola de tooload de espacio de nombres **Essentials** blade, a continuación, haga clic en Centro de eventos de hello para el que desea tooenable o cambiar la configuración de captura de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-140">tooenable Capture on an existing event hub, or toochange your Capture settings, click hello namespace tooload hello **Essentials** blade, then click hello event hub for which you want tooenable or change hello Capture setting.</span></span> <span data-ttu-id="ea8ef-141">Por último, haga clic en hello **propiedades** sección de hello Abrir hoja y, a continuación, editar la configuración de captura de hello, como se muestra en hello siguientes ilustraciones:</span><span class="sxs-lookup"><span data-stu-id="ea8ef-141">Finally, click hello **Properties** section of hello open blade and then edit hello Capture settings, as shown in hello following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="ea8ef-142">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="ea8ef-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="ea8ef-143">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ea8ef-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="ea8ef-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea8ef-144">Next steps</span></span>

<span data-ttu-id="ea8ef-145">La Event Hubs Capture también se puede configurar a través de las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea8ef-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="ea8ef-146">Para más información, consulte [Habilitar Capture mediante la plantilla de Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="ea8ef-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
