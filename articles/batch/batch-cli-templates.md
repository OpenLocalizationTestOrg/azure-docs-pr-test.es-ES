---
title: "aaaRun Azure Batch trabajos to-end sin escribir código (versión preliminar) | Documentos de Microsoft"
description: Crear archivos de plantilla para grupos de hello Azure CLI toocreate por lotes, los trabajos y tareas.
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Uso de plantillas y transferencia de archivos de la CLI de Azure Batch (versión preliminar)

Con hello CLI de Azure es posible toorun los trabajos por lotes sin escribir código.

Archivos de plantilla se pueden crear y usar con hello CLI de Azure que permiten grupos por lotes, los trabajos y toobe de tareas crea. Archivos de entrada de trabajo se pueden cargar fácilmente a cuenta de almacenamiento de hello asociada Hola lote cuenta y trabajo de salida archivos descargados.

## <a name="overview"></a>Información general

Un toohello de extensión CLI de Azure permite por lotes toobe usa-to-end por los usuarios que no son programadores. Se puede crear un grupo, cargan los datos de entrada, trabajos y las tareas asociadas que se creó, y Hola resultante salida datos descargados: no se necesita, código Hola CLI que se va a usar directamente o que se integra en las secuencias de comandos.

Crear plantillas de proceso por lotes en hello [soporte técnico de lote existente en hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) que permite a los archivos JSON toospecify valores de propiedad para la creación de hello de grupos, trabajos, tareas y otros elementos. Con las plantillas de proceso por lotes, hello las capacidades siguientes se han agregado sobre lo que es posible con archivos JSON de hello:

-   Se pueden definir los parámetros. Cuando se usa la plantilla de hello, solo los valores de parámetro de hello son elementos de Hola de toocreate especificado, con otros valores de propiedad de elemento que se especifican en el cuerpo de la plantilla de Hola. Un usuario que se entiende por lotes y el toobe de las aplicaciones que se ejecutan por lotes puede crear plantillas, especificar el grupo de trabajo y valores de propiedad de la tarea. Un usuario menos familiarizados con el proceso por lotes o las aplicaciones solo necesita valores de hello toospecify para los parámetros de hello definido.

-   Generadores de tareas de trabajo cree uno o más tareas asociadas a un trabajo, evitar Hola necesitan para muchos toobe de definiciones de tarea creado y simplificar considerablemente el envío de trabajos.


Archivos de datos de entrada necesitan toobe proporcionado para los trabajos y a menudo se generan archivos de datos de salida. Se asocia una cuenta de almacenamiento, de forma predeterminada, con cada lote cuenta y archivos pueden ser tooand fácilmente transferido desde esta cuenta de almacenamiento mediante la CLI, sin codificación y credenciales de almacenamiento no necesitan.

