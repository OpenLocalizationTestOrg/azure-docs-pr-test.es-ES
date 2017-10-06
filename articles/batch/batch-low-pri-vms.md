---
title: "las cargas de trabajo por lotes de Azure aaaRun en máquinas virtuales de prioridad baja rentables (versión preliminar) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo Hola de tooreduce de las máquinas virtuales de prioridad baja tooprovision de costo de las cargas de trabajo de lote de Azure."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a>Uso de máquinas virtuales de prioridad baja con Batch (versión preliminar)

Lote de Azure ofrece costo de hello tooreduce de baja prioridad las máquinas virtuales (VM) de las cargas de trabajo por lotes. Las máquinas virtuales de prioridad baja posibilitan nuevos tipos de cargas de trabajo de Batch al proporcionar elevada capacidad de proceso que también resulta económica.

Las máquinas virtuales de prioridad baja aprovechan la capacidad sobrante en Azure. Al especificar máquinas virtuales de prioridad baja en sus grupos, Azure Batch puede usar automáticamente este excedente cuando esté disponible.

contrapartida de Hello para el uso de máquinas virtuales de prioridad baja es que pueden ser adelantadas esas máquinas virtuales cuando no hay exceso de capacidad está disponible en Azure. Por este motivo, estas máquinas son las más adecuadas para determinados tipos de cargas de trabajo. Use máquinas virtuales de prioridad baja para cargas de trabajo de procesamiento asincrónico en tiempo de finalización del trabajo de hello es flexible y trabajo Hola se distribuye entre muchas máquinas virtuales y lote.

