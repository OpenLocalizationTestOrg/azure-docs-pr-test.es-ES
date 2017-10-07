---
title: aaaPersist resultados o registros de completar datos tooa trabajos y tareas store - Azure Batch | Documentos de Microsoft
description: Conozca las diferentes opciones para guardar los datos de salida de las tareas y los trabajos del servicio Batch. Puede conservar los datos de almacenamiento de tooAzure o tooanother de datos almacenar.
services: batch
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0b11e387f1694e1ce3e9573db7f6013f0154cad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-output"></a>Trabajo persistente y resultado de la tarea

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Algunos ejemplos comunes de resultados de tareas incluyen:

- Archivos creados cuando los datos de entrada de procesos de la tarea de Hola.
- Archivos de registro asociados con la ejecución de tareas. 

Este artículo describen varias opciones para conservar escenarios de hello y salida de tarea para el que cada opción es más adecuada.   

## <a name="about-hello-batch-file-conventions-standard"></a>Acerca de estándar de hello convenciones de archivos por lotes

Batch define un conjunto opcional de convenciones para nombrar los archivos de salida de tareas en Azure Storage. Hola [estándar convenciones de archivo por lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) describe estas convenciones. estándar de archivo convenciones Hola determina los nombres de Hola de hello contenedor y blob de ruta de destino en el almacenamiento de Azure para un archivo de salida determinado basándose en los nombres de Hola de hello trabajos y tareas.

Es una tooyou si decide toouse Hola convenciones de archivo estándar para asignar nombres a los archivos de datos de salida. También puede nombrar blob y el contenedor de destino de hello pero desea. Si utilizas Hola convenciones de archivo estándar para asignar nombres a archivos de salida, los archivos de salida están disponibles para su visualización en hello [portal de Azure][portal].

Hay varias maneras diferentes que puede usar el estándar de hello convenciones de archivo:

- Si usa archivos de salida de hello lote servicio API toopersist, puede elegir tooname contenedores de destino y los blobs según toohello convenciones de archivo estándar. Hola API del servicio de lote permite toopersist archivos de salida desde el código de cliente, sin necesidad de modificar la aplicación de la tarea.
- Si está desarrollando con. NET, puede usar hello [biblioteca convenciones de archivos por lotes de Azure para .NET][nuget_package]. Una ventaja de usar esta biblioteca es que admite consultar los archivos de salida según el Id. de tootheir o propósito. funciones de consulta integradas Hola hace fácil tooaccess archivos de salida de una aplicación cliente o de otras tareas. Sin embargo, la aplicación de la tarea debe ser modificada toocall biblioteca de convenciones de archivo. Para obtener más información, consulte referencia de Hola para hello [biblioteca convenciones de archivos para .NET](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.aspx).
- Si va a desarrollar con un lenguaje distinto de. NET, puede implementar Hola archivo convenciones estándar de la aplicación.

## <a name="design-considerations-for-persisting-output"></a>Consideraciones de diseño para el almacenamiento de la salida 

Cuando diseñe la solución de lote, considere la posibilidad de siguiente Hola factores relacionado toojob y resultados de las tareas.

* **Duración del nodo de proceso**: los nodos de proceso a menudo son transitorios, especialmente en los grupos con escalado automático habilitado. Salida de una tarea que se ejecuta en un nodo solo está disponible al nodo de hello existe, y solo durante el período de retención de archivos de Hola que has establecido para la tarea hello. Si una tarea produce un resultado que se necesite una vez completada la tarea hello, tarea hello debe cargar su almacén duradero de salida archivos tooa como almacenamiento de Azure.

* **Almacenamiento de la salida**: Azure Storage es el almacén de datos recomendado para la salida de tareas; no obstante, puede usar cualquier almacenamiento duradero. Escribir tareas salida tooAzure almacenamiento se integra en hello API del servicio de lote. Si utiliza otro formato de almacenamiento duradero, necesitará resultado de la tarea de toowrite Hola aplicación lógica toopersist usted mismo.   

* **Recuperación de salida**: puede recuperar resultado de la tarea directamente desde los nodos de proceso de hello en el grupo, o desde el almacenamiento de Azure o en otro almacén de datos si ha conservado la salida de la tarea. tooretrieve una tarea de salida de directamente desde un nodo de proceso, necesita el nombre del archivo de Hola y su ubicación de salida en el nodo de Hola. Si continúa tooAzure de salida de tareas almacenamiento, debe toohello archivo de ruta de acceso completa de hello en archivos de salida de almacenamiento de Azure toodownload Hola con hello SDK de almacenamiento de Azure.

