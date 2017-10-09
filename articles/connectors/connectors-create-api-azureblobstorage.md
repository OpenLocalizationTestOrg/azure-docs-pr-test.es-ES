---
title: "Hola aaaAdd conector en las aplicaciones lógicas de almacenamiento de blobs de Azure | Documentos de Microsoft"
description: "Empezar a trabajar y configurar el conector de almacenamiento de blobs de Azure de hello en una aplicación de lógica"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="03847-103">Usar el conector de almacenamiento de blobs de Azure de hello en una aplicación de lógica</span><span class="sxs-lookup"><span data-stu-id="03847-103">Use hello Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="03847-104">Tooupload de conector de almacenamiento de blobs de Azure de uso hello, actualizar, obtener y eliminar los blobs en la cuenta de almacenamiento, todo dentro de una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="03847-104">Use hello Azure Blob storage connector tooupload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="03847-105">Con Almacenamiento de blobs de Azure:</span><span class="sxs-lookup"><span data-stu-id="03847-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="03847-106">Cree un flujo de trabajo cargando nuevos proyectos u obteniendo archivos recientemente actualizados.</span><span class="sxs-lookup"><span data-stu-id="03847-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="03847-107">Use acciones tooget metadatos de archivo, eliminar un archivo, copia archivos y mucho más.</span><span class="sxs-lookup"><span data-stu-id="03847-107">Use actions tooget file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="03847-108">Por ejemplo, cuando se actualiza una herramienta en un sitio web de Azure (desencadenador), se actualiza un archivo en Blob Storage (acción).</span><span class="sxs-lookup"><span data-stu-id="03847-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="03847-109">Este tema muestra cómo toouse Hola blob conector de almacenamiento en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="03847-109">This topic shows you how toouse hello blob storage connector in a logic app.</span></span>

<span data-ttu-id="03847-110">toolearn más información acerca de las aplicaciones lógicas, consulte [¿cuáles son las aplicaciones lógicas](../logic-apps/logic-apps-what-are-logic-apps.md) y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="03847-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="03847-111">toolearn más información acerca de las aplicaciones lógicas, consulte [¿cuáles son las aplicaciones lógicas](../logic-apps/logic-apps-what-are-logic-apps.md) y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="03847-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-blob-storage"></a><span data-ttu-id="03847-112">Conectar el almacenamiento de blobs de tooAzure</span><span class="sxs-lookup"><span data-stu-id="03847-112">Connect tooAzure blob storage</span></span>
<span data-ttu-id="03847-113">Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero cree un *conexión* toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="03847-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="03847-114">Una conexión proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="03847-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="03847-115">Por ejemplo, cuenta de almacenamiento de tooconnect tooa, crea primero un almacenamiento de blobs *conexión*.</span><span class="sxs-lookup"><span data-stu-id="03847-115">For example, tooconnect tooa storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="03847-116">toocreate una conexión, escriba las credenciales de Hola que suele usar el servicio de hello tooaccess se conecta a.</span><span class="sxs-lookup"><span data-stu-id="03847-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="03847-117">Por lo que con el almacenamiento de Azure, escriba conexión de hello credenciales tooyour almacenamiento cuenta toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="03847-117">So with Azure storage, enter hello credentials tooyour storage account toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="03847-118">Crear conexiones de Hola</span><span class="sxs-lookup"><span data-stu-id="03847-118">Create hello connection</span></span>
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="03847-119">Uso de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="03847-119">Use a trigger</span></span>
<span data-ttu-id="03847-120">Este conector no tiene ningún desencadenador.</span><span class="sxs-lookup"><span data-stu-id="03847-120">This connector does not have any triggers.</span></span> <span data-ttu-id="03847-121">Utilice otra aplicación de lógica de desencadenadores toostart hello, como un desencadenador de periodicidad, un desencadenador de HTTP Webhook, desencadenadores disponibles con otros conectores y mucho más.</span><span class="sxs-lookup"><span data-stu-id="03847-121">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="03847-122">En [Creación de una nueva aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) se puede ver un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="03847-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="03847-123">Uso de una acción</span><span class="sxs-lookup"><span data-stu-id="03847-123">Use an action</span></span>
<span data-ttu-id="03847-124">Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="03847-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span>

1. <span data-ttu-id="03847-125">Seleccione el signo más Hola.</span><span class="sxs-lookup"><span data-stu-id="03847-125">Select hello plus sign.</span></span> <span data-ttu-id="03847-126">Vea elegir entre varias opciones: **agregar una acción**, **agregar una condición**, o uno de hello **más** opciones.</span><span class="sxs-lookup"><span data-stu-id="03847-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="03847-127">Elija **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="03847-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="03847-128">En el cuadro de texto hello, escriba "blob" tooget una lista de todas las acciones disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="03847-128">In hello text box, type “blob” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="03847-129">En nuestro ejemplo, elija **AzureBlob - Obtener metadatos de archivo mediante la ruta de acceso**.</span><span class="sxs-lookup"><span data-stu-id="03847-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="03847-130">Si ya existe una conexión, a continuación, seleccione hello **...** (Mostrar selector) botón tooselect un archivo.</span><span class="sxs-lookup"><span data-stu-id="03847-130">If a connection already exists, then select hello **...** (Show Picker) button tooselect a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="03847-131">Si se le solicitará información de conexión de hello, a continuación, escriba la conexión de hello detalles toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="03847-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="03847-132">[Crear conexiones de hello](connectors-create-api-azureblobstorage.md#create-the-connection) en este tema se describen estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="03847-132">[Create hello connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="03847-133">En este ejemplo, obtenemos Hola metadatos de un archivo.</span><span class="sxs-lookup"><span data-stu-id="03847-133">In this example, we get hello metadata of a file.</span></span> <span data-ttu-id="03847-134">toosee Hola metadatos, agregue otra acción que crea un archivo nuevo con otro conector.</span><span class="sxs-lookup"><span data-stu-id="03847-134">toosee hello metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="03847-135">Por ejemplo, agregar una acción de OneDrive que crea un nuevo archivo "test" basándose en los metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="03847-135">For example, add a OneDrive action that creates a new "test" file based on hello metadata.</span></span> 


5. <span data-ttu-id="03847-136">**Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello).</span><span class="sxs-lookup"><span data-stu-id="03847-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="03847-137">La aplicación lógica se guarda y se puede habilitar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="03847-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="03847-138">[Explorador de almacenamiento](http://storageexplorer.com/) es una herramienta excelente demasiado administrar varias cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="03847-138">[Storage Explorer](http://storageexplorer.com/) is a great tool too manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="03847-139">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="03847-139">Connector-specific details</span></span>

<span data-ttu-id="03847-140">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="03847-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="03847-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03847-141">Next steps</span></span>
<span data-ttu-id="03847-142">[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="03847-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="03847-143">Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="03847-143">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

