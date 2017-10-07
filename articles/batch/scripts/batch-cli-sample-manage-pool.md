---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure de grupos de administración en el lote | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: administración de grupos en Batch"
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>Administración de grupos de Azure Batch con la CLI de Azure

Estas secuencias de comandos muestra algunas de las herramientas de hello disponibles en hello toocreate de CLI de Azure y administrar grupos de nodos de proceso en el servicio de Azure Batch Hola.

> [!NOTE]
> comandos de Hello en este ejemplo crean máquinas virtuales de Azure. Máquinas virtuales en ejecución se acumularán cuenta tooyour de cargos. toominimize estos cargos, eliminar hello las máquinas virtuales una vez que haya terminado el ejemplo hello en ejecución. Consulte el artículo sobre cómo [limpiar los grupos](#clean-up-pools).

Los grupos de Batch se pueden configurar de dos formas, ya sea con una configuración de Cloud Services (solo Windows) o una configuración de Virtual Machine (Windows y Linux). scripts de ejemplo de Hola a continuación muestran cómo toocreate grupos con ambas configuraciones.

## <a name="prerequisites"></a>Requisitos previos

- Instalación Hola CLI de Azure utilizando instrucciones de hello proporcionadas en hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), si aún no lo ha hecho.
- Cree una cuenta de Batch si aún no tiene una. Vea [crear una cuenta de lote con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para una secuencia de comandos de ejemplo que crea una cuenta.
- Configurar una toorun de aplicación de una tarea de inicio si aún no lo ha hecho. Vea [agregar aplicaciones tooAzure por lotes con Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para una secuencia de comandos de ejemplo que crea una aplicación y carga un tooAzure del paquete de aplicación.

## <a name="pool-with-cloud-service-configuration-sample-script"></a>Grupo con script de ejemplo de configuración de Cloud Services

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>Grupo con script de ejemplo de configuración de Virtual Machine

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a>Limpieza de grupos

Después de ejecutar Hola por encima de la secuencia de comandos de ejemplo, ejecute hello siguientes grupos de comando toodelete Hola.
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después toocreate de comandos y manipular grupos de proceso por lotes.
Cada comando de la tabla de hello vincula documentación específica del toocommand.

| Comando | Notas |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Autenticarse en una cuenta de Batch.  |
| [az batch application summary list](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | Enumerar las aplicaciones disponibles de Hola Hola cuenta de lote.  |
| [az batch pool create](https://docs.microsoft.com/cli/azure/batch/pool#create) | Crear un grupo de máquinas virtuales.  |
| [az batch pool set](https://docs.microsoft.com/cli/azure/batch/pool#set) | Actualizar propiedades de un grupo.  |
| [az batch pool node-agent-skus list](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | Enumerar la información disponible de imagen y SKU de agente del nodo.  |
| [az batch pool resize](https://docs.microsoft.com/cli/azure/batch/pool#resize) | Número de Hola de cambio de tamaño de las máquinas virtuales en ejecución en hello especificado grupo.  |
| [az batch pool show](https://docs.microsoft.com/cli/azure/batch/pool#show) | Mostrar propiedades de Hola de un grupo.  |
| [az batch pool delete](https://docs.microsoft.com/cli/azure/batch/pool#delete) | Eliminar Hola especificado grupo.  |
| [az batch pool autoscale enable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | Habilitar el escalado automático de un grupo y aplicar una fórmula.  |
| [az batch pool autoscale disable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | Deshabilitar el escalado automático de un grupo.  |
| [az batch node list](https://docs.microsoft.com/cli/azure/batch/node#list) | Lista de todos los nodos de proceso de hello en hello especificado grupo.  |
| [az batch node reboot](https://docs.microsoft.com/cli/azure/batch/node#reboot) | Reinicie el nodo de cálculo especificado de Hola.  |
| [az batch node delete](https://docs.microsoft.com/cli/azure/batch/node#delete) | Los nodos de hello enumerado de eliminación de hello especificar grupo.  |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos de CLI de lote en hello [documentación de CLI de lote de Azure](../batch-cli-samples.md).

