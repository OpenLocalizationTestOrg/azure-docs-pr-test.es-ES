---
title: "Incorporación del conector de Azure Blob Storage en Logic Apps | Microsoft Docs"
description: "Muestra cómo empezar a trabajar y configurar el conector de Azure Blob Storage en una aplicación lógica"
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
ms.openlocfilehash: bc7908868828bd1628633cf9e57f8c44f8000827
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="84304-103">Uso del conector de Azure Blob Storage en una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="84304-103">Use the Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="84304-104">Use el conector de Azure Blob Storage para cargar, actualizar, obtener y eliminar blobs en la cuenta de almacenamiento, todo dentro de una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="84304-104">Use the Azure Blob storage connector to upload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="84304-105">Con Almacenamiento de blobs de Azure:</span><span class="sxs-lookup"><span data-stu-id="84304-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="84304-106">Cree un flujo de trabajo cargando nuevos proyectos u obteniendo archivos recientemente actualizados.</span><span class="sxs-lookup"><span data-stu-id="84304-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="84304-107">Use acciones para obtener metadatos de archivos, eliminar un archivo, copiar archivos y muchas otras cosas.</span><span class="sxs-lookup"><span data-stu-id="84304-107">Use actions to get file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="84304-108">Por ejemplo, cuando se actualiza una herramienta en un sitio web de Azure (desencadenador), se actualiza un archivo en Blob Storage (acción).</span><span class="sxs-lookup"><span data-stu-id="84304-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="84304-109">En este tema se muestra cómo usar el conector de Azure Blob Storage en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="84304-109">This topic shows you how to use the blob storage connector in a logic app.</span></span>

<span data-ttu-id="84304-110">Para más información sobre Logic Apps, consulte [¿Qué son las aplicaciones lógicas?](../logic-apps/logic-apps-what-are-logic-apps.md) y [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="84304-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="84304-111">Para más información sobre Logic Apps, consulte [¿Qué son las aplicaciones lógicas?](../logic-apps/logic-apps-what-are-logic-apps.md) y [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="84304-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-blob-storage"></a><span data-ttu-id="84304-112">Conexión con el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="84304-112">Connect to Azure blob storage</span></span>
<span data-ttu-id="84304-113">Antes de que la aplicación lógica pueda acceder a cualquier servicio, cree primero una *conexión* a este.</span><span class="sxs-lookup"><span data-stu-id="84304-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="84304-114">Una conexión proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="84304-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="84304-115">Por ejemplo, para conectarse a una cuenta de almacenamiento, debe crear primero una *conexión* con Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="84304-115">For example, to connect to a storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="84304-116">Para crear una conexión, escriba las credenciales que utiliza normalmente para acceder al servicio al que se está conectando.</span><span class="sxs-lookup"><span data-stu-id="84304-116">To create a connection, enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="84304-117">En el caso de Almacenamiento de Azure, para crear la conexión, deberá escribir las credenciales de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="84304-117">So with Azure storage, enter the credentials to your storage account to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="84304-118">Creación de la conexión</span><span class="sxs-lookup"><span data-stu-id="84304-118">Create the connection</span></span>
> [!INCLUDE [Create a connection to Azure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="84304-119">Uso de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="84304-119">Use a trigger</span></span>
<span data-ttu-id="84304-120">Este conector no tiene ningún desencadenador.</span><span class="sxs-lookup"><span data-stu-id="84304-120">This connector does not have any triggers.</span></span> <span data-ttu-id="84304-121">Utilice otros desencadenadores para iniciar la aplicación lógica; por ejemplo, un desencadenador de periodicidad, un desencadenador HTTP webhook, los desencadenadores disponibles con otros conectores, etc.</span><span class="sxs-lookup"><span data-stu-id="84304-121">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="84304-122">En [Creación de una nueva aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) se puede ver un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="84304-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="84304-123">Uso de una acción</span><span class="sxs-lookup"><span data-stu-id="84304-123">Use an action</span></span>
<span data-ttu-id="84304-124">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="84304-124">An action is an operation carried out by the workflow defined in a logic app.</span></span>

1. <span data-ttu-id="84304-125">Seleccione el signo más.</span><span class="sxs-lookup"><span data-stu-id="84304-125">Select the plus sign.</span></span> <span data-ttu-id="84304-126">Aparecen varias opciones: **Agregar una acción**, **Agregar una condición** o una de las opciones de **Más**.</span><span class="sxs-lookup"><span data-stu-id="84304-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="84304-127">Elija **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="84304-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="84304-128">En el cuadro de texto, escriba "blob" para obtener una lista de todas las acciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="84304-128">In the text box, type “blob” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="84304-129">En nuestro ejemplo, elija **AzureBlob - Obtener metadatos de archivo mediante la ruta de acceso**.</span><span class="sxs-lookup"><span data-stu-id="84304-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="84304-130">Si ya existe una conexión, seleccione el botón **...** (Mostrar selector) para seleccionar un archivo.</span><span class="sxs-lookup"><span data-stu-id="84304-130">If a connection already exists, then select the **...** (Show Picker) button to select a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="84304-131">Si se le solicita la información de conexión, escriba los detalles para crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="84304-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="84304-132">Estas propiedades se describen en la sección [Creación de la conexión](connectors-create-api-azureblobstorage.md#create-the-connection) de este tema.</span><span class="sxs-lookup"><span data-stu-id="84304-132">[Create the connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="84304-133">En este ejemplo, obtenemos los metadatos de un archivo.</span><span class="sxs-lookup"><span data-stu-id="84304-133">In this example, we get the metadata of a file.</span></span> <span data-ttu-id="84304-134">Para ver los metadatos, agregue otra acción que cree un archivo nuevo mediante otro conector.</span><span class="sxs-lookup"><span data-stu-id="84304-134">To see the metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="84304-135">Por ejemplo, agregue una acción de OneDrive que cree un nuevo archivo de "prueba" basándose en los metadatos.</span><span class="sxs-lookup"><span data-stu-id="84304-135">For example, add a OneDrive action that creates a new "test" file based on the metadata.</span></span> 


5. <span data-ttu-id="84304-136">**Guarde** los cambios (esquina superior izquierda de la barra de herramientas).</span><span class="sxs-lookup"><span data-stu-id="84304-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="84304-137">La aplicación lógica se guarda y se puede habilitar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="84304-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="84304-138">[Explorador de Storage](http://storageexplorer.com/) es una excelente herramienta para administrar varias cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="84304-138">[Storage Explorer](http://storageexplorer.com/) is a great tool to  manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="84304-139">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="84304-139">Connector-specific details</span></span>

<span data-ttu-id="84304-140">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="84304-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="84304-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="84304-141">Next steps</span></span>
<span data-ttu-id="84304-142">[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="84304-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="84304-143">Explore los demás conectores disponibles en Logic Apps en nuestra [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="84304-143">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

