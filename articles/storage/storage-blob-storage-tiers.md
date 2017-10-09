---
title: "aaaAzure frío almacenamiento de blobs | Documentos de Microsoft"
description: "Las capas de almacenamiento de Almacenamiento de blobs de Azure ofrecen un almacenamiento rentable para datos de objetos basado en patrones de acceso. capa de almacenamiento de acceso esporádico de Hello está optimizado para los datos que se accede con menos frecuencia."
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
ms.openlocfilehash: 56fae3fdae31a6958ebae01fd96a0366e70ae938
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-and-cool-storage-tiers"></a>Almacenamiento de blobs de Azure: capas de almacenamiento de acceso frecuente y esporádico
## <a name="overview"></a>Información general
Azure Storage ofrece dos capas de almacenamiento para almacenamiento de objetos de blobs, por lo que puede almacenar los datos de forma más rentable en función de cómo los use. Hello Azure **capa de almacenamiento activa** está optimizado para almacenar datos que se accede con frecuencia. Hello Azure **capa de almacenamiento frío** está optimizado para almacenar datos con poca frecuencia acceso y larga duración. Datos de capa de almacenamiento de acceso esporádico de hello pueden tolerar una disponibilidad ligeramente inferior, pero todavía requiere gran durabilidad y características similares de acceso de tiempo y el rendimiento como datos activos. En el caso de los datos de acceso esporádico, un Acuerdo de Nivel de Servicio con una disponibilidad ligeramente inferior y unos costos de acceso mayores es aceptable a cambio de unos costos de almacenamiento mucho menores.

En la actualidad, los datos almacenados en la nube de hello crece a un ritmo exponencial. el precio es toomanage para sus necesidades de almacenamiento de expansión, resulta útil tooorganize los datos en función de atributos como la frecuencia de acceso y planeado período de retención. Datos almacenados en la nube de hello pueden ser diferentes en cuanto a cómo se genera, además de procesar y acceder a través de su duración. A algunos datos se accede y se modifican activamente a lo largo de su duración. Algunos datos se obtiene acceso con frecuencia al principio de su duración, con acceso quitar drásticamente como Hola datos edades. Algunos datos permanecen inactivos en la nube de Hola y rara vez es, si alguna vez, tiene acceso a una vez almacenan.

Cada uno de los escenarios de acceso a los datos descritos anteriormente se benefician de una capa de almacenamiento diferenciada que se optimiza para un patrón de acceso concreto. Presentación de Hola de capas de almacenamiento activos e interesantes, Azure Blob storage ahora satisface esta necesidad de niveles diferenciados de almacenamiento con separar modelos de precios.

## <a name="blob-storage-accounts"></a>Cuentas de Almacenamiento de blobs
**Cuentas de Almacenamiento de blobs** son cuentas de almacenamiento especiales para almacenar los datos no estructurados como blobs (objetos) en Almacenamiento de Azure. Con las cuentas de almacenamiento de blobs, ahora puede elegir entre toostore de niveles de almacenamiento interactivas y de acceso esporádico los datos interesantes que se accede con menos frecuencia a un menor costo de almacenamiento y datos activos de almacén de acceso más frecuente en un acceso de menor costo. Las cuentas de almacenamiento de blobs son similares tooyour cuentas de almacenamiento general existente y compartan todos los gran durabilidad de hello, disponibilidad, escalabilidad y características de rendimiento que usan hoy en día, incluida la coherencia de la API de 100% para blobs en bloques y blobs en anexos.

> [!NOTE]
> Las cuentas de Almacenamiento de blobs solo admiten blobs en bloques y en anexos, pero no blobs en páginas.
> 
> 

Las cuentas de almacenamiento de blobs exponen hello **nivel de acceso a** atributo, lo que permite la capa de almacenamiento de hello toospecify como **activa** o **frío** según datos de hello almacenados en hello cuenta. Si hay un cambio en el patrón de uso de Hola de los datos, también puede cambiar entre estos niveles de almacenamiento en cualquier momento.