* **Ver la salida de**: cuando se desplaza tooa tarea del lote en hello Azure portal y seleccione **archivos en el nodo**, se presentan todos los archivos asociados con la tarea hello, Hola no solo los archivos de salida que le interesa. Una vez más, archivos en nodos de proceso están disponibles solo mientras existe el nodo de Hola y solo en tiempo de retención de archivos de Hola ha establecido para la tarea hello. salida de la tarea de tooview que ha guardado tooAzure almacenamiento, puede usar Hola portal de Azure o una aplicación de cliente de almacenamiento de Azure como hello [Azure Storage Explorer][storage_explorer]. tooview los datos en el almacenamiento de Azure con el portal de hello u otra herramienta de salida, debe conocer la ubicación del archivo de Hola y navegar directamente tooit.

## <a name="options-for-persisting-output"></a>Opciones para almacenar la salida

Según el escenario, hay diferentes enfoques que puede seguir el resultado de la tarea de toopersist:

- Usar API de servicio de lote de Hola.  
- Utilice la biblioteca de convenciones de archivo por lotes de Hola para. NET.  
- Implementar Hola lote archivo convenciones estándar de la aplicación.
- Implementar una solución personalizada de movimiento de archivos.

Hola siguientes secciones describe cada enfoque con más detalle.

### <a name="use-hello-batch-service-api"></a>Usar API de servicio de lote Hola

