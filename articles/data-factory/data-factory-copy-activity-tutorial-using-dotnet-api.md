---
title: "Tutorial: Crear una canalización con la actividad de copia mediante la API de NET | Microsoft Docs"
description: "En este tutorial, se crea una canalización de Data Factory de Azure con una actividad de copia mediante la API de .NET."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a>Tutorial: crear una canalización con la actividad de copia mediante la API de NET
> [!div class="op_single_selector"]
> * [Introducción y requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Asistente para copia](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Plantilla de Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API DE REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API de .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

En este artículo, aprenderá cómo toouse [API de .NET](https://portal.azure.com) toocreate una factoría de datos con una canalización que copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure. Si es nuevo tooAzure factoría de datos, lea hello [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo antes de realizar este tutorial.   

En este tutorial, creará una canalización con una actividad en ella: la actividad de copia. actividad de copia de Hello copia datos de un almacén de datos de datos admitidos almacén tooa receptor admitidos. Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable. Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).

pero cualquier canalización puede tener más de una actividad. Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> Para obtener documentación completa sobre la API de .NET para Data Factory, consulte la [referencia de API de .NET de Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).
> 
> canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa. Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Requisitos previos
* Vaya a través de [Tutorial de introducción y los requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget una visión general de tutorial de Hola y Hola completa **prerequisite** pasos.
* Visual Studio 2012, 2013 o 2015
* Descargue e instale el [SDK de .NET de Azure](http://azure.microsoft.com/downloads/)
* Azure PowerShell. Siga las instrucciones de [cómo tooinstall y configurar Azure PowerShell](../powershell-install-configure.md) artículo tooinstall Azure PowerShell en el equipo. Usar PowerShell de Azure toocreate una aplicación de Azure Active Directory.

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
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
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
4. Agregue los siguiente hello **appSetttings** sección toohello **App.config** archivo. Esta configuración se usa por el método de aplicación auxiliar de hello: **GetAuthorizationHeader**.

    Reemplace los valores de **&lt;Id. de aplicación&gt;**, **&lt;Contraseña&gt;**, **&lt;Id. de suscripción&gt;** e **&lt;Id. de inquilino&gt;** por los suyos propios.

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

5. Agregue los siguiente hello **con** el archivo de código fuente de toohello de instrucciones (Program.cs) en el proyecto de Hola.

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
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Reemplazar el valor de Hola de **resourceGroupName** con el nombre de Hola de su grupo de recursos de Azure.
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

    Una factoría de datos puede tener una o más canalizaciones. Una canalización puede tener una o más actividades. Por ejemplo, una toocopy de datos de actividad de copia de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight un tootransform de script de Hive datos de salida de tooproduct de datos de entrada. Puede empezar con la creación de factoría de datos de hello en este paso.
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

    Crear servicios vinculados en un toolink de factoría de datos almacenan sus datos y se factoría de datos de toohello de servicios de proceso. En este tutorial, no se usa ningún servicio de proceso, como Azure HDInsight o Azure Data Lake Analytics. Se usan dos almacenes de datos del tipo Azure Storage (origen) y Azure SQL Database (destino). 

    Por lo tanto, se crean dos servicios vinculados llamados AzureStorageLinkedService y AzureSqlLinkedService del tipo AzureStorage y AzureSqlDatabase.  

    Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure. Esta cuenta de almacenamiento es hello uno en el que se creó un contenedor y cargar datos de hello como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
9. Agregar Hola después el código que crea una **servicio vinculado de SQL Azure** toohello **Main** método.

   > [!IMPORTANT]
   > Reemplace **servername**, **databasename**, **username** y **password** por los nombres del servidor de Azure SQL, de la base de datos, del usuario y de la contraseña.

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure. datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos. Crear tabla emp de hello en esta base de datos como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
10. Agregar Hola después el código que crea **conjuntos de datos de entrada y salida** toohello **Main** método.

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    En el paso anterior de hello, crear servicios vinculados toolink su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure. En este paso, definirá dos conjuntos de datos con el nombre InputDataset y OutputDataset que representan la entrada y los datos de salida que se almacenan en almacenes de datos de Hola que hace referencia AzureStorageLinkedService y AzureSqlLinkedService respectivamente.

    servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure. Y conjunto de datos de blob de entrada de hello (InputDataset) especifica contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.  

    De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure. Y conjunto de datos de tabla SQL (OututDataset) especifica la tabla de Hola Hola Hola de toowhich de base de datos se copian datos desde almacenamiento de blobs de Hola de salida de hello.

    En este paso, creará un conjunto de datos denominado InputDataset que apunta a un archivo blob tooa (emp.txt) en la carpeta raíz de Hola de un contenedor de blobs (adftutorial) en hello representado por hello AzureStorageLinkedService vinculado servicio de almacenamiento de Azure. Si no especifica un valor para el nombre de archivo de hello (o puede omitirla), datos de todos los blobs en la carpeta de entrada de hello son destino toohello copiada. En este tutorial, especifique un valor para el nombre de archivo de Hola.    

    En este paso se crea un conjunto de datos de salida denominado **OutputDataset**. Este conjunto de datos señala tooa table de SQL de base de datos de SQL Azure de hello representado por **AzureSqlLinkedService**.
11. Agregue los siguiente Hola código que **creará y activará una canalización** toohello **Main** método. En este paso, creará una canalización con una **actividad de copia** que utiliza **InputDataset** como entrada y **OutputDataset** como salida.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

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
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    Tenga en cuenta Hola siguientes puntos:
   
    - En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**. Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md). En las soluciones de Data Factory, también puede usar [actividades de transformación de datos](data-factory-data-transformation-activities.md).
    - Entrada de actividad hello se establece demasiado**InputDataset** y salida de actividad hello se establece demasiado**OutputDataset**. 
    - Hola **typeProperties** sección, **BlobSource** se especifica como tipo de origen de Hola y **SqlSink** se especifica como el tipo de receptor de Hola. Para obtener una lista completa de los almacenes de datos compatibles con la actividad de copia de hello como orígenes y receptores, vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn cómo almacenar toouse datos compatibles especificados como un origen/receptor, haga clic en el vínculo hello en la tabla de Hola.  
   
    Actualmente, el conjunto de datos de salida es qué unidades Hola programación. En este tutorial, el conjunto de datos de salida es tooproduce configurado un segmento una vez cada hora. canalización de Hello tiene una hora de inicio y la hora de finalización que son un día separado, lo que es de 24 horas. Por lo tanto, 24 segmentos del conjunto de datos de salida generados por la canalización de Hola.
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

13. Agregar código tooget ejecutar detalles para un toohello de segmento de datos siguientes de Hola **Main** método.

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
            }
        );

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

