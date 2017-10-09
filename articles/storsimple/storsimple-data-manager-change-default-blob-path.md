---
title: ruta de acceso de blob de aaaChange predeterminado Hola | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset de un Azure funcionan toorename una ruta de acceso del archivo de blob (vista previa privada)"
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
ms.openlocfilehash: 2c414603514223c701ab1a3bd0b81ee18f1af666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a><span data-ttu-id="18e78-103">Cambiar una ruta de acceso de blob de ruta de acceso predeterminada de hello (vista previa privada)</span><span class="sxs-lookup"><span data-stu-id="18e78-103">Change a blob path from hello default path (private preview)</span></span>

<span data-ttu-id="18e78-104">Este artículo describe cómo tooset de un Azure funcionan toorename una ruta de acceso de archivo de blob de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="18e78-104">This article describes how tooset up an Azure function toorename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="18e78-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="18e78-105">Prerequisites</span></span>

<span data-ttu-id="18e78-106">Asegúrese de que tiene una definición del trabajo que se ha configurado correctamente en un recurso de datos híbridos de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="18e78-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="18e78-107">Creación de una función de Azure</span><span class="sxs-lookup"><span data-stu-id="18e78-107">Create an Azure function</span></span>

<span data-ttu-id="18e78-108">toocreate una función de Azure, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="18e78-108">toocreate an Azure function, do hello following:</span></span>

