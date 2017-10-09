---
title: "aaa \"evento complete cambiar el tamaño de grupo de lote de Azure | Documentos de Microsoft\""
description: "Referencia del evento completo de cambio de tamaño de grupo de Batch."
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
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a>Evento de finalización de cambio de tamaño del grupo

 Este evento se genera cuando finaliza o no se puede realizar el cambio de tamaño de un grupo.

 Hello en el ejemplo siguiente se muestra hello cuerpo de un evento complete el cambio de tamaño de bloque para un grupo que aumentado su tamaño y se completó correctamente.

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "hello operation succeeded"
}
```

|Elemento|Tipo|Notas|
|-------------|----------|-----------|
|id|String|Hola Id. de grupo de Hola.|
|nodeDeallocationOption|String|Especifica cuando debe quitar nodos del grupo de hello, si el tamaño del grupo de hello disminuye.<br /><br /> Los valores posibles son:<br /><br /> **requeue**: finalizar las tareas en ejecución y volver a ponerlas en cola. tareas de Hola se ejecutarán de nuevo cuando se habilite el trabajo de Hola. Elimine los nodos en cuanto finalicen las tareas.<br /><br /> **terminate**: finalizar las tareas en ejecución. tareas de Hello no se ejecutarán de nuevo. Elimine los nodos en cuanto finalicen las tareas.<br /><br /> **taskcompletion** : permitir toocomplete de tareas está ejecutando actualmente. No programe ninguna tarea nueva mientras espera. Elimine los nodos cuando se hayan completado todas las tareas.<br /><br /> **Retaineddata** : permitir toocomplete de tareas en ejecución actualmente y luego espere tooexpire de períodos de retención de datos. No programe ninguna tarea nueva mientras espera. Elimine los nodos cuando hayan caducado los períodos de retención de todas las tareas.<br /><br /> valor predeterminado de Hello es colocarlo en cola.<br /><br /> Si aumenta el tamaño del grupo de hello, valor de Hola se establece demasiado**válido**.|
|currentDedicated|Int32|número de Hola de nodos de proceso asignadas actualmente toohello grupo.|
|targetDedicated|Int32|número de Hola de nodos de proceso que se solicitan para el grupo de Hola.|
|enableAutoScale|Booleano|Especifica si el tamaño del grupo de hello ajusta automáticamente con el tiempo.|
|isAutoPool|Booleano|Especifica si se ha creado el grupo de Hola a través del mecanismo de grupo de un trabajo.|
|startTime|DateTime|Hola cambiar el tamaño de bloque de hello comenzó.|
|endTime|DateTime|Hello tiempo cambiar el tamaño de bloque de hello completado.|
|resultCode|String|cambiar el tamaño de resultado de Hello de Hola.|
|resultMessage|String|error de cambio de tamaño de Hello incluye detalles de hello del resultado de hello.<br /><br /> Si cambia el tamaño de hello completado correctamente los Estados que Hola operación se realizó correctamente.|
