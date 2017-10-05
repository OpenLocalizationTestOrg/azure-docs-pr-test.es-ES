---
title: "SDK de .NET de administración para Azure Stream Analytics | Microsoft Docs"
description: "Introducción al uso del SDK de .NET de administración de Análisis de transmisiones Aprenda a configurar y ejecutar trabajos de análisis. Cree un proyecto, entradas, salidas y transformaciones."
keywords: "SDK de .NET, API de análisis"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e93de87-0c6f-4f4b-be98-08d63f832897
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/06/2017
ms.author: jeffstok
ms.openlocfilehash: f9aa812e6e82cc0f72d0cd1fe63058e53f794775
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-the-azure-stream-analytics-api-for-net"></a><span data-ttu-id="7027d-106">SDK de .NET de administración: Configuración y ejecución de trabajos de análisis con la API de Análisis de transmisiones de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="7027d-106">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="7027d-107">Aprenda a configurar y ejecutar trabajos de análisis con la API de Stream Analytics para .NET mediante el SDK de .NET de administración.</span><span class="sxs-lookup"><span data-stu-id="7027d-107">Learn how to set up and run analytics jobs using the Stream Analytics API for .NET using the Management .NET SDK.</span></span> <span data-ttu-id="7027d-108">Configure un proyecto, cree orígenes de entrada y salida, transformaciones, e inicie y detenga trabajos.</span><span class="sxs-lookup"><span data-stu-id="7027d-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="7027d-109">En los trabajos de análisis puede transmitir datos desde el almacenamiento de blobs o desde un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="7027d-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="7027d-110">Consulte la [documentación de referencia de administración de la API de Análisis de transmisiones para .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="7027d-110">See the [management reference documentation for the Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="7027d-111">Análisis de transmisiones de Azure es un servicio totalmente administrado que proporciona un procesamiento completo de eventos de baja latencia, alta disponibilidad y escalable a través de la transmisión de datos en la nube.</span><span class="sxs-lookup"><span data-stu-id="7027d-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="7027d-112">Análisis de transmisiones permite a los clientes configurar trabajos de streaming para analizar flujos de datos y realizar análisis casi en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="7027d-112">Stream Analytics enables customers to set up streaming jobs to analyze data streams, and allows them to drive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="7027d-113">El código de ejemplo de este artículo se ha actualizado con la versión v2.x del SDK de .NET de administración de Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="7027d-113">We have updated the sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="7027d-114">Para código de ejemplo con la versión heredada (1.x) del SDK, vea [Uso del SDK v1.x de .NET de administración para Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span><span class="sxs-lookup"><span data-stu-id="7027d-114">For sample code using the uses lagecy (1.x) SDK version, please see [Use the Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7027d-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7027d-115">Prerequisites</span></span>
<span data-ttu-id="7027d-116">Antes de empezar este artículo, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7027d-116">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="7027d-117">Instale Visual Studio 2017 o 2015.</span><span class="sxs-lookup"><span data-stu-id="7027d-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="7027d-118">Descargue e instale el [SDK de .NET de Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7027d-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="7027d-119">Cree un grupo de recursos de Azure en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="7027d-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="7027d-120">A continuación se muestra un ejemplo de script de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7027d-120">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="7027d-121">Para obtener información sobre Azure PowerShell, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7027d-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered to the subscription, remove the remark symbol (#) to run the Register-AzureRMProvider cmdlet to register the provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="7027d-122">Configure un origen de entrada y un destino de salida para usar.</span><span class="sxs-lookup"><span data-stu-id="7027d-122">Set up an input source and output target to use.</span></span> <span data-ttu-id="7027d-123">Para más instrucciones, vea [Agregar entradas](stream-analytics-add-inputs.md) para configurar una entrada de muestra y [Agregar salidas](stream-analytics-add-outputs.md) para configurar una salida de muestra.</span><span class="sxs-lookup"><span data-stu-id="7027d-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) to set up a sample input and [Add Outputs](stream-analytics-add-outputs.md) to set up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="7027d-124">Configuración de un proyecto</span><span class="sxs-lookup"><span data-stu-id="7027d-124">Set up a project</span></span>
<span data-ttu-id="7027d-125">Para crear un trabajo de análisis que use la API de Análisis de transmisiones para. NET, configure primero el proyecto.</span><span class="sxs-lookup"><span data-stu-id="7027d-125">To create an analytics job use the Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="7027d-126">Cree una aplicación de consola .NET de Visual Studio C#.</span><span class="sxs-lookup"><span data-stu-id="7027d-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="7027d-127">En la consola del administrador de paquetes, ejecute los siguientes comandos para instalar los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="7027d-127">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="7027d-128">El primero es el SDK de .NET de administración de Análisis de transmisiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="7027d-128">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="7027d-129">El segundo corresponde a la autenticación de cliente de Azure.</span><span class="sxs-lookup"><span data-stu-id="7027d-129">The second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="7027d-130">Agregue la siguiente sección **appSettings** al archivo App.config:</span><span class="sxs-lookup"><span data-stu-id="7027d-130">Add the following **appSettings** section to the App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="7027d-131">Reemplace los valores para **SubscriptionId** y **ActiveDirectoryTenantId** por sus identificadores de inquilino y de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7027d-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="7027d-132">Para obtener estos valores, ejecute el siguiente cmdlet de Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7027d-132">You can get these values by running the following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="7027d-133">Agregue la siguiente referencia al archivo .csproj:</span><span class="sxs-lookup"><span data-stu-id="7027d-133">Add the following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="7027d-134">Agregue las siguientes instrucciones **using** al archivo de origen (Program.cs) en el proyecto:</span><span class="sxs-lookup"><span data-stu-id="7027d-134">Add the following **using** statements to the source file (Program.cs) in the project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="7027d-135">Agregue un método de autenticación auxiliar:</span><span class="sxs-lookup"><span data-stu-id="7027d-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="7027d-136">Cree un cliente de administración de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7027d-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="7027d-137">Un objeto **StreamAnalyticsManagementClient** le permite administrar el trabajo y los componentes del trabajo, como la entrada, la salida y la transformación.</span><span class="sxs-lookup"><span data-stu-id="7027d-137">A **StreamAnalyticsManagementClient** object allows you to manage the job and the job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="7027d-138">Agregue el siguiente código al comienzo del método **Main** :</span><span class="sxs-lookup"><span data-stu-id="7027d-138">Add the following code to the beginning of the **Main** method:</span></span>

   ```
    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamingJobName = "<YOUR STREAMING JOB NAME>";
    string inputName = "<YOUR JOB INPUT NAME>";
    string transformationName = "<YOUR JOB TRANSFORMATION NAME>";
    string outputName = "<YOUR JOB OUTPUT NAME>";
    
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    
    // Get credentials
    ServiceClientCredentials credentials = GetCredentials().Result;
    
    // Create Stream Analytics management client
    StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
    {
        SubscriptionId = ConfigurationManager.AppSettings["SubscriptionId"]
    };
   ```

<span data-ttu-id="7027d-139">El valor de la variable **resourceGroupName** debe ser el mismo que el nombre del grupo de recursos que creó o eligió en los pasos de requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="7027d-139">The **resourceGroupName** variable's value should be the same as the name of the resource group you created or picked in the prerequisite steps.</span></span>

<span data-ttu-id="7027d-140">Para automatizar el aspecto de la presentación de credenciales de creación del trabajo, consulte [Autenticación de una entidad de servicio con el Administrador de recursos de Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="7027d-140">To automate the credential presentation aspect of job creation, refer to [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="7027d-141">Las secciones restantes de este artículo suponen que este código se encuentra al comienzo del método **Main** .</span><span class="sxs-lookup"><span data-stu-id="7027d-141">The remaining sections of this article assume that this code is at the beginning of the **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="7027d-142">Creación de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7027d-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="7027d-143">El siguiente código crea un trabajo de Análisis de transmisiones bajo el grupo de recursos que ha definido.</span><span class="sxs-lookup"><span data-stu-id="7027d-143">The following code creates a Stream Analytics job under the resource group that you have defined.</span></span> <span data-ttu-id="7027d-144">Agregará una entrada, salida y transformación al trabajo más adelante.</span><span class="sxs-lookup"><span data-stu-id="7027d-144">You will add an input, output, and transformation to the job later.</span></span>

   ```
   // Create a streaming job
   StreamingJob streamingJob = new StreamingJob()
   {
       Tags = new Dictionary<string, string>()
       {
           { "Origin", ".NET SDK" },
           { "ReasonCreated", "Getting started tutorial" }
       },
       Location = "West US",
       EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
       EventsOutOfOrderMaxDelayInSeconds = 5,
       EventsLateArrivalMaxDelayInSeconds = 16,
       OutputErrorPolicy = OutputErrorPolicy.Drop,
       DataLocale = "en-US",
       CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
       Sku = new Sku()
       {
           Name = SkuName.Standard
       }
   };
   StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
   ```

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="7027d-145">Creación de un origen de entrada de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7027d-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="7027d-146">El código siguiente crea un origen de entrada de Análisis de transmisiones con el tipo de origen de entrada de blob y la serialización de CSV.</span><span class="sxs-lookup"><span data-stu-id="7027d-146">The following code creates a Stream Analytics input source with the blob input source type and CSV serialization.</span></span> <span data-ttu-id="7027d-147">Para crear un origen de entrada de centro de eventos, use **EventHubStreamInputDataSource** en lugar de **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="7027d-147">To create an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="7027d-148">De manera similar, puede personalizar el tipo de serialización del origen de entrada.</span><span class="sxs-lookup"><span data-stu-id="7027d-148">Similarly, you can customize the serialization type of the input source.</span></span>

   ```
   // Create an input
   StorageAccount storageAccount = new StorageAccount()
   {
       AccountName = "<YOUR STORAGE ACCOUNT NAME>",
       AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
   };
   Input input = new Input()
   {
       Properties = new StreamInputProperties()
       {
           Serialization = new CsvSerialization()
           {
               FieldDelimiter = ",",
               Encoding = Encoding.UTF8
           },
           Datasource = new BlobStreamInputDataSource()
           {
               StorageAccounts = new[] { storageAccount },
               Container = "<YOUR STORAGE BLOB CONTAINER>",
               PathPattern = "{date}/{time}",
               DateFormat = "yyyy/MM/dd",
               TimeFormat = "HH",
               SourcePartitionCount = 16
           }
       }
   };
   Input createInputResult = streamAnalyticsManagementClient.Inputs.CreateOrReplace(input, resourceGroupName, streamingJobName, inputName);
   ```

<span data-ttu-id="7027d-149">Los orígenes de entrada, ya sean desde el almacenamiento de blobs o un centro de eventos, están vinculados a un trabajo específico.</span><span class="sxs-lookup"><span data-stu-id="7027d-149">Input sources, whether from Blob storage or an event hub, are tied to a specific job.</span></span> <span data-ttu-id="7027d-150">Para usar el mismo origen de entrada para distintos trabajos, debe llamar nuevamente al método y especificar un nombre de trabajo distinto.</span><span class="sxs-lookup"><span data-stu-id="7027d-150">To use the same input source for different jobs, you must call the method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="7027d-151">Prueba del origen de entrada de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7027d-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="7027d-152">El método **TestConnection** prueba si el trabajo de Análisis de transmisiones puede conectarse al origen de entrada así como otros aspectos específicos para el tipo de origen de entrada.</span><span class="sxs-lookup"><span data-stu-id="7027d-152">The **TestConnection** method tests whether the Stream Analytics job is able to connect to the input source as well as other aspects specific to the input source type.</span></span> <span data-ttu-id="7027d-153">Por ejemplo, en el origen de entrada de blob que creó en un paso anterior, el método comprobará que el par de claves y el nombre de cuenta de almacenamiento se pueden usar para conectarse a la cuenta de almacenamiento, así como para comprobar que existe el contenedor especificado.</span><span class="sxs-lookup"><span data-stu-id="7027d-153">For example, in the blob input source you created in an earlier step, the method will check that the Storage account name and key pair can be used to connect to the Storage account as well as check that the specified container exists.</span></span>

   ```
   // Test the connection to the input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="7027d-154">Creación de un destino de salida de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7027d-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="7027d-155">La creación de un destino de salida es muy similar a crear un origen de entrada de Análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="7027d-155">Creating an output target is very similar to creating a Stream Analytics input source.</span></span> <span data-ttu-id="7027d-156">Al igual que los orígenes de entrada, los destinos de salida están vinculados a un trabajo específico.</span><span class="sxs-lookup"><span data-stu-id="7027d-156">Like input sources, output targets are tied to a specific job.</span></span> <span data-ttu-id="7027d-157">Para usar el mismo destino de salida para distintos trabajos, debe llamar nuevamente al método y especificar un nombre de trabajo distinto.</span><span class="sxs-lookup"><span data-stu-id="7027d-157">To use the same output target for different jobs, you must call the method again and specify a different job name.</span></span>

<span data-ttu-id="7027d-158">El siguiente código crea un destino de salida (Base de datos SQL de Azure).</span><span class="sxs-lookup"><span data-stu-id="7027d-158">The following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="7027d-159">Puede personalizar el tipo de datos y/o el tipo de serialización del destino de salida.</span><span class="sxs-lookup"><span data-stu-id="7027d-159">You can customize the output target's data type and/or serialization type.</span></span>

   ```
   // Create an output
   Output output = new Output()
   {
       Datasource = new AzureSqlDatabaseOutputDataSource()
       {
           Server = "<YOUR DATABASE SERVER NAME>",
           Database = "<YOUR DATABASE NAME>",
           User = "<YOUR DATABASE LOGIN>",
           Password = "<YOUR DATABASE LOGIN PASSWORD>",
           Table = "<YOUR DATABASE TABLE NAME>"
       }
   };
   Output createOutputResult = streamAnalyticsManagementClient.Outputs.CreateOrReplace(output, resourceGroupName, streamingJobName, outputName);
   ```

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="7027d-160">Prueba de un destino de salida de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7027d-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="7027d-161">Un destino de salida de Análisis de transmisiones también tiene el método **TestConnection** para probar conexiones.</span><span class="sxs-lookup"><span data-stu-id="7027d-161">A Stream Analytics output target also has the **TestConnection** method for testing connections.</span></span>

   ```
   // Test the connection to the output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="7027d-162">Creación de una transformación de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7027d-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="7027d-163">El siguiente código crea una transformación de Análisis de transmisiones con la consulta "select * from Input" y especifica para asignar una unidad de streaming para el trabajo de Análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="7027d-163">The following code creates a Stream Analytics transformation with the query "select * from Input" and specifies to allocate one streaming unit for the Stream Analytics job.</span></span> <span data-ttu-id="7027d-164">Para obtener más información sobre el ajuste de las unidades de streaming, consulte [Escalación de trabajos de Análisis de transmisiones](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="7027d-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with the value you put for the 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="7027d-165">Al igual que la entrada y la salida, una transformación también está vinculada al trabajo de Stream Analytics específico en el que se creó.</span><span class="sxs-lookup"><span data-stu-id="7027d-165">Like input and output, a transformation is also tied to the specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="7027d-166">Inicio de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7027d-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="7027d-167">Después de crear un trabajo de Análisis de transmisiones y sus entradas, salidas y transformaciones, puede iniciar el trabajo si llama al método **Start** .</span><span class="sxs-lookup"><span data-stu-id="7027d-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start the job by calling the **Start** method.</span></span>

<span data-ttu-id="7027d-168">El siguiente código de ejemplo inicia un trabajo de Análisis de transmisiones con una hora de inicio de salida personalizada definida para el 12 de diciembre de 2012, 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="7027d-168">The following sample code starts a Stream Analytics job with a custom output start time set to December 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="7027d-169">Detención de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7027d-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="7027d-170">Puede detener un trabajo de Análisis de transmisiones en ejecución si llama al método **Stop** .</span><span class="sxs-lookup"><span data-stu-id="7027d-170">You can stop a running Stream Analytics job by calling the **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="7027d-171">Eliminación de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7027d-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="7027d-172">El método **Delete** eliminará el trabajo, además de los subrecursos subyacentes, incluidas las entradas, salidas y transformaciones del trabajo.</span><span class="sxs-lookup"><span data-stu-id="7027d-172">The **Delete** method will delete the job as well as the underlying sub-resources, including input(s), output(s), and transformation of the job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="7027d-173">Obtención de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="7027d-173">Get support</span></span>
<span data-ttu-id="7027d-174">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="7027d-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7027d-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7027d-175">Next steps</span></span>
<span data-ttu-id="7027d-176">Ha aprendido los conceptos básicos del uso de un SDK de .NET para crear y ejecutar trabajos de análisis.</span><span class="sxs-lookup"><span data-stu-id="7027d-176">You've learned the basics of using a .NET SDK to create and run analytics jobs.</span></span> <span data-ttu-id="7027d-177">Para obtener más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="7027d-177">To learn more, see the following:</span></span>

* [<span data-ttu-id="7027d-178">Introducción al Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="7027d-178">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7027d-179">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7027d-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7027d-180">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="7027d-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="7027d-181">[SDK de .NET de administración de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn889315.aspx)</span><span class="sxs-lookup"><span data-stu-id="7027d-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="7027d-182">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="7027d-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7027d-183">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7027d-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[azure.blob.storage]: http://azure.microsoft.com/documentation/services/storage/
[azure.blob.storage.use]: http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/

[azure.event.hubs]: http://azure.microsoft.com/services/event-hubs/
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.forum]: http://go.microsoft.com/fwlink/?LinkId=512151

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
