---
title: aaaGet a trabajar con el almacenamiento de blobs y Visual Studio servicios conectados (proyectos de trabajo Web) | Documentos de Microsoft
description: "Servicios conectados cómo tooget a usar almacenamiento de blobs en un proyecto WebJob después de conectarse tooan almacenamiento de Azure mediante Visual Studio."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: cb2cecacbb1a59f093d5453a91fae33e0f279d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a>Introducción al almacenamiento de blobs de Azure y servicios conectados de Visual Studio (proyectos de WebJobs)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Información general
Este artículo proporciona C# de ejemplos de código que muestran cómo tootrigger un proceso cuando se crea o actualiza un blob de Azure. ejemplos de código de Hello usan hello [SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versión 1.x. Cuando agrega un proyecto de WebJob de tooa de cuenta de almacenamiento mediante el uso de Visual Studio hello **agregar servicios conectados** cuadro de diálogo, paquetes de NuGet de almacenamiento de Azure apropiada de hello está instalado, las referencias adecuadas de .NET Hola son toohello agregado proyecto y cadenas de conexión para la cuenta de almacenamiento de Hola se actualizan en el archivo App.config de hello.

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a>¿Cómo tootrigger una función cuando se crea o actualiza un blob
Esta sección se muestra cómo hello toouse **BlobTrigger** atributo.

 **Nota:** Hola archivos de registro de SDK de WebJobs exámenes toowatch para blobs nuevos o modificados. Este proceso es inherentemente lento; una función podría no obtener activada hasta varios minutos o más una vez creado el blob de Hola.  Si la aplicación necesita tooprocess blobs inmediatamente, Hola recomendado método es toocreate un mensaje de la cola al crear Hola blob y usar hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) atributo en lugar de hello **BlobTrigger** atributo en función de Hola que procesa el blob de Hola.

### <a name="single-placeholder-for-blob-name-with-extension"></a>Único marcador de posición para el nombre de blob con extensión
Hello siguiente ejemplo de código copia blobs de texto que aparecen en hello *entrada* contenedor toohello *salida* contenedor:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

constructor de atributo de Hello toma un parámetro de cadena que especifica el nombre del contenedor de Hola y un marcador de posición para el nombre del blob de Hola. En este ejemplo, si un blob denominado *Blob1.txt* se crea en hello *entrada* contenedor, la función hello crea un blob denominado *Blob1.txt* en hello *salida*  contenedor.

Puede especificar un patrón de nombre con el marcador de posición de nombre de blob de hello, como se muestra en el siguiente ejemplo de código de hello:

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Este código solo copia blobs con nombres que comienzan con "original-". Por ejemplo, *original Blob1.txt* en hello *entrada* contenedor se copia demasiado*copia Blob1.txt* en hello *salida* contenedor.

Si necesita toospecify un patrón de nombre para los nombres de blob que tienen las llaves en nombre de hello, doble llaves Hola. Por ejemplo, si desea toofind blobs hello *imágenes* contenedor que tienen nombres similar al siguiente:

        {20140101}-soundfile.mp3

use esto para el patrón:

        images/{{20140101}}-{name}

En el ejemplo de Hola, Hola *nombre* sería el valor de marcador de posición *soundfile.mp3*.

### <a name="separate-blob-name-and-extension-placeholders"></a>Separar marcadores de posición de extensión y nombre de blob
Hello cambios de ejemplo de código siguiente Hola extensión de archivo mientras realiza la copia blobs que aparecen en hello *entrada* contenedor toohello *salida* contenedor. código de Hello registra extensión Hola de hello *entrada* blob y establece la extensión de Hola de hello *salida* blob demasiado*.txt*.

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a name="types-that-you-can-bind-tooblobs"></a>Tipos que se pueden enlazar tooblobs
Puede usar hello **BlobTrigger** atributo Hola siguientes tipos:

* **cadena**
* **TextReader**
* **Stream**
* **ICloudBlob**
* **CloudBlockBlob**
* **CloudPageBlob**
* Otros tipos deserializados por [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)

Si desea que toowork directamente con hello cuenta de almacenamiento de Azure, también puede agregar un **CloudStorageAccount** firma del método toohello parámetro.

## <a name="getting-text-blob-content-by-binding-toostring"></a>Obtener contenido de blob de texto toostring de enlace
Si se esperan que los blobs de texto, **BlobTrigger** puede ser aplicada tooa **cadena** parámetro. ejemplo de código siguiente Hello enlaza un tooa de blob de texto **cadena** parámetro denominado **logMessage**. función Hello utiliza ese contenido de parámetro toowrite Hola de hello blob toohello panel de SDK de WebJobs.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a>Obtención del contenido del blob serializado mediante el uso de ICloudBlobStreamBinder
Hello ejemplo de código siguiente utiliza una clase que implementa **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** toobind toohello de un blob de atributo **WebImage** tipo.

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK",
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

