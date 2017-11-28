---
title: "supervisar trabajos de análisis de transmisiones de aaaProgrammatically | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprogrammatically supervisar trabajos de análisis de transmisiones creados mediante las API de REST, SDK de Azure o PowerShell."
keywords: "supervisión de .net monitor, supervisión de trabajos, aplicación de supervisión"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 44a9c29c2161ee81ea76ece4646a8691bf5d5b48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="bcd9b-104">Creación de supervisión de trabajos de Análisis de transmisiones mediante programación</span><span class="sxs-lookup"><span data-stu-id="bcd9b-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="bcd9b-105">Este artículo se demuestra cómo tooenable supervisión para un trabajo de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-105">This article demonstrates how tooenable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="bcd9b-106">Los trabajos de Stream Analytics creados a través de las API de REST, el SDK de Azure o PowerShell no tienen habilitada la supervisión de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="bcd9b-107">Puede habilitarlo manualmente en hello portal de Azure desde la página del Monitor del trabajo toohello y al hacer clic en hello Habilitar botón o se puede automatizar este proceso siguiendo los pasos de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-107">You can manually enable it in hello Azure portal by going toohello job’s Monitor page and clicking hello Enable button or you can automate this process by following hello steps in this article.</span></span> <span data-ttu-id="bcd9b-108">Hola datos de supervisión se mostrará en el área de las métricas de Hola de hello portal de Azure para el trabajo de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-108">hello monitoring data will show up in hello Metrics area of hello Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcd9b-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bcd9b-109">Prerequisites</span></span>

<span data-ttu-id="bcd9b-110">Antes de comenzar este proceso, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="bcd9b-110">Before you begin this process, you must have hello following:</span></span>

* <span data-ttu-id="bcd9b-111">Visual Studio 2017 o 2015</span><span class="sxs-lookup"><span data-stu-id="bcd9b-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="bcd9b-112">[SDK de .NET para Azure](https://azure.microsoft.com/downloads/) descargado e instalado</span><span class="sxs-lookup"><span data-stu-id="bcd9b-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="bcd9b-113">Un trabajo de análisis de transmisiones existente que necesita toohave supervisión habilitada</span><span class="sxs-lookup"><span data-stu-id="bcd9b-113">An existing Stream Analytics job that needs toohave monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="bcd9b-114">Creación de un proyecto</span><span class="sxs-lookup"><span data-stu-id="bcd9b-114">Create a project</span></span>

1. <span data-ttu-id="bcd9b-115">Cree una aplicación de consola .NET de Visual Studio C#.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="bcd9b-116">Hola Package Manager Console, siguiente ejecución Hola comandos paquetes de NuGet tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-116">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="bcd9b-117">Hello primero uno es hello Azure Stream Analytics administración .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-117">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="bcd9b-118">Hello segunda es hello Azure SDK del Monitor que se usará supervisión tooenable.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-118">hello second one is hello Azure Monitor SDK that will be used tooenable monitoring.</span></span> <span data-ttu-id="bcd9b-119">Hello en último lugar uno es cliente de Azure Active Directory de Hola que se usará para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-119">hello last one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="bcd9b-120">Agregar Hola siguiente archivo App.config de appSettings sección toohello.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-120">Add hello following appSettings section toohello App.config file.</span></span>
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   <span data-ttu-id="bcd9b-121">Reemplace los valores para *SubscriptionId* y *ActiveDirectoryTenantId* por sus identificadores de inquilino y de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="bcd9b-122">Puede obtener estos valores mediante la ejecución de hello siguiente cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bcd9b-122">You can get these values by running hello following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="bcd9b-123">Agregue Hola siguiente mediante el archivo de código fuente de toohello de instrucciones (Program.cs) en el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-123">Add hello following using statements toohello source file (Program.cs) in hello project.</span></span>
   
   ```
     using System;
     using System.Configuration;
     using System.Threading;
     using Microsoft.Azure;
     using Microsoft.Azure.Management.Insights;
     using Microsoft.Azure.Management.Insights.Models;
     using Microsoft.Azure.Management.StreamAnalytics;
     using Microsoft.Azure.Management.StreamAnalytics.Models;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
   ```