14. Agregar Hola siguiendo el método auxiliar utilizado por hello **Main** método toohello **programa** clase.

    > [!NOTE] 
    > Cuando copie y pegue el siguiente código de hello, asegúrese de que ese Hola copiado el código está en hello como Hola método Main de mismo nivel.

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

15. En hello en el Explorador de soluciones, expanda el proyecto de hello (DataFactoryAPITestApp), haga clic en **referencias**y haga clic en **Agregar referencia**. Active la casilla del ensamblado **System.Configuration**. Después, haga clic en **Aceptar**.
16. Compile la aplicación de consola de Hola. Haga clic en **generar** en el menú de Hola y haga clic en **generar solución**.
17. Confirme que hay al menos un archivo en hello **adftutorial** contenedor en el almacenamiento de blobs de Azure. Si no es así, cree **Emp.txt** de archivos en el Bloc de notas con hello siguen contenido y cargarlo toohello adftutorial contenedor.

    ```
    John, Doe
    Jane, Doe
    ```
18. Ejecutar el ejemplo hello haciendo clic en **depurar** -> **Iniciar depuración** en el menú de Hola. Cuando vea hello **obtención de detalles de un segmento de datos de la serie**, espere unos minutos y presione **ENTRAR**.
19. Use Hola tooverify portal Azure ese factoría de datos de hello **APITutorialFactory** se crea con hello siguientes artefactos:
   * Servicio vinculado: **LinkedService_AzureStorage**
   * Conjunto de datos: **InputDataset** y **OutputDataset**.
   * Canalización: **PipelineBlobSample**
20. Compruebe que se crean los registros de empleados Hola dos en hello **emp** tabla Hola especifica la base de datos SQL de Azure.

## <a name="next-steps"></a>Pasos siguientes
Para obtener documentación completa sobre la API de .NET para Data Factory, consulte la [referencia de API de .NET de Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).

En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia. Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn acerca de cómo almacenan datos toocopy de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola.

