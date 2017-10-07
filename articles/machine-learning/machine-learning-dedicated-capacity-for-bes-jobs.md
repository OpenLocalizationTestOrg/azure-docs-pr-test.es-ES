---
title: "aaaDedicated capacidad para trabajos de servicio de ejecución de máquina aprendizaje por lotes | Documentos de Microsoft"
description: "Información general de los servicios de Azure Batch para trabajos de Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a>Servicio de Azure Batch para trabajos de Machine Learning

El procesamiento de grupo de lote de aprendizaje de máquina proporciona escala administrada por el cliente para hello servicio de ejecución de lote de aprendizaje de máquina de Azure. Clásico procesamiento por lotes de aprendizaje automático realiza en un entorno de varios inquilinos, se ponen en cola el número de hello límites de trabajos simultáneos que puede enviar y trabajos de forma primero en el primero en salir. Esta incertidumbre significa que no se puede predecir con exactitud cuándo se ejecutará el trabajo.

Procesamiento por lotes de grupo permite grupos toocreate en el que puede enviar trabajos por lotes. Controlar tamaño Hola de grupo de Hola y se envía el trabajo de toowhich grupo Hola. Se ejecuta el trabajo de BES en su propio procesamiento espacio proporcionar rendimiento del procesamiento predecible y grupos de recursos de toocreate de capacidad de Hola que corresponden toohello carga de procesamiento que se envía.

## <a name="how-toouse-batch-pool-processing"></a>Cómo el procesamiento por lotes grupo toouse

Configuración de grupo de procesamiento por lotes no está actualmente disponible a través de hello portal de Azure. toouse grupo de lote de procesamiento, debe:

-   Llamar a CSS toocreate una cuenta de grupo de lote y obtener una dirección URL de servicio de grupo y una clave de autorización
-   Crear un servicio web basado en el nuevo Resource Manager y un plan de facturación

toocreate su cuenta, llame al servicio al cliente de Microsoft y soporte técnico (CSS) y proporcione el identificador de suscripción. CSS funcionará con se toodetermine Hola capacidad apropiada para su escenario. CSS, a continuación, configura la cuenta con un número máximo de grupos que puede crear y Hola número máximo de máquinas virtuales (VM) que se pueden colocar en cada grupo de Hola. Una vez que su cuenta está configurada, se le proporciona la dirección URL del servicio de grupo y una clave de autorización.

Después de crea su cuenta, use Hola dirección URL del servicio de grupo y la autorización tooperform clave grupo operaciones de administración en el grupo de lote.

![Arquitectura del servicio de grupo de lote.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

Crear grupos mediante una llamada a operación de crear un grupo de hello en dirección URL del servicio de grupo de Hola que tooyou CSS proporcionado. Cuando se crea un grupo, especifique número Hola de máquinas virtuales y la dirección URL de Hola de hello swagger.json de un nuevo administrador de recursos según el servicio web de aprendizaje automático. Este servicio web se proporciona la asociación de facturación tooestablish Hola. Hola servicio del grupo de proceso por lotes utiliza grupo Hola de hello swagger.json tooassociate con un plan de facturación. Puede ejecutar a cualquier BES servicio web, ambos nuevo administrador de recursos según y clásico, elija en el grupo de Hola.

Puede usar ningún nuevo administrador de recursos en función de servicio web, pero tenga en cuenta que la facturación Hola de trabajos de Hola se cobra con respecto al plan de facturación de hello asociado a ese servicio. Puede que desee toocreate un servicio web y la facturación nuevo plan específicamente para ejecutar trabajos de grupo de lote.

Para más información sobre la implementación de servicios web, vea el artículo [Implementar un servicio web de Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

Una vez que ha creado un grupo, enviar Hola BES trabajo mediante Hola dirección URL de las solicitudes de lote para el servicio web de Hola. Puede elegir toosubmit se tooa grupo o tooclassic el procesamiento por lotes. toosubmit un procesamiento de grupo de trabajo tooBatch, agregue Hola siguiendo el cuerpo de la solicitud de envío de trabajo parámetro toohello:

"AzureBatchPoolId": "&lt;ID de grupo&gt;"

Si no agrega el parámetro hello, trabajo de Hola se ejecuta en el entorno de proceso por lotes clásico Hola. Si el grupo de hello tenga recursos disponibles, el trabajo de hello comienza a ejecutarse inmediatamente. Si el grupo de hello no tiene liberar recursos, el trabajo está en cola hasta que un recurso esté disponible.

Si encuentra que con regularidad alcanzar capacidad Hola de los grupos y necesita una mayor capacidad, puede llamar a CSS y trabajar con un representante de tooincrease las cuotas.

Solicitud de ejemplo:

https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a>Consideraciones al usar el procesamiento de grupo de lote

Grupo de procesamiento por lotes es un servicio facturable permanente y que requiere tooassociate, con un administrador de recursos según el plan de facturación. Solo se factura número Hola de horas de proceso se está ejecutando el grupo de hello; independientemente del número de Hola de trabajos que se ejecutan durante ese grupo de tiempo. Si crea un grupo, se le facturará para horas de proceso de Hola de cada máquina virtual en el grupo de hello hasta que se elimine el grupo de hello, incluso si no hay trabajos por lotes se ejecutan en el grupo de Hola. La facturación para las máquinas virtuales de Hola se inicia cuando ha terminado el aprovisionamiento y se detiene cuando se han eliminado. Puede usar cualquiera de los planes de Hola se encuentra en hello [página de precios de aprendizaje de máquina](https://azure.microsoft.com/pricing/details/machine-learning/).

Ejemplo de facturación:

Si crea un grupo de lote con 2 máquinas virtuales y lo elimina después de 24 horas, el plan de facturación se realiza con un cargo de 48 horas de proceso; independientemente de cuántos trabajos se hayan ejecutado durante ese período.

Si crea un grupo de lote con 4 máquinas virtuales y lo elimina después de 12 horas, el plan de facturación también se realiza con un cargo de 48 horas de proceso.

Se recomienda que sondear toodetermine de estado del trabajo de hello cuando se completan los trabajos. Cuando todos los trabajos han terminado de ejecutarse, llamada Hola Resize Pool operación tooset Hola número de máquinas virtuales de hello toozero de grupo. Si dispone de poco en recursos del grupo y necesita toocreate un nuevo grupo, por ejemplo toobill frente a un plan de facturación diferente, puede eliminar grupo hello en su lugar, cuando han terminado de ejecutar todos los trabajos.


| **Use procesamiento de grupo de lote cuando**    | **Use procesamiento por lotes clásico cuando**  |
|---|---|
|Necesita toorun un gran número de trabajos<br>O<br/>Necesita tooknow que los trabajos se ejecutarán inmediatamente<br/>O<br/>Necesita rendimiento garantizado. Por ejemplo, necesita toorun un número de trabajos en un periodo de tiempo especificado y desea tooscale espera su toomeet de recursos de proceso de sus necesidades.    | Tiene unos pocos trabajos para ejecutar<br/>y<br/> No es necesario Hola trabajos toorun inmediatamente |
