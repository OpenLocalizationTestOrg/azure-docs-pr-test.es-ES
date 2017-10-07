---
title: aaaReliableConcurrentQueue en Azure Service Fabric
description: ReliableConcurrentQueue es una cola de alto rendimiento que permite puestas en cola y eliminaciones de la cola paralelas.
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a>Introducción tooReliableConcurrentQueue en Azure Service Fabric
La cola simultánea confiable es una cola asincrónica, transaccional y replicada que presenta una alta simultaneidad para las operaciones de puesta en cola y eliminación de la cola. Está diseñado toodeliver alto rendimiento y baja latencia por relaja Hola FIFO ordenación estricta proporcionada por [cola confiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) y en su lugar, proporciona una ordenación de mejor esfuerzo.

## <a name="apis"></a>API existentes

|Cola simultánea                |Cola simultánea confiable                                         |
|--------------------------------|------------------------------------------------------------------|
| void Enqueue(T item)           | Task EnqueueAsync(ITransaction tx, T item)                       |
| bool TryDequeue(out T result)  | Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)  |
| int Count()                    | long Count()                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a>Comparación con la [cola confiable](https://msdn.microsoft.com/library/azure/dn971527.aspx)

Confiable cola simultánea se ofrece como alternativa demasiado[cola confiable](https://msdn.microsoft.com/library/azure/dn971527.aspx). Debe usarse en aquellos casos en que no se requiere la ordenación FIFO estricta, ya que para garantizar FIFO se requiere un compromiso con la simultaneidad.  [Cola confiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) utiliza bloqueos tooenforce FIFO ordenación, con permiten tooenqueue como máximo una transacción y en la mayoría de una transacción permite toodequeue a la vez. En comparación, cola simultánea confiable relaja Hola restricción de ordenación y permite cualquier número toointerleave de las transacciones simultáneas su poner en cola y las operaciones de eliminación de cola. El orden de mejor esfuerzo es siempre, sin embargo Hola el orden relativo de dos valores en una cola simultánea confiable puede nunca puede garantizar.

La cola simultánea confiable proporciona un rendimiento mayor y menor latencia que la [cola confiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) siempre que existen varias transacciones simultáneas que realizan puestas en cola y/o eliminaciones de la cola.

Un ejemplo de uso de hello ReliableConcurrentQueue es hello [cola de mensajes](https://en.wikipedia.org/wiki/Message_queue) escenario. En este escenario, crean y agregar elementos toohello cola productores de mensajes de uno o más, y uno o varios de los consumidores del mensaje extracción mensajes de cola de Hola y procesan. Varios productores y consumidores pueden trabajar independientemente, con las transacciones simultáneas en cola la orden tooprocess Hola.

## <a name="usage-guidelines"></a>Directrices de uso
* cola de Hello espera que los elementos de hello en cola Hola tienen un período de retención baja. Es decir, los elementos de hello no quedaría en cola de Hola durante mucho tiempo.
* cola de Hello no garantiza la ordenación de FIFO estricta.
* cola de Hello no lee su propia escritura. Si un elemento está en cola dentro de una transacción, no estará visible tooa dequeuer dentro de Hola misma transacción.
* Las eliminaciones de la cola no están aisladas entre sí. Si el elemento *A* se quitan de la cola de transacciones *txnA*, aunque *txnA* no se confirma, elemento *A* no sería tooa visible simultáneas transacción *txnB*.  Si *txnA* anula, *A* dejarán de estar visible demasiado*txnB* inmediatamente.
* *TryPeekAsync* comportamiento puede implementarse mediante un *TryDequeueAsync* y, a continuación, anular la transacción de Hola. Un ejemplo de esto puede encontrarse en la sección de patrones de programación de Hola.
* El recuento es no transaccional. Puede ser tooget usa una idea del número de Hola de elementos en cola de hello, pero representa un punto en el tiempo y no se puede confiar en ellos.
* Un procesamiento costoso en hello elementos quitados de la cola no deben realizarse mientras está activa, la transacción hello tooavoid transacciones de larga ejecución que pueden tener un impacto en el rendimiento en el sistema de Hola.

## <a name="code-snippets"></a>Fragmentos de código
Echemos un vistazo a algunos fragmentos de código y a sus resultados esperados. El control de excepciones se omite en esta sección.

### <a name="enqueueasync"></a>EnqueueAsync
A continuación, se muestran algunos fragmentos de código para usar EnqueueAsync, seguido de los resultados previstos.

- *Caso 1: Tarea de puesta en cola única*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

Suponga esa tarea Hola se completó correctamente y que no hubo ninguna transacción simultánea modificar cola Hola. usuario de Hello, puede esperar Hola cola toocontain Hola los elementos en cualquiera de hello después de pedidos:

> 10, 20

> 20, 10


- *Caso 2: Tarea de puesta en cola paralela*

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

Suponga que tareas Hola completan correctamente, que se ha ejecutado tareas hello en paralelo y que no había ninguna otra transacción simultánea modificar cola Hola. La inferencia no se puede realizar sobre orden Hola de elementos en cola de Hola. Este fragmento de código, elementos Hola pueden aparecer en cualquiera de los 4 hello! órdenes posibles.  cola de Hello tratará de elementos de hello tookeep en orden de hello original (en cola), pero puede ser tooreorder forzada ellas debido a operaciones de tooconcurrent o errores.


### <a name="dequeueasync"></a>DequeueAsync
Estos son algunos fragmentos de código para usar TryDequeueAsync seguido de salidas de hello esperado. Suponga que esa cola Hola ya se rellena con hello siguientes elementos en cola de hello:
> 10, 20, 30, 40, 50, 60

- *Caso 1: Tarea de quitar de la cola única*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

Suponga esa tarea Hola se completó correctamente y que no hubo ninguna transacción simultánea modificar cola Hola. Puesto que no puede realizarse inferencia sobre orden Hola de elementos de hello en cola de hello, los tres elementos de hello pueden se quita de la cola, en cualquier orden. cola de Hello tratará de elementos de hello tookeep en orden de hello original (en cola), pero puede ser tooreorder forzada ellas debido a operaciones de tooconcurrent o errores.  

- *Caso 2: Tarea de eliminación de la cola paralela*

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

Suponga que tareas Hola completan correctamente, que se ha ejecutado tareas hello en paralelo y que no había ninguna otra transacción simultánea modificar cola Hola. Puesto que no puede realizarse inferencia sobre orden Hola de elementos de hello en cola de hello, Hola listas *dequeue1* y *dequeue2* contendrá entre los dos elementos, en cualquier orden.

Hola le mismo elemento *no* aparecen en ambas listas. Por lo tanto, si dequeue1 tiene *10*, *30*, dequeue2 tendrá *20*, *40*.

- *Caso 3: Ordenación de eliminación de la cola con anulación de transacción*

Anular una transacción con sobre la marcha quita vuelve a colocar elementos de hello en el encabezado de Hola de cola de Hola. no se garantiza el orden de Hello en el que los elementos de Hola se vuelven a poner en el encabezado de Hola de cola de Hola. Echemos un vistazo al siguiente código de hello:

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
Suponga que elementos de Hola se han quitado de la cola en hello siguiendo el orden:
> 10, 20

Cuando se anule la transacción de hello, elementos de Hola se agregaría toohello back-head de cola de hello en cualquiera de hello después de pedidos:
> 10, 20

> 20, 10

Hello mismo sirve para todos los casos donde hello no estaba correctamente *confirmado*.

## <a name="programming-patterns"></a>Modelos de programación
En esta sección, vamos a echar un vistazo a algunos modelos de programación que podrían resultar útiles para usar ReliableConcurrentQueue.

### <a name="batch-dequeues"></a>Eliminaciones de la cola por lotes
Recomienda modelo de programación es para hello consumidor tarea toobatch su quita de la cola en lugar de realizar una eliminación de cola a la vez. usuario de Hello puede toothrottle retrasos entre cada tamaño de lote de proceso por lotes o hello. Hello fragmento de código siguiente muestra este modelo de programación.  Tenga en cuenta que en este ejemplo, el procesamiento de Hola se realiza después de hello transacción se confirma, por lo que si un error fuera toooccur durante el procesamiento, hello elementos sin procesar se perderán sin haber sido transformado.  O bien, se puede realizar el procesamiento de hello en el ámbito de la transacción de hello, sin embargo esto puede tener un impacto negativo en el rendimiento y requiere un tratamiento de los elementos de hello ya procesan.

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a>Procesamiento basado en notificaciones de mejor esfuerzo
Otro patrón de programación interesante usa Hola API de recuento. En este caso, podemos implementar procesamiento basado en notificaciones de mejor esfuerzo para cola de Hola. Hola cola número puede ser usado toothrottle un poner en cola o una tarea de eliminación de cola.  Tenga en cuenta que como en el ejemplo anterior de hello, puesto que se produce el procesamiento de hello fuera de la transacción de hello, sin procesar elementos pueden perderse si se produce un error durante el procesamiento.

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a>Descarga de mejor esfuerzo
No se puede garantizar una descarga de la cola de hello debido toohello naturaleza simultáneas de estructura de datos de Hola.  Es posible que, incluso si no hay operaciones de usuario de cola de hello en curso, una determinada llamada tooTryDequeueAsync no puede devolver un elemento que antes era en cola y confirmada.  elemento de Hello en cola se garantiza demasiado*finalmente* se convierten en toodequeue visible, sin embargo, sin un mecanismo de comunicación fuera de banda, un consumidor independiente no puede saber a esa cola Hola ha alcanzado un estado estable incluso si todos los se han detenido los productores y no se permite ninguna operación nueva de puesta en cola. Por lo tanto, operación de vaciado de hello es mejor esfuerzo tal y como se implementan bajo.

usuario de Hello debe detener toda la demás productor y las tareas del consumidor y espere anulación, antes de intentar la cola de hello toodrain ni toocommit de transacciones en curso.  Si usuario Hola conoce número Hola esperado de elementos en cola de hello, puede configurar una notificación que indica que todos los elementos se han quitado de la cola.

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a>Peek
ReliableConcurrentQueue no proporciona hello *TryPeekAsync* api. Los usuarios pueden obtener peek Hola a semántica mediante el uso de un *TryDequeueAsync* y, a continuación, anular la transacción de Hola. En este ejemplo, quita de la cola se procesan sólo si el valor del elemento de hello es mayor que *10*.

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a>Lecturas obligatorias
* [Inicio rápido de Reliable Services](service-fabric-reliable-services-quick-start.md)
* [Trabajo con Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Notificaciones de Reliable Services](service-fabric-reliable-services-notifications.md)
* [Copia de seguridad y restauración de Reliable Services (recuperación ante desastres)](service-fabric-reliable-services-backup-restore.md)
* [Configuración del administrador de estado confiable](service-fabric-reliable-services-configuration.md)
* [Introducción a los servicios de la API web de Microsoft Azure Service Fabric](service-fabric-reliable-services-communication-webapi.md)
* [Uso avanzado de hello modelo de programación de servicios de confianza](service-fabric-reliable-services-advanced-usage.md)
* [Referencia para desarrolladores de colecciones confiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