Hola **WebImage** código de enlace se proporciona en un **WebImageBinder** clase que deriva de **ICloudBlobStreamBinder**.

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input,
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="how-toohandle-poison-blobs"></a>¿Cómo toohandle dudosos blobs
Cuando un **BlobTrigger** produce un error de la función, Hola SDK lo llama una vez más, en caso de error de hello fue provocado por un error transitorio. Si se produce un error de hello en contenido de Hola de blob de hello, se produce un error en la función hello cada vez que trata de blob de hello tooprocess. De forma predeterminada, Hola SDK llama a una función too5 horas para un blob determinado. Si se produce un error en try quinto hello, Hola SDK agrega una cola de tooa de mensaje denominada *webjobs-blobtrigger-dudosos*.

Hola número máximo de reintentos es configurable. Hola mismo [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) configuración se utiliza para el control de mensajes dudosos blob y control de mensajes de la cola de mensajes dudosos.

mensaje de la cola de Hola para blobs dudosos es un objeto JSON que contiene Hola propiedades siguientes:

* FunctionId (en formato de hello *{nombre del trabajo Web}*. Las funciones. *{Nombre de la función}*, por ejemplo: WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" o "PageBlob")
* ContainerName
* BlobName
* ETag (un identificador de la versión del blob, por ejemplo: "0x8D1DC6E70A277EF")

En los siguientes Hola ejemplo de código, hello **CopyBlob** función tiene código que causa toofail cada vez que se llama. Después de hello SDK lo llama para el número máximo de Hola de reintentos, se crea un mensaje en cola de mensajes dudosos blob hello y ese mensaje sea procesado por hello **LogPoisonBlob** (función).

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

Hola SDK automáticamente deserializa el mensaje de bienvenida de JSON. Aquí es hello **PoisonBlobMessage** clase:

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a>Algoritmo de sondeo de blobs
Hola SDK de WebJobs examina todos los contenedores especificados por **BlobTrigger** atributos al iniciarse la aplicación. En una cuenta de almacenamiento de gran tamaño, este análisis puede demorar un tiempo, por lo que podría pasar mucho tiempo antes de que se encuentren blobs nuevos y que se ejecuten las funciones **BlobTrigger** .

toodetect blobs nuevos o modificados después de iniciarse la aplicación, los registros de hello que SDK lee periódicamente Hola almacenamiento de blobs. Hello registros del blob se almacenan en búfer y que sólo obtengan físicamente escribir cada 10 minutos o por lo tanto, por lo que puede haber un retraso importante después de un blob se crea o se actualiza antes de hello correspondiente **BlobTrigger** se ejecuta la función.

Hay una excepción para los blobs que creas mediante hello **Blob** atributo. Cuando Hola SDK de WebJobs crea un nuevo blob, pasa inmediatamente nuevo blob en hello coincidencia tooany **BlobTrigger** funciones. Por lo tanto, si tiene una cadena de blob entradas y salidas, Hola SDK pueda procesarlos eficazmente. Pero si desea baja latencia de ejecución para sus funciones de procesamiento de blobs para blobs que se crean o actualizan mediante otros medios, se recomienda usar **QueueTrigger** en lugar de **BlobTrigger**.

### <a name="blob-receipts"></a>Recepciones de blobs
Hola SDK de WebJobs asegura de que ninguna **BlobTrigger** función obtiene llama más de una vez para hello mismo nuevo o actualiza el blob. Esto consigue mediante mantener *blob confirmaciones* en orden toodetermine si se ha procesado una versión determinada de blob.

Confirmaciones de BLOB se almacenan en un contenedor denominado *hosts de webjobs de azure* de cuenta de almacenamiento de Azure Hola especificado por la cadena de conexión de AzureWebJobsStorage Hola. Una confirmación de blob tiene Hola siguiente información:

* Hola función a la que se llamó para el blob de hello ("*{nombre del trabajo Web}*. Las funciones. *{Nombre de la función}*", por ejemplo:"WebJob1.Functions.CopyBlob")
* nombre del contenedor de Hola
* tipo de blob de Hello ("BlockBlob" o "PageBlob")
* nombre del blob Hola
* Hola ETag (un identificador de versión de blob, por ejemplo: "0x8D1DC6E70A277EF")

Si desea volver a procesar tooforce de un blob, puede eliminar manualmente el recibo de blob de Hola para dicho blob de hello *hosts de webjobs de azure* contenedor.

## <a name="related-topics-covered-by-hello-queues-article"></a>Temas relacionados cubiertos por artículo de colas de Hola
Para obtener información acerca de cómo el procesamiento de blob toohandle desencadenada por un mensaje de la cola, o de trabajos Web escenarios SDK no tooblob específica de procesamiento, vea [cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).

Temas relacionados que se tratan en dicho artículo Hola siguientes:

* Funciones asincrónicas
* Varias instancias
* Apagado correcto
* Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función
* Establecer las cadenas de conexión de SDK de hello en el código.
* Establecer valores para los parámetros del constructor del SDK de WebJobs en el código
* Configure **MaxDequeueCount** para el control de blobs dudosos.
* Desencadenar una función manualmente
* Escribir registros

## <a name="next-steps"></a>Pasos siguientes
En este artículo se proporciona ejemplos de código que muestran cómo los blobs toohandle escenarios comunes para trabajar con Azure. Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?linkid=390226).

