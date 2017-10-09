---
title: "aaa \"evento de inicio de cambio de tamaño de grupo de lote de Azure | Documentos de Microsoft\""
description: "Referencia del evento de inicio de cambio de tamaño de grupo de Batch."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a>Evento de inicio de cambio de tamaño de grupo

 Este evento se genera se inicia el cambio de tamaño de un grupo. Puesto que el cambio de tamaño de bloque de hello es un evento asíncrono, puede esperar un toobe de evento complete de cambio de tamaño de bloque emitida una vez Hola cambiar el tamaño de operación se completa.

 cambiar el tamaño de Hello siguiente ejemplo se muestra hello cuerpo de un evento de inicio de cambio de tamaño de grupo para un cambio de tamaño grupo desde 0 nodos too2 con un manual.

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|Elemento|Tipo|Notas|
|-------------|----------|-----------|
|poolId|String|Hola Id. de grupo de Hola.|
|nodeDeallocationOption|String|Especifica cuando debe quitar nodos del grupo de hello, si el tamaño del grupo de hello disminuye.<br /><br /> Los valores posibles son:<br /><br /> **requeue**: finalizar las tareas en ejecución y volver a ponerlas en cola. tareas de Hola se ejecutarán de nuevo cuando se habilite el trabajo de Hola. Elimine los nodos en cuanto finalicen las tareas.<br /><br /> **terminate**: finalizar las tareas en ejecución. tareas de Hello no se ejecutarán de nuevo. Elimine los nodos en cuanto finalicen las tareas.<br /><br /> **taskcompletion** : permitir toocomplete de tareas está ejecutando actualmente. No programe ninguna tarea nueva mientras espera. Elimine los nodos cuando se hayan completado todas las tareas.<br /><br /> **Retaineddata** : permitir toocomplete de tareas en ejecución actualmente y luego espere tooexpire de períodos de retención de datos. No programe ninguna tarea nueva mientras espera. Elimine los nodos cuando hayan caducado los períodos de retención de todas las tareas.<br /><br /> valor predeterminado de Hello es colocarlo en cola.<br /><br /> Si aumenta el tamaño del grupo de hello, valor de Hola se establece demasiado**válido**.|
|currentDedicated|Int32|número de Hola de nodos de proceso asignadas actualmente toohello grupo.|
|targetDedicated|Int32|número de Hola de nodos de proceso que se solicitan para el grupo de Hola.|
|enableAutoScale|Booleano|Especifica si el tamaño del grupo de hello ajusta automáticamente con el tiempo.|
|isAutoPool|Booleano|Especifica si se creó el grupo de Hola a través del mecanismo de grupo de un trabajo.|
