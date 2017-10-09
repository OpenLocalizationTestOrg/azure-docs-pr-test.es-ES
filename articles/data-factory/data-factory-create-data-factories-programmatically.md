---
title: aaaCreate las canalizaciones de datos mediante el uso de Azure SDK para .NET | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooprogrammatically crear, supervisar y administrar factorías de datos de Azure mediante el SDK de generador de datos."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a>Creación, supervisión y administración de factorías de datos de Azure mediante el SDK de .NET de Azure Data Factory
## <a name="overview"></a>Información general
Puede crear, supervisar y administrar factorías de datos de Azure mediante programación con el SDK de .NET de la factoría de datos. Este artículo contiene un tutorial que puede seguir toocreate una aplicación de consola .NET de ejemplo que crea y supervisa una factoría de datos. 

> [!NOTE]
> Este artículo no cubre Hola todas las API de .NET del generador de datos. Para obtener documentación completa sobre la API de .NET para Data Factory, consulte la [referencia de API de .NET de Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1). 

## <a name="prerequisites"></a>Requisitos previos
* Visual Studio 2012, 2013 o 2015
* Descargue e instale el [SDK de .NET de Azure](http://azure.microsoft.com/downloads/).
* Azure PowerShell. Siga las instrucciones de [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo tooinstall Azure PowerShell en el equipo. Usar PowerShell de Azure toocreate una aplicación de Azure Active Directory.

### <a name="create-an-application-in-azure-active-directory"></a>Creación de una aplicación en Azure Active Directory
Crear una aplicación de Azure Active Directory, cree una entidad de servicio para la aplicación hello y asignar toohello **colaborador de la factoría de datos** rol.

1. Inicie **PowerShell**.
2. Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta.

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con. Reemplace  **&lt;NameOfAzureSubscription** &gt; con el nombre de Hola de su suscripción de Azure.

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > Tenga en cuenta hacia abajo **SubscriptionId** y **TenantId** de salida de hello de este comando.

5. Crear un grupo de recursos de Azure denominado **ADFTutorialResourceGroup** ejecutando Hola siguiente comando en hello PowerShell.

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    Si ya existe el grupo de recursos de hello, especifique si tooupdate se (Y) o mantener un nivel tan (N).

    Si utiliza un grupo de recursos diferente, necesita toouse Hola nombre de su grupo de recursos en lugar de ADFTutorialResourceGroup en este tutorial.
6. Cree una aplicación de Azure Active Directory.

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    Si se producen Hola tras error, especifique una URL distinta y vuelva a ejecutar el comando de Hola.
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. Crear Hola la entidad de servicio de AD.

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. Agregar servicio principal toohello **colaborador de la factoría de datos** rol.

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. Obtener el identificador de la aplicación hello.

    ```PowerShell
    $azureAdApplication 
    ```
    Anote el identificador de la aplicación de hello (applicationID) de salida de hello.

Debe tener los cuatro valores siguientes de estos pasos:

* Id. de inquilino
* Id. de suscripción
* Identificador de aplicación
* Contraseña (especificada en el primer comando de hello)

## <a name="walkthrough"></a>Tutorial
En el tutorial de hello, se crea una factoría de datos con una canalización que contiene una actividad de copia. Hello actividad de copia copia los datos desde una carpeta en su carpeta de tooanother de almacenamiento de blobs de Azure en hello mismo almacenamiento de blobs. 

Hola actividad de copia realiza el movimiento de datos de hello en Data Factory de Azure. actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable. Vea [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo para obtener más información acerca de la actividad de copia de Hola.

1. Con Visual Studio 2012, 2013 o 2015, cree una aplicación de consola .NET de C#.
   1. Inicie **Visual Studio** 2012/2013/2015.
   2. Haga clic en **archivo**, seleccione demasiado**New**y haga clic en **proyecto**.
   3. Expanda **Plantillas** y seleccione **Visual C#**. En este tutorial, se usa C# pero puede usar cualquier lenguaje .NET.
   4. Seleccione **aplicación de consola** de lista de Hola de tipos de proyecto en hello derecho.
   5. Escriba **DataFactoryAPITestApp** para hello nombre.
   6. Seleccione **C:\ADFGetStarted** para hello ubicación.
   7. Haga clic en **Aceptar** proyecto de hello toocreate.
2. Haga clic en **herramientas**, seleccione demasiado**Administrador de paquetes de NuGet**y haga clic en **Package Manager Console**.
3. Hola **Package Manager Console**, Hola lo siguiente:
   1. Ejecute hello después el paquete de comando tooinstall factoría de datos:`Install-Package Microsoft.Azure.Management.DataFactories`
   2. Ejecute hello después el paquete de Azure Active Directory tooinstall command (usar API de Active Directory en el código de hello):`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`
4. Reemplace el contenido de Hola de **App.config** archivo de proyecto de hello con hello siguen contenido: 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. En el archivo App.Config de hello, actualice los valores de  **&lt;Id. de aplicación&gt;**,  **&lt;contraseña&gt;**,  **&lt; Id. de suscripción&gt;**, y  **&lt;identificador de inquilino&gt;**  con sus propios valores.
6. Agregue Hola siguiente **con** instrucciones toohello **Program.cs** archivo de proyecto de Hola.

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. Agregar Hola después el código que crea una instancia de **DataPipelineManagementClient** clase toohello **Main** método. Utilice este objeto toocreate una factoría de datos, un servicio vinculado, los conjuntos de datos de entrada y salida y una canalización. También se pueden utilizar este sectores de toomonitor de objeto de un conjunto de datos en tiempo de ejecución.

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Reemplazar el valor de Hola de **resourceGroupName** con el nombre de Hola de su grupo de recursos de Azure. Puede crear un grupo de recursos con hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.
   >
   > Actualizar nombre de hello toobe de fábrica (dataFactoryName) de datos único. Nombre de la factoría de datos de hello debe ser único globalmente. Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.
7. Agregar Hola después el código que crea un **factoría de datos** toohello **Main** método.

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. Agregar Hola después el código que crea una **servicio vinculado de almacenamiento de Azure** toohello **Main** método.

   > [!IMPORTANT]
   > Reemplace **storageaccountname** y **accountkey** por el nombre y la clave de su cuenta de Azure Storage.

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. Agregar Hola después el código que crea **conjuntos de datos de entrada y salida** toohello **Main** método.

    Hola **FolderPath** de blob de entrada de Hola se establece demasiado**adftutorial /** donde **adftutorial** es Hola nombre del contenedor de hello en el almacenamiento de blobs. Si este contenedor no existe en el almacenamiento de blobs de Azure, crear un contenedor con este nombre: **adftutorial** y cargar un contenedor de toohello del archivo de texto.

    Hola FolderPath para hello de salida blob se establece en: **adftutorial/apifactoryoutput / {Slice}** donde **segmento** es calculada dinámicamente hello en función de valor de **SliceStart**(fecha y hora de cada sector de inicio).

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. Agregue los siguiente Hola código que **creará y activará una canalización** toohello **Main** método. Esta canalización tiene un elemento **CopyActivity** que toma **BlobSource** como origen y **BlobSink** como receptor.

    Hola actividad de copia realiza el movimiento de datos de hello en Data Factory de Azure. actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable. Vea [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo para obtener más información acerca de la actividad de copia de Hola.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. Agregar Hola después código toohello **Main** conjunto de datos de salida de estado de hello tooget la forma de un segmento de datos de Hola. Solo se espera un segmento en este ejemplo.

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. **(opcional)**  Siguiente de Hola de agregar código tooget ejecutar detalles para un toohello de segmento de datos **Main** método.

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. Agregar Hola siguiendo el método auxiliar utilizado por hello **Main** método toohello **programa** clase. Este método abre un cuadro de diálogo que le permite ofrecer **nombre de usuario** y **contraseña** que usar toolog en tooAzure portal.

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. Hola el Explorador de soluciones, expanda el proyecto de hello: **DataFactoryAPITestApp**, haga clic en **referencias**y haga clic en **Agregar referencia**. Seleccione la casilla del ensamblado de `System.Configuration` y haga clic en **Aceptar**.
15. Compile la aplicación de consola de Hola. Haga clic en **generar** en el menú de Hola y haga clic en **generar solución**.
16. Confirme que hay al menos un archivo en el contenedor de adftutorial hello en el almacenamiento de blobs de Azure. Si no es así, crear archivo Emp.txt en el Bloc de notas con hello después de contenido y cargarlo toohello adftutorial contenedor.

    ```
    John, Doe
    Jane, Doe
    ```
17. Ejecutar el ejemplo hello haciendo clic en **depurar** -> **Iniciar depuración** en el menú de Hola. Cuando vea hello **obtención de detalles de un segmento de datos de la serie**, espere unos minutos y presione **ENTRAR**.
18. Use Hola tooverify portal Azure ese factoría de datos de hello **APITutorialFactory** se crea con hello siguientes artefactos:
    * Servicio vinculado: **AzureStorageLinkedService**
    * Conjunto de datos: **DatasetBlobSource** y **DatasetBlobDestination**.
    * Canalización: **PipelineBlobSample**
19. Compruebe que se crea un archivo de salida en hello **apifactoryoutput** carpeta Hola **adftutorial** contenedor.

## <a name="get-a-list-of-failed-data-slices"></a>Obtener una lista de segmentos de datos con errores 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a>Pasos siguientes
Vea Hola siguiente ejemplo para crear una canalización mediante el SDK de .NET que copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure: 

- [Crear una canalización de datos de toocopy de almacenamiento de blobs tooSQL base de datos](data-factory-copy-activity-tutorial-using-dotnet-api.md)
