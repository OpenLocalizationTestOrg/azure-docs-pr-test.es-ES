---
title: aaaUse .NET SDK para trabajos de administrador de datos de Microsoft Azure StorSimple | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse .NET SDK toolaunch Administrador de datos de StorSimple trabajos (vista previa privada)"
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
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b07fe64369574c994fd28d42786aa02dca435ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a>Use Hola .net SDK de transformación de datos tooinitiate (Private Preview)

## <a name="overview"></a>Información general

Este artículo explica cómo puede usar la característica de transformación de datos de hello en hello StorSimple Data Manager servicio tootransform los datos del dispositivo StorSimple. Hello transformados consume datos de, a continuación, otros servicios de Azure en la nube de Hola. artículo de Hello tiene también una toohelp tutorial crear un trabajo de transformación de datos de una tooinitiate de aplicación de consola de .NET de ejemplo y, a continuación, realizar un seguimiento de finalización.

## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar, asegúrese de que dispone de:
*   Un sistema con Visual Studio 2012, 2013, 2015 o 2017 instalados.
*   Azure Powershell instalado. [Descarga de Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Trabajo de transformación de datos Hola de configuración configuración tooinitialize (instrucciones tooobtain estas opciones se incluyen aquí).
*   Una definición del trabajo que se ha configurado correctamente en un recurso de datos híbridos de un grupo de recursos.
*   Todos los archivos DLL de hello necesario. Descargar estos archivos DLL de hello [repositorio de GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).
*   `Get-ConfigurationParams.ps1`[script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) del repositorio de github de Hola.

## <a name="step-by-step"></a>Paso a paso

Realizar Hola siguiendo los pasos toouse .NET toolaunch un trabajo de transformación de datos.

1. parámetros de configuración de tooretrieve Hola Hola lo siguiente:
    1. Descargar hello `Get-ConfigurationParams.ps1` desde un script de repositorio de github de hello en `C:\DataTransformation` ubicación.
    1. Ejecute hello `Get-ConfigurationParams.ps1` script desde el repositorio de github de Hola. Escriba el siguiente comando de hello:

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        Se pueden pasar en todos los valores de hello ActiveDirectoryKey y AppName.


2. Este script genera Hola siguientes valores:
    * id. de cliente
    * Id. de inquilino
    * Claves de Active Directory (igual que uno que Arri Hola)
    * Id. de suscripción

3. Con Visual Studio 2012, 2013 o 2015, cree una aplicación de consola .NET de C#.

    1. Inicie **Visual Studio 2012/2013/2015**.
    1. Haga clic en **archivo**, seleccione demasiado**New**y haga clic en **proyecto**.
    2. Expanda **Plantillas** y seleccione **Visual C#**.
    3. Seleccione **aplicación de consola** de lista de Hola de tipos de proyecto en hello derecho.
    4. Escriba **DataTransformationApp** para hello **nombre**.
    5. Seleccione **C:\DataTransformation** para hello **ubicación**.
    6. Haga clic en **Aceptar** proyecto de hello toocreate.

4.  Ahora, agregue todos los archivos DLL está presente en hello [dll](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) carpeta como **referencias** en proyecto de Hola que ha creado. archivos dll de toodownload hello, Hola siguientes:

    1. En Visual Studio, vaya demasiado**Vista > Explorador de soluciones**.
    1. Haga clic en hello flecha toohello a la izquierda del proyecto de aplicación de la transformación de datos. Haga clic en **referencias** y, a continuación, haga clic en demasiado**Agregar referencia**.
    2. Toohello ubicación de carpeta de paquetes de saludo, seleccione todos los archivos DLL de Hola y haga clic en **agregar**y, a continuación, haga clic en **Aceptar**.

5. Agregue los siguiente hello **con** el archivo de código fuente de toohello de instrucciones (Program.cs) en el proyecto de Hola.

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. Hola siguiente código inicializa la instancia de trabajo de transformación de datos de Hola. Agregue esta Hola **método Main**. Reemplace los valores de hello de parámetros de configuración obtenida anteriormente. Conecte en valores de hello de **nombre del grupo de recursos** y **nombre de recurso de datos híbrida**. Hola **nombre del grupo de recursos** es hello que hospeda el recurso de datos híbrida hello en qué Hola se configuró la definición del trabajo.

    ```
    // Setup hello configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize hello Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. Especificar Hola ejecutan parámetros con qué Hola definición del trabajo debe toobe

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    O BIEN

    Si desea parámetros de definición de trabajo de toochange Hola durante el tiempo de ejecución, a continuación, agregar Hola siguiente código:

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of hello volume on hello StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require hello latest existing backup toobe picked else use TakeNow tootrigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of hello StorSimple device.
        DeviceName = "device-name",
        // Name of hello container in Azure storage where hello files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) toobe applied on files under hello root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of hello volume on StorSimple device on which hello relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. Tras la inicialización de hello, agregue Hola después código tootrigger un trabajo de transformación de datos en la definición del trabajo Hola. Conectar Hola adecuado **nombre de la definición de trabajo**.

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. Este trabajo carga Hola coincide con los archivos presentes en el directorio raíz de hello en el contenedor especificado de hello StorSimple volumen toohello. Cuando se carga un archivo, se quita un mensaje en cola hello (Hola misma cuenta de almacenamiento como contenedor de hello) con hello en el mismo nombre como definición de trabajo de Hola. Este mensaje se puede usar como un tooinitiate desencadenador adicionales de procesamiento del archivo de Hola.

10. Una vez que se ha desencadenado el trabajo de hello, agregue Hola siguiendo el trabajo de hello tootrack de código para la finalización.

    ```
    Job jobDetails = null;

    // Poll hello job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for hello status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of hello job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // toohold hello console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a>Pasos siguientes

[Usar los datos de interfaz de usuario de administrador de datos de StorSimple tootransform](storsimple-data-manager-ui.md).
