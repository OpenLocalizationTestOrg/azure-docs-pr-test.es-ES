---
title: "conjuntos de datos a gran escala de aaaProcess con factoría de datos y por lotes | Documentos de Microsoft"
description: "Describe cómo tooprocess enormes cantidades de datos de una factoría de datos de Azure de canalización mediante el uso de capacidad de procesamiento en paralelo de lote de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a>Procesamiento de datos a gran escala mediante Data Factory y Batch
En este artículo se describe la arquitectura de una solución de ejemplo en la que se mueven y se procesan conjuntos de datos a gran escala de forma automática y programada. También proporciona una solución de hello-to-end tutorial tooimplement con factoría de datos de Azure y Azure Batch.

Este artículo es más largo de lo habitual, ya que contiene un tutorial de una solución de ejemplo completa. Si estás tooBatch nuevo y el generador de datos, puede obtener información acerca de estos servicios y cómo funcionan conjuntamente. Si sabe algo acerca de los servicios de Hola y se diseña y diseñar una solución, se puede concentrar en hello [sección arquitectura](#architecture-of-sample-solution) del artículo de Hola y si está desarrollando un prototipo o una solución, puede que también desee tootry out instrucciones paso a paso en hello [tutorial](#implementation-of-sample-solution). No dude en hacernos llegar cualquier comentario que tenga sobre el contenido y su uso.

En primer lugar, echemos un vistazo a cómo pueden ayudar servicios de la factoría de datos y por lotes con el procesamiento de grandes conjuntos de datos en la nube de Hola.     

## <a name="why-azure-batch"></a>¿Por qué elegir Azure Batch?
Lote de Azure también permite que las aplicaciones a gran escala paralelas y de alto rendimiento informática (HPC) de toorun eficacia en la nube de Hola. Es un servicio de plataforma que programa el trabajo de proceso intensivo toorun en una colección administrada de máquinas virtuales, y puede automáticamente escala calcular necesidades de hello toomeet de recursos de los trabajos.

Con hello servicio por lotes, se definen las tooexecute de recursos de proceso de Azure las aplicaciones en paralelo y a escala. Puede ejecutar a petición o programado trabajos y no es necesario toomanually crear, configurar y administrar un clúster de HPC, máquinas virtuales individuales, redes virtuales o un trabajo complejo e infraestructura de programación de tareas.

Vea Hola siguientes artículos si no está familiarizado con el lote de Azure ya que esto ayuda a comprender Hola arquitectura e implementación de solución de hello descrita en este artículo.   

* [Datos básicos de Lote de Batch](../batch/batch-technical-overview.md)
* [Información general de las características de Lote](../batch/batch-api-basics.md)

(opcional) toolearn más información acerca de Azure Batch, vea hello [ruta de acceso de aprendizaje para Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).

## <a name="why-azure-data-factory"></a>¿Por qué elegir Azure Data Factory?
Factoría de datos es un servicio de integración de datos en la nube que organiza y automatiza el movimiento de Hola y la transformación de datos. Usar servicio de factoría de datos de hello, puede crear canalizaciones de datos administrados que se mueven datos desde el entorno local y almacén de datos centralizado de tooa de almacenes de datos en la nube (por ejemplo: almacenamiento de blobs de Azure) y el proceso o transformar datos mediante servicios como HDInsight de Azure y Azure Aprendizaje automático. También puede programar toorun de canalizaciones de datos de una manera programada (cada hora, diariamente, semanalmente, etc.) y un monitor y administrarlos en un problemas de tooidentify de vista y tomar medidas.

Vea Hola siguientes artículos si no está familiarizado con Data Factory de Azure ya que esto ayuda a comprender Hola arquitectura e implementación de solución de hello descrita en este artículo.  

* [Introducción al servicio Data Factory de Azure](data-factory-introduction.md)
* [Creación de la primera canalización de datos](data-factory-build-your-first-pipeline.md)   

(opcional) toolearn más información acerca de la factoría de datos de Azure, vea hello [ruta de acceso de aprendizaje de factoría de datos de Azure](https://azure.microsoft.com/documentation/learning-paths/data-factory/).

## <a name="data-factory-and-batch-together"></a>Data Factory y Batch juntos
Factoría de datos incluye las actividades integradas como toocopy/mover datos de actividad de copia de un origen de datos de almacén de almacén de datos de destino tooa y los datos de tooprocess de actividad de Hive con clústeres de Hadoop (HDInsight) en Azure. Consulte en este artículo la lista de [actividades de transformación de datos](data-factory-data-transformation-activities.md) admitidas.

También permite toocreate .NET actividades personalizadas toomove o procesen datos con su propia lógica y ejecutar estas actividades en un clúster de HDInsight de Azure o en un grupo de lote de Azure de máquinas virtuales. Cuando usas Azure Batch, puede configurar grupo de hello tooauto-escala (Agregar o quitar máquinas virtuales en función de la carga de trabajo de hello) según una fórmula que proporcione.     

## <a name="architecture-of-sample-solution"></a>Arquitectura de la solución de ejemplo
Aunque la arquitectura de Hola que se describe en este artículo es una solución simple, es escenarios de toocomplex relevante, como el modelado, servicios financieros, procesamiento de imágenes, representación y genómica análisis de riesgos.

diagrama de Hello muestra 1) cómo organiza la factoría de datos de movimiento de datos y el procesamiento y (2) cómo procesa el lote de Azure Hola datos de forma paralela. Descarga y diagrama de impresión Hola para facilitar su consulta (11 x 17 pulgadas. o tamaño A3): [Orquestación de HPC y de datos mediante Azure Batch y Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).

[![Diagrama de procesamiento de datos de gran escala](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)

Hello lista siguiente proporciona pasos básicos de hello del proceso de Hola. solución de Hello incluye código y explicaciones solución end-to-end de toobuild Hola.

1. **Configure Lote de Azure con un grupo de nodos de proceso (máquinas virtuales)**. Puede especificar el número de Hola de nodos y el tamaño de cada nodo.
2. **Cree una instancia de Azure Data Factory** que esté configurada con entidades que representen Azure Blob Storage, el servicio de proceso Azure Batch, los datos de entrada y salida y un flujo de trabajo o una canalización con las actividades que mueven y transforman datos.
3. **Crear una actividad personalizada de .NET en la canalización de factoría de datos de hello**. actividad Hello es el código de usuario que se ejecuta en hello grupo de lote de Azure.
4. **Almacene grandes cantidades de datos de entrada como blobs en Almacenamiento de Azure**. Los datos se dividen en segmentos lógicos (normalmente, en función de la fecha y la hora).
5. **Factoría de datos de copia de datos que se procesan en paralelo** ubicación secundaria toohello.
6. **Factoría de datos ejecuta la actividad personalizada hello use el grupo de hello asignado por lote**. Además, puede ejecutar actividades al mismo tiempo. Cada actividad procesa un segmento de datos. Hola resultados se almacenan en el almacenamiento de Azure.
7. **Factoría de datos mueve la tercera ubicación de hello resultados finales tooa**, ya sea para su distribución a través de una aplicación, o para su posterior procesamiento por otras herramientas.

## <a name="implementation-of-sample-solution"></a>Implementación de la solución de ejemplo
solución de ejemplo de Hola es deliberadamente simple y es tooshow, cómo toouse factoría de datos y por lotes juntos tooprocess conjuntos de datos. solución de Hello simplemente cuenta el número de Hola de apariciones de un término de búsqueda ("Microsoft") en los archivos de entrada organizados en una serie de tiempo. Genera archivos de toooutput de recuento de Hola.

**Tiempo**: si está familiarizado con conceptos básicos de Azure, la factoría de datos y el lote y tienen requisitos previos de hello completado indicadas a continuación, se estima que esta solución toma toocomplete 1 y 2 horas.

### <a name="prerequisites"></a>Requisitos previos
#### <a name="azure-subscription"></a>Suscripción de Azure
Si carece de suscripción de Azure, puede crear una cuenta de prueba gratuita en tan solo unos minutos. Consulte [Prueba gratuita de un mes](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="azure-storage-account"></a>Cuenta de almacenamiento de Azure
Usar una cuenta de almacenamiento de Azure para almacenar datos de hello en este tutorial. Si no dispone de una, consulte [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account). solución de ejemplo de Hola usa almacenamiento de blobs.

#### <a name="azure-batch-account"></a>Cuenta de Azure Batch
Crear una cuenta de Azure Batch mediante hello [portal de Azure](http://manage.windowsazure.com/). Consulte [Creación y administración de una cuenta de Azure Batch en Azure Portal](../batch/batch-account-create-portal.md). Tenga en cuenta clave de nombre y la cuenta de la cuenta del lote de Azure Hola. También puede usar [AzureRmBatchAccount New](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate una cuenta de lote de Azure. Consulte [Introducción a los cmdlets de PowerShell para Azure Batch](../batch/batch-powershell-cmdlets-get-started.md) para obtener instrucciones detalladas para usar este cmdlet.

solución de ejemplo de Hola utiliza datos de tooprocess de lote de Azure (indirectamente a través de una canalización del generador de datos de Azure) de forma paralela en un grupo de nodos de cálculo (una colección administrada de máquinas virtuales).

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a>Grupo de máquinas virtuales (VM) de Azure Batch
Cree un **grupo Azure Batch** con al menos 2 nodos de proceso.

1. Hola [portal de Azure](https://portal.azure.com), haga clic en **examinar** en Hola menú izquierdo y haga clic en **las cuentas por lotes**.
2. Seleccione su hello tooopen de cuenta de Azure Batch **cuenta de lote** hoja.
3. Haga clic en el icono **Grupos** .
4. Hola **grupos** hoja, haga clic en el botón Agregar en la barra de herramientas de hello tooadd un grupo.
   1. Escriba un Id. de grupo de hello (**Id. de grupo**). Hola Nota **Id. de grupo de hello**; necesita al crear soluciones de hello factoría de datos.
   2. Especifique **Windows Server 2012 R2** para configuración de la familia de sistemas operativos de Hola.
   3. Seleccione un **plan de tarifa de nodos**.
   4. Escriba **2** como valor de hello **destino dedicado** configuración.
   5. Escriba **2** como valor de hello **Max tareas por nodo** configuración.
   6. Haga clic en **Aceptar** grupo de hello toocreate.

#### <a name="azure-storage-explorer"></a>Explorador de Azure Storage
[Explorador de Azure Storage 6 (herramienta)](https://azurestorageexplorer.codeplex.com/) o [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (de ClumsyLeaf Software). Usar estas herramientas para inspeccionar y modificar datos de hello en los proyectos de almacenamiento de Azure, incluidos los registros de Hola de las aplicaciones hospedadas en la nube.

1. Cree un contenedor denominado **mycontainer** con acceso privado (sin acceso anónimo).
2. Si utilizas **CloudXplorer**, crear carpetas y subcarpetas con Hola siguiente estructura:

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   `Inputfolder` y `outputfolder` son carpetas de nivel superior en `mycontainer`. Hola `inputfolder` tiene subcarpetas con marcas de fecha y hora (aaaa-MM-DD-HH).

   Si utilizas **Azure Storage Explorer**, en el paso siguiente de hello, necesita tooupload archivos con nombres: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` y así sucesivamente. Este paso crea automáticamente carpetas Hola.
3. Crear un archivo de texto **file.txt** en su equipo con contenido con la palabra clave de hello **Microsoft**. Por ejemplo: "test custom activity Microsoft test custom activity Microsoft".
4. Cargar Hola archivo toohello siguientes carpetas de entrada en el almacenamiento de blobs de Azure.

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   Si utilizas **Azure Storage Explorer**, cargue el archivo hello **file.txt** demasiado**mycontainer**. Haga clic en **copia** en la barra de herramientas de hello toocreate una copia de blob de Hola. Hola **Copy Blob** cuadro de diálogo, cambio hello **nombre de blob de destino** demasiado`inputfolder/2015-11-16-00/file.txt`. Repita este paso toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` y así sucesivamente. Esta acción crea automáticamente carpetas Hola.
5. Cree otro contenedor denominado: `customactivitycontainer`. Cargar el contenedor de toothis de archivos zip de hello actividad personalizada.

#### <a name="visual-studio"></a>Visual Studio
Instalar Microsoft Visual Studio 2012 o posterior toocreate Hola personalizado lote actividad toobe usa Hola solución factoría de datos.

### <a name="high-level-steps-toocreate-hello-solution"></a>Solución de pasos de alto nivel toocreate Hola
1. Crear una actividad personalizada que contiene la lógica de procesamiento de datos de Hola.
2. Cree un generador de datos de Azure que utiliza la actividad personalizada hello:

### <a name="create-hello-custom-activity"></a>Crear actividad personalizada hello
Hola actividad personalizada de factoría de datos es la esencia de Hola de esta solución de ejemplo. solución de ejemplo de Hola usa la actividad personalizada hello toorun de lote de Azure. Vea [utilizar actividades personalizadas en una canalización del generador de datos de Azure](data-factory-use-custom-activities.md) de actividades personalizadas de toodevelop de información básica de Hola y uso en Data Factory de Azure canalizaciones.

toocreate una actividad personalizada .NET que puede usar en una canalización de factoría de datos de Azure, deberá toocreate un **biblioteca de clases .NET** proyecto con una clase que implementa que **IDotNetActivity** interfaz. Esta interfaz tiene un solo método, **Execute**. Esta es la firma Hola del método hello:

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

método Hello tiene unos componentes claves que necesita toounderstand.

* método Hello toma cuatro parámetros:

  1. **linkedServices**. Lista enumerable de servicios vinculados que vinculan orígenes de datos de entrada/salida (por ejemplo: almacenamiento de blobs de Azure) toohello factoría de datos. En este ejemplo, hay solo un servicio vinculado del tipo Azure Storage que se utilice como entrada y salida.
  2. **datasets**. Se trata de una lista enumerable de conjuntos de datos. Puede usar este ubicaciones de parámetro tooget hello y esquemas definidos por los conjuntos de datos de entrada y salida.
  3. **activity**. Este parámetro representa Hola proceso entidad actual - en este caso, un servicio Azure Batch.
  4. **logger**. permite del registrador de Hello para que escribir comentarios de depuración que superficie como Hola "Usuario" iniciar sesión Hola canalización.
* método Hello devuelve un diccionario que puede ser actividades personalizadas utilizadas toochain juntos en un futuro Hola. Esta característica todavía no está implementada, por lo que devuelve un diccionario vacío de método hello.

#### <a name="procedure-create-hello-custom-activity"></a>Procedimiento: Crear la actividad personalizada hello
1. Cree un proyecto de biblioteca de clases .NET en Visual Studio.

   1. Inicie **Visual Studio 2012**/**2013/2015**.
   2. Haga clic en **archivo**, seleccione demasiado**New**y haga clic en **proyecto**.
   3. Expanda **Plantillas** y seleccione **Visual C\#**. En este tutorial, utilice C\#, pero puede usar cualquier actividad personalizada .NET language toodevelop hello.
   4. Seleccione **biblioteca de clases** de lista de Hola de tipos de proyecto en hello derecho.
   5. Escriba **MyDotNetActivity** para hello **nombre**.
   6. Seleccione **C:\\ADF** para hello **ubicación**. Crear carpeta de hello **ADF** si no existe.
   7. Haga clic en **Aceptar** proyecto de hello toocreate.
2. Haga clic en **herramientas**, seleccione demasiado**Administrador de paquetes de NuGet**y haga clic en **Package Manager Console**.
3. Hola **Package Manager Console**, ejecutar Hola después comando tooimport **Microsoft.Azure.Management.DataFactories**.

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Hola de importación **el almacenamiento de Azure** paquetes de NuGet en los proyectos de toohello. Este paquete es necesario porque usa la API de almacenamiento de blobs de hello en este ejemplo.

    ```powershell
    Install-Package Azure.Storage
    ```
5. Agregue los siguiente hello **con** archivo de código fuente de toohello de directivas en el proyecto de Hola.

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Cambiar el nombre del programa Hola Hola **espacio de nombres** demasiado**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Cambiar nombre de Hola de clase hello demasiado**MyDotNetActivity** y derivan de hello **IDotNetActivity** interfaz tal y como se muestra a continuación.

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Hola implemente (Agregar) **Execute** método de hello **IDotNetActivity** interfaz toohello **MyDotNetActivity** Hola de clase y copia siguiendo el método de toohello de código de ejemplo. Vea hello [Execute Method](#execute-method) sección para ver una explicación de lógica de hello utilizada en este método.

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
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
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
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
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
9. Agregar Hola después de la clase de toohello de métodos de aplicación auxiliar. Estos métodos se invocan hello **Execute** método. Lo más importante, Hola **Calculate** método aísla el código de hello que recorre en iteración cada blob.

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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    Hola **GetFolderPath** método devuelve la carpeta de toohello de ruta de acceso de hello ese conjunto de datos de Hola puntos tooand Hola **GetFileName** método devuelve el nombre de Hola de Hola/archivo de blob que Hola conjunto de datos de destino.

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    Hola **Calculate** método calcula el número de Hola de instancias de la palabra clave **Microsoft** en archivos de entrada de hello (BLOB en la carpeta de hello). término de búsqueda de Hello ("Microsoft") está codificado de forma rígida en el código de hello.

1. Compile el proyecto de Hola. Haga clic en **generar** desde el menú de Hola y haga clic en **generar solución**.
2. Iniciar **el Explorador de Windows**, del sistema y desplácese demasiado**bin\\depurar** o **bin\\versión** carpeta según el tipo de saludo de compilación.
3. Crear un archivo zip **MyDotNetActivity.zip** que contiene todos los archivos binarios de Hola Hola  **\\bin\\depurar** carpeta. Puede que desee tooinclude hello MyDotNetActivity. **pdb** de archivos para que obtengan detalles adicionales, como el número de línea de código fuente de Hola que causó el problema de hello cuando se produce un error.

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. Cargar **MyDotNetActivity.zip** como un contenedor de blobs de blob toohello: `customactivitycontainer` en hello Azure almacenamiento de blobs que hello **StorageLinkedService** servicio Hola vinculado  **ADFTutorialDataFactory** usa. Crear contenedor de blobs de hello `customactivitycontainer` si aún no existe.

#### <a name="execute-method"></a>Método Execute
Esta sección proporciona más detalles y notas acerca del código de hello en hello método Execute.

1. miembros de Hola para recorrer en iteración la colección de entrada de Hola se encuentran en hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) espacio de nombres. Recorrer en iteración la colección de blobs de hello requiere el uso de hello **BlobContinuationToken** clase. En esencia, debe usar un no-bucle con token de hello como mecanismo de Hola para salir Hola bucle while. Para obtener más información, consulte [cómo toouse almacenamiento de blobs en .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Aquí se muestra un bucle básico:

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   Consulte la documentación de Hola para hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) método para obtener más información.
2. Hello código para trabajar con el conjunto de Hola de blobs lógicamente entra dentro de hello hacer-bucle while. Hola **Execute** método, realice de hello-mientras el bucle pasa lista Hola de blobs con el nombre de método de tooa **Calculate**. método Hello devuelve una variable de cadena denominada **salida** que es resultado de hello de tener que se itera a través de todos los blobs de hello en el segmento de Hola.

   Devuelve Hola número de repeticiones del término de búsqueda de hello (**Microsoft**) en el blob de hello pasa toohello **Calculate** método.

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. Una vez Hola **Calculate** método ha realizado el trabajo de hello, debe escribirse tooa nuevo blob. Por lo que para cada conjunto de blobs que se procesa, se puede escribir un nuevo blob con resultados de Hola. toowrite tooa nuevo blob, el primer conjunto de datos de salida de hello buscar.

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. código de Hello también llama a un método auxiliar: **GetFolderPath** ruta de acceso de la carpeta de hello tooretrieve (nombre de contenedor de almacenamiento de hello).

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   Hola **GetFolderPath** conversiones Hola tooan del objeto de conjunto de datos AzureBlobDataSet, que tiene una propiedad denominada FolderPath.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. Hola de llamadas de código de Hello **GetFileName** método tooretrieve Hola archivo nombre (blob). código de Hello es toohello similar por encima de la ruta de acceso de carpeta de código tooget Hola.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. nombre de Hello del archivo hello se escribe mediante la creación de un objeto URI. constructor URI de Hello utiliza hello **BlobEndpoint** nombre de contenedor de propiedad tooreturn Hola. nombre de archivo y ruta de acceso de carpeta de Hola se agregan tooconstruct el URI del blob de salida de hello.  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. se ha escrito el nombre de Hello del archivo hello y ahora puede escribir la cadena de salida de hello de hello **Calculate** tooa nuevo blob de método:

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a>Crear Hola factoría de datos
Hola [Crear actividad personalizada hello](#create-the-custom-activity) sección, se crea una actividad personalizada y archivo zip de hello cargados con los archivos binarios y Hola PDB archivo tooan contenedor de blobs de Azure. En esta sección, creará un Azure **factoría de datos** con un **canalización** que usa hello **actividad personalizada**.

Hola conjunto de datos de entrada para la actividad personalizada hello representa blobs hello (archivos) en la carpeta de entrada de hello (`mycontainer\\inputfolder`) en almacenamiento de blobs. conjunto de datos de salida de Hello para la actividad hello representa blobs de salida de hello en la carpeta de salida de hello (`mycontainer\\outputfolder`) en almacenamiento de blobs.

Quitar uno o varios archivos en carpetas de entrada de hello:

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

Por ejemplo, colocar un archivo (file.txt) con hello siguen contenido en cada una de las carpetas de Hola.

```
test custom activity Microsoft test custom activity Microsoft
```

Cada carpeta de entrada corresponde tooa segmento de factoría de datos de Azure, incluso si la carpeta de hello tiene 2 o más archivos. Cuando se procesa cada segmento de canalización de hello, la actividad personalizada hello recorre en iteración todos los blobs de hello en la carpeta de entrada de Hola para dicho sector.

Verá cinco archivos de salida con hello mismo contenido. Por ejemplo, el archivo de salida de hello de procesar el archivo de hello en la carpeta de hello 2015-11-16: 00 tiene Hola siguen contenido:

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

Si quita varios archivos (file.txt, archivo2.txt, archivo3.txt) con hello mismo contenido toohello carpeta de entrada, vea Hola siguen contenido en el archivo de salida de hello. Cada carpeta (2015-11-16: 00, etc.) corresponde segmento tooa en este ejemplo, incluso si la carpeta de hello tiene varios archivos de entrada.

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

archivo de salida de Hello tiene tres líneas ahora, uno para cada archivo de entrada (blob) en la carpeta de hello asociada con el segmento de hello (2015-11-16: 00).

Se crea una tarea para cada ejecución de actividad. En este ejemplo, hay sólo una actividad en la canalización de Hola. Cuando se procesa un segmento de canalización de hello, actividad personalizada hello se ejecuta en el segmento de lote de Azure tooprocess Hola. Puesto que hay 5 segmentos (cada segmento puede tener varios blobs o archivos), se crearán 5 tareas en Azure Batch. Cuando una tarea se ejecuta en proceso por lotes, es realmente Hola actividad personalizada que se está ejecutando.

Hola tutorial proporciona detalles adicionales.

#### <a name="step-1-create-hello-data-factory"></a>Paso 1: Crear la factoría de datos de Hola
1. Después de iniciar sesión toohello [portal de Azure](https://portal.azure.com/), Hola lo siguiente:

   1. Haga clic en **NEW** en el menú de la izquierda Hola.
   2. Haga clic en **datos + análisis** en hello **New** hoja.
   3. Haga clic en **factoría de datos** en hello **análisis de datos** hoja.
2. Hola **factoría de datos** hoja, escriba **CustomActivityFactory** para hello nombre. nombre de Hola Hola Azure factoría de datos debe ser único globalmente. Si recibe el error hello: **nombre de generador de datos "CustomActivityFactory" no está disponible**, cambiar nombre de Hola Hola factoría de datos (por ejemplo, **yournameCustomActivityFactory**) y pruebe a crear volver a ejecutarlo.
3. Haga clic en **NOMBRE DEL GRUPO DE RECURSOS**y seleccione un grupo de recursos existente o cree uno.
4. Compruebe que está usando la suscripción correcta de Hola y la región donde desea Hola datos generador toobe creado.
5. Haga clic en **crear** en hello **factoría de datos** hoja.
6. Vea factoría de datos de Hola se creen en hello **panel** de hello portal de Azure.
7. Una vez creado correctamente la factoría de datos de hello, consulte página de factoría de datos de hello, que muestra Hola contenido Hola factoría de datos.

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a>Paso 2: Creación de servicios vinculados
Servicios vinculados vinculan almacenes de datos o generador de datos de Azure de tooan de servicios de proceso. En este paso, se vinculan los **el almacenamiento de Azure** cuenta y **Azure Batch** factoría de datos de cuenta tooyour.

#### <a name="create-azure-storage-linked-service"></a>Creación de un servicio vinculado de Almacenamiento de Azure
1. Haga clic en hello **autor e implementar** icono hello **factoría de datos** hoja para **CustomActivityFactory**. Vea Hola Editor de generador de datos.
2. Haga clic en **nuevo almacén de datos** en Hola barra de comandos y elija **almacenamiento de Azure.** Debería ver Hola script JSON para crear un almacenamiento de Azure vinculada servicio en el editor de Hola.

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. Reemplace **nombre de la cuenta** con nombre de saludo de la cuenta de almacenamiento de Azure y **clave de cuenta** por clave de acceso de Hola de hello cuenta de almacenamiento de Azure. toolearn cómo tooget el almacenamiento de tener acceso a clave, consulte [ver, copiar y regenerar almacenamiento de claves de acceso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

4. Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a>Creación del servicio vinculado de Lote de Azure
En este paso, creará un servicio vinculado para su **Azure Batch** cuenta de actividad personalizado de toorun usado hello factoría de datos.

1. Haga clic en **nuevo proceso** en Hola barra de comandos y elija **lote de Azure.** Debería ver Hola script JSON para la creación de un lote de Azure vinculada servicio en el editor de Hola.
2. Hola script JSON:

   1. Reemplace **nombre de la cuenta** con nombre de saludo de la cuenta de lote de Azure.
   2. Reemplace **clave de acceso** por clave de acceso de Hola de hello cuenta de lote de Azure.
   3. Escriba Hola identificador de grupo de Hola para hello **poolName** propiedad**.** Para esta propiedad, puede especificar cualquier nombre de grupo o id. de bloque.
   4. Especificar por lotes de hello URI para hello **batchUri** propiedad JSON.

      > [!IMPORTANT]
      > Hola **URL** de hello **hoja de la cuenta de Azure Batch** en hello siguiendo el formato: \<accountname\>.\< región\>. batch.azure.com. Para hello **batchUri** propiedad Hola JSON, necesita demasiado**quitar "accountname."** desde la dirección URL de Hola. Ejemplo: `"batchUri": "https://eastus.batch.azure.com"`.
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      Para hello **poolName** propiedad, también puede especificar el identificador de hello del grupo de hello en lugar del nombre de Hola de grupo de Hola de.

      > [!NOTE]
      > Hola servicio factoría de datos no admite una opción de petición para el lote de Azure que lo hace para HDInsight. Solo puede usar su propio grupo de Lote de Azure en una factoría de datos de Azure.
      >
      >
   5. Especifique **StorageLinkedService** para hello **linkedServiceName** propiedad. Crea este servicio vinculado en el paso anterior de Hola. Este almacenamiento se usa como área de almacenamiento provisional para archivos y registros.
3. Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.

#### <a name="step-3-create-datasets"></a>Paso 3: Creación de conjuntos de datos
En este paso, creará entrada toorepresent de conjuntos de datos y los datos de salida.

#### <a name="create-input-dataset"></a>Creación de un conjunto de datos de entrada
1. Hola **Editor** para hello factoría de datos, haga clic en **nuevo conjunto de datos** los botones de barra de herramientas de Hola y haga clic en **almacenamiento de blobs de Azure** desde el menú desplegable de Hola.
2. Reemplace Hola JSON en el panel derecho de hello con hello siguiente fragmento de JSON:

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
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

    Más adelante, en este mismo tutorial, creará una canalización cuya hora de finalización es 2015-11-16T00:00:00Z, y cuya hora de finalización es 2015-11-16T05:00:00Z. Se trata de datos programada tooproduce **cada hora**, por lo que hay 5 segmentos de entrada/salida (entre **00**: 00:00 -\> **05**: 00:00).

    Hola **frecuencia** y **intervalo** de conjunto de datos de entrada de Hola se establece demasiado**hora** y **1**, lo que significa que Hola entrada segmento está disponible cada hora.

    Estos son los tiempos de inicio de Hola para cada segmento, que se representan mediante **SliceStart** variable del sistema en hello por encima del fragmento de JSON.

    | **Segmento** | **Hora de inicio**          |
    |-----------|-------------------------|
    | 1         | 2015-11-16T**00**:00:00 |
    | 2         | 2015-11-16T**01**:00:00 |
    | 3         | 2015-11-16T**02**:00:00 |
    | 4         | 2015-11-16T**03**:00:00 |
    | 5         | 2015-11-16T**04**:00:00 |

    Hola **folderPath** se calcula mediante el uso de la parte de año, mes, día y hora de Hola de hora de inicio del segmento de hello (**SliceStart**). Por lo tanto, mostramos cómo una carpeta de entrada es el intervalo de tooa asignado.

    | **Segmento** | **Hora de inicio**          | **Carpeta de entrada**  |
    |-----------|-------------------------|-------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02** |
    | 4         | 2015-11-16T**03**:00:00 | 2015-11-16-**03** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04** |

1. Haga clic en **implementar** en Hola toocreate de barra de herramientas e implementar hello **InputDataset** tabla.

#### <a name="create-output-dataset"></a>Creación del conjunto de datos de salida
En este paso, creará otro conjunto de datos de tipo de datos de salida de AzureBlob toorepresent Hola.

1. Hola **Editor** para hello factoría de datos, haga clic en **nuevo conjunto de datos** los botones de barra de herramientas de Hola y haga clic en **almacenamiento de blobs de Azure** desde el menú desplegable de Hola.
2. Reemplace Hola JSON en el panel derecho de hello con hello siguiente fragmento de JSON:

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
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

    Se genera un blob o archivo de salida para cada segmento de entrada. Así es cómo se asigna el nombre al archivo de salida de cada segmento. Todos los archivos de salida de hello se generan en una carpeta de salida: `mycontainer\\outputfolder`.

    | **Segmento** | **Hora de inicio**          | **Archivo de salida**       |
    |-----------|-------------------------|-----------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00.txt** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01.txt** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02.txt** |
    | 4         | 2015-11-16T**03**:00:00 | 2015-11-16-**03.txt** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04.txt** |

    Recuerde que Hola a todos los archivos en una carpeta de entrada (por ejemplo: 2015-11-16: 00) forman parte de un segmento con la hora de inicio de hello: 2015-11-16: 00. Cuando se procesa este segmento, actividad personalizada hello recorre cada archivo y genera una línea en el archivo de salida de hello con número de Hola de repeticiones del término de búsqueda ("Microsoft"). Si hay tres archivos en la carpeta de hello 2015-11-16: 00, hay tres líneas en el archivo de salida de hello: 2015-11-16-00.txt.

1. Haga clic en **implementar** en Hola toocreate de barra de herramientas e implementar hello **OutputDataset**.

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a>Paso 4: Crear y ejecutar canalización Hola con actividades personalizadas
En este paso, creará una canalización con una actividad de la actividad personalizada hello que creó anteriormente.

> [!IMPORTANT]
> Si no ha cargado hello **file.txt** tooinput carpetas en el contenedor de blobs de hello, hacerlo antes de crear la canalización de Hola. Hola **isPaused** propiedad se establece toofalse en canalización Hola JSON, por lo que la canalización Hola se ejecuta inmediatamente como Hola **iniciar** fecha es Hola anteriores.
>
>

1. Hola Editor de generador de datos, haga clic en **nueva canalización** en la barra de comandos de Hola. Si no ve el comando hello, haga clic en **... (Puntos suspensivos)**  toosee se.
2. Reemplace Hola JSON en el panel derecho de hello con hello siguiente secuencia de comandos JSON:

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   Tenga en cuenta Hola siguientes puntos:

   * Hay sólo una actividad en la canalización de Hola y que es de tipo: **DotNetActivity**.
   * **AssemblyName** se establece el nombre toohello de hello DLL: **MyDotNetActivity.dll**.
   * **Punto de entrada** se establece demasiado**MyDotNetActivityNS.MyDotNetActivity**. Es básicamente \<espacioDeNombres\>.\<nombreDeClase\> en el código.
   * **PackageLinkedService** se establece demasiado**StorageLinkedService** que señala el almacenamiento de blobs de toohello que contiene el archivo zip de hello actividad personalizada. Si usas cuentas de almacenamiento de Azure diferentes para los archivos de entrada/salida y el archivo zip de actividad personalizada de hello, tienen toocreate almacenamiento de Azure de otro servicio vinculado. En este artículo se da por supuesto que está usando Hola la misma cuenta de almacenamiento de Azure.
   * **PackageFile** se establece demasiado**customactivitycontainer/MyDotNetActivity.zip**. Se encuentra en formato de hello: \<containerforthezip\>/\<nameofthezip.zip\>.
   * toma la actividad personalizada Hello **InputDataset** como entrada y **OutputDataset** como salida.
   * Hola **linkedServiceName** propiedad de actividad personalizada hello señala toohello **AzureBatchLinkedService**, lo que indica a Data Factory de Azure esa actividad personalizada hello necesita toorun en lote de Azure.
   * Hola **simultaneidad** configuración es importante. Si utiliza el valor predeterminado de hello, que es 1, incluso si tiene 2 o más nodos de cálculo en grupo de lote de Azure de hello, segmentos de Hola se procesan uno tras otro. Por lo tanto, no se sacar partido de la capacidad de procesamiento en paralelo de Hola de lote de Azure. Si establece **simultaneidad** tooa mayor valor, digamos 2, significa que dos segmentan (corresponde tootwo tareas en el lote de Azure) pueden ser procesados en hello mismo tiempo, en cuyo caso, ambas máquinas virtuales de Hola Hola se utilizan el grupo de lote de Azure. Por consiguiente, establecer propiedad de simultaneidad de hello correctamente.
   * De manera predeterminada, solo se ejecuta una tarea (segmento) en una máquina virtual en un momento dado. Hello motivo es que, de forma predeterminada, hello **tareas máxima por máquina virtual** se establece too1 para un grupo de lote de Azure. Como parte de los requisitos previos, creó un grupo con este too2 de conjunto de propiedades, por lo que dos segmentos de la factoría de datos se pueden ejecutar en una máquina virtual en hello mismo tiempo.

    -   **isPaused** propiedad se establece toofalse de forma predeterminada. canalización de Hola se ejecuta inmediatamente en este ejemplo porque se inician los segmentos de Hola Hola anteriores. Puede establecer esta canalización de Hola de propiedad tootrue toopause y establecer toorestart toofalse atrás.

    -   Hola **iniciar** tiempo y **final** tiempos son cinco horas separadas y segmentos se producen cada hora, por lo que cinco segmentos son generadas por la canalización de Hola.

1. Haga clic en **implementar** en la canalización de hello toodeploy la barra de comandos de Hola.

#### <a name="step-5-test-hello-pipeline"></a>Paso 5: Probar la canalización de Hola
En este paso, para probar la canalización de hello, al colocar los archivos en carpetas de entrada de Hola. Comenzaremos con la canalización de hello pruebas con un archivo por una carpeta de entrada.

1. En la hoja de la factoría de datos de Hola Hola portal de Azure, haga clic en **diagrama**.

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. En la vista de diagrama de hello, haga doble clic en el conjunto de datos de entrada: **InputDataset**.

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. Debería ver Hola **InputDataset** hoja con todas las cinco segmentos de lista. Hola aviso **hora de inicio del segmento** y **hora de finalización de segmento** para cada sector.

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. Hola **vista de diagrama**, haga clic en **OutputDataset**.
5. Debería ver que los sectores de salida cinco Hola están en estado listo de hello si ya se han producido.

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. Hola tooview portal Azure de uso **tareas** asociados con hello **sectores** y vea qué VM cada sector se ejecutó en. Para obtener más información, consulte la sección [Integración de Data Factory y Batch](#data-factory-and-batch-integration) .
7. Debería ver los archivos de salida de hello de hello `outputfolder` de `mycontainer` almacenamiento de blobs de Azure.

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   Debería ver cinco archivos de salida, uno para cada segmento de entrada. Cada uno de hello salida archivo debe tener contenido toohello similar después de salida:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   Hello diagrama siguiente ilustra cómo asignan los segmentos de la factoría de datos de hello tootasks en el lote de Azure. En este ejemplo, un segmento tiene solo una ejecución.

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. Ahora, probemos con varios archivos en una carpeta. Crear archivos: **file2.txt**, **archivo3.txt**, **file4.txt**, y **file5.txt** con hello en el mismo contenido como en file.txt en carpeta hello: **2015-11-06-01**.
9. En la carpeta de salida de hello, **eliminar** archivo de salida de hello: **2015-11-16-01.txt**.
10. Ahora, en hello **OutputDataset** hoja, segmento de hello contextual con **hora de inicio del segmento** establecido demasiado**16/11/2015 01:00:00 AM**y haga clic en **ejecutar**segmento hello toorerun/volver-process. Ahora, el segmento de hello tiene cinco archivos en lugar de un archivo.

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. Una vez ejecutada de segmento de Hola y su estado es **listo**, comprobar que el contenido de hello en archivo de salida de hello para este segmento (**2015-11-16-01.txt**) en hello `outputfolder` de `mycontainer` en el almacenamiento de blobs. Debería haber una línea para cada archivo de sector de Hola.

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> Si no se eliminara Hola salida archivo 2015-11-16-01.txt antes de intentar con cinco archivos de entrada, verá una línea de segmento anterior Hola ejecutar y cinco líneas de segmento actual Hola ejecutar. De forma predeterminada, contenido de hello es toooutput anexado archivo si ya existe.
>
>

#### <a name="data-factory-and-batch-integration"></a>Integración de Data Factory y Lote
Hola servicio factoría de datos crea un trabajo de lote de Azure con el nombre de hello: `adf-poolname:job-xxx`.

![Data Factory de Azure: trabajos por lotes](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

Se crea una tarea en el trabajo de Hola para cada ejecución de la actividad de un segmento. Si hay 10 toobe lista de segmentos procesados, 10 tareas se crean en el trabajo de Hola. Puede tener más de un sector que se ejecuta en paralelo si dispone de varios nodos de proceso en el grupo de Hola. Si las tareas máximo de Hola por calculan nodo está establecido demasiado > 1, puede haber más de una división quedando Hola mismo proceso.

En este ejemplo, hay 5 segmentos y, por tanto, 5 tareas en Azure Batch. Con hello **simultaneidad** establecido demasiado**5** Hola de canalización JSON de factoría de datos de Azure y **tareas máxima por máquina virtual** establecido demasiado**2** en Azure Batch bloque con **2** máquinas virtuales, Hola tareas se ejecuta rápida (compruebe las horas de inicio y finalización para las tareas).

Utilice el proceso por lotes de hello tooview portal hello y sus tareas asociadas con hello **sectores** y vea qué VM cada sector se ejecutó en.

![Data Factory de Azure: tareas de trabajos por lotes](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a>Depurar Hola canalización
La depuración se compone de varias técnicas básicas:

1. Si no se establece demasiado el segmento de entrada de hello**listo**, confirme que es correcta la estructura de carpetas de entrada de Hola y file.txt existe en las carpetas de entrada de Hola.

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. Hola **Execute** método de la actividad personalizada, utilice hello **IActivityLogger** información sobre los objetos toolog que le ayude a solucionar problemas. mensajes de saludo registrado aparecen en usuario hello\_archivo de registro de 0.

   Hola **OutputDataset** hoja, haga clic en Hola segmento toosee Hola **el segmento de datos** hoja para dicho sector. Verá **ejecuciones de actividad** para ese segmento. Debería ver una actividad ejecutar para el intervalo de saludo. Si hace clic en **ejecutar** en la barra de comandos de hello, puede iniciar otra actividad ejecutar para hello mismo segmento.

   Al hacer clic en la ejecución de la actividad de hello, vea hello **detalles de ejecución de la actividad** hoja con una lista de archivos de registro. Vea los mensajes registrados en hello **usuario\_registro 0** archivo. Cuando se produce un error, verá tres ejecuciones de actividad porque Hola de reintentos se establece too3 en hello canalización/JSON de la actividad. Al hacer clic en la ejecución de la actividad de hello, consulte los archivos de registro de hello que se puede revisar el error de hello tootroubleshoot.

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   Hola lista de archivos de registro, haga clic en hello **0.log usuario**. En el panel derecho de Hola se muestran resultados de hello del uso de hello **IActivityLogger.Write** método.

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   Compruebe system-0.log para ver si hay alguna excepción o mensaje de error del sistema.

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. Incluir hello **PDB** de archivos en el archivo zip de Hola para que los detalles del error Hola tienen información como **pila de llamadas** cuando se produce un error.
4. Todos los Hola archivos en el archivo zip de hello para la actividad personalizada hello debe estar en hello **nivel superior** sin subcarpetas.

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. Asegúrese de que hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip), y **packageLinkedService** (debe Azure toohello de punto de almacenamiento de blobs que contiene el archivo zip de Hola) se establecen valores de toocorrect.
6. Si corrige un segmento de hello tooreprocess error y quiere, haga clic en segmento Hola Hola **OutputDataset** hoja y haga clic en **ejecutar**.

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > Verá un **contenedor** en la instancia de Azure Blob Storage denominado: `adfjobs`. Este contenedor no se elimina automáticamente, pero puede eliminarla con seguridad una vez que haya solución Hola pruebas. De forma similar, Hola solución factoría de datos crea un lote de Azure **trabajo** denominado: `adf-\<pool ID/name\>:job-0000000001`. Puede eliminar este trabajo después de probar soluciones de hello si lo desea.
   >
   >
7. actividad personalizada Hello no utiliza hello **app.config** archivo desde el paquete. Por lo tanto, si el código lee las cadenas de conexión del archivo de configuración de hello, no funciona en tiempo de ejecución. Hola se recomienda una vez con Azure Batch toohold los secretos en un **KeyVault Azure**, use un keyvault de hello tooprotect principal de servicio basada en certificados y distribuir el grupo de lote de hello certificado tooAzure. Hola actividad personalizada. NET, a continuación, puede tener acceso a los secretos de hello KeyVault en tiempo de ejecución. Esta solución es un genérico y puede escalarse tooany tipo de secreto, no solo la cadena de conexión.

    Hay una solución más fácil (pero no es una práctica recomendada): puede crear un **servicio vinculado de SQL Azure** con valores de cadena de conexión, cree un conjunto de datos que usa Hola servicios vinculados y conjunto de datos de cadena Hola como un conjunto de datos de entrada ficticio toohello la actividad personalizada. NET. También puede, a continuación, Hola de acceso vinculado cadena de conexión del servicio en el código de actividad personalizada hello y debe funcionar bien en tiempo de ejecución.  

#### <a name="extend-hello-sample"></a>Ampliar el ejemplo hello
Puede extender este ejemplo toolearn más información sobre las características de Data Factory de Azure y Azure Batch. Por ejemplo, sectores tooprocess en un intervalo de tiempo diferente, Hola pasos:

1. Agregar Hola siguiendo las subcarpetas de Hola `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 09-2015-11-16 y coloque los archivos de entrada en esas carpetas. Cambiar la hora de finalización de Hola de canalización de Hola desde `2015-11-16T05:00:00Z` demasiado`2015-11-16T10:00:00Z`. Hola **vista de diagrama**, haga doble clic en hello **InputDataset**y confirme que los segmentos de entrada de hello están listos. Haga doble clic en **OuptutDataset** toosee estado de saludo de los sectores de salida. Si se encuentran en estado listo, compruebe la carpeta de salida de hello de archivos de salida de hello.
2. Aumentar o disminuir hello **simultaneidad** configuración toounderstand cómo afecta al rendimiento de saludo de la solución, especialmente Hola de procesamiento que se produce en el lote de Azure. (Vea el paso 4: crear y ejecutar la canalización de Hola para obtener más información sobre hello **simultaneidad** configuración.)
3. Cree un grupo con un valor mayor o menor en **Máximo de tareas por máquina virtual**. toouse Hola nuevo grupo creado, Hola de actualización de servicio vinculado Azure Batch en soluciones de hello factoría de datos. (Vea el paso 4: crear y ejecutar la canalización de Hola para obtener más información sobre hello **tareas máxima por máquina virtual** configuración.)
4. Cree un grupo de Azure Batch con la característica de **escalado automático** . El escalado automático de nodos de proceso en un grupo de lote de Azure es realizar un ajuste dinámico Hola de procesamiento de la potencia utilizada por la aplicación. 

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
5. En la solución de ejemplo de Hola Hola **Execute** método invoca hello **Calculate** método que procesa una tooproduce de segmento de datos de entrada un segmento de datos de salida. Puede escribir su propio método tooprocess los datos de entrada y reemplace la llamada al método Calculate de hello en el método Execute de hello con un método de llamada tooyour.

### <a name="next-steps-consume-hello-data"></a>Pasos siguientes: consumir datos Hola
Después de procesar datos, puede consumirlos con herramientas en línea como **Microsoft Power BI**. Estos son toohelp vínculos entender Power BI y cómo toouse en Azure:

* [Exploración de un conjunto de datos en Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [Introducción a Hola Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [Actualizar datos en Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [Azure y Power BI](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a>Referencias
* [Factoría de datos de Azure](https://azure.microsoft.com/documentation/services/data-factory/)

  * [Introducción tooAzure servicio de factoría de datos](data-factory-introduction.md)
  * [Introducción a Azure Data Factory](data-factory-build-your-first-pipeline.md)
  * [Uso de actividades personalizadas en una canalización de Factoría de datos de Azure](data-factory-use-custom-activities.md)
* [Azure Batch](https://azure.microsoft.com/documentation/services/batch/)

  * [Datos básicos de Lote de Batch](../batch/batch-technical-overview.md)
  * [Información general de las características de Azure Batch](../batch/batch-api-basics.md)
  * [Crear y administrar la cuenta de Azure Batch en hello portal de Azure](../batch/batch-account-create-portal.md)
  * [Introducción a la biblioteca de Lote de Azure para .NET](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
