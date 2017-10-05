---
title: "Supervisión de trabajos de Stream Analytics mediante programación | Microsoft Docs"
description: "Obtenga información sobre cómo supervisar los trabajos de Stream Analytics creados a través de las API de REST, el SDK de Azure o PowerShell."
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
ms.openlocfilehash: 0d39e77316a03a705586af3ba970a7be1208ec85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="cb822-104">Creación de supervisión de trabajos de Análisis de transmisiones mediante programación</span><span class="sxs-lookup"><span data-stu-id="cb822-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="cb822-105">En este artículo se demuestra cómo habilitar la supervisión de un trabajo de Análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="cb822-105">This article demonstrates how to enable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="cb822-106">Los trabajos de Stream Analytics creados a través de las API de REST, el SDK de Azure o PowerShell no tienen habilitada la supervisión de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cb822-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="cb822-107">Puede habilitarla manualmente en Azure Portal dirigiéndose a la página Supervisión del trabajo y haciendo clic en el botón Habilitar, o bien puede automatizar este proceso siguiendo los pasos que se describen en este artículo.</span><span class="sxs-lookup"><span data-stu-id="cb822-107">You can manually enable it in the Azure portal by going to the job’s Monitor page and clicking the Enable button or you can automate this process by following the steps in this article.</span></span> <span data-ttu-id="cb822-108">Los datos de supervisión se mostrarán en el área Métricas de Azure Portal para el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="cb822-108">The monitoring data will show up in the Metrics area of the Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb822-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cb822-109">Prerequisites</span></span>

<span data-ttu-id="cb822-110">Antes de empezar este proceso, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cb822-110">Before you begin this process, you must have the following:</span></span>

* <span data-ttu-id="cb822-111">Visual Studio 2017 o 2015</span><span class="sxs-lookup"><span data-stu-id="cb822-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="cb822-112">[SDK de .NET para Azure](https://azure.microsoft.com/downloads/) descargado e instalado</span><span class="sxs-lookup"><span data-stu-id="cb822-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="cb822-113">Un trabajo de Stream Analytics existente que requiera la habilitación de supervisión</span><span class="sxs-lookup"><span data-stu-id="cb822-113">An existing Stream Analytics job that needs to have monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="cb822-114">Creación de un proyecto</span><span class="sxs-lookup"><span data-stu-id="cb822-114">Create a project</span></span>

1. <span data-ttu-id="cb822-115">Cree una aplicación de consola .NET de Visual Studio C#.</span><span class="sxs-lookup"><span data-stu-id="cb822-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="cb822-116">En la consola del administrador de paquetes, ejecute los siguientes comandos para instalar los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="cb822-116">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="cb822-117">El primero es el SDK de .NET de administración de Análisis de transmisiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="cb822-117">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="cb822-118">El segundo es el SDK de Azure Monitor que se usará para habilitar la supervisión.</span><span class="sxs-lookup"><span data-stu-id="cb822-118">The second one is the Azure Monitor SDK that will be used to enable monitoring.</span></span> <span data-ttu-id="cb822-119">El último es el cliente de Azure Active Directory que se usará para autenticación.</span><span class="sxs-lookup"><span data-stu-id="cb822-119">The last one is the Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="cb822-120">Agregue la siguiente sección appSettings al archivo App.config:</span><span class="sxs-lookup"><span data-stu-id="cb822-120">Add the following appSettings section to the App.config file.</span></span>
   
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
   <span data-ttu-id="cb822-121">Reemplace los valores para *SubscriptionId* y *ActiveDirectoryTenantId* por sus identificadores de inquilino y de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="cb822-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="cb822-122">Para obtener estos valores, ejecute el siguiente cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cb822-122">You can get these values by running the following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="cb822-123">Agregue las siguientes instrucciones using al archivo de origen (Program.cs) en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="cb822-123">Add the following using statements to the source file (Program.cs) in the project.</span></span>
   
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
5. <span data-ttu-id="cb822-124">Agregue un método auxiliar de autenticación:</span><span class="sxs-lookup"><span data-stu-id="cb822-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="cb822-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="cb822-125">public static string GetAuthorizationHeader()</span></span>
   
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
   
             throw new InvalidOperationException("Failed to acquire token");
     <span data-ttu-id="cb822-126">}</span><span class="sxs-lookup"><span data-stu-id="cb822-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="cb822-127">Creación de clientes de administración</span><span class="sxs-lookup"><span data-stu-id="cb822-127">Create management clients</span></span>

