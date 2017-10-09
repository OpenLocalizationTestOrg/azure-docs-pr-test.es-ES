---
title: "aaaManagement .NET SDK v1.x para análisis de transmisiones de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: d205c388880e3d9c2ca5df218f4b68abac8c9780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a>Administración .NET SDK v1.x: configurar y trabajos de análisis de ejecución mediante Hola API de análisis de transmisiones de Azure para .NET
Obtenga información acerca de cómo tooset seguridad y trabajos de análisis de ejecución mediante API de análisis de transmisiones de Hola para usar .NET Hola administración .NET SDK. Configure un proyecto, cree orígenes de entrada y salida, transformaciones, e inicie y detenga trabajos. En los trabajos de análisis puede transmitir datos desde el almacenamiento de blobs o desde un centro de eventos.

Vea hello [documentación de referencia de administración de API de análisis de transmisiones de Hola para .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).

Análisis de transmisiones de Azure es un servicio completamente administrado, lo que proporciona el procesamiento de eventos de baja latencia, alta disponibilidad, escalable y complejos en la transmisión de datos en la nube de Hola. Análisis de transmisiones permite que los clientes tooset la transmisión por secuencias de flujos de datos de tooanalyze de trabajos y les permite toodrive cerca de análisis en tiempo real.  

> [!NOTE]
> El código de ejemplo de este artículo todavía usa una versión heredada (1.x) del SDK de .NET de administración de Azure Stream Analytics. Para el código de ejemplo con la versión actualizada de SDK de hello, visite [Hola Use .NET SDK de administración de análisis de transmisiones](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este artículo, debe tener el siguiente hello:

* Instale Visual Studio 2017 o 2015.
* Descargue e instale el [SDK de .NET de Azure](https://azure.microsoft.com/downloads/).
* Cree un grupo de recursos de Azure en su suscripción. Hola aquí te mostramos una secuencia de comandos de PowerShell de Azure de ejemplo. Para obtener información sobre Azure PowerShell, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* Configurar un origen de entrada y salida toouse de destino. Para obtener más instrucciones, consulte [agregar entradas](stream-analytics-add-inputs.md) tooset una entrada de ejemplo y [agregar resultados](stream-analytics-add-outputs.md) tooset la salida de ejemplo.

## <a name="set-up-a-project"></a>Configuración de un proyecto
toocreate un trabajo de análisis usar hello API de análisis de secuencia para. NET, primero configura el proyecto.

1. Cree una aplicación de consola .NET de Visual Studio C#.
2. Hola Package Manager Console, siguiente ejecución Hola comandos paquetes de NuGet tooinstall Hola. Hello primero uno es hello Azure Stream Analytics administración .NET SDK. Hello segunda es cliente de Azure Active Directory de Hola que se usará para la autenticación.
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. Agregue los siguiente hello **appSettings** archivo App.config de sección toohello:
   
        <appSettings>
          <!--CSM Prod related values-->
          <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
          <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
          <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
          <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION" />
          <add key="ActiveDirectoryTenantId" value="YOU TENANT ID" />
        </appSettings>

    Reemplace los valores para **SubscriptionId** y **ActiveDirectoryTenantId** por sus identificadores de inquilino y de suscripción de Azure. Puede obtener estos valores mediante la ejecución de hello siguiente cmdlet de PowerShell de Azure:

        Get-AzureAccount

4. Agregue Hola después de referencia en el archivo .csproj:

        <Reference Include="System.Configuration" />

1. Agregue los siguiente hello **con** el archivo de código fuente de toohello de instrucciones (Program.cs) en el proyecto de hello:
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. Agregue un método de autenticación auxiliar:

   ```   
   private static async Task<string> GetAuthorizationHeader()
   {
       var context = new AuthenticationContext(
           ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
           ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);

        AuthenticationResult result = await context.AcquireTokenASync(
           resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
           clientId: ConfigurationManager.AppSettings["AsaClientId"],
           redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
           promptBehavior: PromptBehavior.Always);

        if (result != null)
            return result.AccessToken;

       throw new InvalidOperationException("Failed tooacquire token");
   }
   ```  

## <a name="create-a-stream-analytics-management-client"></a>Cree un cliente de administración de Análisis de transmisiones
A **StreamAnalyticsManagementClient** objeto permite toomanage Hola hello y trabajo trabajo componentes, como entrada, salida y transformación.

Agregar Hola sigue el principio de toohello de código de hello **Main** método:

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";
    string streamAnalyticsInputName = "<YOUR JOB INPUT NAME>";
    string streamAnalyticsOutputName = "<YOUR JOB OUTPUT NAME>";
    string streamAnalyticsTransformationName = "<YOUR JOB TRANSFORMATION NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
        ConfigurationManager.AppSettings["SubscriptionId"],
        GetAuthorizationHeader().Result);

    // Create Stream Analytics management client
    StreamAnalyticsManagementClient client = new StreamAnalyticsManagementClient(aadTokenCredentials);

Hola **resourceGroupName** valor de la variable debe ser Hola igual Hola nombre de recurso de hello grupo se crea o se ha seleccionado en los pasos de requisitos previos de Hola.

aspecto de presentación de credencial tooautomate Hola de creación de trabajos, consulte demasiado[autenticar una entidad de servicio con el Administrador de recursos de Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Hello las secciones restantes de este artículo se suponen que este código está al principio de Hola de hello **Main** método.

## <a name="create-a-stream-analytics-job"></a>Creación de un trabajo de Análisis de transmisiones
Hello código siguiente crea un trabajo de análisis de transmisiones en el grupo de recursos de Hola que haya definido. Se agregarán más adelante un trabajo de toohello de entrada, salida y transformación.

    // Create a Stream Analytics job
    JobCreateOrUpdateParameters jobCreateParameters = new JobCreateOrUpdateParameters()
    {
        Job = new Job()
        {
            Name = streamAnalyticsJobName,
            Location = "<LOCATION>",
            Properties = new JobProperties()
            {
                EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Adjust,
                Sku = new Sku()
                {
                    Name = "Standard"
                }
            }
        }
    };

    JobCreateOrUpdateResponse jobCreateResponse = client.StreamingJobs.CreateOrUpdate(resourceGroupName, jobCreateParameters);


## <a name="create-a-stream-analytics-input-source"></a>Creación de un origen de entrada de Análisis de transmisiones
Hello código siguiente crea un origen de entrada de análisis de transmisiones con el tipo de origen de entrada de blob de Hola y serialización de CSV. toocreate un origen de entrada de concentrador de eventos, use **EventHubStreamInputDataSource** en lugar de **BlobStreamInputDataSource**. De forma similar, puede personalizar el tipo de serialización de Hola Hola de origen de entrada.

    // Create a Stream Analytics input source
    InputCreateOrUpdateParameters jobInputCreateParameters = new InputCreateOrUpdateParameters()
    {
        Input = new Input()
        {
            Name = streamAnalyticsInputName,
            Properties = new StreamInputProperties()
            {
                Serialization = new CsvSerialization
                {
                    Properties = new CsvSerializationProperties
                    {
                        Encoding = "UTF8",
                        FieldDelimiter = ","
                    }
                },
                DataSource = new BlobStreamInputDataSource
                {
                    Properties = new BlobStreamInputDataSourceProperties
                    {
                        StorageAccounts = new StorageAccount[]
                        {
                            new StorageAccount()
                            {
                                AccountName = "<YOUR STORAGE ACCOUNT NAME>",
                                AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
                            }
                        },
                        Container = "samples",
                        PathPattern = ""
                    }
                }
            }
        }
    };

    InputCreateOrUpdateResponse inputCreateResponse =
        client.Inputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobInputCreateParameters);

Orígenes de entrada, ya sea de almacenamiento de blobs o un concentrador de eventos, son tooa relacionados de trabajo específico. toouse Hola mismo origen de entrada para los distintos trabajos, debe llamar al método hello nuevo y especifique un nombre de trabajo diferente.

## <a name="test-a-stream-analytics-input-source"></a>Prueba del origen de entrada de Análisis de transmisiones
Hola **TestConnection** pruebas método si el trabajo de análisis de transmisiones de hello es capaz de tooconnect toohello de entrada de origen, así como otro toohello específico de aspectos de entrada de tipo de origen. Por ejemplo, en hello blob origen de entrada que creó en un paso anterior, método hello comprobará que nombre de cuenta de almacenamiento de Hola y par de claves puede ser usado tooconnect toohello cuenta de almacenamiento, así como comprobar que existe ese contenedor especificado Hola.

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a>Creación de un destino de salida de Análisis de transmisiones
Crear un destino de salida es un origen de entrada de análisis de transmisiones de toocreating muy similar. Como orígenes de entrada, los destinos de salida son tooa relacionados de trabajo específico. toouse Hola mismo destino de salida para los distintos trabajos, debe llamar al método hello nuevo y especifique un nombre de trabajo diferente.

Hola siguiente código crea un destino de salida (base de datos de SQL Azure). Puede personalizar el tipo de datos del destino de salida de Hola o tipo de serialización.

    // Create a Stream Analytics output target
    OutputCreateOrUpdateParameters jobOutputCreateParameters = new OutputCreateOrUpdateParameters()
    {
        Output = new Output()
        {
            Name = streamAnalyticsOutputName,
            Properties = new OutputProperties()
            {
                DataSource = new SqlAzureOutputDataSource()
                {
                    Properties = new SqlAzureOutputDataSourceProperties()
                    {
                        Server = "<YOUR DATABASE SERVER NAME>",
                        Database = "<YOUR DATABASE NAME>",
                        User = "<YOUR DATABASE LOGIN>",
                        Password = "<YOUR DATABASE LOGIN PASSWORD>",
                        Table = "<YOUR DATABASE TABLE NAME>"
                    }
                }
            }
        }
    };

    OutputCreateOrUpdateResponse outputCreateResponse =
        client.Outputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobOutputCreateParameters);

