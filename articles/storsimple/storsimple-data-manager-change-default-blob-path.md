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
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a>Cambiar una ruta de acceso de blob de ruta de acceso predeterminada de hello (vista previa privada)

Este artículo describe cómo tooset de un Azure funcionan toorename una ruta de acceso de archivo de blob de forma predeterminada. 

## <a name="prerequisites"></a>Requisitos previos

Asegúrese de que tiene una definición del trabajo que se ha configurado correctamente en un recurso de datos híbridos de un grupo de recursos.

## <a name="create-an-azure-function"></a>Creación de una función de Azure

toocreate una función de Azure, Hola siguientes:

1. Vaya toohello [portal de Azure](http://portal.azure.com/).

2. En hello parte superior del panel izquierdo de hello, haga clic en **nuevo**. 

3. Hola **búsqueda** , escriba **aplicación de la función**, y, a continuación, presione ENTRAR.

    ![Escriba "Aplicación de la función" en el cuadro de búsqueda de Hola](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. Hola **resultados** lista, haga clic en **aplicación de la función**.

    ![Recurso de aplicación de la función de hello seleccione en la lista de resultados de Hola](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    Hola **aplicación de la función** se abre la ventana.

5. Haga clic en **Crear**.

    ![botón de "Crear" de ventana de aplicación de la función Hello](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. En hello **función aplicación** hoja de configuración, Hola siguientes:

    a. Hola **nombre de la aplicación** cuadro, el nombre de la aplicación de tipo Hola.
    
    b. Hola **suscripción** cuadro, escriba un nombre Hola de suscripción de Hola.

    c. En **grupo de recursos**, haga clic en **crear nuevo**y, a continuación, Hola nombre del tipo de grupo de recursos de Hola.

    d. Hola **Plan de hospedaje** , escriba **consumo previsto**.

    e. Hola **ubicación** cuadro de ubicación de tipo hello.

    f. En **Cuenta de almacenamiento**, seleccione una cuenta de almacenamiento existente o cree una nueva. Una cuenta de almacenamiento se usa internamente para la función hello.

    ![Introducción de los datos de configuración de Function App](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. Haga clic en **Crear**.  
    se crea la aplicación de la función de Hello.

8. En el panel izquierdo de hello, haga clic en **más servicios**y, a continuación, Hola siguientes:
    
    a. Hola **filtro** , escriba **servicios de aplicaciones**.
    
    b. Haga clic en **App Services**. 

    ![Vínculo de "Más servicios" en el panel izquierdo de Hola](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. En la lista hello de servicios de aplicaciones, haga clic en nombre de Hola de aplicación de la función de hello.  
    se abre la página de aplicación de función de Hola.

10. En el panel izquierdo de hello, haga clic en **nueva función**y, a continuación, Hola siguientes: 

    a. Hola **lenguaje** lista, seleccione **C#**.
    
    b. En la matriz de Hola de iconos de plantilla, seleccione **QueueTrigger CSharp**.

    c. Hola **el nombre de la función** , escriba un nombre para la función.

    d. Hola **nombre de la cola** cuadro, escriba el nombre de definición de trabajo de transformación de datos.

    e. En **conexión de la cuenta de almacenamiento**, haga clic en **nueva**y, a continuación, seleccione cuenta de hello correspondiente toohello trabajo de transformación de datos.  
        Tome nota del nombre de la conexión de Hola. se requiere nombre de Hello más adelante en hello Azure función.

       ![Creación de una función de C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    f. Haga clic en **Crear**.  
    Hola **función** abre la ventana.

11. Hola **función** ventana, ejecute _.csx_ de archivos y, a continuación, Hola siguientes:

    a. Pegue el siguiente código de hello:

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

    b. Reemplace **STORAGE_CONNECTIONNAME** en la línea 11 por la conexión de cuenta de almacenamiento (consulte el punto 8c).

    c. En hello esquina superior izquierda, haga clic en **guardar**.

    ![Función Guardar](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. toocomplete Hola (función), agregue un archivo más haciendo Hola siguiente:

    a. Haga clic en **View files** (Ver archivos).

       ![Hola vínculo "Ver archivos"](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    b. Haga clic en **Agregar**.
    
    c. Escriba **project.json** y presione Entrar.
    
    d. Hola **project.json** de archivo, pegue el siguiente código de hello:

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

    e. Haga clic en **Guardar**.

Acaba de crear una función de Azure. Esta función se desencadena cada vez que se genere un nuevo blob por trabajo de transformación de datos de Hola.

## <a name="next-steps"></a>Pasos siguientes

[Usar los datos de tootransform de interfaz de usuario de administrador de datos de StorSimple](storsimple-data-manager-ui.md)