<span data-ttu-id="cb822-128">El código siguiente configurará las variables y los clientes de administración necesarios.</span><span class="sxs-lookup"><span data-stu-id="cb822-128">The following code will set up the necessary variables and management clients.</span></span>

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="cb822-129">Habilitación de supervisión para un trabajo de Stream Analytics existente</span><span class="sxs-lookup"><span data-stu-id="cb822-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="cb822-130">El código siguiente habilitará la supervisión de un trabajo de Stream Analytics **existente**.</span><span class="sxs-lookup"><span data-stu-id="cb822-130">The following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="cb822-131">La primera parte del código realiza una solicitud GET en el servicio Análisis de transmisiones para recuperar información sobre el trabajo de Análisis de transmisiones en concreto.</span><span class="sxs-lookup"><span data-stu-id="cb822-131">The first part of the code performs a GET request against the Stream Analytics service to retrieve information about the particular Stream Analytics job.</span></span> <span data-ttu-id="cb822-132">Usa la propiedad *Id* (recuperada de la solicitud GET) como parámetro del método Put en la segunda mitad del código que envía una solicitud PUT al servicio Insights para habilitar la supervisión para el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="cb822-132">It uses the *Id* property (retrieved from the GET request) as a parameter for the Put method in the second half of the code, which sends a PUT request to the Insights service to enable monitoring for the Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="cb822-133">Si previamente ha habilitado la supervisión de otro trabajo de Stream Analytics, a través del Azure Portal o mediante programación con el siguiente código, **es recomendable proporcionar el mismo nombre de cuenta de almacenamiento que usó cuando habilitó anteriormente la supervisión.**</span><span class="sxs-lookup"><span data-stu-id="cb822-133">If you have previously enabled monitoring for a different Stream Analytics job, either through the Azure portal or programmatically via the below code, **we recommend that you provide the same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="cb822-134">La cuenta de almacenamiento está vinculada a la región en la que se ha creado el trabajo de Stream Analytics, no específicamente al trabajo.</span><span class="sxs-lookup"><span data-stu-id="cb822-134">The storage account is linked to the region that you created your Stream Analytics job in, not specifically to the job itself.</span></span>
> 
> <span data-ttu-id="cb822-135">Todos los trabajos de Stream Analytics (y todos los demás recursos de Azure) de esa misma región comparten esta cuenta de almacenamiento para almacenar los datos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="cb822-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account to store monitoring data.</span></span> <span data-ttu-id="cb822-136">Si proporciona otra cuenta de almacenamiento, puede provocar efectos secundarios no deseados en la supervisión de sus otros trabajos de Stream Analytics u otros recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="cb822-136">If you provide a different storage account, it might cause unintended side effects in the monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="cb822-137">El nombre de la cuenta de almacenamiento utilizado para reemplazar `<YOUR STORAGE ACCOUNT NAME>` en el siguiente código debe ser una cuenta de almacenamiento que esté en la misma suscripción que el trabajo de Stream Analytics para el que está habilitando la supervisión.</span><span class="sxs-lookup"><span data-stu-id="cb822-137">The storage account name that you use to replace `<YOUR STORAGE ACCOUNT NAME>` in the following code should be a storage account that is in the same subscription as the Stream Analytics job that you are enabling monitoring for.</span></span>
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



## <a name="get-support"></a><span data-ttu-id="cb822-138">Obtención de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="cb822-138">Get support</span></span>

<span data-ttu-id="cb822-139">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="cb822-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb822-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb822-140">Next steps</span></span>

* [<span data-ttu-id="cb822-141">Introducción a Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cb822-141">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="cb822-142">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cb822-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="cb822-143">Escalación de trabajos de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cb822-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="cb822-144">Referencia del lenguaje de consulta de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cb822-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="cb822-145">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cb822-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