## <a name="test-a-stream-analytics-output-target"></a>Prueba de un destino de salida de Análisis de transmisiones
Un destino de los resultados del análisis de transmisiones también tiene hello **TestConnection** método para probar las conexiones.

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a>Creación de una transformación de Análisis de transmisiones
Hello código siguiente crea una transformación de análisis de transmisiones con consulta Hola "seleccionar * de entrada" y especifica una unidad de streaming tooallocate de trabajo de análisis de transmisiones de Hola. Para obtener más información sobre el ajuste de las unidades de streaming, consulte [Escalación de trabajos de Análisis de transmisiones](stream-analytics-scale-jobs.md).

    // Create a Stream Analytics transformation
    TransformationCreateOrUpdateParameters transformationCreateParameters = new TransformationCreateOrUpdateParameters()
    {
        Transformation = new Transformation()
        {
            Name = streamAnalyticsTransformationName,
            Properties = new TransformationProperties()
            {
                StreamingUnits = 1,
                Query = "select * from Input"
            }
        }
    };

    var transformationCreateResp =
        client.Transformations.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, transformationCreateParameters);

Al igual que la entrada y salida, una transformación también es trabajo de análisis de transmisiones específico toohello relacionados que se creó en.

## <a name="start-a-stream-analytics-job"></a>Inicio de un trabajo de Análisis de transmisiones
Después de crear un trabajo de análisis de transmisiones y su las entradas, salidas y transformación, puede iniciar el trabajo de Hola Hola que realiza la llamada **iniciar** método.

Hola siguiente código de ejemplo inicia un trabajo de análisis de transmisiones con una salida personalizada inicio tiempo conjunto tooDecember 12, 2012, 12:12:12 UTC:

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a>Detención de un trabajo de Análisis de transmisiones
Puede detener un trabajo de análisis de transmisiones de ejecución que realiza la llamada hello **detener** método.

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a>Eliminación de un trabajo de Análisis de transmisiones
Hola **eliminar** método eliminará trabajo hello, así como Hola subyacente recursos secundarios, incluidos las entradas, salidas y transformación de trabajo de Hola.

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a>Obtención de soporte técnico
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
Ha aprendido Fundamentos de hello del uso de un toocreate del SDK de .NET y ejecutar trabajos de análisis. toolearn más información, vea Hola recursos siguientes:

* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [SDK de .NET de administración de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn889315.aspx)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
