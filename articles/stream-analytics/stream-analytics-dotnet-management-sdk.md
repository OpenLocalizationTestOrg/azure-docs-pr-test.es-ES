---
title: "aaaManagement .NET SDK para el análisis de transmisiones de Azure | Documentos de Microsoft"
description: "Introducción al uso del SDK de .NET de administración de Análisis de transmisiones Obtenga información acerca de cómo tooset una copia de seguridad y ejecutar trabajos de análisis. Cree un proyecto, entradas, salidas y transformaciones."
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
ms.openlocfilehash: 507c11938bc5bf2249a2e41f6bcc076db8ead3f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="a4add-106">SDK de .NET de administración: Configurar y ejecutar trabajos de análisis mediante Hola API de análisis de transmisiones de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="a4add-106">Management .NET SDK: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="a4add-107">Obtenga información acerca de cómo tooset seguridad y trabajos de análisis de ejecución mediante API de análisis de transmisiones de Hola para usar .NET Hola administración .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="a4add-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="a4add-108">Configure un proyecto, cree orígenes de entrada y salida, transformaciones, e inicie y detenga trabajos.</span><span class="sxs-lookup"><span data-stu-id="a4add-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="a4add-109">En los trabajos de análisis puede transmitir datos desde el almacenamiento de blobs o desde un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="a4add-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="a4add-110">Vea hello [documentación de referencia de administración de API de análisis de transmisiones de Hola para .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4add-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="a4add-111">Análisis de transmisiones de Azure es un servicio completamente administrado, lo que proporciona el procesamiento de eventos de baja latencia, alta disponibilidad, escalable y complejos en la transmisión de datos en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4add-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="a4add-112">Análisis de transmisiones permite que los clientes tooset la transmisión por secuencias de flujos de datos de tooanalyze de trabajos y les permite toodrive cerca de análisis en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="a4add-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="a4add-113">Código de ejemplo de Hola en este artículo hemos actualizado con la versión de SDK de .NET de Azure Stream Analytics administración v2.x.</span><span class="sxs-lookup"><span data-stu-id="a4add-113">We have updated hello sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="a4add-114">Para código de ejemplo con hello usa lagecy (1.x) versión del SDK, visite [usar Hola v1.x de SDK de .NET de administración de análisis de transmisiones](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span><span class="sxs-lookup"><span data-stu-id="a4add-114">For sample code using hello uses lagecy (1.x) SDK version, please see [Use hello Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4add-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a4add-115">Prerequisites</span></span>
<span data-ttu-id="a4add-116">Antes de comenzar este artículo, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="a4add-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="a4add-117">Instale Visual Studio 2017 o 2015.</span><span class="sxs-lookup"><span data-stu-id="a4add-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="a4add-118">Descargue e instale el [SDK de .NET de Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a4add-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="a4add-119">Cree un grupo de recursos de Azure en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="a4add-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="a4add-120">Hola aquí te mostramos una secuencia de comandos de PowerShell de Azure de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a4add-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="a4add-121">Para obtener información sobre Azure PowerShell, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4add-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="a4add-122">Configurar un origen de entrada y salida toouse de destino.</span><span class="sxs-lookup"><span data-stu-id="a4add-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="a4add-123">Para obtener más instrucciones, consulte [agregar entradas](stream-analytics-add-inputs.md) tooset una entrada de ejemplo y [agregar resultados](stream-analytics-add-outputs.md) tooset la salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a4add-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="a4add-124">Configuración de un proyecto</span><span class="sxs-lookup"><span data-stu-id="a4add-124">Set up a project</span></span>
<span data-ttu-id="a4add-125">toocreate un trabajo de análisis usar hello API de análisis de secuencia para. NET, primero configura el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a4add-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="a4add-126">Cree una aplicación de consola .NET de Visual Studio C#.</span><span class="sxs-lookup"><span data-stu-id="a4add-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="a4add-127">Hola Package Manager Console, siguiente ejecución Hola comandos paquetes de NuGet tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="a4add-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="a4add-128">Hello primero uno es hello Azure Stream Analytics administración .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="a4add-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="a4add-129">Hello segunda es para la autenticación de cliente de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4add-129">hello second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="a4add-130">Agregue los siguiente hello **appSettings** archivo App.config de sección toohello:</span><span class="sxs-lookup"><span data-stu-id="a4add-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="a4add-131">Reemplace los valores para **SubscriptionId** y **ActiveDirectoryTenantId** por sus identificadores de inquilino y de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4add-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="a4add-132">Puede obtener estos valores mediante la ejecución de hello siguiente cmdlet de PowerShell de Azure:</span><span class="sxs-lookup"><span data-stu-id="a4add-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="a4add-133">Agregue Hola después de referencia en el archivo .csproj:</span><span class="sxs-lookup"><span data-stu-id="a4add-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="a4add-134">Agregue los siguiente hello **con** el archivo de código fuente de toohello de instrucciones (Program.cs) en el proyecto de hello:</span><span class="sxs-lookup"><span data-stu-id="a4add-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="a4add-135">Agregue un método de autenticación auxiliar:</span><span class="sxs-lookup"><span data-stu-id="a4add-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="a4add-136">Cree un cliente de administración de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a4add-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="a4add-137">A **StreamAnalyticsManagementClient** objeto permite toomanage Hola hello y trabajo trabajo componentes, como entrada, salida y transformación.</span><span class="sxs-lookup"><span data-stu-id="a4add-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="a4add-138">Agregar Hola sigue el principio de toohello de código de hello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="a4add-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

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

<span data-ttu-id="a4add-139">Hola **resourceGroupName** valor de la variable debe ser Hola igual Hola nombre de recurso de hello grupo se crea o se ha seleccionado en los pasos de requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4add-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="a4add-140">aspecto de presentación de credencial tooautomate Hola de creación de trabajos, consulte demasiado[autenticar una entidad de servicio con el Administrador de recursos de Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="a4add-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="a4add-141">Hello las secciones restantes de este artículo se suponen que este código está al principio de Hola de hello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="a4add-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="a4add-142">Creación de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a4add-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="a4add-143">Hello código siguiente crea un trabajo de análisis de transmisiones en el grupo de recursos de Hola que haya definido.</span><span class="sxs-lookup"><span data-stu-id="a4add-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="a4add-144">Se agregarán más adelante un trabajo de toohello de entrada, salida y transformación.</span><span class="sxs-lookup"><span data-stu-id="a4add-144">You will add an input, output, and transformation toohello job later.</span></span>

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

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="a4add-145">Creación de un origen de entrada de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a4add-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="a4add-146">Hello código siguiente crea un origen de entrada de análisis de transmisiones con el tipo de origen de entrada de blob de Hola y serialización de CSV.</span><span class="sxs-lookup"><span data-stu-id="a4add-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="a4add-147">toocreate un origen de entrada de concentrador de eventos, use **EventHubStreamInputDataSource** en lugar de **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="a4add-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="a4add-148">De forma similar, puede personalizar el tipo de serialización de Hola Hola de origen de entrada.</span><span class="sxs-lookup"><span data-stu-id="a4add-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

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

<span data-ttu-id="a4add-149">Orígenes de entrada, ya sea de almacenamiento de blobs o un concentrador de eventos, son tooa relacionados de trabajo específico.</span><span class="sxs-lookup"><span data-stu-id="a4add-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="a4add-150">toouse Hola mismo origen de entrada para los distintos trabajos, debe llamar al método hello nuevo y especifique un nombre de trabajo diferente.</span><span class="sxs-lookup"><span data-stu-id="a4add-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="a4add-151">Prueba del origen de entrada de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a4add-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="a4add-152">Hola **TestConnection** pruebas método si el trabajo de análisis de transmisiones de hello es capaz de tooconnect toohello de entrada de origen, así como otro toohello específico de aspectos de entrada de tipo de origen.</span><span class="sxs-lookup"><span data-stu-id="a4add-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="a4add-153">Por ejemplo, en hello blob origen de entrada que creó en un paso anterior, método hello comprobará que nombre de cuenta de almacenamiento de Hola y par de claves puede ser usado tooconnect toohello cuenta de almacenamiento, así como comprobar que existe ese contenedor especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="a4add-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="a4add-154">Creación de un destino de salida de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a4add-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="a4add-155">Crear un destino de salida es un origen de entrada de análisis de transmisiones de toocreating muy similar.</span><span class="sxs-lookup"><span data-stu-id="a4add-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="a4add-156">Como orígenes de entrada, los destinos de salida son tooa relacionados de trabajo específico.</span><span class="sxs-lookup"><span data-stu-id="a4add-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="a4add-157">toouse Hola mismo destino de salida para los distintos trabajos, debe llamar al método hello nuevo y especifique un nombre de trabajo diferente.</span><span class="sxs-lookup"><span data-stu-id="a4add-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="a4add-158">Hola siguiente código crea un destino de salida (base de datos de SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="a4add-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="a4add-159">Puede personalizar el tipo de datos del destino de salida de Hola o tipo de serialización.</span><span class="sxs-lookup"><span data-stu-id="a4add-159">You can customize hello output target's data type and/or serialization type.</span></span>

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

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="a4add-160">Prueba de un destino de salida de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a4add-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="a4add-161">Un destino de los resultados del análisis de transmisiones también tiene hello **TestConnection** método para probar las conexiones.</span><span class="sxs-lookup"><span data-stu-id="a4add-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="a4add-162">Creación de una transformación de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a4add-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="a4add-163">Hello código siguiente crea una transformación de análisis de transmisiones con consulta Hola "seleccionar * de entrada" y especifica una unidad de streaming tooallocate de trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4add-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="a4add-164">Para obtener más información sobre el ajuste de las unidades de streaming, consulte [Escalación de trabajos de Análisis de transmisiones](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="a4add-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="a4add-165">Al igual que la entrada y salida, una transformación también es trabajo de análisis de transmisiones específico toohello relacionados que se creó en.</span><span class="sxs-lookup"><span data-stu-id="a4add-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="a4add-166">Inicio de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a4add-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="a4add-167">Después de crear un trabajo de análisis de transmisiones y su las entradas, salidas y transformación, puede iniciar el trabajo de Hola Hola que realiza la llamada **iniciar** método.</span><span class="sxs-lookup"><span data-stu-id="a4add-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="a4add-168">Hola siguiente código de ejemplo inicia un trabajo de análisis de transmisiones con una salida personalizada inicio tiempo conjunto tooDecember 12, 2012, 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="a4add-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="a4add-169">Detención de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a4add-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="a4add-170">Puede detener un trabajo de análisis de transmisiones de ejecución que realiza la llamada hello **detener** método.</span><span class="sxs-lookup"><span data-stu-id="a4add-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="a4add-171">Eliminación de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a4add-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="a4add-172">Hola **eliminar** método eliminará trabajo hello, así como Hola subyacente recursos secundarios, incluidos las entradas, salidas y transformación de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4add-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="a4add-173">Obtención de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="a4add-173">Get support</span></span>
<span data-ttu-id="a4add-174">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="a4add-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4add-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a4add-175">Next steps</span></span>
<span data-ttu-id="a4add-176">Ha aprendido Fundamentos de hello del uso de un toocreate del SDK de .NET y ejecutar trabajos de análisis.</span><span class="sxs-lookup"><span data-stu-id="a4add-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="a4add-177">toolearn más información, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a4add-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="a4add-178">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a4add-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a4add-179">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a4add-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a4add-180">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="a4add-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="a4add-181">[SDK de .NET de administración de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn889315.aspx)</span><span class="sxs-lookup"><span data-stu-id="a4add-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="a4add-182">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="a4add-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a4add-183">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a4add-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