1. <span data-ttu-id="18e78-109">Vaya toohello [portal de Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="18e78-109">Go toohello [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="18e78-110">En hello parte superior del panel izquierdo de hello, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="18e78-110">At hello top of hello left pane, click **New**.</span></span> 

3. <span data-ttu-id="18e78-111">Hola **búsqueda** , escriba **aplicación de la función**, y, a continuación, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="18e78-111">In hello **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Escriba "Aplicación de la función" en el cuadro de búsqueda de Hola](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="18e78-113">Hola **resultados** lista, haga clic en **aplicación de la función**.</span><span class="sxs-lookup"><span data-stu-id="18e78-113">In hello **Results** list, click **Function App**.</span></span>

    ![Recurso de aplicación de la función de hello seleccione en la lista de resultados de Hola](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="18e78-115">Hola **aplicación de la función** se abre la ventana.</span><span class="sxs-lookup"><span data-stu-id="18e78-115">hello **Function App** window opens.</span></span>

5. <span data-ttu-id="18e78-116">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="18e78-116">Click **Create**.</span></span>

    ![botón de "Crear" de ventana de aplicación de la función Hello](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="18e78-118">En hello **función aplicación** hoja de configuración, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="18e78-118">On hello **Function App** configuration blade, do hello following:</span></span>

    <span data-ttu-id="18e78-119">a.</span><span class="sxs-lookup"><span data-stu-id="18e78-119">a.</span></span> <span data-ttu-id="18e78-120">Hola **nombre de la aplicación** cuadro, el nombre de la aplicación de tipo Hola.</span><span class="sxs-lookup"><span data-stu-id="18e78-120">In hello **App name** box, type hello app name.</span></span>
    
    <span data-ttu-id="18e78-121">b.</span><span class="sxs-lookup"><span data-stu-id="18e78-121">b.</span></span> <span data-ttu-id="18e78-122">Hola **suscripción** cuadro, escriba un nombre Hola de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e78-122">In hello **Subscription** box, type hello name of hello subscription.</span></span>

    <span data-ttu-id="18e78-123">c.</span><span class="sxs-lookup"><span data-stu-id="18e78-123">c.</span></span> <span data-ttu-id="18e78-124">En **grupo de recursos**, haga clic en **crear nuevo**y, a continuación, Hola nombre del tipo de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e78-124">Under **Resource Group**, click **Create new**, and then type hello name of hello resource group.</span></span>

    <span data-ttu-id="18e78-125">d.</span><span class="sxs-lookup"><span data-stu-id="18e78-125">d.</span></span> <span data-ttu-id="18e78-126">Hola **Plan de hospedaje** , escriba **consumo previsto**.</span><span class="sxs-lookup"><span data-stu-id="18e78-126">In hello **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="18e78-127">e.</span><span class="sxs-lookup"><span data-stu-id="18e78-127">e.</span></span> <span data-ttu-id="18e78-128">Hola **ubicación** cuadro de ubicación de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="18e78-128">In hello **Location** box, type hello location.</span></span>

    <span data-ttu-id="18e78-129">f.</span><span class="sxs-lookup"><span data-stu-id="18e78-129">f.</span></span> <span data-ttu-id="18e78-130">En **Cuenta de almacenamiento**, seleccione una cuenta de almacenamiento existente o cree una nueva.</span><span class="sxs-lookup"><span data-stu-id="18e78-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="18e78-131">Una cuenta de almacenamiento se usa internamente para la función hello.</span><span class="sxs-lookup"><span data-stu-id="18e78-131">A storage account is used internally for hello function.</span></span>

    ![Introducción de los datos de configuración de Function App](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="18e78-133">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="18e78-133">Click **Create**.</span></span>  
    <span data-ttu-id="18e78-134">se crea la aplicación de la función de Hello.</span><span class="sxs-lookup"><span data-stu-id="18e78-134">hello function app is created.</span></span>

8. <span data-ttu-id="18e78-135">En el panel izquierdo de hello, haga clic en **más servicios**y, a continuación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="18e78-135">In hello left pane, click **More services**, and then do hello following:</span></span>
    
    <span data-ttu-id="18e78-136">a.</span><span class="sxs-lookup"><span data-stu-id="18e78-136">a.</span></span> <span data-ttu-id="18e78-137">Hola **filtro** , escriba **servicios de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="18e78-137">In hello **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="18e78-138">b.</span><span class="sxs-lookup"><span data-stu-id="18e78-138">b.</span></span> <span data-ttu-id="18e78-139">Haga clic en **App Services**.</span><span class="sxs-lookup"><span data-stu-id="18e78-139">Click **App Services**.</span></span> 

    ![Vínculo de "Más servicios" en el panel izquierdo de Hola](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="18e78-141">En la lista hello de servicios de aplicaciones, haga clic en nombre de Hola de aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="18e78-141">In hello list of app services, click hello name of hello function app.</span></span>  
    <span data-ttu-id="18e78-142">se abre la página de aplicación de función de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e78-142">hello function app page opens.</span></span>

10. <span data-ttu-id="18e78-143">En el panel izquierdo de hello, haga clic en **nueva función**y, a continuación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="18e78-143">In hello left pane, click **New Function**, and then do hello following:</span></span> 

    <span data-ttu-id="18e78-144">a.</span><span class="sxs-lookup"><span data-stu-id="18e78-144">a.</span></span> <span data-ttu-id="18e78-145">Hola **lenguaje** lista, seleccione **C#**.</span><span class="sxs-lookup"><span data-stu-id="18e78-145">In hello **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="18e78-146">b.</span><span class="sxs-lookup"><span data-stu-id="18e78-146">b.</span></span> <span data-ttu-id="18e78-147">En la matriz de Hola de iconos de plantilla, seleccione **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="18e78-147">In hello array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="18e78-148">c.</span><span class="sxs-lookup"><span data-stu-id="18e78-148">c.</span></span> <span data-ttu-id="18e78-149">Hola **el nombre de la función** , escriba un nombre para la función.</span><span class="sxs-lookup"><span data-stu-id="18e78-149">In hello **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="18e78-150">d.</span><span class="sxs-lookup"><span data-stu-id="18e78-150">d.</span></span> <span data-ttu-id="18e78-151">Hola **nombre de la cola** cuadro, escriba el nombre de definición de trabajo de transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="18e78-151">In hello **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="18e78-152">e.</span><span class="sxs-lookup"><span data-stu-id="18e78-152">e.</span></span> <span data-ttu-id="18e78-153">En **conexión de la cuenta de almacenamiento**, haga clic en **nueva**y, a continuación, seleccione cuenta de hello correspondiente toohello trabajo de transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="18e78-153">Under **Storage account connection**, click **new**, and then select hello account that corresponds toohello data-transformation job.</span></span>  
        <span data-ttu-id="18e78-154">Tome nota del nombre de la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e78-154">Make a note of hello connection name.</span></span> <span data-ttu-id="18e78-155">se requiere nombre de Hello más adelante en hello Azure función.</span><span class="sxs-lookup"><span data-stu-id="18e78-155">hello name is required later in hello Azure function.</span></span>

       ![Creación de una función de C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="18e78-157">f.</span><span class="sxs-lookup"><span data-stu-id="18e78-157">f.</span></span> <span data-ttu-id="18e78-158">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="18e78-158">Click **Create**.</span></span>  
    <span data-ttu-id="18e78-159">Hola **función** abre la ventana.</span><span class="sxs-lookup"><span data-stu-id="18e78-159">hello **Function** window opens.</span></span>

11. <span data-ttu-id="18e78-160">Hola **función** ventana, ejecute _.csx_ de archivos y, a continuación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="18e78-160">In hello **Function** window, run _.csx_ file, and then do hello following:</span></span>

    <span data-ttu-id="18e78-161">a.</span><span class="sxs-lookup"><span data-stu-id="18e78-161">a.</span></span> <span data-ttu-id="18e78-162">Pegue el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="18e78-162">Paste hello following code:</span></span>

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

        // Create hello blob client.
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
            // Skip toocopy hello blob toonew container, if source blob doesn't exist
            log.Info($"hello specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy toonew container
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

    <span data-ttu-id="18e78-163">b.</span><span class="sxs-lookup"><span data-stu-id="18e78-163">b.</span></span> <span data-ttu-id="18e78-164">Reemplace **STORAGE_CONNECTIONNAME** en la línea 11 por la conexión de cuenta de almacenamiento (consulte el punto 8c).</span><span class="sxs-lookup"><span data-stu-id="18e78-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="18e78-165">c.</span><span class="sxs-lookup"><span data-stu-id="18e78-165">c.</span></span> <span data-ttu-id="18e78-166">En hello esquina superior izquierda, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="18e78-166">At hello top left, click **Save**.</span></span>

    ![Función Guardar](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="18e78-168">toocomplete Hola (función), agregue un archivo más haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="18e78-168">toocomplete hello function, add one more file by doing hello following:</span></span>

    <span data-ttu-id="18e78-169">a.</span><span class="sxs-lookup"><span data-stu-id="18e78-169">a.</span></span> <span data-ttu-id="18e78-170">Haga clic en **View files** (Ver archivos).</span><span class="sxs-lookup"><span data-stu-id="18e78-170">Click **View files**.</span></span>

       ![Hola vínculo "Ver archivos"](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="18e78-172">b.</span><span class="sxs-lookup"><span data-stu-id="18e78-172">b.</span></span> <span data-ttu-id="18e78-173">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="18e78-173">Click **Add**.</span></span>
    
    <span data-ttu-id="18e78-174">c.</span><span class="sxs-lookup"><span data-stu-id="18e78-174">c.</span></span> <span data-ttu-id="18e78-175">Escriba **project.json** y presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="18e78-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="18e78-176">d.</span><span class="sxs-lookup"><span data-stu-id="18e78-176">d.</span></span> <span data-ttu-id="18e78-177">Hola **project.json** de archivo, pegue el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="18e78-177">In hello **project.json** file, paste hello following code:</span></span>

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

    <span data-ttu-id="18e78-178">e.</span><span class="sxs-lookup"><span data-stu-id="18e78-178">e.</span></span> <span data-ttu-id="18e78-179">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="18e78-179">Click **Save**.</span></span>

<span data-ttu-id="18e78-180">Acaba de crear una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="18e78-180">You have created an Azure function.</span></span> <span data-ttu-id="18e78-181">Esta función se desencadena cada vez que se genere un nuevo blob por trabajo de transformación de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e78-181">This function is triggered each time a new blob is generated by hello data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18e78-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18e78-182">Next steps</span></span>

[<span data-ttu-id="18e78-183">Usar los datos de tootransform de interfaz de usuario de administrador de datos de StorSimple</span><span class="sxs-lookup"><span data-stu-id="18e78-183">Use StorSimple Data Manager UI tootransform your data</span></span>](storsimple-data-manager-ui.md)
