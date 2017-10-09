---
title: ejemplos de almacenamiento de aaaAzure mediante Java | Documentos de Microsoft
description: "Consulte, descargue y ejecute código de ejemplo y aplicaciones para Almacenamiento de Azure. Detectar Introducción ejemplos para blobs, colas, tablas y archivos, utilizando las bibliotecas cliente de almacenamiento de Java de Hola."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 6aec326cbfedc1166fc61037ac39d33c15d28d2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a>Ejemplos de Azure Storage con Java

## <a name="java-sample-index"></a>Índice de ejemplos Java

Hello tabla siguiente proporciona una visión general de nuestros ejemplos hello y repositorio escenarios incluidas en cada ejemplo. Haga clic en hello vínculos tooview Hola correspondiente código de ejemplo en GitHub.

<table style="font-size:90%"><thead><tr><th style="font-size:110%">Extremo</th><th style="font-size:110%">Escenario</th><th style="font-size:110%">Código de ejemplo</th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><b>Blob</b></td>
<td>Append Blob</td> 
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td> 
</tr> 
<tr> 
<td>Blob en bloques</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr> 
<tr> 
<td>Cifrado de cliente</td>
<td><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Introducción a Cifrado de cliente de Azure en Java</a></td>
</tr> 
<tr> 
<td>Copia de blobs</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr> 
<tr> 
<td>Create Container</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr> 
<tr> 
<td>Delete Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr> 
<tr> 
<td>Delete Container</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr> 
<tr> 
<td>Metadatos/propiedades/estadísticas de blobs</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr> 
<tr> 
<td>ACL/metadatos/propiedades de contenedor</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr> 
<tr> 
<td>Get Page Ranges</td>
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Ejemplo de pruebas de blob en páginas</a></td>
</tr> 
<tr> 
<td>Contenedor/blob de concesión</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr> 
<tr> 
<td>Contenedor/blob de lista</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr> 
<tr> 
<td>Blob en páginas</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr>
<tr> 
<td>SAS</td>
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Ejemplo de pruebas de SAS</a></td>
</tr>   
<tr> 
<td>Propiedades de servicio</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr>           
<tr> 
<td>Instantánea de blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a> (Introducción a Blob service de Azure en Java)</td>
</tr> 
<tr> 
<td rowspan="9"><b>Archivo</b></td>
<td>Crear recursos compartidos/directorios/archivos</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</td> 
</tr>
<tr> 
<td>Eliminar recursos compartidos/directorios/archivos</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</td> 
</tr> 
<tr> 
<td>Metadatos/propiedades de directorio</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</td> 
</tr> 
<tr> 
<td>Descargar archivos</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</td> 
</tr> 
<tr> 
<td>Propiedades/metadatos/métricas de archivo</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</td> 
</tr> 
<tr> 
<td>Propiedades de servicio de archivo</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</td> 
</tr> 
<tr> 
<td>Directorios y archivos de lista</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</td> 
</tr>
<tr> 
<td>Recursos compartidos de lista</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</td> 
</tr>
<tr> 
<td>Propiedades/metadatos/estadísticas de recurso compartido</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a> (Introducción a Azure File service en Java)</td> 
</tr>
<tr> 
<td rowspan="8"><b>Cola</b></td>
<td>Agregar mensaje</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Ejemplos de la biblioteca de cliente de Java de Storage</a></td> 
</tr> 
<tr> 
<td>Cifrado de cliente</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Ejemplos de la biblioteca de cliente de Java de Storage</a></td> 
</tr> 
<tr> 
<td>Crear colas</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introducción al servicio Cola de Azure en .NET</a></td> 
</tr> 
<tr> 
<td>Eliminar mensaje/cola</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introducción al servicio Cola de Azure en .NET</a></td> 
</tr> 
<tr> 
<td>Inspección de mensajes</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introducción al servicio Cola de Azure en .NET</a></td> 
</tr> 
<tr> 
<td>ACL/metadatos/estadísticas de cola</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Introducción al servicio Cola de Azure en .NET</a></td> 
</tr> 
<tr> 
<td>Propiedades de Queue Service</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Introducción al servicio Cola de Azure en .NET</a></td> 
</tr> 
<tr> 
<td>Actualizar mensaje</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introducción al servicio Cola de Azure en .NET</a></td> 
</tr> 
<tr> 
<td rowspan="7"><b>Table</b></td>
<td>Crear tabla</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table service in Java</a> (Introducción a Azure Table service en Java)</td> 
</tr> 
<tr> 
<td>Eliminar entidad/tabla</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table service in Java</a> (Introducción a Azure Table service en Java)</td> 
</tr> 
<tr> 
<td>Insertar/combinar/reemplazar entidad</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Ejemplos de la biblioteca de cliente de Java de Storage</a></td> 
</tr> 
<tr> 
<td>Query Entities</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table service in Java</a> (Introducción a Azure Table service en Java)</td> 
</tr> 
<tr> 
<td>Consultar tablas</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table service in Java</a> (Introducción a Azure Table service en Java)</td> 
</tr> 
<tr> 
<td>ACL/propiedades de tabla</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table service in Java</a> (Introducción a Azure Table service en Java)</td> 
</tr> 
<tr> 
<td>Update Entity</td> 
<td><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Ejemplos de la biblioteca de cliente de Java de Storage</a></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a>Biblioteca de ejemplos de código de Azure

biblioteca de ejemplo completo de hello tooview, vaya toohello [ejemplos de código de Azure](https://azure.microsoft.com/resources/samples/?service=storage) library, que incluye ejemplos para el almacenamiento de Azure que puede descargar y ejecutar localmente. Biblioteca de código de ejemplo de Hola proporciona código de ejemplo en formato zip. Como alternativa, puede examinar y clonar el repositorio de GitHub de Hola para cada ejemplo.

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a>Guías de introducción

Extraer del repositorio Hola siguiendo guías si desea obtener instrucciones sobre cómo tooinstall y empezar a trabajar con hello bibliotecas de cliente de almacenamiento de Azure.

* [Getting Started with Azure Blob Service in Java](../blobs/storage-java-how-to-use-blob-storage.md) (Introducción a Blob service de Azure en Java)
* [Introducción al servicio Cola de Azure en .NET](../storage-java-how-to-use-queue-storage.md)
* [Getting Started with Azure Table service in Java](../../cosmos-db/table-storage-how-to-use-java.md) (Introducción a Azure Table service en Java)
* [Getting Started with Azure File Service in Java](../storage-java-how-to-use-file-storage.md) (Introducción a Azure File service en Java)

## <a name="next-steps"></a>Pasos siguientes

Para información sobre ejemplos para otros lenguajes:

* .NET: [ejemplos de Azure Storage con .NET](../storage-samples-dotnet.md)
* Todos los otros lenguajes: [ejemplos de Azure Storage](../storage-samples.md)
