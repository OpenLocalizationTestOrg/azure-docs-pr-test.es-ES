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
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a>Creación de supervisión de trabajos de Análisis de transmisiones mediante programación

Este artículo se demuestra cómo tooenable supervisión para un trabajo de análisis de transmisiones. Los trabajos de Stream Analytics creados a través de las API de REST, el SDK de Azure o PowerShell no tienen habilitada la supervisión de forma predeterminada. Puede habilitarlo manualmente en hello portal de Azure desde la página del Monitor del trabajo toohello y al hacer clic en hello Habilitar botón o se puede automatizar este proceso siguiendo los pasos de hello en este artículo. Hola datos de supervisión se mostrará en el área de las métricas de Hola de hello portal de Azure para el trabajo de análisis de transmisiones.

## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar este proceso, debe tener el siguiente hello:

* Visual Studio 2017 o 2015
* [SDK de .NET para Azure](https://azure.microsoft.com/downloads/) descargado e instalado
* Un trabajo de análisis de transmisiones existente que necesita toohave supervisión habilitada

## <a name="create-a-project"></a>Creación de un proyecto

1. Cree una aplicación de consola .NET de Visual Studio C#.
2. Hola Package Manager Console, siguiente ejecución Hola comandos paquetes de NuGet tooinstall Hola. Hello primero uno es hello Azure Stream Analytics administración .NET SDK. Hello segunda es hello Azure SDK del Monitor que se usará supervisión tooenable. Hello en último lugar uno es cliente de Azure Active Directory de Hola que se usará para la autenticación.
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. Agregar Hola siguiente archivo App.config de appSettings sección toohello.
   
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
   Reemplace los valores para *SubscriptionId* y *ActiveDirectoryTenantId* por sus identificadores de inquilino y de suscripción de Azure. Puede obtener estos valores mediante la ejecución de hello siguiente cmdlet de PowerShell:
   
   ```
   Get-AzureAccount
   ```
4. Agregue Hola siguiente mediante el archivo de código fuente de toohello de instrucciones (Program.cs) en el proyecto de Hola.
   
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
5. Agregue un método auxiliar de autenticación:
   
     public static string GetAuthorizationHeader()
   
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
     }

## <a name="create-management-clients"></a>Creación de clientes de administración

Hello código siguiente configurará las variables necesarias de Hola y los clientes de administración.

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a>Habilitación de supervisión para un trabajo de Stream Analytics existente

habilita la supervisión para el código siguiente Hola un **existente** trabajo de análisis de transmisiones. primera parte del código de hello de Hello realiza una solicitud GET con información de tooretrieve de servicio de análisis de transmisiones de hello acerca de trabajo de análisis de transmisiones de hello concreto. Usa hello *identificador* propiedad (recuperada de la solicitud de obtención de hello) como un parámetro para el método Put Hola Hola segunda mitad de código de hello, que envía una solicitud PUT toohello visión supervisión del servicio tooenable para hello análisis de transmisiones trabajo.

>[!WARNING]
>Si previamente ha habilitado la supervisión de un trabajo de análisis de transmisiones diferentes, ya sea mediante Hola portal de Azure, o mediante programación a través de Hola por debajo del código, **se recomienda que proporcione Hola que ha utilizado al mismo nombre de cuenta de almacenamiento, habilitado previamente de supervisión.**
> 
> cuenta de almacenamiento de Hello es región toohello vinculado que creó el trabajo de análisis de transmisiones en no específicamente toohello dicho trabajo.
> 
> Análisis de transmisiones de todos los trabajos (y todos los demás recursos de Azure) en esa misma región comparten esta toostore de cuenta de almacenamiento que los datos de supervisión. Si proporciona una cuenta de almacenamiento diferentes, pueden producir efectos secundarios imprevistos Hola de supervisión de los otros trabajos de análisis de transmisiones u otros recursos de Azure.
> 
> nombre de cuenta de almacenamiento de Hola que usar tooreplace `<YOUR STORAGE ACCOUNT NAME>` en el siguiente código de hello debe ser una cuenta de almacenamiento que se encuentra en hello misma suscripción que el trabajo de análisis de transmisiones de Hola que va a habilitar la supervisión de.
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



## <a name="get-support"></a>Obtención de soporte técnico

Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes

* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