5. <span data-ttu-id="bcd9b-124">Agregue un método auxiliar de autenticación:</span><span class="sxs-lookup"><span data-stu-id="bcd9b-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="bcd9b-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="bcd9b-125">public static string GetAuthorizationHeader()</span></span>
   
         {
             AuthenticationResult result = null;
             var thread = new Thread(() =>
             {
                 try
                 {
                     var context = new AuthenticationContext(
                         ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
                         ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
   
                     result = context.AcquireToken(
                         resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                         clientId: ConfigurationManager.AppSettings["AsaClientId"],
                         redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
                         promptBehavior: PromptBehavior.Always);
                 }
                 catch (Exception threadEx)
                 {
                     Console.WriteLine(threadEx.Message);
                 }
             });
   
             thread.SetApartmentState(ApartmentState.STA);
             thread.Name = "AcquireTokenThread";
             thread.Start();
             thread.Join();
   
             if (result != null)
             {
                 return result.AccessToken;
             }
   
             throw new InvalidOperationException("Failed tooacquire token");
     <span data-ttu-id="bcd9b-126">}</span><span class="sxs-lookup"><span data-stu-id="bcd9b-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="bcd9b-127">Creación de clientes de administración</span><span class="sxs-lookup"><span data-stu-id="bcd9b-127">Create management clients</span></span>

<span data-ttu-id="bcd9b-128">Hello código siguiente configurará las variables necesarias de Hola y los clientes de administración.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-128">hello following code will set up hello necessary variables and management clients.</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials =
        new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader());

    Uri resourceManagerUri = new
    Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    // Create Stream Analytics and Insights management client
    StreamAnalyticsManagementClient streamAnalyticsClient = new
    StreamAnalyticsManagementClient(aadTokenCredentials, resourceManagerUri);
    InsightsManagementClient insightsClient = new
    InsightsManagementClient(aadTokenCredentials, resourceManagerUri);

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="bcd9b-129">Habilitación de supervisión para un trabajo de Stream Analytics existente</span><span class="sxs-lookup"><span data-stu-id="bcd9b-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="bcd9b-130">habilita la supervisión para el código siguiente Hola un **existente** trabajo de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-130">hello following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="bcd9b-131">primera parte del código de hello de Hello realiza una solicitud GET con información de tooretrieve de servicio de análisis de transmisiones de hello acerca de trabajo de análisis de transmisiones de hello concreto.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-131">hello first part of hello code performs a GET request against hello Stream Analytics service tooretrieve information about hello particular Stream Analytics job.</span></span> <span data-ttu-id="bcd9b-132">Usa hello *identificador* propiedad (recuperada de la solicitud de obtención de hello) como un parámetro para el método Put Hola Hola segunda mitad de código de hello, que envía una solicitud PUT toohello visión supervisión del servicio tooenable para hello análisis de transmisiones trabajo.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-132">It uses hello *Id* property (retrieved from hello GET request) as a parameter for hello Put method in hello second half of hello code, which sends a PUT request toohello Insights service tooenable monitoring for hello Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="bcd9b-133">Si previamente ha habilitado la supervisión de un trabajo de análisis de transmisiones diferentes, ya sea mediante Hola portal de Azure, o mediante programación a través de Hola por debajo del código, **se recomienda que proporcione Hola que ha utilizado al mismo nombre de cuenta de almacenamiento, habilitado previamente de supervisión.**</span><span class="sxs-lookup"><span data-stu-id="bcd9b-133">If you have previously enabled monitoring for a different Stream Analytics job, either through hello Azure portal or programmatically via hello below code, **we recommend that you provide hello same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="bcd9b-134">cuenta de almacenamiento de Hello es región toohello vinculado que creó el trabajo de análisis de transmisiones en no específicamente toohello dicho trabajo.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-134">hello storage account is linked toohello region that you created your Stream Analytics job in, not specifically toohello job itself.</span></span>
> 
> <span data-ttu-id="bcd9b-135">Análisis de transmisiones de todos los trabajos (y todos los demás recursos de Azure) en esa misma región comparten esta toostore de cuenta de almacenamiento que los datos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account toostore monitoring data.</span></span> <span data-ttu-id="bcd9b-136">Si proporciona una cuenta de almacenamiento diferentes, pueden producir efectos secundarios imprevistos Hola de supervisión de los otros trabajos de análisis de transmisiones u otros recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-136">If you provide a different storage account, it might cause unintended side effects in hello monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="bcd9b-137">nombre de cuenta de almacenamiento de Hola que usar tooreplace `<YOUR STORAGE ACCOUNT NAME>` en el siguiente código de hello debe ser una cuenta de almacenamiento que se encuentra en hello misma suscripción que el trabajo de análisis de transmisiones de Hola que va a habilitar la supervisión de.</span><span class="sxs-lookup"><span data-stu-id="bcd9b-137">hello storage account name that you use tooreplace `<YOUR STORAGE ACCOUNT NAME>` in hello following code should be a storage account that is in hello same subscription as hello Stream Analytics job that you are enabling monitoring for.</span></span>
> 
> 

    // Get an existing Stream Analytics job
    JobGetParameters jobGetParameters = new JobGetParameters()
    {
        PropertiesToExpand = "inputs,transformation,outputs"
    };
    JobGetResponse jobGetResponse = streamAnalyticsClient.StreamingJobs.Get(resourceGroupName, streamAnalyticsJobName, jobGetParameters);

    // Enable monitoring
    ServiceDiagnosticSettingsPutParameters insightPutParameters = new ServiceDiagnosticSettingsPutParameters()
    {
            Properties = new ServiceDiagnosticSettings()
            {
                StorageAccountName = "<YOUR STORAGE ACCOUNT NAME>"
            }
    };
    insightsClient.ServiceDiagnosticSettingsOperations.Put(jobGetResponse.Job.Id, insightPutParameters);



## <a name="get-support"></a><span data-ttu-id="bcd9b-138">Obtención de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="bcd9b-138">Get support</span></span>

<span data-ttu-id="bcd9b-139">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="bcd9b-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcd9b-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bcd9b-140">Next steps</span></span>

* [<span data-ttu-id="bcd9b-141">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="bcd9b-141">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bcd9b-142">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bcd9b-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bcd9b-143">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="bcd9b-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bcd9b-144">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="bcd9b-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bcd9b-145">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bcd9b-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

