---
title: Cambio del valor predeterminado de la ruta de acceso del blob | Microsoft Docs
description: "Aprenda a configurar una función de Azure para cambiar el nombre de una ruta de acceso del archivo de blob (versión preliminar privada)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 057d4d7370207859617eb63238bf425bfa6d3e16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="change-a-blob-path-from-the-default-path-private-preview"></a><span data-ttu-id="c5881-103">Cambio del valor predeterminado de la ruta de acceso de un blob (versión preliminar privada)</span><span class="sxs-lookup"><span data-stu-id="c5881-103">Change a blob path from the default path (private preview)</span></span>

<span data-ttu-id="c5881-104">En este artículo se describe cómo configurar una función de Azure para cambiar el nombre de una ruta de acceso de archivo de blob predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c5881-104">This article describes how to set up an Azure function to rename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c5881-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c5881-105">Prerequisites</span></span>

<span data-ttu-id="c5881-106">Asegúrese de que tiene una definición del trabajo que se ha configurado correctamente en un recurso de datos híbridos de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c5881-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="c5881-107">Creación de una función de Azure</span><span class="sxs-lookup"><span data-stu-id="c5881-107">Create an Azure function</span></span>

<span data-ttu-id="c5881-108">Para crear una función de Azure, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c5881-108">To create an Azure function, do the following:</span></span>