Las máquinas virtuales de prioridad baja son significativamente menos caras que las máquinas virtuales dedicadas. Para más información sobre precios, consulte [Precios de Batch](https://azure.microsoft.com/pricing/details/batch/).

Para obtener una explicación adicional de máquinas virtuales de prioridad baja, consulte el anuncio de entrada de blog de hello: [por lotes informática en una fracción del precio de hello](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).

> [!IMPORTANT]
> Las máquinas virtuales de prioridad baja se encuentran actualmente en versión preliminar y solo están disponibles para cargas de trabajo que se ejecutan en Batch. 
>
>

## <a name="use-cases-for-low-priority-vms"></a>Casos de uso de máquinas virtuales de prioridad baja

Proporciona características de Hola de máquinas virtuales de prioridad baja, qué cargas de trabajo pueden y no pueden usarlos? En general, las cargas de trabajo de procesamiento por lotes son una buena opción, ya que los trabajos se dividen en muchas tareas paralelas o hay muchos trabajos que se escalan horizontalmente y que se distribuyen en muchas máquinas virtuales.

-   uso de toomaximize de exceso de capacidad en los trabajos de Azure, que se puede puede escalar horizontalmente.

-   En ocasiones, las máquinas virtuales no estén disponibles o se adelantará, lo que dará como resultado de capacidad reducida para trabajos y puede provocar la vuelve a ejecutar y la interrupción de tootask. Trabajos, por tanto, deben ser flexibles en el tiempo de Hola que pueden tomar toorun.

-   Los trabajos con tareas más largas pueden resultar más afectados si se interrumpen. Si de larga ejecución tareas implementan progreso toosave de puntos de comprobación que se ejecutan, a continuación, el impacto de interrupción sería mucho menor. Tareas con tiempos de ejecución suelen mejor toowork con máquinas virtuales de prioridad baja como impacto Hola de interrupción es mucho menor.

-   Trabajos MPI que usan varias máquinas virtuales no están toouse idóneo de larga ejecución máquinas virtuales de prioridad baja como una máquina virtual adelantamiento van a tener toobe, vuelva a ejecutar el trabajo de cliente potencial es probable que toohello entero.

Algunos ejemplos de procesamiento por lotes usan casos toouse adapta perfectamente las máquinas virtuales de prioridad baja son:

-   **Desarrollo y pruebas**: en concreto, si se están desarrollando soluciones a gran escala se pueden obtener ahorros significativos. Aunque todos los tipos de pruebas pueden beneficiarse, será especialmente ventajoso para pruebas de carga y regresión a gran escala.

-   **Complementar capacidad a petición**: máquinas virtuales de prioridad baja se pueden utilizar para complementar la VM regular dedicadas - si está disponible, trabajos pueden escalar y, por lo tanto, para reducir el costo, realizar más rápidas; cuando no esté disponible, línea de base de Hola de dedicado máquinas virtuales están disponibles.

-   **Tiempo de ejecución de trabajo flexible**: si hay flexibilidad en los trabajos del temporizador hello tiene toocomplete, a continuación, pueden tolerar caídas potencials de capacidad; sin embargo, con hello suma de los trabajos de las máquinas virtuales de prioridad baja se ejecutará con frecuencia más rápido y para un menor costo.

Grupos de proceso por lotes pueden ser configurado toouse máquinas virtuales de prioridad baja de varias maneras, dependiendo de la flexibilidad de hello en tiempo de ejecución del trabajo:

-   Las máquinas virtuales de prioridad baja solo se pueden usar en un grupo; Batch simplemente recuperará cualquier capacidad reemplazada cuando esté disponible. Se trata de los trabajos de tooexecute de manera más baratos hello como máquinas virtuales de prioridad baja sólo se utilizan.

-   Las máquinas virtuales de prioridad baja se pueden usar conjuntamente con una línea de base fija de máquinas virtuales dedicadas. Hello número fijo de máquinas virtuales dedicadas garantiza que es siempre algunos tookeep capacidad un progreso del trabajo.

-   Puede haber dinámica combinación de máquinas virtuales de prioridad baja y dedicadas, para que las máquinas virtuales de prioridad baja baratas se usan únicamente cuando esté disponible, pero Hola precio completo dedicado las máquinas virtuales se escalan cuando sea necesario, tookeep una cantidad mínima de trabajos de capacidad disponible tookeep Hola progreso.

## <a name="batch-support-for-low-priority-vms"></a>Compatibilidad de Batch con máquinas virtuales de prioridad baja

Lote de Azure proporciona varias funciones que hace más fácil tooconsume y beneficiarán de las máquinas virtuales de prioridad baja:

-   Los grupos de Batch pueden contener tanto máquinas virtuales dedicadas como máquinas virtuales de prioridad baja. número de Hola de cada tipo de máquina virtual puede especificarse cuando se crea un grupo, o cambiar en cualquier momento para un grupo existente, mediante la operación de cambio de tamaño explícito de Hola o con escala automática. Envío de trabajos y tareas puede permanecer sin cambios y no es necesario tener en cuenta los tipos de VM de hello en el grupo de Hola. También es posible toohave un grupo completamente utilice prioridad baja máquinas virtuales toorun trabajos de manera más asequible como sea posible, pero de spin up dedicadas máquinas virtuales si la capacidad de hello cae por debajo de un umbral mínimo, para mantener los trabajos que se ejecutan.

-   Grupos de lote automáticamente búsqueda toohello número de destino de máquinas virtuales de prioridad baja. Si las máquinas virtuales son adelantadas, lote intentará hello tooreplace pierde la capacidad y el destino de toohello devuelto.

-   En caso de hello de tareas que se interrumpa, lote detectará y poner automáticamente toobe de tareas, vuelva a ejecutar.

-   Las máquinas virtuales de prioridad baja tienen una cuota de núcleos que difiere de la de las máquinas virtuales dedicadas. 
    Hola comillas de cierre para máquinas virtuales de prioridad baja es mayor que el de las máquinas virtuales dedicadas, porque las máquinas virtuales de prioridad baja costo es menor. Consulte [Límites y cuotas del servicio Batch](batch-quota-limit.md#resource-quotas) para más información.    

> [!NOTE]
> Máquinas virtuales de prioridad baja no se admiten actualmente para las cuentas de lote donde se establece el modo de asignación de grupo de hello demasiado[suscripción usuario](batch-account-create-portal.md#user-subscription-mode).
>
>

## <a name="create-and-update-pools"></a>Creación y actualización de grupos

Un grupo de lote puede contener dedicadas y prioridad baja de máquinas virtuales (también denominados tooas calcular nodos). Puede establecer el número de destino de Hola de nodos de proceso para las máquinas virtuales dedicadas y prioridad baja. número de destino de nodos Hello especifica el número de Hola de máquinas virtuales que desee toohave en grupo Hola.

Por ejemplo, toocreate a un grupo con máquinas virtuales del servicio de nube de Azure con un destino de 5 había dedicado a las máquinas virtuales y 20 máquinas virtuales de prioridad baja:

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

toocreate a un grupo con máquinas virtuales de Azure (en este caso, las máquinas virtuales de Linux) con un destino de 5 había dedicado a las máquinas virtuales y 20 máquinas virtuales de prioridad baja:

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

Puede obtener el número actual de Hola de nodos para máquinas virtuales dedicadas y de baja prioridad:

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

Nodos de grupo tienen una propiedad tooindicate si el nodo de hello es una máquina virtual dedicada o baja:

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

Cuando se ve relegados uno o varios nodos en un grupo, una operación de nodos de la lista en el grupo también devolverá los nodos, número actual de Hola de nodos de prioridad baja permanecerán sin cambios, pero esos nodos tendrán su estado establecido toothe **cambiado**estado. Lote intentará toofind reemplazo máquinas virtuales y, si es correcto, nodos de hello pasará a través de **crear** y, a continuación, **iniciando** Estados antes de estar disponibles para la ejecución de la tarea, al igual que los nuevos nodos.

## <a name="scale-a-pool-containing-low-priority-vms"></a>Escalado de un grupo que contiene máquinas virtuales de prioridad baja

Como con grupos formada únicamente por máquinas virtuales dedicadas, es posible tooscale una grupo de contenedor prioridad baja las máquinas virtuales llamando al método de cambio de tamaño de Hola o mediante el uso de escala automática.

operación de cambio de tamaño de bloque Hello toma un parámetro opcional en segundo lugar que actualiza el valor de **targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

fórmula de escala automática de grupo de Hello es compatible con las máquinas virtuales de prioridad baja como sigue:

-   Puede obtener o establecer valor de hello de la variable definida por el servicio de hello **$TargetLowPriorityNodes**.

-   Puede obtener valor de saludo de la variable definida por el servicio de hello **$CurrentLowPriorityNodes**.

-   Puede obtener valor de saludo de la variable definida por el servicio de hello **$PreemptedNodeCount**. 
    Esta variable devuelve número Hola de nodos Hola adelantadas estado y le permite escalar hacia arriba o hacia abajo el número de Hola de nodos dedicados, según el número de Hola de adelantamiento nodos que no están disponibles.

## <a name="jobs-and-tasks"></a>Trabajos y tareas

Trabajos y tareas que requieren compatibilidad con muy poco para los nodos de prioridad baja; solo se admite Hello es como sigue:

-   Hola JobManagerTask propiedad de un trabajo tiene una propiedad nueva, **AllowLowPriorityNode**. 
    Cuando esta propiedad es true, se puede programar la tarea del Administrador de trabajos de Hola en un nodo dedicado o baja. Si esta propiedad es false, tarea del Administrador de trabajos de hello será tooa programada sólo nodo dedicado.

-   Un [variable de entorno](batch-compute-node-environment-variables.md) es aplicación de la tarea de tooa disponibles para que pueda determinar si se está ejecutando en un nodo de prioridad baja o dedicado. variable de entorno de Hello es AZ_BATCH_NODE_IS_DEDICATED.

## <a name="handling-preemption"></a>Control de reemplazos

Máquinas virtuales en ocasiones pueden tener preferencia sobre; Cuando esto sucede, lote Hola siguientes:

-   Hello adelantamiento de máquinas virtuales tienen su estado actualizan también**cambiado**.
-   Si las tareas que se estaban ejecutando en hello adelantadas máquinas virtuales de nodos, dichas tareas se poner en cola y se vuelva a ejecutar.
-   Hola VM también se elimina, datos tooany almacenados localmente en hello VM se pierde una vez más importantes.
-   grupo de Hello continuamente intentos de número de destino de hello tooreach de prioridad baja nodos disponibles. Cuando se encuentra la capacidad de reemplazo, los nodos mantienen sus identificaciones, pero se reinicializan, pasando por los estados**Creando** e **Iniciando** antes de que estén disponibles para la programación de tareas.
-   Recuentos de adelantamiento están disponibles como una métrica en hello portal de Azure.

## <a name="metrics"></a>Métricas

Nuevas métricas están disponibles en hello [portal de Azure](https://portal.azure.com) para los nodos de prioridad baja. Estas son las métricas:

- Recuento de nodos de baja prioridad
- Recuento de núcleos de baja prioridad 
- Recuento de nodos con prioridad

métricas de tooview Hola portal de Azure:

1. Navegue tooyour cuenta de lote en el portal de Hola y ver la configuración de Hola para su cuenta de lote.
2. Seleccione **métricas** de hello **supervisión** sección.
3. Seleccione las métricas de Hola que desee de hello **métricas disponibles** lista.

![Métricas para nodos de baja prioridad](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>Pasos siguientes

* Hola de lectura [Introducción a la característica por lotes para los desarrolladores](batch-api-basics.md), información esencial para todo aquel que preparar toouse por lotes. artículo de Hello contiene información más detallada sobre los recursos del servicio por lotes como hello, nodos, trabajos y las tareas y grupos de muchas características de la API que puede usar al compilar la aplicación de lote.
* Obtenga información acerca de hello [herramientas y API de lote](batch-apis-tools.md) disponibles para la creación de soluciones de lote.
