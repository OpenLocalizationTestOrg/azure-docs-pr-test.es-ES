---
title: "aaaUse actividades personalizadas en una canalización de factoría de datos de Azure"
description: "Obtenga información acerca de cómo las actividades personalizadas de toocreate y usarlos en una canalización del generador de datos de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a>Uso de actividades personalizadas en una canalización de Factoría de datos de Azure

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Actividad de Hive](data-factory-hive-activity.md) 
> * [Actividad de Pig](data-factory-pig-activity.md)
> * [Actividad MapReduce](data-factory-map-reduce.md)
> * [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Actividad de Spark](data-factory-spark.md)
> * [Actividad de ejecución de Batch de Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Actividad Actualizar recurso de Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Actividad de procedimiento almacenado](data-factory-stored-proc-activity.md)
> * [Actividad U-SQL de Data Lake Analytics](data-factory-usql-activity.md)
> * [Actividad personalizada de .NET](data-factory-use-custom-activities.md)

Hay dos tipos de actividades que puede usar en una canalización de Data Factory de Azure.

- [Las actividades de movimiento de datos](data-factory-data-movement-activities.md) toomove datos entre [admite almacenes de datos de origen y el receptor](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- [Las actividades de transformación de datos](data-factory-data-transformation-activities.md) datos tootransform mediante servicios como HDInsight de Azure y Azure Batch, aprendizaje automático de Azure de proceso. 

datos de toomove hacia/desde un almacén de datos que no es compatible con la factoría de datos, crear un **actividad personalizada** con su propios datos movimiento lógica y uso actividad hello en una canalización. Del mismo modo, tootransform/procesar los datos de forma que no es compatible con la factoría de datos, crear una actividad personalizada con su propia lógica de transformación de datos y utilizar la actividad hello en una canalización. 

Puede configurar una actividad personalizada toorun en un **Azure Batch** grupo de máquinas virtuales o basados en Windows **HDInsight de Azure** clúster. Si usa Azure Batch, solo puede utilizar un grupo de Azure Batch existente. Sin embargo, al utilizar HDInsight, puede utilizar un clúster de HDInsight existente o un clúster creado automáticamente cuando se solicita en tiempo de ejecución.  

Hello en el tutorial siguiente proporciona instrucciones paso a paso para crear una actividad personalizada de .NET y usar la actividad personalizada hello en una canalización. Tutorial de Hello usa un **Azure Batch** servicio vinculado. servicio vinculado de toouse un HDInsight de Azure en su lugar, cree un servicio vinculado de tipo **HDInsight** (su propio clúster de HDInsight) o **HDInsightOnDemand** (factoría de datos crea un clúster de HDInsight a petición). A continuación, configure hello de la actividad personalizada toouse servicio vinculado de HDInsight. Vea [servicios vinculados de HDInsight de Azure de uso](#use-hdinsight-compute-service) sección para obtener más información sobre el uso de la actividad personalizada hello toorun de HDInsight de Azure.

> [!IMPORTANT]
> - las actividades de .NET personalizadas Hola ejecutarán solo en clústeres de HDInsight basados en Windows. Una solución alternativa para esta limitación es toouse Hola mapa reducir actividad toorun Java código personalizado en un clúster de HDInsight basados en Linux. Otra opción es toouse un grupo de lote de Azure de las máquinas virtuales toorun actividades personalizadas en lugar de utilizar un clúster de HDInsight.
> - No es posible toouse una puerta de enlace de administración de datos de orígenes de datos de actividad personalizada tooaccess local. Actualmente, [Data Management Gateway](data-factory-data-management-gateway.md) solo admite la actividad de copia de hello y actividad de procedimiento almacenado de factoría de datos.   

## <a name="walkthrough-create-a-custom-activity"></a>Tutorial: creación de una actividad personalizada
### <a name="prerequisites"></a>Requisitos previos
* Visual Studio 2012/2013/2015
* Descargue e instale el [SDK de .NET de Azure](https://azure.microsoft.com/downloads/)

### <a name="azure-batch-prerequisites"></a>Requisitos previos de Lote de Azure
En el tutorial de hello, ejecute sus actividades personalizadas de .NET con Azure Batch como un recurso de proceso. **Lote de Azure** es una plataforma de alto rendimiento (HPC) informática eficacia en la nube de Hola y del servicio para ejecutar paralelas a gran escala. Lote de Azure programa toorun de trabajo de proceso intensivo en administrada **colección de máquinas virtuales**, y puede automáticamente escala calcular necesidades de hello toomeet de recursos de los trabajos. Vea [conceptos básicos de Azure Batch] [ batch-technical-overview] artículo para obtener una descripción detallada de hello servicio Azure Batch.

Para ver tutorial Hola, cree una cuenta de lote de Azure con un grupo de máquinas virtuales. Estos son los pasos de hello:

1. Crear un **cuenta de Azure Batch** con hello [portal de Azure](http://portal.azure.com). Para obtener instrucciones, consulte el artículo [Creación y administración de una cuenta de Azure Batch][batch-create-account].
2. Anote el nombre de la cuenta de hello Azure Batch, clave de cuenta, URI y nombre del grupo. Vaya necesitando toocreate un servicio vinculado Azure Batch.
    1. En página de inicio de hello para la cuenta de lote de Azure, verá un **URL** Hola siguiendo el formato: `https://myaccount.westus.batch.azure.com`. En este ejemplo, **myaccount** es nombre Hola de hello cuenta de lote de Azure. URI que se use en definición de servicio vinculado de hello es dirección URL de hello sin nombre Hola de cuenta de hello. Por ejemplo: `https://<region>.batch.azure.com`.
    2. Haga clic en **claves** en el menú izquierdo de Hola y Hola copia **clave de acceso principal**.
    3. toouse un grupo existente, haga clic en **grupos** en el menú de Hola y tome nota de hello **identificador** del grupo de Hola. Si no tienes un grupo existente, mueva toohello siguiente paso.     
2. Cree un **grupo de Lote de Azure**.

   1. Hola [portal de Azure](https://portal.azure.com), haga clic en **examinar** en Hola menú izquierdo y haga clic en **las cuentas por lotes**.
   2. Seleccione su hello tooopen de cuenta de Azure Batch **cuenta de lote** hoja.
   3. Haga clic en el icono **Grupos** .
   4. Hola **grupos** hoja, haga clic en el botón Agregar en la barra de herramientas de hello tooadd un grupo.
      1. Escriba un Id. de grupo de hello (Id. de grupo). Hola Nota **Id. de grupo de hello**; necesita al crear soluciones de hello factoría de datos.
      2. Especifique **Windows Server 2012 R2** para configuración de la familia de sistemas operativos de Hola.
      3. Seleccione un **plan de tarifa de nodos**.
      4. Escriba **2** como valor de hello **destino dedicado** configuración.
      5. Escriba **2** como valor de hello **Max tareas por nodo** configuración.
   5. Haga clic en **Aceptar** grupo de hello toocreate.
   6. Tome nota de hello **identificador** del grupo de Hola. 



### <a name="high-level-steps"></a>Pasos de alto nivel
Estos son los pasos de alto nivel dos Hola que realizar como parte de este tutorial: 

1. Cree una actividad personalizada que contenga una lógica de procesamiento o transformación de datos simple.
2. Cree un generador de datos de Azure con una canalización que usa la actividad personalizada hello.

### <a name="create-a-custom-activity"></a>creación de una actividad personalizada
crear una actividad personalizada. NET, toocreate una **biblioteca de clases .NET** proyecto con una clase que implementa que **IDotNetActivity** interfaz. Esta interfaz solo tiene un método, [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , y su firma es:

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


método Hello toma cuatro parámetros:

- **linkedServices**. Esta propiedad es una lista enumerable de servicios de almacenamiento de datos vinculado hace referencia a los conjuntos de datos de entrada y salida de actividad hello.   
- **datasets**. Esta propiedad es una lista enumerable de conjuntos de datos de entrada y salida de actividad hello. Puede usar este ubicaciones de parámetro tooget hello y esquemas definidos por los conjuntos de datos de entrada y salida.
- **activity**. Esta propiedad representa la actividad actual de hello. Puede ser usado tooaccess propiedades extendidas asociadas con la actividad personalizada hello. Consulte [Acceso a las propiedades extendidas](#access-extended-properties) para más información.
- **logger**. Este objeto le permite escribir comentarios de depuración que superficie en Inicio de sesión de usuario de hello para la canalización de Hola.

método Hello devuelve un diccionario que puede ser actividades personalizadas utilizadas toochain juntos en un futuro Hola. Esta característica todavía no está implementada, por lo que devuelve un diccionario vacío de método hello.  

### <a name="procedure"></a>Procedimiento
1. Cree un proyecto de **biblioteca de clases .NET** .
   <ol type="a">
     <li>Inicie <b>Visual Studio 2017</b>, <b>Visual Studio 2015</b>, <b>Visual Studio 2013</b> o <b>Visual Studio 2012</b>.</li>
     <li>Haga clic en <b>archivo</b>, seleccione demasiado<b>New</b>y haga clic en <b>proyecto</b>.</li>
     <li>Expanda <b>Plantillas</b> y seleccione <b>Visual C#</b>. En este tutorial, use C#, pero puede usar cualquier actividad personalizada .NET language toodevelop hello.</li>
     <li>Seleccione <b>biblioteca de clases</b> de lista de Hola de tipos de proyecto en hello derecho. En VS 2017, elija <b>Biblioteca de clases (.NET Framework)</b> </li>
     <li>Escriba <b>MyDotNetActivity</b> para hello <b>nombre</b>.</li>
     <li>Seleccione <b>C:\ADFGetStarted</b> para hello <b>ubicación</b>.</li>
     <li>Haga clic en <b>Aceptar</b> proyecto de hello toocreate.</li>
   </ol>
2.Haga clic en **herramientas**, seleccione demasiado**Administrador de paquetes de NuGet**y haga clic en **Package Manager Console**.
3. Hola consola de administrador de paquetes, ejecutar Hola después comando tooimport **Microsoft.Azure.Management.DataFactories**.

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Hola de importación **el almacenamiento de Azure** paquetes de NuGet en los proyectos de toohello.

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > Selector de servicio de factoría de datos requiere la versión de Hola 4.3 de WindowsAzure.Storage. Si agrega una referencia tooa una versión posterior del ensamblado de almacenamiento de Azure en el proyecto de actividad personalizada, verá un error cuando se ejecuta la actividad hello. error de hello tooresolve, consulte [Appdomain aislamiento](#appdomain-isolation) sección. 
5. Agregue los siguiente hello **mediante** archivo de código fuente de toohello las instrucciones en el proyecto de Hola.

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Cambiar el nombre del programa Hola Hola **espacio de nombres** demasiado**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Cambiar nombre de Hola de clase hello demasiado**MyDotNetActivity** y derivan de hello **IDotNetActivity** interfaz tal y como se muestra en el siguiente fragmento de código de hello:

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Hola implemente (Agregar) **Execute** método de hello **IDotNetActivity** interfaz toohello **MyDotNetActivity** Hola de clase y copia siguiendo el método de toohello de código de ejemplo.

    Hello en el ejemplo siguiente cuenta Hola número de repeticiones del término de búsqueda de hello ("Microsoft") en cada blob asociado a un segmento de datos.

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. Agregue Hola siguiendo métodos auxiliares: 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    Hola GetFolderPath método devuelve Hola ruta de acceso toohello que Hola conjunto de datos que señala la carpeta tooand Hola GetFileName devuelve Hola nombre de método hello/archivo de blob que Hola conjunto de datos de destino. Si havefolderPath se define usando variables como {Year}, {Month} devuelve {Day} etc., método hello Hola cadena tal cual sin sustituirlos con valores de tiempo de ejecución. Consulte la sección [Acceso a las propiedades extendidas](#access-extended-properties) para más información sobre cómo acceder a SliceStart, SliceEnd, etc.    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    Hola método Calculate calcula número Hola de instancias de la palabra clave de Microsoft en archivos de entrada de hello (BLOB en la carpeta de hello). término de búsqueda de Hello ("Microsoft") está codificado de forma rígida en el código de hello.
10. Compile el proyecto de Hola. Haga clic en **generar** desde el menú de Hola y haga clic en **generar solución**.

    > [!IMPORTANT]
    > Versión del conjunto 4.5.2 de .NET Framework, como .NET framework de destino de hello para el proyecto: haga clic en proyecto de Hola y haga clic en **propiedades** tooset de .NET framework de destino de Hola. Data Factory no admite actividades personalizadas que se compilaron con versiones de .NET Framework posteriores a la 4.5.2.

11. Iniciar **el Explorador de Windows**, del sistema y desplácese demasiado**bin\debug** o **bin\release** carpeta según el tipo de saludo de compilación.
12. Crear un archivo zip **MyDotNetActivity.zip** que contiene todos los archivos binarios de Hola Hola <project folder>carpeta \bin\Debug. Incluir hello **MyDotNetActivity.pdb** de archivos para que obtengan detalles adicionales, como el número de línea de código fuente de Hola que causó el problema de hello si hubo un error. 

    > [!IMPORTANT]
    > Todos los Hola archivos en el archivo zip de hello para la actividad personalizada hello debe estar en hello **nivel superior** con ningún subcarpetas.

    ![Archivos de salida binarios](./media/data-factory-use-custom-activities/Binaries.png)
14. Cree el contenedor de blobs **customactivitycontainer**, si aún no existe. 
15. Cargar MyDotNetActivity.zip como un customactivitycontainer de toohello de blob en un **general** almacenamiento de blobs de Azure (almacenamiento de blobs activos/frío) que se hace referencia mediante AzureStorageLinkedService.  

> [!IMPORTANT]
> Si agrega esta solución de tooa del proyecto de actividad de .NET en Visual Studio que contiene un proyecto de la factoría de datos y agregar un proyecto de actividad de too.NET de referencia de proyecto de aplicación de hello factoría de datos, no es necesario dos últimos pasos de la creación manual de Hola de tooperform archivo zip de Hola y cargarlo toohello almacenamiento de blobs de Azure de uso general. Cuando publique las entidades de la factoría de datos con Visual Studio, estos pasos se realizan automáticamente por el proceso de publicación de Hola. Para obtener más información, consulte la sección [Proyecto de Data Factory en Visual Studio](#data-factory-project-in-visual-studio).

## <a name="create-a-pipeline-with-custom-activity"></a>Crear una canalización con una actividad personalizada
Se ha creado una actividad personalizada y cargado el archivo zip de hello con el contenedor de blobs de tooa de los archivos binarios en una **general** cuenta de almacenamiento de Azure. En esta sección, se crea un generador de datos de Azure con una canalización que usa la actividad personalizada hello.

conjunto de datos de entrada de Hello para la actividad personalizada hello representa blobs (archivos) en carpeta de hello customactivityinput adftutorial del contenedor de en el almacenamiento de blobs de Hola. conjunto de datos de salida de Hello para la actividad de hello representa blobs de salida en la carpeta de hello customactivityoutput adftutorial del contenedor de en el almacenamiento de blobs de Hola.

Crear **file.txt** archivo con hello siguiente contenido y cargarlo demasiado**customactivityinput** carpeta de hello **adftutorial** contenedor. Crear contenedor de hello adftutorial si aún no existe. 

```
test custom activity Microsoft test custom activity Microsoft
```

carpeta de entrada de Hello corresponde tooa segmento de factoría de datos de Azure incluso si la carpeta de hello tiene dos o más archivos. Cuando se procesa cada segmento de canalización de hello, la actividad personalizada hello recorre en iteración todos los blobs de hello en la carpeta de entrada de Hola para dicho sector.

Verá un archivo con en la carpeta de hello adftutorial\customactivityoutput de salida con una o varias líneas (igual que el número de blobs en la carpeta de entrada de hello):

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


Estos son los pasos de hello que lleva a cabo en esta sección:

1. Crear una **factoría de datos**.
2. Crear **servicios vinculados** para grupo de Azure Batch Hola de máquinas virtuales en qué Hola actividad personalizada se ejecuta y Hola almacenamiento de Azure que contiene Hola blobs de entrada/salida.
3. Crear la entrada y salida **conjuntos de datos** que representan la entrada y salida de actividad personalizada hello.
4. Crear un **canalización** que usa la actividad personalizada hello.

> [!NOTE]
> Crear hello **file.txt** y cargarlo contenedor de blobs de tooa si aún no lo ha hecho. Consulte las instrucciones en la sección anterior de Hola.   

### <a name="step-1-create-hello-data-factory"></a>Paso 1: Crear la factoría de datos de Hola
1. Después de iniciar sesión toohello el portal de Azure, Hola pasos:
   1. Haga clic en **NEW** en el menú de la izquierda Hola.
   2. Haga clic en **datos + análisis** en hello **New** hoja.
   3. Haga clic en **factoría de datos** en hello **análisis de datos** hoja.
   
    ![Nuevo menú de Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. Hola **factoría de datos** hoja, escriba **CustomActivityFactory** para hello nombre. nombre de Hola Hola Azure factoría de datos debe ser único globalmente. Si recibe el error hello: **nombre de generador de datos "CustomActivityFactory" no está disponible**, cambiar nombre de Hola Hola factoría de datos (por ejemplo, **yournameCustomActivityFactory**) y pruebe a crear volver a ejecutarlo.

    ![Nueva hoja de Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. Haga clic en **NOMBRE DEL GRUPO DE RECURSOS**y seleccione un grupo de recursos existente o cree uno.
4. Compruebe que está usando Hola correcto **suscripción** y **región** donde desea Hola datos generador toobe creado.
5. Haga clic en **crear** en hello **factoría de datos** hoja.
6. Vea factoría de datos de Hola se creen en hello **panel** de hello portal de Azure.
7. Una vez creado correctamente la factoría de datos de hello, consulte hoja de la factoría de datos de hello, que muestra Hola contenido Hola factoría de datos.
    
    ![Hoja de la Factoría de datos](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a>Paso 2: Creación de servicios vinculados
Servicios vinculados vinculan almacenes de datos o generador de datos de Azure de tooan de servicios de proceso. En este paso, vincular su cuenta de almacenamiento de Azure y la factoría de datos de Azure Batch cuenta tooyour.

#### <a name="create-azure-storage-linked-service"></a>Creación de un servicio vinculado de Almacenamiento de Azure
1. Haga clic en hello **autor e implementar** icono hello **factoría de datos** hoja para **CustomActivityFactory**. Vea Hola Editor de generador de datos.
2. Haga clic en **nuevo almacén de datos** en Hola barra de comandos y elija **almacenamiento de Azure**. Debería ver Hola script JSON para crear un almacenamiento de Azure vinculada servicio en el editor de Hola.
    
    ![Nuevo almacén de datos: Azure Storage](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. Reemplace `<accountname>` con el nombre de la cuenta de almacenamiento de Azure y `<accountkey>` con la clave de acceso del programa Hola a cuenta de almacenamiento de Azure. toolearn cómo tooget el almacenamiento de tener acceso a clave, consulte [ver, copiar y regenerar almacenamiento de claves de acceso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

    ![Servicio vinculado de Azure Storage](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.

#### <a name="create-azure-batch-linked-service"></a>Creación del servicio vinculado de Lote de Azure
1. Hola Editor de generador de datos, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo proceso**y, a continuación, seleccione **Azure Batch** en el menú de Hola.

    ![Nuevo proceso: Azure Batch](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. Asegúrese de hello siguiente secuencia de comandos de cambios toohello JSON:

   1. Especifique el nombre de la cuenta de Azure Batch para hello **accountName** propiedad. Hola **URL** de hello **hoja de la cuenta de Azure Batch** en hello siguiendo el formato: `http://accountname.region.batch.azure.com`. Para hello **batchUri** propiedad Hola JSON, necesita tooremove `accountname.` de dirección URL y el uso de Hola Hola `accountname` para hello `accountName` propiedad JSON.
   2. Especificar clave de cuenta de lote de Azure de Hola para hello **accessKey** propiedad.
   3. Especifique el nombre de hello del grupo de Hola que creó como parte de los requisitos previos para hello **poolName** propiedad. También puede especificar el identificador de hello del grupo de hello en lugar del nombre de Hola de grupo de Hola de.
   4. Especifique el URI de lote de Azure para hello **batchUri** propiedad. Ejemplo: `https://westus.batch.azure.com`.  
   5. Especificar hello **AzureStorageLinkedService** para hello **linkedServiceName** propiedad.

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       Para hello **poolName** propiedad, también puede especificar el identificador de hello del grupo de hello en lugar del nombre de Hola de grupo de Hola de.

      > [!IMPORTANT]
      > Hola servicio factoría de datos no admite una opción de petición para el lote de Azure que lo hace para HDInsight. Solo puede usar su propio grupo de Lote de Azure en una factoría de datos de Azure.   
    

### <a name="step-3-create-datasets"></a>Paso 3: Creación de conjuntos de datos
En este paso, creará entrada toorepresent de conjuntos de datos y los datos de salida.

#### <a name="create-input-dataset"></a>Creación de un conjunto de datos de entrada
1. Hola **Editor** para hello factoría de datos, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo conjunto de datos**y, a continuación, seleccione **almacenamiento de blobs de Azure** desde el menú desplegable de Hola.
2. Reemplace Hola JSON en el panel derecho de hello con hello siguiente fragmento de JSON:

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   Más adelante, en este mismo tutorial, creará una canalización con la hora de inicio 2016-11-16T00:00:00Z y la de finalización 2016-11-16T05:00:00Z. Es tooproduce programada datos cada hora, por lo que hay cinco segmentos de entrada/salida (entre **00**: 00:00 -> **05**: 00:00).

   Hola **frecuencia** y **intervalo** de conjunto de datos de entrada de Hola se establece demasiado**hora** y **1**, lo que significa que Hola entrada segmento está disponible cada hora. En este ejemplo, es Hola mismo archivo (file.txt) en intputfolder Hola.

   Estas son las horas de inicio de Hola para cada segmento, que se representa mediante la variable del sistema SliceStart Hola por encima del fragmento de JSON.
3. Haga clic en **implementar** en Hola toocreate de barra de herramientas e implementar hello **InputDataset**. Confirme que aparece hello **tabla creado correctamente** mensaje en la barra de título de Hola de hello Editor.

#### <a name="create-an-output-dataset"></a>Crear un conjunto de datos de salida
1. Hola **editor de la factoría de datos**, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo conjunto de datos**y, a continuación, seleccione **almacenamiento de blobs de Azure**.
2. Reemplace el script JSON de hello en el panel derecho de hello con hello siguiente secuencia de comandos JSON:

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     Ubicación de salida es **adftutorial/customactivityoutput/** y nombre de archivo de salida es aaaa-MM-dd-HH.txt, donde AAAA-MM-dd-HH es Hola año, mes, fecha y hora del segmento de saludo se está generando. Consulte la [Referencia para desarrolladores][adf-developer-reference] para obtener más información.

    Se genera un blob o archivo de salida para cada segmento de entrada. Así es cómo se asigna el nombre al archivo de salida de cada segmento. Todos los archivos de salida de hello se generan en una carpeta de salida: **adftutorial\customactivityoutput**.

   | Segmento | Hora de inicio | Archivo de salida |
   |:--- |:--- |:--- |
   | 1 |2016-11-16T00:00:00 |2016-11-16-00.txt |
   | 2 |2016-11-16T01:00:00 |2016-11-16-01.txt |
   | 3 |2016-11-16T02:00:00 |2016-11-16-02.txt |
   | 4 |2016-11-16T03:00:00 |2016-11-16-03.txt |
   | 5 |2016-11-16T04:00:00 |2016-11-16-04.txt |

    Recuerde que todos los archivos de hello en una carpeta de entrada son parte de un segmento con horas de inicio de hello mencionadas anteriormente. Cuando se procesa este segmento, actividad personalizada hello recorre cada archivo y genera una línea en el archivo de salida de hello con número de Hola de repeticiones del término de búsqueda ("Microsoft"). Si hay tres archivos en hello inputfolder, hay tres líneas en archivo de salida de hello para cada intervalo por hora: 2016-11-16-00.txt 2016-11-16:01:00:00.txt, etcetera.
3. Hola toodeploy **OutputDataset**, haga clic en **implementar** en la barra de comandos de Hola.

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a>Crear y ejecutar una canalización que usa la actividad personalizada hello
1. Hola Editor de generador de datos, haga clic en **... Más**y, a continuación, seleccione **nueva canalización** en la barra de comandos de Hola. 
2. Reemplace Hola JSON en el panel derecho de hello con hello siguiente secuencia de comandos JSON:

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    Tenga en cuenta Hola siguientes puntos:

   * **Simultaneidad** se establece demasiado**2** para que dos segmentos se procesan en paralelo con 2 máquinas virtuales en el grupo de lote de Azure de Hola.
   * Hay una actividad en la sección de actividades de Hola y es de tipo: **DotNetActivity**.
   * **AssemblyName** se establece el nombre toohello de hello DLL: **MyDotnetActivity.dll**.
   * **Punto de entrada** se establece demasiado**MyDotNetActivityNS.MyDotNetActivity**.
   * **PackageLinkedService** se establece demasiado**AzureStorageLinkedService** que señala el almacenamiento de blobs de toohello que contiene el archivo zip de hello actividad personalizada. Si utiliza varias cuentas de almacenamiento de Azure para archivos de entrada/salida y hello archivo zip de actividad personalizada, crear otro servicio vinculado de almacenamiento de Azure. En este artículo se da por supuesto que está usando Hola la misma cuenta de almacenamiento de Azure.
   * **PackageFile** se establece demasiado**customactivitycontainer/MyDotNetActivity.zip**. Se encuentra en formato de hello: containerforthezip/nameofthezip.zip.
   * toma la actividad personalizada Hello **InputDataset** como entrada y **OutputDataset** como salida.
   * propiedad de linkedServiceName Hola de actividad personalizada hello señala toohello **AzureBatchLinkedService**, lo que indica a Data Factory de Azure esa actividad personalizada hello necesita toorun en máquinas virtuales de lote de Azure.
   * **isPaused** propiedad se establece demasiado**false** de forma predeterminada. canalización de Hola se ejecuta inmediatamente en este ejemplo porque se inician los segmentos de Hola Hola anteriores. Puede establecer esta canalización de Hola de propiedad tootrue toopause y establecer toorestart toofalse atrás.
   * Hola **iniciar** tiempo y **final** tiempos son **cinco** horas separadas y segmentos se producen cada hora, por lo que cinco segmentos son generadas por la canalización de Hola.
3. canalización de hello toodeploy, haga clic en **implementar** en la barra de comandos de Hola.

### <a name="monitor-hello-pipeline"></a>Canalización de Hola de Monitor
1. En la hoja de la factoría de datos de Hola Hola portal de Azure, haga clic en **diagrama**.

    ![Icono Diagrama](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. Hola vista de diagrama, haga clic en hello OutputDataset.

    ![Vista de diagrama](./media/data-factory-use-custom-activities/diagram.png)
3. Debería ver que los sectores de salida cinco Hola están en estado listo de Hola. Si no están en estado listo hello, aún no se han producido aún. 

   ![Segmentos de salida](./media/data-factory-use-custom-activities/OutputSlices.png)
4. Compruebe que se generan archivos de salida de hello en el almacenamiento de blobs de hello en hello **adftutorial** contenedor.

   ![salida de la actividad personalizada][image-data-factory-ouput-from-custom-activity]
5. Si abre el archivo de salida de hello, debería ver Hola salida toohello similar después de salida:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. Hola de uso [portal de Azure] [ azure-preview-portal] o toomonitor de cmdlets de PowerShell de Azure la factoría de datos, canalizaciones y conjuntos de datos. Puede ver mensajes de Hola **ActivityLogger** en el código de hello para la actividad personalizada hello en los registros de hello (específicamente 0.log usuario) que puede descargarse desde el portal de Hola o mediante cmdlets.

   ![registros de descarga de la actividad personalizada][image-data-factory-download-logs-from-custom-activity]

Consulte [Supervisión y administración de canalizaciones de la Factoría de datos de Azure](data-factory-monitor-manage-pipelines.md) para obtener información detallada sobre los pasos que hay que seguir para supervisar los conjuntos de datos y las canalizaciones.      

## <a name="data-factory-project-in-visual-studio"></a>Proyecto de Data Factory en Visual Studio  
Puede crear y publicar entidades de Data Factory usando Visual Studio en lugar de Azure Portal. Para obtener información acerca de cómo crear y publicar las entidades de la factoría de datos mediante el uso de Visual Studio, vea [crear su primera canalización mediante Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) y [copiar los datos de Blob de Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) artículos.

Hola siguiendo los pasos adicionales si va a crear el proyecto de la factoría de datos en Visual Studio:
 
1. Agregar proyecto toohello solución de Visual Studio que contiene el proyecto de actividad personalizada hello de hello factoría de datos. 
2. Agregue un proyecto de actividad de .NET de toohello de referencia de proyecto de la factoría de datos de Hola. Haga clic en proyecto de la factoría de datos, seleccione demasiado**agregar**y, a continuación, haga clic en **referencia**. 
3. Hola **Agregar referencia** cuadro de diálogo, seleccione hello **MyDotNetActivity** del proyecto y haga clic en **Aceptar**.
4. Generar y publicar soluciones de Hola.

    > [!IMPORTANT]
    > Cuando publique las entidades de la factoría de datos, un archivo zip se crea automáticamente y es el contenedor de blob cargado toohello: customactivitycontainer. Si no existe el contenedor de blob de hello, automáticamente se crea demasiado.  


## <a name="data-factory-and-batch-integration"></a>Integración de Data Factory y Lote
Hola servicio factoría de datos crea un trabajo de lote de Azure con el nombre de hello: **adf poolname: trabajo-xxx**. Haga clic en **trabajos** desde el menú de la izquierda Hola. 

![Data Factory de Azure: trabajos por lotes](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

Se crea una tarea para cada ejecución de actividad de un segmento. Si hay cinco segmentos de toobe listo procesado, se crean cinco tareas de este trabajo. Si hay varios nodos de ejecución en el grupo de lote de Hola, dos o más segmentos pueden ejecutar en paralelo. Si se establece el nodo de proceso de tareas máximo de Hola por demasiado > 1, también puede tener más de un segmento con hello mismo proceso.

![Data Factory de Azure: tareas de trabajos por lotes](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

Hola siguiente diagrama ilustra la relación de hello entre tareas de Data Factory de Azure y por lotes.

![Factoría de datos y Lote](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a>Solución de errores
La solución de problemas se compone de varias técnicas básicas:

1. Si ve Hola tras error, puede que esté usando un almacenamiento de blobs activa/recuperación en lugar de usar un almacenamiento de blobs de Azure de uso general. Cargar Hola zip archivo tooa **cuenta de almacenamiento de Azure para fines generales**. 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. Si ve Hola tras error, confirme ese nombre Hola de clase Hola Hola CS coincidencias hello en nombre de archivo que especificó para hello **EntryPoint** propiedad de canalización de hello JSON. En el tutorial de hello, nombre de clase hello es: MyDotNetActivity y Hola EntryPoint Hola JSON es: MyDotNetActivityNS. **MyDotNetActivity**.

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   Si coinciden los nombres de hello, confirme que todos los archivos binarios de hello son Hola **carpeta raíz** del archivo zip de Hola. Es decir, cuando se abre el archivo zip de hello, debería ver todos los archivos de hello en la carpeta raíz de hello, no en todas las subcarpetas.   
3. Si no se establece demasiado el segmento de entrada de hello**listo**, confirme que la estructura de carpetas de entrada de hello es correcta y **file.txt** existe en las carpetas de entrada de Hola.
3. Hola **Execute** método de la actividad personalizada, utilice hello **IActivityLogger** información sobre los objetos toolog que le ayude a solucionar problemas. mensajes de saludo registrado aparecen en archivos de registro de usuario de hello (uno o más archivos con nombre: usuario 0.log, 1.log de usuario, usuario 2.log, etcetera.).

   Hola **OutputDataset** hoja, haga clic en Hola segmento toosee Hola **el segmento de datos** hoja para dicho sector. Verá **ejecuciones de actividad** para ese segmento. Debería ver una actividad ejecutar para el intervalo de saludo. Si hace clic en ejecutar en la barra de comandos de hello, puede iniciar otra actividad ejecutar para hello mismo segmento.

   Al hacer clic en la ejecución de la actividad de hello, vea hello **detalles de ejecución de la actividad** hoja con una lista de archivos de registro. Vea los mensajes registrados en el archivo de hello user_0.log. Cuando se produce un error, verá tres ejecuciones de actividad porque Hola de reintentos se establece too3 en hello canalización/JSON de la actividad. Al hacer clic en la ejecución de la actividad de hello, consulte los archivos de registro de hello que se puede revisar el error de hello tootroubleshoot.

   Hola lista de archivos de registro, haga clic en hello **0.log usuario**. En el panel derecho de Hola se muestran resultados de hello del uso de hello **IActivityLogger.Write** método. Si no ve todos los mensajes, compruebe si tiene más archivos de registro llamados user_1.log, user_2.log, etc. En caso contrario, código de hello puede haya fallado después Hola último mensaje registrado.

   Además, consulte **system-0.log** para ver si hay alguna excepción o mensaje de error del sistema.
4. Incluir hello **PDB** de archivos en el archivo zip de Hola para que los detalles del error Hola tienen información como **pila de llamadas** cuando se produce un error.
5. Todos los Hola archivos en el archivo zip de hello para la actividad personalizada hello debe estar en hello **nivel superior** con ningún subcarpetas.
6. Asegúrese de que hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip), y **packageLinkedService** (debe apuntar toohello **general**almacenamiento de blobs de Azure que contiene el archivo zip de Hola) se establecen valores de toocorrect.
7. Si corrige un segmento de hello tooreprocess error y quiere, haga clic en segmento Hola Hola **OutputDataset** hoja y haga clic en **ejecutar**.
8. Si ve Hola tras error, que usa el paquete de almacenamiento de Azure Hola de versión > 4.3.0. Selector de servicio de factoría de datos requiere la versión de Hola 4.3 de WindowsAzure.Storage. Vea [Appdomain aislamiento](#appdomain-isolation) sección para una solución alternativa, si tiene que utilizar Hola una versión posterior del ensamblado del almacenamiento de Azure. 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    Si puede usar la versión de Hola 4.3.0 del paquete de almacenamiento de Azure, quite Hola existente referencia tooAzure paquete almacenamiento de información de versión > 4.3.0. A continuación, ejecute el siguiente comando desde la consola de administrador de paquetes de NuGet de Hola. 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    Compile el proyecto de Hola. Eliminar Azure.Storage ensamblado de versión > 4.3.0 desde la carpeta bin\Debug del saludo. Crear un archivo zip con archivos binarios y un archivo PDB de Hola. Reemplazar el archivo zip antiguo de hello por este otro en contenedor de blobs de hello (customactivitycontainer). Hola vuelva a ejecutar intervalos que no se pudo (haga clic en el segmento y haga clic en ejecutar).   
8. actividad personalizada Hello no utiliza hello **app.config** archivo desde el paquete. Por lo tanto, si el código lee las cadenas de conexión del archivo de configuración de hello, no funciona en tiempo de ejecución. Hola se recomienda una vez con Azure Batch toohold los secretos en un **Azure KeyVault**, usar un hello tooprotect principal de servicio basada en certificados **keyvault**y distribuir el certificado de Hola tooAzure grupo de lote. Hola actividad personalizada. NET, a continuación, puede tener acceso a los secretos de hello KeyVault en tiempo de ejecución. Esta solución es una solución genérica y puede escalarse tooany tipo de secreto, no solo la cadena de conexión.

   Hay una solución más fácil (pero no es una práctica recomendada): puede crear un **servicio vinculado de SQL Azure** con valores de cadena de conexión, cree un conjunto de datos que usa Hola servicios vinculados y conjunto de datos de cadena Hola como un conjunto de datos de entrada ficticio toohello la actividad personalizada. NET. También puede, a continuación, Hola de acceso había vinculado cadena de conexión del servicio en el código de actividad personalizada hello.  

## <a name="update-custom-activity"></a>Actualización de una actividad personalizada
Si actualiza el código de hello para la actividad personalizada hello, compilación y cargar el archivo zip de Hola que contiene el nuevo almacenamiento de blobs de toohello de los archivos binarios.

## <a name="appdomain-isolation"></a>Aislamiento de AppDomain
Vea [Cross AppDomain ejemplo](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) que muestra cómo toocreate una actividad personalizada que no está restringida versiones tooassembly utilizadas por el iniciador de la factoría de datos de hello (ejemplo: WindowsAzure.Storage v4.3.0, v6.0.x Newtonsoft.Json, etcetera.).

## <a name="access-extended-properties"></a>Acceso a las propiedades extendidas
Puede declarar propiedades extendidas en JSON de la actividad de hello tal y como se muestra en el siguiente ejemplo de Hola:

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


En el ejemplo de Hola, hay dos propiedades extendidas: **SliceStart** y **DataFactoryName**. valor de Hola para SliceStart se basa en la variable del sistema SliceStart Hola. Consulte el artículo sobre las [variables del sistema](data-factory-functions-variables.md) para ver una lista de las variables del sistema admitidas. valor de Hola para DataFactoryName es tooCustomActivityFactory codificado de forma rígida.

tooaccess estas propiedades extendidas en hello **Execute** método, use código similar toohello siguiente código:

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a>Escalado automático de Azure Batch
También puede crear un grupo de Lote de Azure con la característica **autoescala** . Por ejemplo, podría crear un grupo de lote de azure con 0 VM dedicadas y una fórmula de Autoescala según el número de Hola de las tareas pendientes. 

fórmula de ejemplo de Hola aquí logra Hola siguiente comportamiento: cuando inicialmente se crea el grupo de hello, empieza por 1 máquina virtual. Métrica de $PendingTasks define el número de Hola de tareas en ejecución + activo (en cola) estado.  fórmula de Hello busca Hola promedio de las tareas pendientes de hello últimos 180 segundos y establece el valor de TargetDedicated en consecuencia. Garantiza que TargetDedicated nunca supera las 25 VM. Por lo tanto, tal y como se envían las nuevas tareas, grupo crece automáticamente y como tareas se completan, las máquinas virtuales, se convierten en uno por uno libre y escalado automático de hello disminuye esas máquinas virtuales. startingNumberOfVMs y maxNumberofVMs pueden ser necesidades tooyour ajustada.

Fórmula de escalado automático:

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

Para más información, consulte [Escalado automático de los nodos de proceso en un grupo de Lote de Azure](../batch/batch-automatic-scaling.md) .

Si grupo hello usa predeterminado hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Hola servicio por lotes puede tardar 15 a 30 minutos tooprepare Hola VM antes de ejecutar la actividad personalizada hello.  Si el grupo de hello está usando un autoScaleEvaluationInterval diferente, podría tardar Hola servicio por lotes autoScaleEvaluationInterval + 10 minutos.

## <a name="use-hdinsight-compute-service"></a>Uso del servicio de proceso de HDInsight
En el tutorial de hello, utiliza actividades personalizadas de lote de Azure compute toorun Hola. También puede utilizar su propio clúster de HDInsight basados en Windows o hacer factoría de datos crea un clúster de HDInsight basados en Windows a petición y tiene actividad personalizada hello ejecutar en el clúster de HDInsight Hola. Estos son los pasos de alto nivel de hello para el uso de un clúster de HDInsight.

> [!IMPORTANT]
> las actividades de .NET personalizadas Hola ejecutarán solo en clústeres de HDInsight basados en Windows. Una solución alternativa para esta limitación es toouse Hola mapa reducir actividad toorun Java código personalizado en un clúster de HDInsight basados en Linux. Otra opción es toouse un grupo de lote de Azure de las máquinas virtuales toorun actividades personalizadas en lugar de utilizar un clúster de HDInsight.
 

1. Cree un servicio vinculado de HDInsight de Azure.   
2. Servicio en lugar de vinculado de HDInsight de uso **AzureBatchLinkedService** Hola de canalización JSON.

Si desea que tootest con el tutorial de hello, cambio **iniciar** y **final** el tiempo de espera de la canalización de Hola para que pueda probar el escenario de hello con hello servicio HDInsight de Azure.

#### <a name="create-azure-hdinsight-linked-service"></a>Creación de un servicio vinculado de HDInsight de Azure
Hola servicio Data Factory de Azure admite la creación de un clúster a petición y usar datos de salida de tooprocess tooproduce de entrada. También puede utilizar su propio clúster tooperform Hola igual. Cuando se utiliza el clúster de HDInsight a petición, se crea un clúster para cada sector. Sin embargo, si usa su propio clúster de HDInsight, clúster de hello es listo tooprocess Hola segmento inmediatamente. Por lo tanto, cuando se usa el clúster a petición, no verá los datos de salida de hello tan pronto como cuando usa su propio clúster.

> [!NOTE]
> En tiempo de ejecución, una instancia de una actividad de .NET sólo se ejecuta en un nodo de trabajo en clúster de HDInsight de hello; no puede ser toorun escalado en varios nodos. Pueden ejecutar varias instancias de actividad de .NET en paralelo en distintos nodos del clúster de HDInsight Hola.
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a>toouse un clúster de HDInsight a petición
1. Hola **portal de Azure**, haga clic en **autor e implementar** en la página principal de hello factoría de datos.
2. Hola Editor de generador de datos, haga clic en **nuevo proceso** de comando de hello barra y seleccione **clúster de HDInsight a petición** en el menú de Hola.
3. Asegúrese de hello siguiente secuencia de comandos de cambios toohello JSON:

   1. Para hello **clusterSize** propiedad, especifique el tamaño Hola Hola del clúster de HDInsight.
   2. Para hello **timeToLive** propiedad, especifique cuánto tiempo cliente hello puede estar inactivo antes de eliminarla.
   3. Para hello **versión** propiedad, especifique la versión de HDInsight de hello desea toouse. Si excluye esta propiedad, se utiliza la versión más reciente de Hola.  
   4. Para hello **linkedServiceName**, especifique **AzureStorageLinkedService**.

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > las actividades de .NET personalizadas Hola ejecutarán solo en clústeres de HDInsight basados en Windows. Una solución alternativa para esta limitación es toouse Hola mapa reducir actividad toorun Java código personalizado en un clúster de HDInsight basados en Linux. Otra opción es toouse un grupo de lote de Azure de las máquinas virtuales toorun actividades personalizadas en lugar de utilizar un clúster de HDInsight.

4. Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.

##### <a name="toouse-your-own-hdinsight-cluster"></a>toouse su propio clúster de HDInsight:
1. Hola **portal de Azure**, haga clic en **autor e implementar** en la página principal de hello factoría de datos.
2. Hola **Editor de generador de datos**, haga clic en **nuevo proceso** de comando de hello barra y seleccione **clúster de HDInsight** en el menú de Hola.
3. Asegúrese de hello siguiente secuencia de comandos de cambios toohello JSON:

   1. Para hello **clusterUri** propiedad, escriba la dirección URL de Hola para HDInsight. Por ejemplo, https://<clustername>.azurehdinsight.net/.     
   2. Para hello **nombre de usuario** propiedad, escriba nombre de usuario de hello con clúster de HDInsight de toohello de acceso.
   3. Para hello **contraseña** propiedad, escriba la contraseña de hello para el usuario de Hola.
   4. Para hello **LinkedServiceName** propiedad, escriba **AzureStorageLinkedService**.
4. Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.

Consulte [Servicios vinculados de procesos](data-factory-compute-linked-services.md) para más información.

Hola **JSON de canalización**, utilice HDInsight (a petición o su propia) servicio vinculado:

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a>Creación de una actividad personalizada mediante el SDK de .NET
En el tutorial de hello en este artículo, se crea una factoría de datos con una canalización que usa la actividad personalizada hello mediante Hola portal de Azure. Hola siguiente código muestra cómo toocreate Hola factoría de datos con el SDK de .NET en su lugar. Puede encontrar más detalles sobre el uso de SDK tooprogrammatically crean canalizaciones en hello [crear una canalización con la actividad de copia mediante el uso de API de .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) artículo. 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

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
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

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
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
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
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
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

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
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
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

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
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a>Depurar una actividad personalizada en Visual Studio
Hola [factoría de datos de Azure: entorno local](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) ejemplo en GitHub incluye una herramienta que permite toodebug actividades personalizadas de .NET en Visual Studio.  


## <a name="sample-custom-activities-on-github"></a>Actividades personalizadas de ejemplo en GitHub
| Muestra | Qué hace la actividad personalizada |
| --- | --- |
| [Descargador de datos HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample). |Descarga los datos desde un almacenamiento de blobs mediante la actividad personalizada de C# de factoría de datos de tooAzure de extremo HTTP. |
| [Ejemplo de Análisis de opiniones de Twitter.](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Invoca un modelo de aprendizaje automático de Azure y realiza un análisis de opiniones, puntuación, predicción, etc. |
| [Ejecutar script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). |Invoca el script de R; para ello, ejecuta RScript.exe en el clúster de HDInsight que ya tiene instalado R. |
| [Actividad .NET entre AppDomain](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Utiliza las versiones de ensamblado diferente de la utilizada por el iniciador de la factoría de datos de Hola |
| [Reproceso de un modelo en Azure Analysis Services](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  Reprocesa un modelo en Azure Analysis Services. |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