> [!NOTE]
> Capa de almacenamiento de hello variación puede costar dinero adicional. Vea hello [precios y facturación](storage-blob-storage-tiers.md#pricing-and-billing) sección para obtener más detalles.
> 
> 

Escenarios de uso de ejemplo para la capa de almacenamiento activas de hello incluyen:

* Datos que están en uso activo o toobe esperado acceso (lectura de y se escriba en) con frecuencia.
* Datos que están almacenado provisionalmente para su procesamiento y eventual capa de almacenamiento de acceso esporádico de toohello de migración.

Escenarios de uso de ejemplo para el nivel de acceso esporádico almacenamiento Hola incluyen:

* Conjuntos de datos de copia de seguridad, archivo y recuperación ante desastres.
* Anterior contenido multimedia no verse con frecuencia ya pero es esperado toobe disponible inmediatamente cuando tiene acceso a.
* Grandes conjuntos de datos que necesita toobe almacenan costo eficazmente mientras que se va a recopilar los datos más para procesarlas en el futuro. (*por ejemplo,*, almacenamiento a largo plazo de datos científicos, datos de telemetría sin procesar de una instalación de fabricación)
* Datos originales (sin procesar) que deben conservarse, incluso después de que se han procesado en un formato útil final. (*por ejemplo,*, archivos multimedia sin procesar tras la transcodificación en otros formatos)
* Cumplimiento de normas y los datos de archivo que necesita toobe almacenan durante mucho tiempo y apenas nunca se tiene acceso. (*por ejemplo*, grabaciones de cámaras de seguridad, radiografías o resonancias antiguas en centros sanitarios, grabaciones de audio y transcripciones de llamadas de clientes para servicios financieros)

Para más información sobre las cuentas de almacenamiento, consulte [Acerca de las cuentas de almacenamiento de Azure](storage-create-storage-account.md) .

Para las aplicaciones que requieren solo bloquear o anexar el almacenamiento de blobs, se recomienda utilizar cuentas de almacenamiento de blobs, tootake aprovechar Hola diferenciados modelo de precios de almacenamiento en capas. Sin embargo, sabemos que esto puede no ser posible en ciertas circunstancias donde utilizando almacenamiento general serían cuentas Hola toogo de manera, como:

* Necesita toouse tablas, colas, o archivos y quiere que los blobs almacenados en Hola la misma cuenta de almacenamiento. Tenga en cuenta que no hay ninguna ventaja técnica toostoring en hello que misma cuenta distinta a tener Hola mismo claves compartidas.
* Todavía es necesario el modelo de implementación de toouse Hola clásico. Las cuentas de almacenamiento de blobs solo están disponibles a través del modelo de implementación de hello Azure Resource Manager.
* Necesita toouse blobs en páginas. Las cuentas de Almacenamiento de blobs no admiten los blobs en páginas. Por lo general, se recomienda usar blobs en bloques, salvo que se necesiten específicamente blobs en páginas.
* Usar una versión de hello [Storage Services REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) que es anterior a 2014-02-14 o una biblioteca de cliente con una versión inferior a 4.x y no se puede actualizar la aplicación.

> [!NOTE]
> En la actualidad, las cuentas de Blob Storage se admiten en todas las regiones de Azure.
> 
> 

## <a name="comparison-between-hello-storage-tiers"></a>Comparación entre las capas de almacenamiento de Hola
Hello tabla siguiente resaltan comparación Hola entre dos capas de almacenamiento hello:

<table border="1" cellspacing="0" cellpadding="0" style="border: 1px solid #000000;">
<col width="250">
<col width="250">
<col width="250">
<tbody>
<tr>
    <td><strong><center></center></strong></td>
    <td><strong><center>Capa de almacenamiento de acceso frecuente</center></strong></td>
    <td><strong><center>Capa de almacenamiento de acceso esporádico</center></strong></td
</tr>
<tr>
    <td><strong><center>Disponibilidad</center></strong></td>
    <td><center>99.9%</center></td>
    <td><center>99%</center></td>
</tr>
<tr>
    <td><strong><center>Disponibilidad<br>(lecturas de RA-GRS)</center></strong></td>
    <td><center>99.99%</center></td>
    <td><center>99.9%</center></td>
</tr>
<tr>
    <td><strong><center>Cargos de uso</center></strong></td>
    <td><center>Mayores costos de almacenamiento<br>Menores costos de acceso y transacciones</center></td>
    <td><center>Menores costos de almacenamiento<br>Mayores costos de acceso y transacciones</center></td>
</tr>
<tr>
    <td><strong><center>Tamaño mínimo de objeto<center></strong></td>
    <td colspan="2"><center>N/D</center></td>
</tr>
<tr>
    <td><strong><center>Duración mínima del almacenamiento<center></strong></td>
    <td colspan="2"><center>N/D</center></td>
</tr>
<tr>
    <td><strong><center>Latencia<br>(Tiempo toofirst byte)<center></strong></td>
    <td colspan="2"><center>milisegundos</center></td>
</tr>
<tr>
    <td><strong><center>Objetivos de escalabilidad y rendimiento<center></strong></td>
    <td colspan="2"><center>Igual que las cuentas de almacenamiento de uso general</center></td>
</tr>
</tbody>
</table>

> [!NOTE]
> Almacenamiento de blobs cuentas compatibilidad Hola mismos destinos de rendimiento y escalabilidad como cuentas de almacenamiento general. Consulte [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) para obtener más información.
> 
> 

## <a name="pricing-and-billing"></a>Precios y facturación
Las cuentas de almacenamiento de blobs usan un nuevo modelo de precios para el almacenamiento de blob en función de la capa de almacenamiento de Hola. Cuando se usa una cuenta de almacenamiento de blobs, se aplica Hola después de facturación consideraciones:

* **Los costos de almacenamiento**: además toohello cantidad de datos almacenados, costo de hello del almacenamiento de datos varía dependiendo de la capa de almacenamiento de Hola. Hola por gigabyte costo es menor de nivel de acceso esporádico almacenamiento de Hola que para la capa de almacenamiento activas de Hola.
* **Los costos de acceso a datos**: para los datos en la capa de almacenamiento de acceso esporádico de hello, se le cobrará un cargo de acceso de datos por gigabyte para lecturas y escrituras.
* **Costos de transacciones**: en ambas capas hay un cargo por transacción. Sin embargo, costo por transacción de hello para el nivel de acceso esporádico almacenamiento hello es mayor que para la capa de almacenamiento activas de Hola.
* **Los costos de transferencia de datos de replicación geográfica**: solo se aplica con la replicación geográfica configurada, incluidos GRS y RA-GRS tooaccounts. La transferencia de datos de replicación geográfica incurre en un cargo por gigabyte.
* **Costos de transferencia de datos salientes**: las transferencias de datos salientes (los datos que se transfieren fuera de una región de Azure) conllevan un cargo por el uso del ancho de banda por gigabyte, lo que es coherente con las cuentas de almacenamiento de uso general.
* **Capa de almacenamiento de variación Hola**: cambiar la capa de almacenamiento de Hola de toohot frío, le cobrará un tooreading igual de forma gratuita todos los datos de hello existente en la cuenta de almacenamiento de Hola para cada transición. En hello otra parte, cambiar la capa de almacenamiento de Hola de toocool activa será de forma gratuita.

> [!NOTE]
> En orden tooallow usuarios tootry out Hola nuevos niveles de almacenamiento y validar la funcionalidad después del lanzamiento, cargo de Hola para cambiar la capa de almacenamiento de Hola de toohot frío se cobrará desactivado hasta el 30 de junio de 2016. A partir del 1 de julio de 2016, Hola aplicará cargo aplicado tooall realice la transición de toohot frío. Para obtener más detalles sobre el modelo para las cuentas de almacenamiento de blobs de precios de hello, consulte [precios de almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/) página. Para obtener más detalles sobre los datos de salida de hello ver gastos de transferencia, [detalles de precios de transferencias de datos](https://azure.microsoft.com/pricing/details/data-transfers/) página.
> 
> 

## <a name="quick-start"></a>Inicio rápido
En esta sección, demostraremos hello mediante Hola portal de Azure los escenarios siguientes:

* ¿Cómo toocreate una cuenta de almacenamiento de blobs.
* ¿Cómo toomanage una cuenta de almacenamiento de blobs.

### <a name="using-hello-azure-portal"></a>Uso de hello portal de Azure
#### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a>Crear una cuenta de almacenamiento de Blob mediante Hola portal de Azure
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, seleccione **New** > **datos + almacenamiento** > **cuenta de almacenamiento**.
3. Escriba un nombre para la cuenta de almacenamiento.
   
    Este nombre debe ser único globalmente; se usa como parte de la dirección URL de hello utiliza objetos de hello tooaccess en la cuenta de almacenamiento de Hola.  
4. Seleccione **el Administrador de recursos** como modelo de implementación de Hola.
   
    Almacenamiento en capas sólo puede utilizarse con las cuentas de almacenamiento de administrador de recursos; se trata de hello recomendada el modelo de implementación de nuevos recursos. Para obtener más información, consulte hello [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).  
5. En la lista de desplegable de tipo de cuenta de hello, seleccione **almacenamiento de blobs**.
   
    Aquí es donde seleccionar tipo de saludo de la cuenta de almacenamiento. Almacenamiento en capas no está disponible en almacenamiento general; solo está disponible en hello cuenta del tipo de almacenamiento de Blob.     
   
    Tenga en cuenta que cuando se selecciona esta opción, el nivel de rendimiento de Hola se establece tooStandard. Almacenamiento en capas no está disponible con el nivel de rendimiento de hello Premium.
6. Seleccione opción de replicación de Hola Hola cuenta de almacenamiento: **LRS**, **GRS**, o **RA-GRS**. valor predeterminado de Hello es **RA-GRS**.
   
    LRS = almacenamiento con redundancia local; GRS = almacenamiento con redundancia geográfica (2 regiones); RA-GRS es el almacenamiento con redundancia geográfica con acceso de lectura (2 regiones con lectura acceso a toohello en segundo lugar).
   
    Para más información sobre las opciones de replicación del Almacenamiento de Azure, consulte [Replicación de Almacenamiento de Azure](storage-redundancy.md).
7. Capa de almacenamiento derecho de hello SELECT para sus necesidades: Hola conjunto **nivel de acceso a** tooeither **frío** o **activa**. valor predeterminado de Hello es **activa**.
8. Seleccione la suscripción de hello en que desea que la nueva cuenta de almacenamiento de toocreate Hola.
9. Especifique un nuevo grupo de recursos o seleccione un grupo de recursos existente. Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
10. Seleccione la región de hello para la cuenta de almacenamiento.
11. Haga clic en **crear** cuenta de almacenamiento de toocreate Hola.

#### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a>Cambiar el nivel de almacenamiento de Hola de una cuenta de almacenamiento de Blob mediante Hola portal de Azure
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. cuenta de almacenamiento de toonavigate tooyour, seleccione todos los recursos, a continuación, seleccione su cuenta de almacenamiento.
3. En la hoja de configuración de hello, haga clic en **configuración** tooview o cambio de configuración de la cuenta de hello.
4. Capa de almacenamiento derecho de hello SELECT para sus necesidades: Hola conjunto **nivel de acceso a** tooeither **frío** o **activa**.
5. Haga clic en Guardar en la parte superior de Hola de hoja de Hola.

> [!NOTE]
> Capa de almacenamiento de hello variación puede costar dinero adicional. Vea hello [precios y facturación](storage-blob-storage-tiers.md#pricing-and-billing) sección para obtener más detalles.
> 
> 

## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a>La evaluación y la migración de cuentas de almacenamiento de tooBlob
propósito de esta sección Hello es toohelp usuarios toomake un suave transición toousing cuentas de almacenamiento de blobs. Hay dos escenarios de usuario:

* Tiene una cuenta de almacenamiento general existente y desea tooevaluate una cuenta de almacenamiento de blobs con capa de almacenamiento de información adecuada de hello tooa de cambio.
* Ha decidido toouse una cuenta de almacenamiento de blobs o ya tiene uno y desea tooevaluate si debe utilizar la capa de almacenamiento de acceso rápido o frío de Hola.

En ambos casos, Hola primera regla de negocio es tooestimate Hola costo de almacenar y obtener acceso a los datos almacenados en una cuenta de almacenamiento de blobs y comparar los costos actuales.

### <a name="evaluating-blob-storage-account-tiers"></a>Evaluación de los niveles de la cuenta de Almacenamiento de blobs
En orden tooestimate Hola del costo de almacenar y obtener acceso a los datos almacenados en una cuenta de almacenamiento de blobs, se necesita tooevaluate el patrón de uso existentes o aproximado su patrón de uso esperado. En general, le interesará tooknow:

* El consumo del almacenamiento: ¿cuántos datos se almacenan y cómo cambia esta cifra mensualmente?
* ¿El patrón de acceso de almacenamiento: la cantidad de datos se va leer de y cuenta toohello escrito (incluidos los nuevos datos)? ¿Cuántas transacciones se utilizan para el acceso a datos y qué tipos de transacciones son?

#### <a name="monitoring-existing-storage-accounts"></a>Supervisión de las cuentas de almacenamiento existentes
toomonitor el almacenamiento existente cuentas y recopilar estos datos, se puede hacer uso de análisis de almacenamiento de Azure que realiza el registro y proporciona datos de métricas para una cuenta de almacenamiento.
Análisis de almacenamiento puede almacenar métricas que incluyen datos de estadísticas y la capacidad de transacciones agregados sobre solicitudes toohello servicio de almacenamiento de Blob para las cuentas de almacenamiento general así como las cuentas de almacenamiento de blobs.
Estos datos se almacenan en tablas conocidas en hello misma cuenta de almacenamiento.

Para más información, consulte [Acerca de las métricas del análisis de almacenamiento](https://msdn.microsoft.com/library/azure/hh343258.aspx) y [Esquema de tabla de métricas de análisis de almacenamiento](https://msdn.microsoft.com/library/azure/hh343264.aspx).

> [!NOTE]
> Cuentas de almacenamiento de blobs exponen Hola punto de conexión de servicio de la tabla solo para almacenar y tener acceso a datos de métricas de Hola para esa cuenta.
> 
> 

consumo de almacenamiento de toomonitor hello para el servicio de almacenamiento Blob de hello, necesitará las métricas de capacidad de hello tooenable.
Con esta opción habilitada, los datos de capacidad se registran diariamente para el servicio de Blob de una cuenta de almacenamiento y se graba como una entrada de la tabla que se escribe toohello *$MetricsCapacityBlob* tabla dentro de hello misma cuenta de almacenamiento.

Hola a toomonitor Hola el patrón de acceso de datos de servicio de almacenamiento Blob, necesitará métricas tooenable Hola de transacciones por hora en el nivel de API.
Con esta opción habilitada, por la API de transacciones se agregan cada hora y registra como una entrada de la tabla que se escribe toohello *$MetricsHourPrimaryTransactionsBlob* tabla dentro de hello misma cuenta de almacenamiento. Hola *$MetricsHourSecondaryTransactionsBlob* registros en la tabla Hola extremo secundario de toohello de transacciones en el caso de las cuentas de almacenamiento de RA-GRS.

> [!NOTE]
> Si tiene una cuenta de almacenamiento de uso general en la que ha almacenado blobs de páginas y discos de máquinas virtuales junto con datos de blobs en bloques y anexos, este proceso de estimación no se podrá aplicar, Esto es porque no tendrá ninguna manera de capacidad distintivo y transacción métricas adicionales basadas en el tipo de saludo de blob para solo bloquear y anexar BLOB, los cuales se pueden migra tooa cuenta de almacenamiento Blob.
> 
> 

tooget una buena aproximación de su consumo de datos y el patrón de acceso, se recomienda elegir un período de retención para las métricas de Hola que sea representativa de su uso normal y extrapolar.
Una opción es datos de métricas de hello tooretain de 7 días y los datos de hello recopilar todas las semanas, para el análisis final Hola del mes de Hola.
Otra opción es últimos 30 días de datos de métricas de hello tooretain para hello y recopile y analice datos Hola final Hola del período de 30 días de Hola.

Para más información acerca de cómo habilitar, recopilar y visualizar datos de métricas, consulte [Habilitar las métricas de almacenamiento de Azure y ver sus datos](storage-enable-and-view-metrics.md).

> [!NOTE]
> El almacenamiento, acceso y descarga de datos de análisis también se cobra como los datos de usuario normales.
> 
> 

#### <a name="utilizing-usage-metrics-tooestimate-costs"></a>Utilización de los costos de tooestimate de métricas de uso
##### <a name="storage-costs"></a>Costos de almacenamiento
Hola entrada más reciente en la tabla de métricas de capacidad de hello *$MetricsCapacityBlob* con clave de fila de hello *"datos"* muestra Hola capacidad de almacenamiento utilizado por los datos de usuario.
Hola entrada más reciente en la tabla de métricas de capacidad de hello *$MetricsCapacityBlob* con clave de fila de hello *'análisis'* muestra Hola capacidad de almacenamiento utilizado por los registros de análisis de Hola.

Esta capacidad total consumida por ambos registros de datos y análisis de usuario (si está habilitado) puede ser, a continuación, utiliza el costo de hello tooestimate de almacenar datos en la cuenta de almacenamiento de Hola.
Hola mismo método también puede utilizarse para calcular el costo de almacenamiento de bloque y anexar blobs en las cuentas de almacenamiento general.

##### <a name="transaction-costs"></a>Costos de transacciones
suma de Hola de *'TotalBillableRequests'*, en todas las entradas de una API de transacciones de hello tabla de métricas indica el número total de Hola de transacciones para esa API determinada. *Por ejemplo,*, Hola número total de *'GetBlob'* las transacciones en un período determinado se pueden calcular mediante suma de Hola de solicitudes facturables total para todas las entradas con la clave de fila de hello *' usuario; GetBlob'*.

Orden tooestimate costos de transacción para las cuentas de almacenamiento de blobs, deberá toobreak hacia abajo de las transacciones de hello en tres grupos ya que tienen un precio distinto.

* Transacciones de escritura como *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'* y *'CopyBlob'*.
* Transacciones de eliminación como *'DeleteBlob'* y *'DeleteContainer'*.
* Las restantes transacciones.

Orden tooestimate costos de transacción para las cuentas de almacenamiento general, deberá tooaggregate todas las transacciones con independencia de la operación de Hola/API.

##### <a name="data-access-and-geo-replication-data-transfer-costs"></a>Costos de transferencia de datos de acceso y de replicación geográfica
Mientras no se proporciona el análisis de almacenamiento cantidad Hola de datos lee de y escribir tooa cuenta de almacenamiento, puede calcularse de forma aproximada examinando la tabla de métricas de transacciones de Hola.
suma de Hola de *'TotalIngress'* en todas las entradas de una API de métricas de transacciones de hello tabla indica la cantidad total que Hola de datos de entrada en bytes para esa API determinada.
De igual forma suma de Hola de *'TotalEgress'* indica la cantidad total de Hola de datos de salida, en bytes.

En orden tooestimate Hola datos acceso a los costes de las cuentas de almacenamiento de blobs, será necesario toobreak hacia abajo de las transacciones de hello en dos grupos.

* puede se puede estimar Hola cantidad de datos recuperados de la cuenta de almacenamiento de hello examinando la suma de Hola de *'TotalEgress'* para principalmente hello *'GetBlob'* y *'CopyBlob'* operaciones.
* cantidad de Hola de los datos escritos toohello cuenta de almacenamiento se puede estimar examinando la suma de Hola de *'TotalIngress'* para principalmente hello *'PutBlob'*, *'PutBlock'*, *'CopyBlob'* y *'AppendBlock'* operaciones.

Hola costo de transferencia de datos de replicación geográfica para cuentas de almacenamiento también se calcula utilizando la estimación de hello para la cantidad de Hola de los datos escritos en el caso de una cuenta de almacenamiento GRS o RA-GRS de Blob.

> [!NOTE]
> Para obtener un ejemplo más detallado sobre cómo calcular los costos de hello para el uso de capa de almacenamiento de acceso rápido o frío de hello, por favor, eche un vistazo a Hola P+F titulada *'¿qué niveles de acceso activa y recuperación y ¿cómo se puede determinar qué una toouse'?* Hola [página de precios de almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/).
> 
> 

### <a name="migrating-existing-data"></a>Migración de datos existentes
Las cuentas de Almacenamiento de blobs son especiales para almacenar solo blobs y anexar blobs. Cuentas de almacenamiento general existentes, que le permiten toostore tablas, colas, archivos y discos, así como blobs, no pueden ser convertido tooBlob cuentas de almacenamiento. toouse Hola capas de almacenamiento, necesitará toocreate nuevas cuentas de almacenamiento de blobs y migrar los datos existentes en las cuentas de hello recién creado.

Puede usar Hola después los datos existentes de métodos toomigrate en las cuentas de almacenamiento de Blob desde dispositivos de almacenamiento local, de proveedores de almacenamiento de nube de terceros o de las cuentas de almacenamiento general existentes en Azure:

#### <a name="azcopy"></a>AzCopy
AzCopy es una utilidad de línea de comandos de Windows diseñada para la copia de alto rendimiento de tooand de datos del almacenamiento de Azure. Puede usar AzCopy toocopy datos en su cuenta de almacenamiento Blob de las cuentas de almacenamiento general existentes o tooupload datos de los dispositivos de almacenamiento local en su cuenta de almacenamiento de blobs.

Para obtener más información, consulte [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md).

#### <a name="data-movement-library"></a>Biblioteca de movimiento de datos
Biblioteca de movimiento de datos de almacenamiento Azure para .NET se basa en el marco de movimiento de datos de núcleo de Hola que alimenta AzCopy. Hola biblioteca está diseñada para alto rendimiento, tooAzCopy similar de operaciones de transferencia de datos fácil y confiables. Esto le permite tootake todas las ventajas de las características de hello proporcionadas por AzCopy en la aplicación de forma nativa sin necesidad de toodeal con ejecutar y supervisar instancias externas de AzCopy.

Para más información, consulte [Azure Storage Data Movement Library for .Net](https://github.com/Azure/azure-storage-net-data-movement)

#### <a name="rest-api-or-client-library"></a>API de REST o biblioteca de cliente
Puede crear una aplicación personalizada toomigrate los datos en una cuenta de almacenamiento Blob mediante una de las bibliotecas de cliente de Azure de Hola u Hola API de REST de servicios de almacenamiento de Azure. Almacenamiento de Azure proporciona bibliotecas de cliente enriquecidas para varios lenguajes y aplicaciones como .NET, Java, C++, Node.JS, PHP, Ruby y Python. bibliotecas de cliente de Hello ofrecen capacidades avanzadas como la lógica de reintento, registro y cargas en paralelo. También puede desarrollar directamente contra Hola API de REST, que se puede llamar mediante cualquier lenguaje que realiza las solicitudes HTTP/HTTPS.

Para más información, consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](storage-dotnet-how-to-use-blobs.md).

> [!NOTE]
> Blobs cifradas mediante el cifrado de cliente almacenan metadatos relacionados con el cifrado almacenada con hello blob. Es fundamental que cualquier mecanismo de copia debe asegurarse de que Hola metadatos del blob y especialmente Hola metadatos relacionados con el cifrado, se conserva. Si copia blobs de hello sin estos metadatos, el contenido de blob hello no pueda recuperarse nuevo. Para más información acerca de los metadatos relacionados con el cifrado, consulte [Cifrado del lado de cliente y Azure Key Vault para Microsoft Azure Storage](storage-client-side-encryption.md).
> 
> 

## <a name="faqs"></a>Preguntas más frecuentes
1. **¿Siguen disponibles las cuentas de almacenamiento existentes?**
   
    Sí, las cuentas de almacenamiento existentes siguen estando disponibles y no se han cambiado sus precios ni sus funciones.  No tienen Hola capacidad toochoose una capa de almacenamiento pero no tendrá posibilidades de interconexión en hello futuras.
2. **¿Por qué y cuándo conviene empezar a usar cuentas de Almacenamiento de blobs?**
   
    Las cuentas de almacenamiento de blobs están adaptadas para almacenar blobs y nos permiten toointroduce nuevas características centrada en el blob. En el futuro, las cuentas de almacenamiento de blobs son Hola recomendada método para almacenar objetos BLOB, como funciones en el futuro, como almacenamiento jerárquico y los niveles se introducirán en función de este tipo de cuenta. Sin embargo, resulta una tooyou cuando le gustaría toomigrate según sus requisitos empresariales.
3. **¿Puedo convertir mi tooa de cuenta de almacenamiento cuenta de almacenamiento Blob existente?**
   
    No. Cuenta de almacenamiento BLOB es un tipo diferente de la cuenta de almacenamiento y deberá toocreate lo nuevo y migrar los datos, como se explicó anteriormente.
4. **¿Se puede almacenar objetos en ambas capas de almacenamiento en hello misma cuenta?**
   
    Hola *'Nivel de acceso a'* atributo que indica la capa de almacenamiento de Hola se establece en un nivel de cuenta y aplica a objetos tooall en esa cuenta. No se puede establecer el atributo de nivel de acceso de hello en un nivel de objeto.
5. **¿Puedo cambiar la capa de almacenamiento de Hola de mi cuenta de almacenamiento de Blob?**
   
    Sí. Será capaz de toochange capa de almacenamiento de Hola por establecer hello *'Nivel de acceso a'* atributo Hola cuenta de almacenamiento. Capa de almacenamiento de hello variación aplicará tooall los objetos almacenados en la cuenta de hello. Capa de almacenamiento de Hola de cambio de toocool activa no implicará cualquier cargo, mientras que cambiar de acceso esporádico toohot, se le cobrará un por costo de GB para leer todos los datos de hello en cuenta Hola.
6. **¿Con qué frecuencia se puede cambiar capa de almacenamiento de Hola de mi cuenta de almacenamiento de Blob?**
   
    Mientras no se aplican una limitación en con qué frecuencia se puede cambiar la capa de almacenamiento de Hola, ten en cuenta que cambiar la capa de almacenamiento de Hola de frío toohot supondrán un coste adicional importante. No se recomienda cambiar la capa de almacenamiento de hello con frecuencia.
7. **¿Se blobs hello en la capa de almacenamiento de acceso esporádico de hello comportarse de manera diferente que los de la capa de almacenamiento activas de Hola Hola?**
   
    Los blobs en la capa de almacenamiento activas de hello tienen Hola mismo latencia como blobs en las cuentas de almacenamiento general. Blobs en la capa de almacenamiento de acceso esporádico de hello con una latencia similar (en milisegundos) como blobs en cuentas de almacenamiento general.
   
    Blobs en la capa de almacenamiento de acceso esporádico de hello tendrá un nivel de servicio disponibilidad (SLA) ligeramente inferior a blobs de hello almacenados en la capa de almacenamiento activas de Hola. Para más información, consulte [Acuerdo de Nivel de Servicio para Almacenamiento](https://azure.microsoft.com/support/legal/sla/storage).
8. **¿Puedo almacenar blobs en páginas y discos de máquinas virtuales en las cuentas de Almacenamiento de blobs?**
   
    Las cuentas de Almacenamiento de blobs solo admiten blobs en bloques y en anexos, pero no blobs en páginas. Discos de máquina virtual de Azure están respaldados por blobs de página y así las cuentas de almacenamiento de blobs no pueden ser toostore usa discos de máquina virtual. Sin embargo, resulta posible toostore copias de seguridad de discos de máquina virtual de hello como blobs en bloques en una cuenta de almacenamiento de blobs.
9. **¿Se necesita toochange Mis cuentas de almacenamiento de blobs de toouse las aplicaciones existentes?**
   
    Las cuentas de almacenamiento de blobs tienen una coherencia del 100 % con la API con las cuentas de almacenamiento de uso general para blobs en bloques y en anexos. Siempre que la aplicación está utilizando los blobs en bloques o blobs en anexos y utilizas versión 2014-02-14 de Hola de hello [Storage Services REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) o mayor la aplicación debería funcionar. Si está utilizando una versión anterior del protocolo de hello, deberá tooupdate la nueva versión de aplicación toouse Hola así como toowork sin problemas con ambos tipos de cuentas de almacenamiento. En general, se recomienda siempre usando Hola versión más reciente, independientemente de qué tipo de cuenta de almacenamiento que use.
10. **¿Habrá un cambio en la experiencia del usuario?**
    
    Las cuentas de almacenamiento de blobs son cuentas de almacenamiento general tooa muy similar para el almacenamiento de bloque y blobs en anexos y admiten todas las características clave de Hola de almacenamiento de Azure, como gran durabilidad y disponibilidad, escalabilidad, rendimiento y seguridad. Distintas cuentas de almacenamiento de tooBlob específicos de características y restricciones hello y sus niveles de almacenamiento que se ha llamado anteriormente, todo lo que sigue siendo else Hola igual.

## <a name="next-steps"></a>Pasos siguientes
### <a name="evaluate-blob-storage-accounts"></a>Evaluación de cuentas de Almacenamiento de blobs
[Comprobación de la disponibilidad de las cuentas de Almacenamiento de blobs por región](https://azure.microsoft.com/regions/#services)

[Evaluación del uso de las cuentas de almacenamiento actuales mediante la habilitación de las métricas de Almacenamiento de Azure](storage-enable-and-view-metrics.md)

[Comprobación de los precios de almacenamiento de blobs por región](https://azure.microsoft.com/pricing/details/storage/)

[Detalles de precios de Transferencias de datos](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a>Empezar a utilizar cuentas de Almacenamiento de blobs
[Introducción al Almacenamiento de blobs de Azure mediante .NET](storage-dotnet-how-to-use-blobs.md)

[Mover datos tooand desde el almacenamiento de Azure](storage-moving-data.md)

[Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](storage-use-azcopy.md)

[Examen y exploración de cuentas de almacenamiento](http://storageexplorer.com/)