Por ejemplo, [ffmpeg](http://ffmpeg.org/) es una aplicación popular que procesa archivos de audio y video. Hola CLI de lote de Azure puede ser usado tooinvoke ffmpeg tootranscode origen archivos de vídeo toodifferent resoluciones.

-   Se crea una plantilla de grupo. usuario de Hello crear plantilla de hello sabe cómo toocall Hola ffmpeg aplicación y a sus requisitos; especifican Hola SO adecuado, la máquina virtual de tamaño, cómo ffmpeg está instalado (de un paquete de aplicación o mediante un administrador de paquetes, por ejemplo) y otros valores de propiedad del grupo. Por lo que cuando se usa la plantilla de hello, solo el identificador del grupo de Hola y número de máquinas virtuales necesitan toobe especificado, se crean parámetros.

-   Se crea una plantilla de trabajo. plantilla de Hola de creación de Hello usuario sabe cómo ffmpeg necesidades toobe invoca otra resolución de tootranscode origen tooa vídeo y especifica la línea de comandos de la tarea de hello; También sabe que hay una carpeta que contiene los archivos de vídeo de origen de hello, con una tarea obligatoria por archivo de entrada.

-   Un usuario final con un conjunto de archivos de vídeo tootranscode primero crea un grupo mediante la plantilla de grupo de hello, especificar solo Id. de grupo de Hola y el número de máquinas virtuales necesarias. A continuación, puede cargar tootranscode de archivos de origen de Hola. A continuación, se puede enviar un trabajo con la plantilla de trabajo de hello, especificando solo Id. de grupo de hello y una ubicación de archivos de origen de hello cargada. se crea el trabajo por lotes de Hello, con una tarea por cada archivo de entrada que se está generando. Por último, los archivos de salida de hello transcodifica pueden ser descarga.

## <a name="installation"></a>Instalación

capacidades de transferencia de plantilla y el archivo Hello requieren un toobe de extensión instalada.

Para obtener instrucciones sobre cómo ver tooinstall hello Azure CLI [instalar Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).

Una vez Hola que CLI de Azure se ha instalado, Hola lote extensión se puede instalar mediante el siguiente comando CLI:

```azurecli
az component update --add batch-extensions --allow-third-party
```

Para obtener más información acerca de la extensión de lote de Hola, consulte [Azure de Microsoft CLI de lote extensiones para Windows, Mac y Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).

## <a name="templates"></a>Plantillas

Hola CLI de lote de Azure permite elementos como grupos, los trabajos y toobe de tareas que se creó mediante la especificación de un archivo JSON que contiene los valores y nombres de propiedad. Por ejemplo:

```azurecli
az batch pool create –-json-file AppPool.json
```

Plantillas de proceso por lotes de Azure son plantillas de administrador de recursos tooAzure similares, en la funcionalidad y la sintaxis. Son archivos JSON que contienen los nombres de propiedad de elemento y valores, pero agregar Hola después conceptos principales:

-   **Parámetros**

    -   Permitir toobe de valores de propiedad especificado en una sección de cuerpo, con solo los valores de parámetros que necesitan toobe proporcionado cuando se usa la plantilla de Hola. Por ejemplo, podría colocarse hello contiene toda la definición de un grupo en el cuerpo de Hola y solo un parámetro definido para el Id. de grupo; Por tanto, sólo una cadena de identificador de grupo debe toocreate toobe proporcionado un grupo.
        
    -   cuerpo de la plantilla de Hello puede crearse alguien con conocimientos del lote y Hola aplicaciones toobe ejecutada por lote; solo los valores de parámetros definidos por el autor de hello deben proporcionarse cuando se usa la plantilla de Hola. Un usuario sin Hola lote detallada o conocimiento de las aplicaciones, por tanto, puede usar las plantillas.

-   **Variables**

    -   Permitir toobe de valores de parámetro simples o complejas especificado en un solo lugar y utilizar en uno o varios lugares en el cuerpo de la plantilla de Hola. Las variables pueden simplificar y reducir el tamaño de Hola de plantilla de hello, así como que sea más fácil de mantener si tiene uno cuyo valor puede cambiar propiedades de ubicación de toochange.

-   **Construcciones de nivel superiores**

    -   Algunas construcciones de nivel superiores están disponibles en la plantilla de Hola que todavía no están disponibles en hello las API de lote. Por ejemplo, un generador de tareas puede definirse en una plantilla de trabajo que crea varias tareas de trabajo de hello mediante una definición de tarea común. Estas construcciones evitar Hola necesidad toocode para dinámicamente crear varios archivos JSON, por ejemplo, un archivo por cada tarea, así como para crear aplicaciones de tooinstall de archivos a través de un administrador de paquetes, por ejemplo de secuencia de comandos.

    -   En algún punto, cuando agregan aplicables, que estas construcciones pueden toothe lote servicio y está disponible en hello las API de lote, interfaces de usuario, etcetera.

### <a name="pool-templates"></a>Plantillas de grupo

Además, funciones de plantilla estándar de toohello de parámetros y variables, Hola siguientes construcciones de nivel superiores son compatibles con plantilla de grupo de hello:

-   **Referencias de paquetes**

    -   Opcionalmente, permite software toobe copian toopool nodos mediante paquete administradores. Administrador de paquetes de saludo y el Id. de paquete se especifican. Que se va a toodeclare capaz de uno o más paquetes evita Hola necesidad toocreate un script que obtiene los paquetes de saludo necesario, Hola script de instalación y ejecutar script de Hola en cada nodo de grupo.

Hola aquí te mostramos un ejemplo de una plantilla que crea un grupo de máquinas virtuales de Linux con ffmpeg instalada y solo requiere un número de hello y cadena de Id. de grupo de máquinas virtuales toobe proporcionado toouse:

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

Si se denomina archivo de plantilla de hello _ffmpeg.json grupo_, a continuación, sería necesario invocar una plantilla de hello como sigue:

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a>Plantillas de trabajo

Además, funciones de plantilla estándar de toohello de parámetros y variables, Hola siguientes construcciones de nivel superiores son compatibles con plantilla de trabajo de hello:

-   **Fábrica de tareas**

    -   Crea varias tareas para un trabajo a partir de una definición de tarea. Se admiten tres tipos de fábricas de tareas: barrido paramétrico, tarea por archivo y colección de tareas.

Hola te mostramos un ejemplo de una plantilla que crea un trabajo que utiliza ffmpeg para transcodificar tooone de archivos de vídeo MP4 de dos resoluciones más bajas, con una tarea creada por el archivo de vídeo de origen:

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

Si se denomina archivo de plantilla de hello _ffmpeg.json de trabajo_, a continuación, sería necesario invocar una plantilla de hello como sigue:

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a>Grupos de archivos y transferencia de archivos

La mayoría de los trabajos y tareas requieren archivos de entrada y generan archivos de salida. Ambos archivos de entrada y archivos de salida normalmente necesitan toobe transferido desde el nodo de toohello de cliente de Hola o de cliente de hello nodo toohello. Hola extensión de CLI de lote de Azure abstrae la transferencia de archivos de ubicación y utiliza la cuenta de almacenamiento de Hola que se crea de forma predeterminada para cada cuenta de lote.

Un grupo de archivos es el mismo contenedor de tooa que se crea en Hola cuenta de almacenamiento de Azure. grupo de archivos de Hello puede tener subcarpetas.

Hola extensión lote CLI proporciona comandos para cargar archivos del grupo de archivos especificado tooa de cliente y descargar archivos desde el cliente de tooa de grupo de archivo especificado de Hola.

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

Las plantillas de grupo y de trabajo permiten archivos almacenados en toobe de grupos de archivos especificado para la copia en los nodos de grupo o desactivar el grupo de nodos en espera tooa grupo de archivos. Por ejemplo, en la plantilla de trabajo que se especificó anteriormente, se especifica los archivo de hello grupo "ffmpeg-entrada" para el generador de tareas de hello como ubicación de los archivos de vídeo de origen de hello copiado en el nodo de hello para la transcodificación; las Hola Hola archivo grupo "ffmpeg-output" se utiliza como ubicación donde se archivos de salida de hello transcodifica hello copia nodo de hello toofrom ejecutando cada tarea.

## <a name="summary"></a>Resumen

Actualmente se han agregado soporte técnico de transferencia de plantilla y el archivo solo toohello CLI de Azure. objetivo de Hello es público de hello tooexpand que puede usar toousers de lote que no necesitan código toodevelop con hello las API de lote, por ejemplo, los investigadores, los usuarios de TI y así sucesivamente. Sin codificar de forma, los usuarios con conocimientos de Azure, lote y Hola aplicaciones toobe ejecutada por lote pueden crear plantillas para la creación de grupo y de trabajo. Con parámetros de plantilla, los usuarios sin un conocimiento detallado de las aplicaciones de hello y por lotes pueden utilizar plantillas de Hola.

Probar Hola extensión de lote para hello Azure CLI y proporcionarnos los comentarios y sugerencias, ya sea hello en los comentarios de este artículo o a través de hello [foro de Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).

## <a name="next-steps"></a>Pasos siguientes

- Consulte blog de plantillas de proceso por lotes hello: [Hola de trabajos de ejecución por lotes de Azure mediante Azure CLI: no se necesita código](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).
- Documentación detallada de instalación y uso, ejemplos y código fuente están disponibles en hello [repositorio de GitHub de Azure](https://github.com/Azure/azure-batch-cli-extensions).
