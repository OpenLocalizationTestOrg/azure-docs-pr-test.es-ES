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
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a><span data-ttu-id="9beed-103">Use Hola .net SDK de transformación de datos tooinitiate (Private Preview)</span><span class="sxs-lookup"><span data-stu-id="9beed-103">Use hello .Net SDK tooinitiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="9beed-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9beed-104">Overview</span></span>

<span data-ttu-id="9beed-105">Este artículo explica cómo puede usar la característica de transformación de datos de hello en hello StorSimple Data Manager servicio tootransform los datos del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9beed-105">This article explains how you can use hello data transformation feature within hello StorSimple Data Manager service tootransform StorSimple device data.</span></span> <span data-ttu-id="9beed-106">Hello transformados consume datos de, a continuación, otros servicios de Azure en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="9beed-106">hello transformed data is then consumed by other Azure services in hello cloud.</span></span> <span data-ttu-id="9beed-107">artículo de Hello tiene también una toohelp tutorial crear un trabajo de transformación de datos de una tooinitiate de aplicación de consola de .NET de ejemplo y, a continuación, realizar un seguimiento de finalización.</span><span class="sxs-lookup"><span data-stu-id="9beed-107">hello article also has a walkthrough toohelp create a sample .NET console application tooinitiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9beed-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9beed-108">Prerequisites</span></span>

