---
title: aaaAzure ejemplo de secuencia de comandos de CLI - ejecutando un trabajo con lote | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure - Ejecución de un trabajo con Batch"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Ejecución de trabajos en Azure Batch con la CLI de Azure

Este script crea un trabajo por lotes y agrega una serie de trabajo de toohello de tareas. También se muestra cómo toomonitor un trabajo y sus tareas. Por último, se muestra cómo tooquery Hola servicio por lotes eficaz para obtener información acerca de las tareas del trabajo de Hola.

## <a name="prerequisites"></a>Requisitos previos

- Instalación Hola CLI de Azure utilizando instrucciones de hello proporcionadas en hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), si aún no lo ha hecho.
- Cree una cuenta de Batch si aún no tiene una. Vea [crear una cuenta de lote con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para una secuencia de comandos de ejemplo que crea una cuenta.
- Configurar una toorun de aplicación de una tarea de inicio si aún no lo ha hecho. Vea [agregar aplicaciones tooAzure por lotes con Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para una secuencia de comandos de ejemplo que crea una aplicación y carga un tooAzure del paquete de aplicación.
- Configurar un grupo de en qué Hola se ejecutará el trabajo. Consulte [Administración de grupos de Azure Batch con la CLI de Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) para ver un script de ejemplo que crea un grupo con una configuración de servicios en la nube o de máquinas virtuales.

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>Limpieza de un trabajo

Después de ejecutar Hola por encima de la secuencia de comandos de ejemplo, ejecute hello después comando tooremove el trabajo y todas sus tareas. Tenga en cuenta que el grupo de hello necesitará toobe eliminar por separado. Consulte [Administración de grupos de Azure Batch con la CLI de Azure](./batch-cli-sample-manage-pool.md) para obtener más información sobre cómo crear y eliminar grupos.

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toocreate un proceso por lotes y las tareas. Cada comando de la tabla de hello vincula documentación específica del toocommand.

| Comando | Notas |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Autenticarse en una cuenta de Batch.  |
| [az batch job create](https://docs.microsoft.com/cli/azure/batch/job#create) | Crea un trabajo de Batch.  |
| [az batch job set](https://docs.microsoft.com/cli/azure/batch/job#set) | Actualiza las propiedades de un trabajo de Batch.  |
| [az batch job show](https://docs.microsoft.com/cli/azure/batch/job#show) | Recupera los detalles de un trabajo de Batch especificado.  |
| [az batch task create](https://docs.microsoft.com/cli/azure/batch/task#create) | Agrega que una tarea toohello especifica el trabajo por lotes.  |
| [az batch task show](https://docs.microsoft.com/cli/azure/batch/task#show) | Recupera los detalles de Hola de una tarea de hello especifican trabajo por lotes.  |
| [az batch task list](https://docs.microsoft.com/cli/azure/batch/task#list) | Muestra las tareas de hello asociadas con el trabajo especificado Hola.  |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos de CLI de lote en hello [documentación de CLI de lote de Azure](../batch-cli-samples.md).
