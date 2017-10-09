---
title: "aaaCreate una función en desencadenado por almacenamiento de blobs de Azure | Documentos de Microsoft"
description: "Usar funciones de Azure toocreate una función sin servidor invocada por elementos había agregado tooAzure el almacenamiento de blobs."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="297bb-103">Crear una función desencadenada por Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="297bb-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="297bb-104">Obtenga información acerca de cómo toocreate una función que se desencadena cuando los archivos están cargados tooor actualizado en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="297bb-104">Learn how toocreate a function triggered when files are uploaded tooor updated in Azure Blob storage.</span></span>

![Ver el mensaje en los registros de Hola.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="297bb-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="297bb-106">Prerequisites</span></span>

+ <span data-ttu-id="297bb-107">Descargue e instale hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="297bb-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="297bb-108">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="297bb-108">An Azure subscription.</span></span> <span data-ttu-id="297bb-109">Si no tiene una, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="297bb-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="297bb-110">Creación de una Function App de Azure</span><span class="sxs-lookup"><span data-stu-id="297bb-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App creada correctamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="297bb-112">A continuación, cree una función en la aplicación de hello nueva función.</span><span class="sxs-lookup"><span data-stu-id="297bb-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="297bb-113">Creación de una función desencadenada por Blob Storage</span><span class="sxs-lookup"><span data-stu-id="297bb-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="297bb-114">Expanda la aplicación de la función y haga clic en hello  **+**  aparece al lado demasiado**funciones**.</span><span class="sxs-lookup"><span data-stu-id="297bb-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="297bb-115">Si se trata de la primera función en la aplicación de la función de hello, seleccione **función personalizada**.</span><span class="sxs-lookup"><span data-stu-id="297bb-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="297bb-116">Esto muestra el conjunto completo de Hola de plantillas de función.</span><span class="sxs-lookup"><span data-stu-id="297bb-116">This displays hello complete set of function templates.</span></span>

    ![Página de inicio rápido de funciones en hello portal de Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="297bb-118">Seleccione hello **BlobTrigger** plantilla de idioma que desee y usar la configuración como se especifica en la tabla de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="297bb-118">Select hello **BlobTrigger** template for your desired language, and use hello settings as specified in hello table.</span></span>

    ![Crear función de almacenamiento desencadenada Blob Hola.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="297bb-120">Configuración</span><span class="sxs-lookup"><span data-stu-id="297bb-120">Setting</span></span> | <span data-ttu-id="297bb-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="297bb-121">Suggested value</span></span> | <span data-ttu-id="297bb-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="297bb-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="297bb-123">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="297bb-123">**Path**</span></span>   | <span data-ttu-id="297bb-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="297bb-124">mycontainer/{name}</span></span>    | <span data-ttu-id="297bb-125">Ubicación de Blob Storage que se está supervisando.</span><span class="sxs-lookup"><span data-stu-id="297bb-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="297bb-126">nombre de archivo de Hola de blob de Hola se pasa en el enlace de hello como hello _nombre_ parámetro.</span><span class="sxs-lookup"><span data-stu-id="297bb-126">hello file name of hello blob is passed in hello binding as hello _name_ parameter.</span></span>  |
    | <span data-ttu-id="297bb-127">**Conexión de la cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="297bb-127">**Storage account connection**</span></span> | <span data-ttu-id="297bb-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="297bb-128">AzureWebJobStorage</span></span> | <span data-ttu-id="297bb-129">Puede usar la conexión de la cuenta de almacenamiento Hola ya está en uso por la aplicación de la función o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="297bb-129">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="297bb-130">**Asigne un nombre a la función**</span><span class="sxs-lookup"><span data-stu-id="297bb-130">**Name your function**</span></span> | <span data-ttu-id="297bb-131">Único en la Function App</span><span class="sxs-lookup"><span data-stu-id="297bb-131">Unique in your function app</span></span> | <span data-ttu-id="297bb-132">Nombre de la función desencadenada por este blob.</span><span class="sxs-lookup"><span data-stu-id="297bb-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="297bb-133">Haga clic en **crear** toocreate la función.</span><span class="sxs-lookup"><span data-stu-id="297bb-133">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="297bb-134">A continuación, conectarse a tooyour cuenta de almacenamiento de Azure y crear hello **mycontainer** contenedor.</span><span class="sxs-lookup"><span data-stu-id="297bb-134">Next, you connect tooyour Azure Storage account and create hello **mycontainer** container.</span></span>

## <a name="create-hello-container"></a><span data-ttu-id="297bb-135">Crear contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="297bb-135">Create hello container</span></span>

1. <span data-ttu-id="297bb-136">En la función, haga clic en **Integrar**, expanda **Documentación** y copie los dos valores de **Nombre de cuenta** y **Clave de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="297bb-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="297bb-137">Use estas cuentas de almacenamiento de credenciales tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="297bb-137">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="297bb-138">Si ya se ha conectado la cuenta de almacenamiento, omitir toostep 4.</span><span class="sxs-lookup"><span data-stu-id="297bb-138">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Obtener las credenciales de conexión de cuenta de almacenamiento de Hola.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="297bb-140">Ejecute hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) de herramientas, haga clic en hello conectarse icono de hello izquierda, elija **utilizar un nombre de la cuenta de almacenamiento y la clave**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="297bb-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Ejecutar la herramienta de explorador de la cuenta de almacenamiento de Hola.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="297bb-142">Escriba Hola **nombre-cuenta** y **clave de cuenta** del paso 1, haga clic en **siguiente** y, a continuación, **conectar**.</span><span class="sxs-lookup"><span data-stu-id="297bb-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Escriba las credenciales de almacenamiento de Hola y conectarse.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="297bb-144">Expanda Hola adjunta cuenta de almacenamiento, haga clic en **contenedores de blobs**, haga clic en **crear contenedor de blob**, tipo `mycontainer`, y, a continuación, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="297bb-144">Expand hello attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Cree una cola de almacenamiento.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="297bb-146">Ahora que tiene un contenedor de blobs, puede probar función hello mediante la carga de un contenedor de toohello de archivo.</span><span class="sxs-lookup"><span data-stu-id="297bb-146">Now that you have a blob container, you can test hello function by uploading a file toohello container.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="297bb-147">Probar función hello</span><span class="sxs-lookup"><span data-stu-id="297bb-147">Test hello function</span></span>

1. <span data-ttu-id="297bb-148">Nuevo en hello portal de Azure, examinar tooyour función expanda hello **registros** final Hola de página de Hola y asegúrese de que dicho registro de transmisión por secuencias no está en pausa.</span><span class="sxs-lookup"><span data-stu-id="297bb-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="297bb-149">En el Explorador de almacenamiento, expanda la cuenta de almacenamiento, **Contenedores de blobs** y **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="297bb-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="297bb-150">Haga clic en **Cargar** y en **Cargar archivos…**</span><span class="sxs-lookup"><span data-stu-id="297bb-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Cargar un contenedor de blobs de toohello de archivo.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="297bb-152">Hola **cargar archivos** diálogo cuadro, haga clic en hello **archivos** campo.</span><span class="sxs-lookup"><span data-stu-id="297bb-152">In hello **Upload files** dialog box, click hello **Files** field.</span></span> <span data-ttu-id="297bb-153">Examinar el archivo tooa en el equipo local, como un archivo de imagen, selecciónelo y haga clic en **abiertos** y, a continuación, **cargar**.</span><span class="sxs-lookup"><span data-stu-id="297bb-153">Browse tooa file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="297bb-154">Volver atrás tooyour función registros y compruebe que se ha leído el blob Hola.</span><span class="sxs-lookup"><span data-stu-id="297bb-154">Go back tooyour function logs and verify that hello blob has been read.</span></span>

   ![Ver el mensaje en los registros de Hola.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="297bb-156">Cuando se ejecuta la aplicación de la función en el plan de consumo de hello predeterminado, puede haber un retraso de seguridad tooseveral minutos entre blob que se agregaron o actualizaron de Hola y Hola función va a desencadenar.</span><span class="sxs-lookup"><span data-stu-id="297bb-156">When your function app runs in hello default Consumption plan, there may be a delay of up tooseveral minutes between hello blob being added or updated and hello function being triggered.</span></span> <span data-ttu-id="297bb-157">Si necesita una latencia baja en las funciones desencadenadas por el blob, considere la posibilidad de ejecutar la Function App en un plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="297bb-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="297bb-158">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="297bb-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="297bb-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="297bb-159">Next steps</span></span>

<span data-ttu-id="297bb-160">Ha creado una función que se ejecuta cuando un blob se agrega tooor actualizado en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="297bb-160">You have created a function that runs when a blob is added tooor updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="297bb-161">Para obtener más información sobre los desencadenadores de Blob Storage, vea [Enlaces de Blob Storage en Azure Functions](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="297bb-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