1. <span data-ttu-id="c5881-109">Vaya al [Portal de Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c5881-109">Go to the [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="c5881-110">En la parte superior del panel izquierdo, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="c5881-110">At the top of the left pane, click **New**.</span></span> 

3. <span data-ttu-id="c5881-111">En el cuadro de **Búsqueda**, escriba **Funcion App** y presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="c5881-111">In the **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Escritura de "Function App" en el cuadro de búsqueda](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="c5881-113">En la lista **Results** (Resultados), haga clic en **Function App**.</span><span class="sxs-lookup"><span data-stu-id="c5881-113">In the **Results** list, click **Function App**.</span></span>

    ![Selección del recurso Function App en la lista de resultados](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="c5881-115">Se abrirá la ventana **Function App**.</span><span class="sxs-lookup"><span data-stu-id="c5881-115">The **Function App** window opens.</span></span>

5. <span data-ttu-id="c5881-116">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c5881-116">Click **Create**.</span></span>

    ![Botón "Crear" de la ventana de Function App](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="c5881-118">En la hoja de configuración **Function App**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c5881-118">On the **Function App** configuration blade, do the following:</span></span>

    <span data-ttu-id="c5881-119">a.</span><span class="sxs-lookup"><span data-stu-id="c5881-119">a.</span></span> <span data-ttu-id="c5881-120">En el cuadro **Nombre de aplicación**, escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c5881-120">In the **App name** box, type the app name.</span></span>
    
    <span data-ttu-id="c5881-121">b.</span><span class="sxs-lookup"><span data-stu-id="c5881-121">b.</span></span> <span data-ttu-id="c5881-122">En el cuadro **Suscripción**, escriba el nombre de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="c5881-122">In the **Subscription** box, type the name of the subscription.</span></span>

    <span data-ttu-id="c5881-123">c.</span><span class="sxs-lookup"><span data-stu-id="c5881-123">c.</span></span> <span data-ttu-id="c5881-124">En **Grupo de recursos**, haga clic en **Crear nuevo** y escriba el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c5881-124">Under **Resource Group**, click **Create new**, and then type the name of the resource group.</span></span>

    <span data-ttu-id="c5881-125">d.</span><span class="sxs-lookup"><span data-stu-id="c5881-125">d.</span></span> <span data-ttu-id="c5881-126">En el cuadro **Plan de hospedaje**, escriba **Plan de consumo**.</span><span class="sxs-lookup"><span data-stu-id="c5881-126">In the **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="c5881-127">e.</span><span class="sxs-lookup"><span data-stu-id="c5881-127">e.</span></span> <span data-ttu-id="c5881-128">En el cuadro **Ubicación**, escriba la ubicación.</span><span class="sxs-lookup"><span data-stu-id="c5881-128">In the **Location** box, type the location.</span></span>

    <span data-ttu-id="c5881-129">f.</span><span class="sxs-lookup"><span data-stu-id="c5881-129">f.</span></span> <span data-ttu-id="c5881-130">En **Cuenta de almacenamiento**, seleccione una cuenta de almacenamiento existente o cree una nueva.</span><span class="sxs-lookup"><span data-stu-id="c5881-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="c5881-131">Una cuenta de almacenamiento se usa de forma interna para la función.</span><span class="sxs-lookup"><span data-stu-id="c5881-131">A storage account is used internally for the function.</span></span>

    ![Introducción de los datos de configuración de Function App](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="c5881-133">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c5881-133">Click **Create**.</span></span>  
    <span data-ttu-id="c5881-134">La instancia de Function App se creará.</span><span class="sxs-lookup"><span data-stu-id="c5881-134">The function app is created.</span></span>

8. <span data-ttu-id="c5881-135">En el panel izquierdo, haga clic en **More services** (Más servicios), y realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c5881-135">In the left pane, click **More services**, and then do the following:</span></span>
    
    <span data-ttu-id="c5881-136">a.</span><span class="sxs-lookup"><span data-stu-id="c5881-136">a.</span></span> <span data-ttu-id="c5881-137">En el cuadro **Filtro**, escriba **App Services**.</span><span class="sxs-lookup"><span data-stu-id="c5881-137">In the **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="c5881-138">b.</span><span class="sxs-lookup"><span data-stu-id="c5881-138">b.</span></span> <span data-ttu-id="c5881-139">Haga clic en **App Services**.</span><span class="sxs-lookup"><span data-stu-id="c5881-139">Click **App Services**.</span></span> 

    ![Vínculo "More services" (Más servicios" del panel izquierdo](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="c5881-141">En la lista de instancias de App Services, haga clic en el nombre de la instancia de Function App.</span><span class="sxs-lookup"><span data-stu-id="c5881-141">In the list of app services, click the name of the function app.</span></span>  
    <span data-ttu-id="c5881-142">La página de la instancia de Function App se abrirá.</span><span class="sxs-lookup"><span data-stu-id="c5881-142">The function app page opens.</span></span>

10. <span data-ttu-id="c5881-143">En el panel izquierdo, haga clic en **New Function** (Función nueva) y realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c5881-143">In the left pane, click **New Function**, and then do the following:</span></span> 

    <span data-ttu-id="c5881-144">a.</span><span class="sxs-lookup"><span data-stu-id="c5881-144">a.</span></span> <span data-ttu-id="c5881-145">En la lista **Language** (Lenguaje), seleccione **C#**.</span><span class="sxs-lookup"><span data-stu-id="c5881-145">In the **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="c5881-146">b.</span><span class="sxs-lookup"><span data-stu-id="c5881-146">b.</span></span> <span data-ttu-id="c5881-147">En la matriz de iconos de plantilla, seleccione **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="c5881-147">In the array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="c5881-148">c.</span><span class="sxs-lookup"><span data-stu-id="c5881-148">c.</span></span> <span data-ttu-id="c5881-149">En el cuadro **Asigne un nombre a la función**, escriba un nombre para la función.</span><span class="sxs-lookup"><span data-stu-id="c5881-149">In the **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="c5881-150">d.</span><span class="sxs-lookup"><span data-stu-id="c5881-150">d.</span></span> <span data-ttu-id="c5881-151">En el cuadro **Queue name** (Nombre de la cola), escriba el nombre de la definición del trabajo de transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="c5881-151">In the **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="c5881-152">e.</span><span class="sxs-lookup"><span data-stu-id="c5881-152">e.</span></span> <span data-ttu-id="c5881-153">En **Conexión de cuenta de almacenamiento**, haga clic en **Nueva** y seleccione la cuenta que corresponda al trabajo de transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="c5881-153">Under **Storage account connection**, click **new**, and then select the account that corresponds to the data-transformation job.</span></span>  
        <span data-ttu-id="c5881-154">Anote el nombre de la conexión.</span><span class="sxs-lookup"><span data-stu-id="c5881-154">Make a note of the connection name.</span></span> <span data-ttu-id="c5881-155">La función de Azure necesitará este nombre más adelante.</span><span class="sxs-lookup"><span data-stu-id="c5881-155">The name is required later in the Azure function.</span></span>

       ![Creación de una función de C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="c5881-157">f.</span><span class="sxs-lookup"><span data-stu-id="c5881-157">f.</span></span> <span data-ttu-id="c5881-158">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c5881-158">Click **Create**.</span></span>  
    <span data-ttu-id="c5881-159">Se abrirá la ventana **Función**.</span><span class="sxs-lookup"><span data-stu-id="c5881-159">The **Function** window opens.</span></span>

11. <span data-ttu-id="c5881-160">En la ventana **Función**, ejecute el archivo _.csx_ y haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c5881-160">In the **Function** window, run _.csx_ file, and then do the following:</span></span>

    <span data-ttu-id="c5881-161">a.</span><span class="sxs-lookup"><span data-stu-id="c5881-161">a.</span></span> <span data-ttu-id="c5881-162">Pegue el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="c5881-162">Paste the following code:</span></span>

    ```
    using System;
    using System.Configuration;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Queue;
    using Microsoft.WindowsAzure.Storage;
    using System.Collections.Generic;
    using System.Linq;

    public static void Run(QueueItem myQueueItem, TraceWriter log)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["STORAGE_CONNECTIONNAME"]);

        string storageAccUriEndswith = "windows.net/";
        string uri = myQueueItem.TargetLocation.Replace("%20", " ");
        log.Info($"Blob Uri: {uri}");

        // Remove storage account uri string
        uri = uri.Substring(uri.IndexOf(storageAccUriEndswith) + storageAccUriEndswith.Length);

        string containerName = uri.Substring(0, uri.IndexOf("/")); 

        // Remove container name string
        uri = uri.Substring(containerName.Length + 1);

        // Current blob path
        string blobName = uri; 

        string volumeName = uri.Substring(containerName.Length + 1);
        volumeName = uri.Substring(0, uri.IndexOf("/"));

        // Remove volume name string
        uri = uri.Substring(volumeName.Length + 1);

        string newContainerName = uri.Substring(0, uri.IndexOf("/")).ToLower();
        string newBlobName = uri.Substring(newContainerName.Length + 1);

        log.Info($"Container name: {containerName}");
        log.Info($"Volume name: {volumeName}");
        log.Info($"New container name: {newContainerName}");

        log.Info($"Blob name: {blobName}");
        log.Info($"New blob name: {newBlobName}");

        // Create the blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Container reference
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlobContainer newContainer = blobClient.GetContainerReference(newContainerName);
        newContainer.CreateIfNotExists();

        if(!container.Exists())
        {
            log.Info($"Container - {containerName} not exists");
            return;
        }

        if(!newContainer.Exists())
        {
            log.Info($"Container - {newContainerName} not exists");
            return;
        }

        CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
        if (!blob.Exists())
        {
            // Skip to copy the blob to new container, if source blob doesn't exist
            log.Info($"The specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy to new container
            blob.DeleteIfExists();
            log.Info($"Blob file path renamed completed successfully");
        }
        else
        {
            log.Info($"Blob file path renamed already done");
            // Delete old blob, if already exists.
            blob.DeleteIfExists();
        }
    }

    public class QueueItem
    {
        public string SourceLocation {get;set;}
        public long SizeInBytes {get;set;}
        public string Status {get;set;}
        public string JobID {get;set;}
        public string TargetLocation {get; set;}
    }

    ```

    <span data-ttu-id="c5881-163">b.</span><span class="sxs-lookup"><span data-stu-id="c5881-163">b.</span></span> <span data-ttu-id="c5881-164">Reemplace **STORAGE_CONNECTIONNAME** en la línea 11 por la conexión de cuenta de almacenamiento (consulte el punto 8c).</span><span class="sxs-lookup"><span data-stu-id="c5881-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="c5881-165">c.</span><span class="sxs-lookup"><span data-stu-id="c5881-165">c.</span></span> <span data-ttu-id="c5881-166">En la parte superior izquierda, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c5881-166">At the top left, click **Save**.</span></span>

    ![Función Guardar](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="c5881-168">Para completar la función, haga lo siguiente para agregar un archivo más:</span><span class="sxs-lookup"><span data-stu-id="c5881-168">To complete the function, add one more file by doing the following:</span></span>

    <span data-ttu-id="c5881-169">a.</span><span class="sxs-lookup"><span data-stu-id="c5881-169">a.</span></span> <span data-ttu-id="c5881-170">Haga clic en **View files** (Ver archivos).</span><span class="sxs-lookup"><span data-stu-id="c5881-170">Click **View files**.</span></span>

       ![Vínculo "View files" (Ver archivos)](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="c5881-172">b.</span><span class="sxs-lookup"><span data-stu-id="c5881-172">b.</span></span> <span data-ttu-id="c5881-173">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c5881-173">Click **Add**.</span></span>
    
    <span data-ttu-id="c5881-174">c.</span><span class="sxs-lookup"><span data-stu-id="c5881-174">c.</span></span> <span data-ttu-id="c5881-175">Escriba **project.json** y presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="c5881-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="c5881-176">d.</span><span class="sxs-lookup"><span data-stu-id="c5881-176">d.</span></span> <span data-ttu-id="c5881-177">En el archivo **project.json**, peque el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="c5881-177">In the **project.json** file, paste the following code:</span></span>

    ```
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "windowsazure.storage": "8.1.1"
        }
        }
    }
    }

    ```

    <span data-ttu-id="c5881-178">e.</span><span class="sxs-lookup"><span data-stu-id="c5881-178">e.</span></span> <span data-ttu-id="c5881-179">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c5881-179">Click **Save**.</span></span>

<span data-ttu-id="c5881-180">Acaba de crear una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="c5881-180">You have created an Azure function.</span></span> <span data-ttu-id="c5881-181">Esta función se desencadena cada vez que el trabajo de transformación de datos genera un blob nuevo.</span><span class="sxs-lookup"><span data-stu-id="c5881-181">This function is triggered each time a new blob is generated by the data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5881-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5881-182">Next steps</span></span>

[<span data-ttu-id="c5881-183">Uso de la IU de StorSimple Data Manager para transformar los datos</span><span class="sxs-lookup"><span data-stu-id="c5881-183">Use StorSimple Data Manager UI to transform your data</span></span>](storsimple-data-manager-ui.md)
