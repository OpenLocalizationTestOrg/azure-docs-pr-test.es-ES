---
title: aaa "eventos de inicio de tarea de lote de Azure | Documentos de Microsoft"
description: Referencia del evento de inicio de tarea de Batch.
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a>Evento de inicio de tarea

 Este evento se genera cuando una tarea ha estado toostart programada en un nodo de proceso por el programador de Hola. Tenga en cuenta que si se vuelve a intentar o poner en cola tareas Hola este evento se emitirá nuevo para hello misma tarea pero Hola número de reintentos y versión de la tarea de sistema se actualizará según corresponda.


 Hello en el ejemplo siguiente se muestra hello cuerpo de un evento de inicio de la tarea.

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|Nombre del elemento|Tipo|Notas|
|------------------|----------|-----------|
|jobId|String|Hola Id. de trabajo de Hola que contiene la tarea hello.|
|id|String|Hola Id. de tarea hello.|
|taskType|String|tipo de Hola de tarea hello. Puede ser "JobManager", que indica que es una tarea del administrador de trabajos, o "User", que indica que no lo es.|
|systemTaskVersion|Int32|Se trata de un contador de reintentos interno de hello en una tarea. Internamente el servicio por lotes Hola puede volver a intentar una tooaccount de tarea para problemas transitorios. Estos problemas pueden incluir toorecover interno de intentos de contraseña o errores de programación de nodos de ejecución en un estado incorrecto.|
|[nodeInfo](#nodeInfo)|Tipo complejo|Contiene información sobre el nodo de proceso de hello en qué Hola se ejecutó la tarea.|
|[multiInstanceSettings](#multiInstanceSettings)|Tipo complejo|Especifica que la tarea hello es tarea de varias instancias que requieren varios nodos de ejecución.  Consulte [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) para detalles.|
|[constraints](#constraints)|Tipo complejo|restricciones de ejecución de Hola que se aplican toothis tarea.|
|[executionInfo](#executionInfo)|Tipo complejo|Contiene información sobre la ejecución de Hola de tarea hello.|

###  <a name="nodeInfo"></a> nodeInfo

|Nombre del elemento|Tipo|Notas|
|------------------|----------|-----------|
|poolId|String|Hola Id. del grupo de hello en qué Hola se ejecutó la tarea.|
|nodeId|String|Hola el identificador del nodo de hello en qué Hola se ejecutó la tarea.|

###  <a name="multiInstanceSettings"></a> multiInstanceSettings

|Nombre del elemento|Tipo|Notas|
|------------------|----------|-----------|
|numberOfInstances|int|número de Hola de nodos de proceso requeridos por la tarea hello.|

###  <a name="constraints"></a> constraints

|Nombre del elemento|Tipo|Notas|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|Hola número máximo de veces que se puede reintentar la tarea hello. Hola servicio por lotes vuelve a intentar una tarea si su código de salida es distinto de cero.<br /><br /> Tenga en cuenta que este valor controla específicamente número Hola de reintentos. servicio de lote de Hello intentará tarea hello una vez y, a continuación, puede volver a intentar la toothis límite. Por ejemplo, si el número máximo de reintentos de hello es 3, lote intenta una tarea too4 horas (un intento de inicial y 3 reintentos).<br /><br /> Si el número máximo de reintentos de hello es 0, Hola servicio por lotes no vuelva a intentar tareas.<br /><br /> Si el número máximo de reintentos de hello es -1, el servicio de lote de hello reintenta tareas sin límite.<br /><br /> valor predeterminado de Hello es 0 (no hay ningún reintento).|

###  <a name="executionInfo"></a> executionInfo

|Nombre del elemento|Tipo|Notas|
|------------------|----------|-----------|
|retryCount|Int32|Hola número de veces que se ha reintentado la tarea hello Hola servicio por lotes. tarea Hello se vuelve a intentar si finaliza con un código de salida distinto de cero, los toohello especifica MaxTaskRetryCount|
