---
title: aaaAzure estrechamente, perfecto y almacenamiento de blobs de archivo | Documentos de Microsoft
description: "Almacenamiento de archivo, esporádico y frecuente para cuentas de Azure Blog Storage."
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: eb33ed4f-1b17-4fd6-82e2-8d5372800eef
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/05/2017
ms.author: mihauss
ms.openlocfilehash: 42fb699bf16147ba8a4d9f75a62debadea5af65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-cool-and-archive-preview-storage-tiers"></a>Azure Blob Storage: niveles de almacenamiento de archivo, esporádico y frecuente (versión preliminar)

## <a name="overview"></a>Información general

Azure Storage ofrece tres niveles de almacenamiento para el almacenamiento de objetos Blob, por lo que puede almacenar los datos de forma más rentable en función de cómo los use. Hello Azure **capa de almacenamiento activa** está optimizado para almacenar datos que se accede con frecuencia. Hello Azure **capa de almacenamiento frío** está optimizado para almacenar datos que se tiene acceso con poca frecuencia y que se almacenan durante al menos un mes. Hola [capa de almacenamiento de archivo (vista previa)](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) está optimizado para almacenar datos que raramente se tiene acceso y almacenados durante al menos seis meses con los requisitos de latencia flexible (en orden de Hola de horas). Hola *archivo* capa de almacenamiento solo puede usarse en el nivel de blob de hello y no Hola toda cuenta de almacenamiento. Datos de capa de almacenamiento de acceso esporádico de hello pueden tolerar una disponibilidad ligeramente inferior, pero todavía requiere gran durabilidad y características similares de acceso de tiempo y el rendimiento como datos activos. En el caso de los datos de acceso esporádico y de archivo, un Acuerdo de Nivel de Servicio con una disponibilidad ligeramente inferior y unos costos de acceso mayores se puede aceptar a cambio de unos costos de almacenamiento mucho menores.

En la actualidad, los datos almacenados en la nube de hello crece a un ritmo exponencial. el precio es toomanage para sus necesidades de almacenamiento de expansión, resulta útil tooorganize los datos en función de atributos como la frecuencia de acceso y planeado período de retención. Datos almacenados en la nube de hello pueden ser diferentes en cuanto a cómo se genera, además de procesar y acceder a través de su duración. A algunos datos se accede y se modifican activamente a lo largo de su duración. Algunos datos se obtiene acceso con frecuencia al principio de su duración, con acceso quitar drásticamente como Hola datos edades. Algunos datos permanecen inactivos en la nube de Hola y rara vez es, si alguna vez, tiene acceso a una vez almacenan.

Cada uno de los escenarios de acceso a los datos se beneficia de un nivel de almacenamiento diferenciado que se optimiza para un patrón de acceso concreto. Con los niveles de almacenamiento de archivo, esporádico y frecuente, Azure Blob Storage satisface la necesidad de que haya niveles de almacenamiento diferenciados con modelos de fijación de precios independientes.

## <a name="blob-storage-accounts"></a>Cuentas de Almacenamiento de blobs

**Cuentas de Almacenamiento de blobs** son cuentas de almacenamiento especiales para almacenar los datos no estructurados como blobs (objetos) en Almacenamiento de Azure. Con las cuentas de almacenamiento de blobs, ahora puede elegir entre una y capas de almacenamiento de acceso esporádico a nivel de cuenta o sin interrupción, interesantes y niveles en nivel de blob de hello, basándose en los patrones de acceso de archivo. Almacenar los datos inactivos rara vez se accede al costo de almacenamiento más bajo hello, menos datos interesantes que se accede con frecuencia en un almacenamiento de menor costo de los activos y almacenar datos activos que se accede con más frecuencia en hello menor costo de acceso. Las cuentas de almacenamiento de blobs son similares tooyour cuentas de almacenamiento general existente y compartan todos los gran durabilidad de hello, disponibilidad, escalabilidad y características de rendimiento que usan hoy en día, incluida la coherencia de la API de 100 por ciento para blobs en bloques y anexar blobs.

> [!NOTE]
> Las cuentas de Almacenamiento de blobs solo admiten blobs en bloques y en anexos, pero no blobs en páginas.

Las cuentas de almacenamiento de blobs exponen hello **nivel de acceso a** atributo, lo que permite la capa de almacenamiento de hello toospecify como **activa** o **frío** según datos de hello almacenados en hello cuenta. Si hay un cambio en el patrón de uso de Hola de los datos, también puede cambiar entre estos niveles de almacenamiento en cualquier momento. nivel de archivo Hello (versión preliminar) solo puede aplicarse a nivel de blob de Hola.