Con la versión de 2017-05-01, Hola servicio por lotes agrega compatibilidad para especificar archivos de salida en el almacenamiento de Azure para datos de la tarea cuando se [agregar un trabajo de tarea tooa](https://docs.microsoft.com/rest/api/batchservice/add-a-task-to-a-job) o [agregar una colección de trabajo de tareas tooa](https://docs.microsoft.com/rest/api/batchservice/add-a-collection-of-tasks-to-a-job).

Hola API del servicio por lotes admite tooan de datos de persistencia tarea cuenta de almacenamiento de Azure de los grupos creados con la configuración de máquina virtual de Hola. Con hello API del servicio de lote, puede conservar datos de la tarea sin modificar la aplicación hello que se ejecuta la tarea. Si lo desea puede cumplir toohello [estándar convenciones de archivo por lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) para asignar nombres a los archivos de Hola que se mantendrán tooAzure almacenamiento. 

Utilice la tarea de toopersist de hello API del servicio de lote de salida cuando:

- Desea que los datos de toopersist de tareas por lotes y las tareas de administrador en los grupos creados con la configuración de máquina virtual de Hola.
- Desea que el contenedor de almacenamiento Azure tooan toopersist de datos con un nombre arbitrario.
- Desea que el contenedor de almacenamiento de Azure toopersist datos tooan denominado toohello correspondiente [estándar convenciones de archivo por lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

> [!NOTE]
> Hola API del servicio de lote no admite almacenar datos de tareas que se ejecutan en los grupos creados con la configuración del servicio de nube de Hola. Para obtener información acerca de la tarea de persistencia de salida de los grupos de configuración de servicios de nube de hello, consulte [conservar trabajos y tareas tooAzure datos almacenamiento con la biblioteca de convenciones de archivo por lotes de Hola para .NET toopersist](batch-task-output-file-conventions.md)
> 
> 

Para obtener más información sobre el resultado de la tarea de persistencia con hello API del servicio de lote, consulte [tooAzure de datos de tarea almacenamiento con hello API del servicio de lote se conservan](batch-task-output-files.md). Consulte también Hola proyecto en GitHub, que muestra cómo la biblioteca de cliente de toouse Hola por lotes para tareas de .NET toopersist salida toodurable almacenamiento de ejemplo [PersistOutputs] [github_persistoutputs].

### <a name="use-hello-batch-file-conventions-library-for-net"></a>Usar la biblioteca de convenciones de archivo por lotes de Hola para .NET

Los desarrolladores compilar soluciones de lote con C# y .NET pueden usar hello [biblioteca convenciones de archivos para .NET] [ nuget_package] toopersist tarea datos tooan cuenta de almacenamiento de Azure, según toohello [archivo por lotes Convenciones estándares](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). biblioteca de convenciones de archivos de Hello controla móvil tooAzure de archivos de salida almacenamiento y nomenclatura de contenedores de destino y blobs de una manera muy conocida.

ellos sin necesidad de Hola Hola convenciones de archivos admite la biblioteca consultar archivos de salida por identificador o propósito, lo que toolocate fácil completar archivo URI. 

Utilizar la biblioteca de convenciones de archivo por lotes de Hola para tareas de .NET toopersist de salida cuando:

- Desea toostream datos tooAzure almacenamiento mientras todavía se ejecuta la tarea hello.
- Desea que los datos de toopersist de los grupos creados con la configuración del servicio de nube de Hola o configuración de máquina virtual de Hola.
- La aplicación cliente u otras tareas de hello toolocate de necesidades del trabajo y descargar los archivos de salida de tareas por Id. o por propósito. 
- Desea tooperform carga orientada hacia la comprobación o temprano de primeros resultados.
- Desea que el resultado de la tarea de tooview Hola portal de Azure.

Para obtener más información sobre Guardar resultado de la tarea con la biblioteca de convenciones de archivos de Hola para. NET, vea [conservar trabajos y tareas tooAzure datos almacenamiento con la biblioteca de convenciones de archivo por lotes de Hola para .NET toopersist ](batch-task-output-file-conventions.md). Consulte también Hola proyecto en GitHub, que muestra la biblioteca de toouse Hola convenciones de archivo para tareas de .NET toopersist salida toodurable almacenamiento de ejemplo [PersistOutputs] [github_persistoutputs].

Hello [PersistOutputs] [github_persistoutputs] el proyecto de ejemplo en GitHub muestra cómo la biblioteca de cliente de toouse Hola por lotes para tareas de .NET toopersist había salida toodurable almacenamiento.

### <a name="implement-hello-batch-file-conventions-standard"></a>Implementar Hola convenciones de archivo por lotes estándar

Si se usa un lenguaje distinto de. NET, puede implementar hello [estándar convenciones de archivo por lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) en su propia aplicación. 

Puede que desee tooimplement Hola estándar de nombres de archivo convenciones por sí mismo cuando se desea un esquema de nomenclatura de eficacia comprobado, o cuando desee que el resultado de la tarea de tooview Hola portal de Azure.

### <a name="implement-a-custom-file-movement-solution"></a>Implementar una solución personalizada de movimiento de archivos

También puede implementar su propia solución completa de movimiento de archivos. Use este enfoque en los siguientes casos:

- Desea que el almacén de datos de tooa toopersist tarea datos que no sea el almacenamiento de Azure. almacén de datos de tooupload archivos tooa como SQL Azure o DataLake de Azure, puede crear un script personalizado o una ubicación de toothat tooupload ejecutable. A continuación, puede llamarlo en línea de comandos de hello después de ejecutar el archivo ejecutable principal. Por ejemplo, en un nodo de Windows, puede llamar a estos dos comandos:`doMyWork.exe && uploadMyFilesToSql.exe`
- Desea tooperform carga orientada hacia la comprobación o temprano de primeros resultados.
- Desea toomaintain un control granular sobre el control de errores. Por ejemplo, puede que desee tooimplement su propia solución si desea toouse tarea dependencia acciones tootake ciertos cargar acciones según los códigos de salida de tarea específica. Para obtener más información sobre las acciones de dependencia de tareas, consulte [crear dependencias entre tareas toorun tareas que dependen de otras tareas](batch-task-dependencies.md). 

## <a name="next-steps"></a>Pasos siguientes

- Explorar uso Hola nuevas características de datos de la tarea hello API del servicio de lote toopersist en [tooAzure de datos de tarea almacenamiento con hello API del servicio de lote se conservan](batch-task-output-files.md).
- Obtenga información acerca del uso de biblioteca de convenciones de archivo por lotes de Hola para .NET en [conservar trabajos y tareas tooAzure datos almacenamiento con la biblioteca de convenciones de archivo por lotes de Hola para .NET toopersist ](batch-task-output-file-conventions.md).
- Vea Hola [PersistOutputs] [github_persistoutputs] toodurable almacenamiento de resultados del proyecto de ejemplo en GitHub, que demuestra cómo toouse ambos Hola biblioteca de cliente de Batch para .NET y la biblioteca de convenciones de archivos de Hola para tareas de .NET toopersist.

[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/
