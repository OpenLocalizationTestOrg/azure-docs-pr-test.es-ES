---
title: aaa "variables de entorno de nodo de proceso de Azure Batch | Documentos de Microsoft"
description: Referencia de la variable de entorno de nodo de proceso para Azure Batch Analytics.
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/05/2017
ms.author: tamram
ms.openlocfilehash: 860f34b530579a81fbd5cf8ffa31df79d917c080
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-compute-node-environment-variables"></a>Variables de entorno del nodo de ejecución de Azure Batch
Hola [servicio Azure Batch](https://azure.microsoft.com/services/batch/) establece Hola siguiendo las variables de entorno en nodos de proceso. Puede hacer referencia a estas variables de entorno en líneas de comandos de la tarea y en programas de Hola y ejecutan scripts mediante líneas de comandos de Hola.

Para obtener más información sobre el uso de variables del entorno con Batch, consulte [Configuración del entorno para las tareas](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks).

## <a name="environment-variable-visibility"></a>Visibilidad de la variable del entorno

Estas variables de entorno son visibles solo en el contexto de Hola de hello **usuario tareas**, Hola cuenta de usuario en el nodo de hello en la que se ejecuta una tarea. Que se van a *no* verlas si se [conectarse de forma remota](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes) tooa nodo a través del protocolo de escritorio remoto (RDP) o Secure Shell (SSH) y lista de variables de entorno de Hola de proceso. Es igual que la cuenta de hello que es utilizada por la tarea hello porque la cuenta de usuario de Hola que se usa para la conexión remota no es Hola.

## <a name="command-line-expansion-of-environment-variables"></a>Expansión de línea de comandos de las variables del entorno

líneas de comandos de Hello ejecutadas las tareas en proceso no se ejecutan en un shell de los nodos. Por lo tanto, estas líneas de comandos de forma nativa no se puede aprovechar las ventajas de características del shell, como la expansión de variables de entorno (Esto incluye hello `PATH`). tootake provecho de estas características, debe **invocar shell hello** en línea de comandos de Hola. Por ejemplo, ejecute `cmd.exe` en nodos de proceso en Windows o `/bin/sh` en nodos de Linux:

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>Variables de entorno

| Nombre de la variable                     | Descripción                                                              | Disponibilidad | Ejemplo |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| AZ_BATCH_ACCOUNT_NAME           | Hola nombre de cuenta de lote de Hola Hola tarea pertenece.                  | Todas las tareas.   | mybatchaccount |
| AZ_BATCH_CERTIFICATES_DIR       | Un directorio en hello [directorio de trabajo de tarea] [ files_dirs] en qué certificados se almacenan para Linux nodos de proceso. Tenga en cuenta que esta variable de entorno no se aplica tooWindows nodos de proceso.                                                  | Todas las tareas.   |  /mnt/batch/tasks/workitems/batchjob001/job-1/task001/certs |
| AZ_BATCH_JOB_ID                 | Id. de Hello del trabajo de Hola que Hola tarea que pertenece. | Todas las tareas excepto la tarea de inicio. | batchjob001 |
| AZ_BATCH_JOB_PREP_DIR           | ruta de acceso completa de Hola de preparación del trabajo hello [directorio tareas] [ files_dirs] en el nodo de Hola. | Todas las tareas excepto la tarea de inicio y la tarea de preparación del trabajo. Solo está disponible si el trabajo de Hola se configura con una tarea de preparación del trabajo. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation |
| AZ_BATCH_JOB_PREP_WORKING_DIR   | ruta de acceso completa de Hola de preparación del trabajo hello [directorio de trabajo de tarea] [ files_dirs] en el nodo de Hola. | Todas las tareas excepto la tarea de inicio y la tarea de preparación del trabajo. Solo está disponible si el trabajo de Hola se configura con una tarea de preparación del trabajo. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd |
| AZ_BATCH_NODE_ID                | Id. de Hola de nodo Hola Hola tarea se asigna a. | Todas las tareas. | tvm-1219235766_3-20160919t172711z |
| AZ_BATCH_NODE_ROOT_DIR          | ruta de acceso completa de Hola de raíz de Hola de todos los [por lotes directorios] [ files_dirs] en el nodo de Hola. | Todas las tareas. | C:\user\tasks |
| AZ_BATCH_NODE_SHARED_DIR        | ruta de acceso completa de Hola de hello [directorio compartido] [ files_dirs] en el nodo de Hola. Todas las tareas que se ejecutan en un nodo tienen acceso de lectura/escritura toothis directory. Las tareas que se ejecutan en otros nodos no tienen directorio toothis de acceso remoto (no es un directorio de red "compartido"). | Todas las tareas. | C:\user\tasks\shared |
| AZ_BATCH_NODE_STARTUP_DIR       | ruta de acceso completa de Hola de hello [iniciar directorio tareas] [ files_dirs] en el nodo de Hola. | Todas las tareas. | C:\user\tasks\startup |
| AZ_BATCH_POOL_ID                | Id. de Hello del grupo de Hola Hola tarea se está ejecutando. | Todas las tareas. | batchpool001 |
| AZ_BATCH_TASK_DIR               | ruta de acceso completa de Hola de hello [directorio tareas] [ files_dirs] en el nodo de Hola. Este directorio contiene Hola `stdout.txt` y `stderr.txt` para la tarea hello y hello AZ_BATCH_TASK_WORKING_DIR. | Todas las tareas. | C:\user\tasks\workitems\batchjob001\job-1\task001 |
| AZ_BATCH_TASK_ID                | Hola Id. de tarea actual Hola. | Todas las tareas excepto la tarea de inicio. | task001 |
| AZ_BATCH_TASK_WORKING_DIR       | ruta de acceso completa de Hola de hello [directorio de trabajo de tarea] [ files_dirs] en el nodo de Hola. Hola actuales tarea tiene acceso de lectura/escritura toothis directory. | Todas las tareas. | C:\user\tasks\workitems\batchjob001\job-1\task001\wd |
| CCP_NODES                       | lista de Hola de nodos y el número de núcleos por nodo que se asignan tooa [tareas varias instancias][multi_instance]. Nodos y núcleos se muestran en formato de Hola`numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`, donde número Hola de nodos es seguido de uno o más direcciones IP del nodo y número de Hola de núcleos para cada uno. |  Tareas principales y secundarias de varias instancias. |`2 10.0.0.4 1 10.0.0.5 1` |
| AZ_BATCH_NODE_LIST              | lista de Hola de nodos que se asignan tooa [tareas varias instancias] [ multi_instance] en formato de hello `nodeIP;nodeIP`. | Tareas principales y secundarias de varias instancias. | `10.0.0.4;10.0.0.5` |
| AZ_BATCH_HOST_LIST              | lista de Hola de nodos que se asignan tooa [tareas varias instancias] [ multi_instance] en formato de hello `nodeIP,nodeIP`. | Tareas principales y secundarias de varias instancias. | `10.0.0.4,10.0.0.5` |
| AZ_BATCH_MASTER_NODE            | Hello dirección IP y puerto de hello nodo de ejecución de la tarea principal de Hola de un [tareas varias instancias] [ multi_instance] se ejecuta. | Tareas principales y secundarias de varias instancias. | `10.0.0.4:6000`|
| AZ_BATCH_TASK_SHARED_DIR | Una ruta de acceso de directorio que es idéntica para la tarea principal de hello y cada subtarea de un [tareas varias instancias][multi_instance]. Hello ruta de acceso existe en cada nodo en el que se ejecuta la tarea de varias instancias de Hola y es accesible toohello comandos de tarea ejecutando en ese nodo de lectura/escritura (ambos hello [comando coordinación] [ coord_cmd] hello y[comando aplicaciones][app_cmd]). Subtareas o una tarea principal que se ejecutan en otros nodos no tiene directorio toothis de acceso remoto (no es un directorio de red "compartido"). | Tareas principales y secundarias de varias instancias. | C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask |
| AZ_BATCH_IS_CURRENT_NODE_MASTER | Especifica si el nodo actual de hello es nodo maestro de Hola para un [tareas varias instancias][multi_instance]. Los valores posibles son `true` y `false`.| Tareas principales y secundarias de varias instancias. | `true` |
| AZ_BATCH_NODE_IS_DEDICATED | Si `true`, nodo de hello actual es un nodo dedicado. Si `false`, es un [nodo de prioridad baja](batch-low-pri-vms.md). | Todas las tareas. | `true` |

[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command