> [!NOTE]
> Capa de almacenamiento de hello variación puede costar dinero adicional. Vea hello [precios y facturación](#pricing-and-billing) sección para obtener más detalles.

### <a name="hot-access-tier"></a>Nivel de acceso frecuente

Escenarios de uso de ejemplo para la capa de almacenamiento activas de hello incluyen:

* Datos que están en uso activo o toobe esperado acceso (lectura de y se escriba en) con frecuencia.
* Datos que están almacenado provisionalmente para su procesamiento y eventual capa de almacenamiento de acceso esporádico de toohello de migración.

### <a name="cool-access-tier"></a>Nivel de acceso esporádico

Escenarios de uso de ejemplo para el nivel de acceso esporádico almacenamiento Hola incluyen:

* Conjuntos de datos de copia de seguridad y recuperación ante desastres a corto plazo.
* Anterior contenido multimedia no verse con frecuencia ya pero es esperado toobe disponible inmediatamente cuando tiene acceso a.
* Grandes conjuntos de datos que necesita toobe almacenan costo eficazmente mientras que se va a recopilar los datos más para procesarlas en el futuro. (*Por ejemplo,*, almacenamiento a largo plazo de datos científicos, datos de telemetría sin procesar de una instalación de fabricación)

### <a name="archive-access-tier-preview"></a>Nivel de acceso de archivo (versión preliminar)

[Almacenamiento de archivo](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) tiene el costo más bajo de almacenamiento de Hola y mayor toohot de costos en comparación con la recuperación de datos y almacenamiento frío.

Mientras un blob está en un almacenamiento de archivo, no se puede leer, copiar, sobrescribir ni modificar. Tampoco puede tomar instantáneas de un blob en almacenamiento de archivo. Sin embargo, puede utilizar toodelete de las operaciones existentes, mostrar, obtener propiedades y metadatos del blob o cambiar el nivel de hello del blob de. tooread datos de almacenamiento de archivo, primero debe cambiar nivel de Hola de hello blob toohot o bien. Este proceso se conoce como rehidratación y puede tardar hasta too15 horas toocomplete para blobs menor que 50 GB. Tiempo adicional necesario para blobs mayores varía en función de límite de rendimiento de blob de Hola.

Durante la rehidratación, puede comprobar Hola "estado de archivo" blob propiedad tooconfirm si ha cambiado el nivel de Hola. estado de Hello lee "rehidratar-pendientes-a-caliente" o "rehidratar-pendientes-a-frío" según el nivel de destino de Hola. Tras la terminación, Hola se quita la propiedad de blob "archivar el estado" y "nivel de acceso a" hello propiedad de blob. refleja el nivel de acceso rápido o frío de Hola.  

Escenarios de uso de ejemplo para la capa de almacenamiento de archivo hello incluyen:

* Conjuntos de datos de recuperación ante desastres, archivo y copia de seguridad a largo plazo
* Datos originales (sin procesar) que deben conservarse, incluso después de que se han procesado en un formato útil final. (*Por ejemplo,*, archivos multimedia sin procesar tras la transcodificación en otros formatos)
* Cumplimiento de normas y los datos de archivo que necesita toobe almacenan durante mucho tiempo y apenas nunca se tiene acceso. (*Por ejemplo*, grabaciones de cámaras de seguridad, radiografías o resonancias antiguas en centros sanitarios, grabaciones de audio y transcripciones de llamadas de clientes para servicios financieros)

### <a name="recommendations"></a>Recomendaciones

Para más información sobre las cuentas de almacenamiento, consulte [Acerca de las cuentas de almacenamiento de Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) .

Para las aplicaciones que requieren solo bloquear o anexar el almacenamiento de blobs, se recomienda utilizar cuentas de almacenamiento de blobs, tootake aprovechar Hola diferenciados modelo de precios de almacenamiento en capas. Sin embargo, sabemos que esto puede no ser posible en ciertas circunstancias donde utilizando almacenamiento general serían cuentas Hola toogo de manera, como:

* Necesita toouse tablas, colas, o archivos y quiere que los blobs almacenados en Hola la misma cuenta de almacenamiento. Tenga en cuenta que no hay ninguna ventaja técnica toostoring en hello que misma cuenta distinta a tener Hola mismo claves compartidas.

* Todavía es necesario el modelo de implementación de toouse Hola clásico. Las cuentas de almacenamiento de blobs solo están disponibles a través del modelo de implementación de hello Azure Resource Manager.

* Necesita toouse blobs en páginas. Las cuentas de Almacenamiento de blobs no admiten los blobs en páginas. Por lo general, se recomienda usar blobs en bloques, salvo que se necesiten específicamente blobs en páginas.

* Usar una versión de hello [Storage Services REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) que es anterior a 2014-02-14 o una biblioteca de cliente con una versión inferior a 4.x y no se puede actualizar la aplicación.

> [!NOTE]
> En la actualidad, las cuentas de Blob Storage se admiten en todas las regiones de Azure.
 

## <a name="blob-level-tiering-feature-preview"></a>Característica de asignación de niveles en blobs (versión preliminar)

Ahora nivel de BLOB de interconexión permite toochange Hola nivel de los datos en el nivel de objeto de hello mediante una operación única denominada [establecer el nivel de Blob](/rest/api/storageservices/set-blob-tier). Puede cambiar fácilmente Hola de nivel de acceso de un blob entre Hola activa, frío o niveles de almacenamiento como cambien los patrones de uso, sin tener datos toomove entre cuentas. Todos los cambios de nivel se realizan de inmediato, excepto cuando se rehidrata un blob desde el archivo. Blobs en todo el almacenamiento de tres niveles pueden coexistir en Hola misma cuenta. Los blobs que no tiene un nivel asignado explícitamente hereda capa Hola de configuración de nivel de acceso de cuenta de hello.

toouse estas características en vista previa, siga las instrucciones de Hola Hola [almacenamiento de Azure y el nivel de Blob de interconexión anuncio del blog](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering).

seguimiento de Hola enumera algunas restricciones que se aplican durante la vista previa para la interconexión de nivel de blob:

* Solo admiten el almacenamiento de archivo las cuentas nuevas de Blob Storage creadas en el este de EE. UU. 2 después de inscribirse correctamente en la versión preliminar.

* Solo admiten la asignación de capas en el nivel de blob las cuentas nuevas de Blob Storage creadas en regiones públicas después de inscribirse correctamente en la versión preliminar.

* La asignación de niveles en blobs y el almacenamiento de archivo solo se admiten en el almacenamiento [LRS] (../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#locally-redundant-storage). [GRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#geo-redundant-storage) y [RA-GRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#read-access-geo-redundant-storage) se admitirán en futuras Hola.

* No puede cambiar el nivel Hola de un blob con instantáneas.

* No puede copiar ni crear instantáneas de un blob en almacenamiento de archivo.

## <a name="comparison-of-hello-storage-tiers"></a>Comparación de niveles de almacenamiento de Hola

Hello en la tabla siguiente muestra una comparación Hola interactivas y de acceso esporádico de capas de almacenamiento. Hola archivo blob nivel nivel no está en vista previa, por lo que hay ningún SLA para él.

| | **Nivel de almacenamiento frecuente** | **Nivel de almacenamiento esporádico** |
| ---- | ----- | ----- |
| **Disponibilidad** | 99,9 % | 99% |
| **Disponibilidad** <br> **(lecturas de RA-GRS)**| 99,99% | 99,9 % |
| **Cargos de uso** | Mayores costos de almacenamiento, menores costos de acceso y transacciones | Menores costos de almacenamiento, mayores costos de acceso y transacciones |
| **Tamaño mínimo de objeto** | N/D | N/D |
| **Duración mínima del almacenamiento** | N/D | N/D |
| **Latency** <br> **(Tiempo toofirst byte)** | milisegundos | milisegundos |
| **Objetivos de escalabilidad y rendimiento** | Igual que las cuentas de almacenamiento de uso general | Igual que las cuentas de almacenamiento de uso general |

> [!NOTE]
> Almacenamiento de blobs cuentas compatibilidad Hola mismos destinos de rendimiento y escalabilidad como cuentas de almacenamiento general. Consulte [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para obtener más información.


## <a name="pricing-and-billing"></a>Precios y facturación
Las cuentas de almacenamiento de blobs usan un modelo de precios para el almacenamiento de blob en función de la capa de almacenamiento de Hola. Cuando se usa una cuenta de almacenamiento de blobs, se aplica Hola después de facturación consideraciones:

* **Los costos de almacenamiento**: además toohello cantidad de datos almacenados, costo de hello del almacenamiento de datos varía dependiendo de la capa de almacenamiento de Hola. Hola por gigabyte costo es menor de nivel de acceso esporádico almacenamiento de Hola que para la capa de almacenamiento activas de Hola.

* **Los costos de acceso a datos**: para los datos en la capa de almacenamiento de acceso esporádico de hello, se le cobrará un cargo de acceso de datos por gigabyte para lecturas y escrituras.

* **Costos de transacciones**: en ambas capas hay un cargo por transacción. Sin embargo, costo por transacción de hello para el nivel de acceso esporádico almacenamiento hello es mayor que para la capa de almacenamiento activas de Hola.

* **Los costos de transferencia de datos de replicación geográfica**: solo se aplica con la replicación geográfica configurada, incluidos GRS y RA-GRS tooaccounts. La transferencia de datos de replicación geográfica incurre en un cargo por gigabyte.

* **Costos de transferencia de datos salientes**: las transferencias de datos salientes (los datos que se transfieren fuera de una región de Azure) conllevan un cargo por el uso del ancho de banda por gigabyte, lo que es coherente con las cuentas de almacenamiento de uso general.

* **Capa de almacenamiento de variación Hola**: cambiar la capa de almacenamiento de Hola de toohot frío incurre en un tooreading igual de forma gratuita todos los datos de hello existente en la cuenta de almacenamiento de Hola para cada transición. En hello otra parte, cambiar la capa de almacenamiento de Hola de toocool activa es de forma gratuita.

> [!NOTE]
> Para obtener más detalles sobre Hola modelo para las cuentas de almacenamiento de blobs de precios, consulte [precios de almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/) página. Para obtener más detalles sobre los gastos de transferencia de datos de salida de hello, consulte [detalles de precios de transferencias de datos](https://azure.microsoft.com/pricing/details/data-transfers/) página.

## <a name="quickstart"></a>Guía de inicio rápido

En esta sección se muestra hello mediante Hola portal de Azure los escenarios siguientes:

* ¿Cómo toocreate una cuenta de almacenamiento de blobs.
* ¿Cómo toomanage una cuenta de almacenamiento de blobs.

No se pueden establecer tooarchive de nivel de acceso de hello en hello en los ejemplos siguientes porque esta configuración aplica la cuenta de almacenamiento completo toohello. El nivel de acceso de archivo solo puede establecerse en un blob concreto.

### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a>Crear una cuenta de almacenamiento de Blob mediante Hola portal de Azure

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. En el menú del concentrador hello, seleccione **New** > **datos + almacenamiento** > **cuenta de almacenamiento**.

3. Escriba un nombre para la cuenta de almacenamiento.
   
    Este nombre debe ser único globalmente; se usa como parte de la dirección URL de hello utiliza objetos de hello tooaccess en la cuenta de almacenamiento de Hola.  

4. Seleccione **el Administrador de recursos** como modelo de implementación de Hola.
   
    Almacenamiento en capas sólo puede utilizarse con las cuentas de almacenamiento de administrador de recursos; se trata de hello recomendada el modelo de implementación de nuevos recursos. Para obtener más información, consulte hello [Introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).  

5. En la lista de desplegable de tipo de cuenta de hello, seleccione **almacenamiento de blobs**.
   
    Aquí es donde seleccionar tipo de saludo de la cuenta de almacenamiento. Almacenamiento en capas no está disponible en almacenamiento general; solo está disponible en hello cuenta del tipo de almacenamiento de Blob.     
   
    Tenga en cuenta que cuando se selecciona esta opción, el nivel de rendimiento de Hola se establece tooStandard. Almacenamiento en capas no está disponible con el nivel de rendimiento de hello Premium.

6. Seleccione opción de replicación de Hola Hola cuenta de almacenamiento: **LRS**, **GRS**, o **RA-GRS**. valor predeterminado de Hello es **RA-GRS**.
   
    LRS = almacenamiento con redundancia local; GRS = almacenamiento con redundancia geográfica (2 regiones); RA-GRS es el almacenamiento con redundancia geográfica con acceso de lectura (2 regiones con lectura acceso a toohello en segundo lugar).
   
    Para más información sobre las opciones de replicación del Almacenamiento de Azure, consulte [Replicación de Almacenamiento de Azure](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

7. Capa de almacenamiento derecho de hello SELECT para sus necesidades: Hola conjunto **nivel de acceso a** tooeither **frío** o **activa**. valor predeterminado de Hello es **activa**. 

8. Seleccione la suscripción de hello en que desea que la nueva cuenta de almacenamiento de toocreate Hola.

9. Especifique un nuevo grupo de recursos o seleccione un grupo de recursos existente. Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

10. Seleccione la región de hello para la cuenta de almacenamiento.

11. Haga clic en **crear** cuenta de almacenamiento de toocreate Hola.

### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a>Cambiar el nivel de almacenamiento de Hola de una cuenta de almacenamiento de Blob mediante Hola portal de Azure

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. cuenta de almacenamiento de toonavigate tooyour, seleccione todos los recursos, a continuación, seleccione su cuenta de almacenamiento.

3. En la hoja de configuración de hello, haga clic en **configuración** tooview o cambio de configuración de la cuenta de hello.

4. Capa de almacenamiento derecho de hello SELECT para sus necesidades: Hola conjunto **nivel de acceso a** tooeither **frío** o **activa**...

5. Haga clic en Guardar en la parte superior de Hola de hoja de Hola.

> [!NOTE]
> Capa de almacenamiento de hello variación puede costar dinero adicional. Vea hello [precios y facturación](#pricing-and-billing) sección para obtener más detalles.


## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a>La evaluación y la migración de cuentas de almacenamiento de tooBlob
propósito de esta sección Hello es toohelp usuarios toomake un suave transición toousing cuentas de almacenamiento de blobs. Hay dos escenarios de usuario:

* Tiene una cuenta de almacenamiento general existente y desea tooevaluate una cuenta de almacenamiento de blobs con capa de almacenamiento de información adecuada de hello tooa de cambio.
* Ha decidido toouse una cuenta de almacenamiento de blobs o ya tiene uno y desea tooevaluate si debe utilizar la capa de almacenamiento de acceso rápido o frío de Hola.

En ambos casos, Hola primera regla de negocio es tooestimate Hola costo de almacenar y obtener acceso a los datos almacenados en una cuenta de almacenamiento de blobs y comparar los costos actuales.

## <a name="evaluating-blob-storage-account-tiers"></a>Evaluación de los niveles de la cuenta de Almacenamiento de blobs

En orden tooestimate Hola del costo de almacenar y obtener acceso a los datos almacenados en una cuenta de almacenamiento de blobs, necesita tooevaluate el patrón de uso existentes o aproximar su patrón de uso esperado. En general, desea tooknow:

* El consumo del almacenamiento: ¿cuántos datos se almacenan y cómo cambia esta cifra mensualmente?

* ¿El patrón de acceso de almacenamiento: la cantidad de datos se va leer de y cuenta toohello escrito (incluidos los nuevos datos)? ¿Cuántas transacciones se utilizan para el acceso a datos y qué tipos de transacciones son?

## <a name="monitoring-existing-storage-accounts"></a>Supervisión de las cuentas de almacenamiento existentes

toomonitor el almacenamiento existente cuentas y recopilar estos datos, se puede hacer uso de análisis de almacenamiento de Azure que realiza el registro y proporciona datos de métricas para una cuenta de almacenamiento. Análisis de almacenamiento puede almacenar métricas que incluyen datos de estadísticas y la capacidad de transacciones agregados sobre solicitudes toohello servicio de almacenamiento de Blob para las cuentas de almacenamiento general así como las cuentas de almacenamiento de blobs. Estos datos se almacenan en tablas conocidas en hello misma cuenta de almacenamiento.

Para más información, consulte [Acerca de las métricas de Storage Analytics](https://msdn.microsoft.com/library/azure/hh343258.aspx) y [Esquema de tabla de métricas de Storage Analytics](https://msdn.microsoft.com/library/azure/hh343264.aspx)

> [!NOTE]
> Cuentas de almacenamiento de blobs exponen Hola punto de conexión de servicio de la tabla solo para almacenar y tener acceso a datos de métricas de Hola para esa cuenta.

consumo de almacenamiento de toomonitor hello para el servicio de almacenamiento Blob de hello, necesita las métricas de capacidad de hello tooenable.
Con esta opción habilitada, los datos de capacidad se registran diariamente para el servicio de Blob de una cuenta de almacenamiento y se graba como una entrada de la tabla que se escribe toohello *$MetricsCapacityBlob* tabla dentro de hello misma cuenta de almacenamiento.

Hola a toomonitor Hola el patrón de acceso de datos para el servicio de almacenamiento de blobs, deberá métricas tooenable Hola de transacciones por hora en el nivel de API. Con esta opción habilitada, por la API de transacciones se agregan cada hora y registra como una entrada de la tabla que se escribe toohello *$MetricsHourPrimaryTransactionsBlob* tabla dentro de hello misma cuenta de almacenamiento. Hola *$MetricsHourSecondaryTransactionsBlob* registros en la tabla Hola extremo secundario de las transacciones toohello al usar cuentas de almacenamiento de RA-GRS.

> [!NOTE]
> Si tiene una cuenta de almacenamiento de uso general en la que ha almacenado blobs de páginas y discos de máquinas virtuales junto con datos de blobs en bloques y anexos, este proceso de estimación no se podrá aplicar, Esto es porque no dispone de ninguna manera de distinguir la capacidad y transacción métricas adicionales basadas en el tipo de saludo de blob para solo bloquean y blobs en anexos, lo que pueden migra tooa cuenta de almacenamiento Blob.

tooget una buena aproximación de su consumo de datos y el patrón de acceso, se recomienda elegir un período de retención para las métricas de Hola que sea representativa de su uso normal y extrapolar. Una opción es datos de métricas de hello tooretain de 7 días y los datos de hello recopilar todas las semanas, para el análisis final Hola del mes de Hola. Otra opción es últimos 30 días de datos de métricas de hello tooretain para hello y recopile y analice datos Hola final Hola del período de 30 días de Hola.

Para más información acerca de cómo habilitar, recopilar y visualizar datos de métricas, consulte [Habilitar las métricas de Azure Storage y ver sus datos](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

> [!NOTE]
> El almacenamiento, acceso y descarga de datos de análisis también se cobra como los datos de usuario normales.

### <a name="utilizing-usage-metrics-tooestimate-costs"></a>Utilización de los costos de tooestimate de métricas de uso

### <a name="storage-costs"></a>Costos de almacenamiento

Hola entrada más reciente en la tabla de métricas de capacidad de hello *$MetricsCapacityBlob* con clave de fila de hello *"datos"* muestra Hola capacidad de almacenamiento utilizado por los datos de usuario. Hola entrada más reciente en la tabla de métricas de capacidad de hello *$MetricsCapacityBlob* con clave de fila de hello *'análisis'* muestra Hola capacidad de almacenamiento utilizado por los registros de análisis de Hola.

Esta capacidad total consumida por ambos registros de datos y análisis de usuario (si está habilitado) puede ser, a continuación, utiliza el costo de hello tooestimate de almacenar datos en la cuenta de almacenamiento de Hola. Hola mismo método también puede utilizarse para calcular el costo de almacenamiento de bloque y anexar blobs en las cuentas de almacenamiento general.

### <a name="transaction-costs"></a>Costos de transacciones

suma de Hola de *'TotalBillableRequests'*, en todas las entradas de una API de transacciones de hello tabla de métricas indica el número total de Hola de transacciones para esa API determinada. *Por ejemplo*, Hola número total de *'GetBlob'* las transacciones en un período determinado se pueden calcular mediante suma de Hola de solicitudes facturables total para todas las entradas con la clave de fila de hello *' usuario; GetBlob'*.

Orden tooestimate costos de transacción para las cuentas de almacenamiento de blobs, deberá toobreak hacia abajo de las transacciones de hello en tres grupos ya que tienen un precio distinto.

* Transacciones de escritura como *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'* y *'CopyBlob'*.
* Transacciones de eliminación como *'DeleteBlob'* y *'DeleteContainer'*.
* Las restantes transacciones.

Orden tooestimate costos de transacción para las cuentas de almacenamiento general, deberá tooaggregate todas las transacciones con independencia de la operación de Hola/API.

### <a name="data-access-and-geo-replication-data-transfer-costs"></a>Costos de transferencia de datos de acceso y de replicación geográfica

Mientras no se proporciona el análisis de almacenamiento cantidad Hola de datos lee de y escribir tooa cuenta de almacenamiento, puede calcularse de forma aproximada examinando la tabla de métricas de transacciones de Hola. suma de Hola de *'TotalIngress'* en todas las entradas de una API de métricas de transacciones de hello tabla indica la cantidad total que Hola de datos de entrada en bytes para esa API determinada. De igual forma suma de Hola de *'TotalEgress'* indica la cantidad total de Hola de datos de salida, en bytes.

En orden tooestimate Hola datos acceso a los costes de las cuentas de almacenamiento de blobs, es necesario toobreak hacia abajo de las transacciones de hello en dos grupos. 

* puede se puede estimar Hola cantidad de datos recuperados de la cuenta de almacenamiento de hello examinando la suma de Hola de *'TotalEgress'* para principalmente hello *'GetBlob'* y *'CopyBlob'* operaciones.

* cantidad de Hola de los datos escritos toohello cuenta de almacenamiento se puede estimar examinando la suma de Hola de *'TotalIngress'* para principalmente hello *'PutBlob'*, *'PutBlock'*, *'CopyBlob'* y *'AppendBlock'* operaciones.

Hola costo de transferencia de datos de replicación geográfica para las cuentas de almacenamiento también se calcula utilizando la estimación de Hola para cantidades de Hola de datos escritos al usar una cuenta de almacenamiento GRS o RA-GRS de Blob.

> [!NOTE]
> Para obtener un ejemplo más detallado sobre cómo calcular los costos de hello para el uso de capa de almacenamiento de acceso rápido o frío de Hola, eche un vistazo a Hola P+F titulada *'¿qué niveles de acceso activa y recuperación y ¿cómo se puede determinar qué una toouse'?* Hola [página de precios de almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/).
 
## <a name="migrating-existing-data"></a>Migración de datos existentes

Las cuentas de Almacenamiento de blobs son especiales para almacenar solo blobs y anexar blobs. Cuentas de almacenamiento general existentes, que le permiten toostore tablas, colas, archivos y discos, así como blobs, no pueden ser convertido tooBlob cuentas de almacenamiento. toouse Hola capas de almacenamiento, que necesita toocreate nuevas cuentas de almacenamiento de blobs y migra los datos existentes en las cuentas de hello recién creado.

Puede usar Hola después los datos existentes de métodos toomigrate en las cuentas de almacenamiento de Blob desde dispositivos de almacenamiento local, de proveedores de almacenamiento de nube de terceros o de las cuentas de almacenamiento general existentes en Azure:

### <a name="azcopy"></a>AzCopy

AzCopy es una utilidad de línea de comandos de Windows diseñada para la copia de alto rendimiento de tooand de datos del almacenamiento de Azure. Puede usar AzCopy toocopy datos en su cuenta de almacenamiento Blob de las cuentas de almacenamiento general existentes o tooupload datos de los dispositivos de almacenamiento local en su cuenta de almacenamiento de blobs.

Para obtener más información, consulte [transferir datos con la utilidad de línea de comandos de AzCopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

### <a name="data-movement-library"></a>Data Movement Library

Biblioteca de movimiento de datos de almacenamiento Azure para .NET se basa en el marco de movimiento de datos de núcleo de Hola que alimenta AzCopy. biblioteca de Hello está diseñado para alto rendimiento, confiable y tooAzCopy similar de operaciones de transferencia de datos fácil. Esto le permite tootake todas las ventajas de las características de hello proporcionadas por AzCopy en la aplicación de forma nativa sin necesidad de toodeal con ejecutar y supervisar instancias externas de AzCopy.

Para más información, consulte [Azure Storage Data Movement Library for .Net](https://github.com/Azure/azure-storage-net-data-movement)

### <a name="rest-api-or-client-library"></a>API de REST o biblioteca de cliente

Puede crear una aplicación personalizada toomigrate los datos en una cuenta de almacenamiento Blob mediante una de las bibliotecas de cliente de Azure de Hola u Hola API de REST de servicios de almacenamiento de Azure. Almacenamiento de Azure proporciona bibliotecas de cliente enriquecidas para varios lenguajes y aplicaciones como .NET, Java, C++, Node.JS, PHP, Ruby y Python. bibliotecas de cliente de Hello ofrecen capacidades avanzadas como la lógica de reintento, registro y cargas en paralelo. También puede desarrollar directamente contra Hola API de REST, que se puede llamar mediante cualquier lenguaje que realiza las solicitudes HTTP/HTTPS.

Para más información, consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](storage-dotnet-how-to-use-blobs.md).

> [!NOTE]
> Blobs cifradas mediante el cifrado de cliente almacenan metadatos relacionados con el cifrado almacenada con hello blob. Es fundamental que cualquier mecanismo de copia debe asegurarse de que Hola metadatos del blob y especialmente Hola metadatos relacionados con el cifrado, se conserva. Si copia blobs de hello sin estos metadatos, el contenido de blob Hola puede no recuperar de nuevo. Para más información acerca de los metadatos relacionados con el cifrado, consulte [Cifrado del lado de cliente y Azure Key Vault para Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).
 
## <a name="faq"></a>P+F

1. **¿Siguen disponibles las cuentas de almacenamiento existentes?**
   
    Sí, las cuentas de almacenamiento existentes siguen estando disponibles y no se han cambiado sus precios ni sus funciones.  No tienen Hola capacidad toochoose una capa de almacenamiento pero no tendrá posibilidades de interconexión en hello futuras.

2. **¿Por qué y cuándo conviene empezar a usar cuentas de Almacenamiento de blobs?**
   
    Las cuentas de almacenamiento de blobs están adaptadas para almacenar blobs y nos permiten toointroduce nuevas características centrada en el blob. En el futuro, las cuentas de almacenamiento de blobs son Hola recomendada método para almacenar objetos BLOB, como funciones en el futuro, como almacenamiento jerárquico y los niveles se introducirán en función de este tipo de cuenta. Sin embargo, resulta una tooyou cuando le gustaría toomigrate según sus requisitos empresariales.

3. **¿Puedo convertir mi tooa de cuenta de almacenamiento cuenta de almacenamiento Blob existente?**
   
    No. Una cuenta de Blob Storage es un tipo de cuenta de almacenamiento diferente y es preciso crearla desde cero y migrar los datos, como ya se ha explicado.

4. **¿Se puede almacenar objetos en ambas capas de almacenamiento en hello misma cuenta?**
   
    Hola *'Nivel de acceso a'* atributo indica el valor de Hola de capa de almacenamiento de hello establecido en el nivel de cuenta y se aplica a objetos tooall en esa cuenta. Sin embargo, característica Hola nivel de blob de niveles (versión preliminar) permitirá tooset Hola nivel de acceso en blobs específicos, y esto anulará la configuración de nivel de acceso de Hola de cuenta de hello. 

5. **¿Puedo cambiar la capa de almacenamiento de Hola de mi cuenta de almacenamiento de Blob?**
   
    Sí. Puede cambiar la capa de almacenamiento de Hola Hola establecer *'Nivel de acceso a'* atributo Hola cuenta de almacenamiento. Variación capa de almacenamiento de Hola aplica a objetos tooall almacenados en la cuenta de hello. Capa de almacenamiento de hello cambiante de toocool activa no incurre en cualquier cargo, al cambiar de acceso esporádico toohot incurren en un costo de GB para leer todos los datos de hello en la cuenta de hello por.

6. **¿Con qué frecuencia se puede cambiar capa de almacenamiento de Hola de mi cuenta de almacenamiento de Blob?**
   
    Mientras no se aplican una limitación en con qué frecuencia se puede cambiar la capa de almacenamiento de Hola, tenga en cuenta que cambiar la capa de almacenamiento de Hola de frío toohot puede incurrir en cargos significativos. No se recomienda cambiar la capa de almacenamiento de hello con frecuencia.

7. **¿Blobs hello en la capa de almacenamiento de acceso esporádico de hello comportarse de manera diferente que los de la capa de almacenamiento activas de Hola Hola?**
   
    Los blobs en la capa de almacenamiento activas de hello tienen Hola mismo latencia como blobs en las cuentas de almacenamiento general. Blobs en la capa de almacenamiento de acceso esporádico de hello con una latencia similar (en milisegundos) como blobs en cuentas de almacenamiento general.
   
    Blobs en la capa de almacenamiento de acceso esporádico de hello tienen un nivel de servicio disponibilidad (SLA) ligeramente inferior a blobs de hello almacenados en la capa de almacenamiento activas de Hola. Para más información, consulte [Acuerdo de Nivel de Servicio para Almacenamiento](https://azure.microsoft.com/support/legal/sla/storage).

8. **¿Puedo almacenar blobs en páginas y discos de máquinas virtuales en las cuentas de Almacenamiento de blobs?**
   
    Las cuentas de Almacenamiento de blobs solo admiten blobs en bloques y en anexos, pero no blobs en páginas. Discos de máquina virtual de Azure están respaldados por blobs de página y así las cuentas de almacenamiento de blobs no pueden ser toostore usa discos de máquina virtual. Sin embargo, resulta posible toostore copias de seguridad de discos de máquina virtual de hello como blobs en bloques en una cuenta de almacenamiento de blobs.

9. **¿Es necesario toochange Mis cuentas de almacenamiento de blobs de toouse las aplicaciones existentes?**
   
    Las cuentas de almacenamiento de blobs tienen una coherencia del 100 % con la API con las cuentas de almacenamiento de uso general para blobs en bloques y en anexos. Siempre que la aplicación está utilizando los blobs en bloques o blobs en anexos y utilizas versión 2014-02-14 de Hola de hello [Storage Services REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) o mayor la aplicación debería funcionar. Si está utilizando una versión anterior del protocolo de hello, a continuación, debe actualizar la nueva versión de aplicación toouse Hola así como toowork sin problemas con ambos tipos de cuentas de almacenamiento. En general, se recomienda siempre usando Hola versión más reciente, independientemente de qué tipo de cuenta de almacenamiento que use.

10. **¿Hay un cambio en la experiencia del usuario?**
    
    Las cuentas de almacenamiento de blobs son cuentas de almacenamiento general tooa muy similar para el almacenamiento de bloque y blobs en anexos y admiten todas las características clave de Hola de almacenamiento de Azure, como gran durabilidad y disponibilidad, escalabilidad, rendimiento y seguridad. Distintas cuentas de almacenamiento de tooBlob específicos de características y restricciones hello y sus niveles de almacenamiento que se ha llamado anteriormente, todo lo que sigue siendo else Hola igual.

## <a name="next-steps"></a>Pasos siguientes

### <a name="evaluate-blob-storage-accounts"></a>Evaluación de cuentas de Almacenamiento de blobs

[Comprobación de la disponibilidad de las cuentas de Almacenamiento de blobs por región](https://azure.microsoft.com/regions/#services)

[Evaluación del uso de las cuentas de almacenamiento actuales mediante la habilitación de las métricas de Almacenamiento de Azure](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Comprobación de los precios de almacenamiento de blobs por región](https://azure.microsoft.com/pricing/details/storage/)

[Detalles de precios de Transferencias de datos](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a>Empezar a utilizar cuentas de Almacenamiento de blobs

[Introducción al Almacenamiento de blobs de Azure mediante .NET](storage-dotnet-how-to-use-blobs.md)

[Mover datos tooand desde el almacenamiento de Azure](../common/storage-moving-data.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Examen y exploración de cuentas de almacenamiento](http://storageexplorer.com/)