<span data-ttu-id="9beed-109">Antes de comenzar, asegúrese de que dispone de:</span><span class="sxs-lookup"><span data-stu-id="9beed-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="9beed-110">Un sistema con Visual Studio 2012, 2013, 2015 o 2017 instalados.</span><span class="sxs-lookup"><span data-stu-id="9beed-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="9beed-111">Azure Powershell instalado.</span><span class="sxs-lookup"><span data-stu-id="9beed-111">Azure Powershell installed.</span></span> <span data-ttu-id="9beed-112">[Descarga de Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="9beed-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="9beed-113">Trabajo de transformación de datos Hola de configuración configuración tooinitialize (instrucciones tooobtain estas opciones se incluyen aquí).</span><span class="sxs-lookup"><span data-stu-id="9beed-113">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="9beed-114">Una definición del trabajo que se ha configurado correctamente en un recurso de datos híbridos de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9beed-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="9beed-115">Todos los archivos DLL de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="9beed-115">All hello required dlls.</span></span> <span data-ttu-id="9beed-116">Descargar estos archivos DLL de hello [repositorio de GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="9beed-116">Download these dlls from hello [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="9beed-117">`Get-ConfigurationParams.ps1`[script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) del repositorio de github de Hola.</span><span class="sxs-lookup"><span data-stu-id="9beed-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="9beed-118">Paso a paso</span><span class="sxs-lookup"><span data-stu-id="9beed-118">Step-by-step</span></span>

<span data-ttu-id="9beed-119">Realizar Hola siguiendo los pasos toouse .NET toolaunch un trabajo de transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="9beed-119">Perform hello following steps toouse .NET toolaunch a data transformation job.</span></span>

1. <span data-ttu-id="9beed-120">parámetros de configuración de tooretrieve Hola Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9beed-120">tooretrieve hello configuration parameters, do hello following steps:</span></span>
    1. <span data-ttu-id="9beed-121">Descargar hello `Get-ConfigurationParams.ps1` desde un script de repositorio de github de hello en `C:\DataTransformation` ubicación.</span><span class="sxs-lookup"><span data-stu-id="9beed-121">Download hello `Get-ConfigurationParams.ps1` from hello github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="9beed-122">Ejecute hello `Get-ConfigurationParams.ps1` script desde el repositorio de github de Hola.</span><span class="sxs-lookup"><span data-stu-id="9beed-122">Run hello `Get-ConfigurationParams.ps1` script from hello github repository.</span></span> <span data-ttu-id="9beed-123">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="9beed-123">Type hello following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="9beed-124">Se pueden pasar en todos los valores de hello ActiveDirectoryKey y AppName.</span><span class="sxs-lookup"><span data-stu-id="9beed-124">You can pass in any values for hello ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="9beed-125">Este script genera Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="9beed-125">This script outputs hello following values:</span></span>
    * <span data-ttu-id="9beed-126">id. de cliente</span><span class="sxs-lookup"><span data-stu-id="9beed-126">Client ID</span></span>
    * <span data-ttu-id="9beed-127">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="9beed-127">Tenant ID</span></span>
    * <span data-ttu-id="9beed-128">Claves de Active Directory (igual que uno que Arri Hola)</span><span class="sxs-lookup"><span data-stu-id="9beed-128">Active Directory key (same as hello one entered above)</span></span>
    * <span data-ttu-id="9beed-129">Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="9beed-129">Subscription ID</span></span>

3. <span data-ttu-id="9beed-130">Con Visual Studio 2012, 2013 o 2015, cree una aplicación de consola .NET de C#.</span><span class="sxs-lookup"><span data-stu-id="9beed-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="9beed-131">Inicie **Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="9beed-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="9beed-132">Haga clic en **archivo**, seleccione demasiado**New**y haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="9beed-132">Click **File**, point too**New**, and click **Project**.</span></span>
    2. <span data-ttu-id="9beed-133">Expanda **Plantillas** y seleccione **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="9beed-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="9beed-134">Seleccione **aplicación de consola** de lista de Hola de tipos de proyecto en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="9beed-134">Select **Console Application** from hello list of project types on hello right.</span></span>
    4. <span data-ttu-id="9beed-135">Escriba **DataTransformationApp** para hello **nombre**.</span><span class="sxs-lookup"><span data-stu-id="9beed-135">Enter **DataTransformationApp** for hello **Name**.</span></span>
    5. <span data-ttu-id="9beed-136">Seleccione **C:\DataTransformation** para hello **ubicación**.</span><span class="sxs-lookup"><span data-stu-id="9beed-136">Select **C:\DataTransformation** for hello **Location**.</span></span>
    6. <span data-ttu-id="9beed-137">Haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="9beed-137">Click **OK** toocreate hello project.</span></span>

4.  <span data-ttu-id="9beed-138">Ahora, agregue todos los archivos DLL está presente en hello [dll](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) carpeta como **referencias** en proyecto de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="9beed-138">Now, add all DLLs present in hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in hello project that you created.</span></span> <span data-ttu-id="9beed-139">archivos dll de toodownload hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9beed-139">toodownload hello dll files, do hello following:</span></span>

    1. <span data-ttu-id="9beed-140">En Visual Studio, vaya demasiado**Vista > Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="9beed-140">In Visual Studio, go too**View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="9beed-141">Haga clic en hello flecha toohello a la izquierda del proyecto de aplicación de la transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="9beed-141">Click hello arrow toohello left of Data Transformation App project.</span></span> <span data-ttu-id="9beed-142">Haga clic en **referencias** y, a continuación, haga clic en demasiado**Agregar referencia**.</span><span class="sxs-lookup"><span data-stu-id="9beed-142">Click **References** and then right-click too**Add Reference**.</span></span>
    2. <span data-ttu-id="9beed-143">Toohello ubicación de carpeta de paquetes de saludo, seleccione todos los archivos DLL de Hola y haga clic en **agregar**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9beed-143">Browse toohello location of hello packages folder, select all hello DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="9beed-144">Agregue los siguiente hello **con** el archivo de código fuente de toohello de instrucciones (Program.cs) en el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="9beed-144">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="9beed-145">Hola siguiente código inicializa la instancia de trabajo de transformación de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9beed-145">hello following code initializes hello data transformation job instance.</span></span> <span data-ttu-id="9beed-146">Agregue esta Hola **método Main**.</span><span class="sxs-lookup"><span data-stu-id="9beed-146">Add this in hello **Main method**.</span></span> <span data-ttu-id="9beed-147">Reemplace los valores de hello de parámetros de configuración obtenida anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9beed-147">Replace hello values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="9beed-148">Conecte en valores de hello de **nombre del grupo de recursos** y **nombre de recurso de datos híbrida**.</span><span class="sxs-lookup"><span data-stu-id="9beed-148">Plug in hello values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="9beed-149">Hola **nombre del grupo de recursos** es hello que hospeda el recurso de datos híbrida hello en qué Hola se configuró la definición del trabajo.</span><span class="sxs-lookup"><span data-stu-id="9beed-149">hello **Resource Group Name** is hello one that hosts hello Hybrid Data Resource on which hello job definition was configured.</span></span>

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

7. <span data-ttu-id="9beed-150">Especificar Hola ejecutan parámetros con qué Hola definición del trabajo debe toobe</span><span class="sxs-lookup"><span data-stu-id="9beed-150">Specify hello parameters with which hello job definition needs toobe run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="9beed-151">O BIEN</span><span class="sxs-lookup"><span data-stu-id="9beed-151">(OR)</span></span>

    <span data-ttu-id="9beed-152">Si desea parámetros de definición de trabajo de toochange Hola durante el tiempo de ejecución, a continuación, agregar Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="9beed-152">If you want toochange hello job definition parameters during run time, then add hello following code:</span></span>

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

8. <span data-ttu-id="9beed-153">Tras la inicialización de hello, agregue Hola después código tootrigger un trabajo de transformación de datos en la definición del trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="9beed-153">After hello initialization, add hello following code tootrigger a data transformation job on hello job definition.</span></span> <span data-ttu-id="9beed-154">Conectar Hola adecuado **nombre de la definición de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="9beed-154">Plug in hello appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="9beed-155">Este trabajo carga Hola coincide con los archivos presentes en el directorio raíz de hello en el contenedor especificado de hello StorSimple volumen toohello.</span><span class="sxs-lookup"><span data-stu-id="9beed-155">This job uploads hello matched files present under hello root directory on hello StorSimple volume toohello specified container.</span></span> <span data-ttu-id="9beed-156">Cuando se carga un archivo, se quita un mensaje en cola hello (Hola misma cuenta de almacenamiento como contenedor de hello) con hello en el mismo nombre como definición de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9beed-156">When a file is uploaded, a message is dropped in hello queue (in hello same storage account as hello container) with hello same name as hello job definition.</span></span> <span data-ttu-id="9beed-157">Este mensaje se puede usar como un tooinitiate desencadenador adicionales de procesamiento del archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9beed-157">This message can be used as a trigger tooinitiate any further processing of hello file.</span></span>

10. <span data-ttu-id="9beed-158">Una vez que se ha desencadenado el trabajo de hello, agregue Hola siguiendo el trabajo de hello tootrack de código para la finalización.</span><span class="sxs-lookup"><span data-stu-id="9beed-158">Once hello job has been triggered, add hello following code tootrack hello job for completion.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="9beed-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9beed-159">Next steps</span></span>

<span data-ttu-id="9beed-160">[Usar los datos de interfaz de usuario de administrador de datos de StorSimple tootransform](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="9beed-160">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
