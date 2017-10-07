---
title: "replicación de aaaData en el almacenamiento de Azure | Documentos de Microsoft"
description: "Los datos de su cuenta de Microsoft Azure Storage se replican para garantizar la durabilidad y la alta disponibilidad. Entre las opciones de replicación se incluyen el almacenamiento con redundancia local (LRS), el almacenamiento con redundancia de zona (ZRS), el almacenamiento con redundancia geográfica (GRS) y el almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS)."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 86bdb6d4-da59-4337-8375-2527b6bdf73f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 539bc54f57fe8cb661665d2788961a0783b5ae7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-replication"></a>Replicación de almacenamiento de Azure

datos de Hello en su cuenta de almacenamiento siempre es de Microsoft Azure replican tooensure durabilidad y alta disponibilidad. Copias de replicación de los datos, ya sea dentro de Hola mismo centro de datos o el segundo centro de datos tooa, según la opción de replicación que elija. La replicación protege los datos y conserva el tiempo de actividad de la aplicación en caso de hello de errores de hardware transitorios. Si los datos están replicados tooa segundo centro de datos, está protegido de un error grave en la ubicación principal Hola.

La replicación garantiza que la cuenta de almacenamiento cumple hello [contrato de nivel de servicio (SLA) para el almacenamiento](https://azure.microsoft.com/support/legal/sla/storage/) incluso de cara de Hola de errores. Vea Hola SLA para obtener información sobre el almacenamiento de Azure garantiza la durabilidad y disponibilidad.

Cuando se crea una cuenta de almacenamiento, puede seleccionar una de las siguientes opciones de replicación de hello:

* [Almacenamiento con redundancia local (LRS)](#locally-redundant-storage)
* [Almacenamiento con redundancia de zona (ZRS)](#zone-redundant-storage)
* [Almacenamiento con redundancia geográfica (GRS)](#geo-redundant-storage)
* [Almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS).](#read-access-geo-redundant-storage)

Almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS) es la opción predeterminada de hello cuando se crea una cuenta de almacenamiento.

Hello en la tabla siguiente proporciona una introducción rápida de diferencias de hello entre LRS, ZRS, GRS y RA-GRS, mientras que las secciones siguientes tratan cada tipo de replicación con más detalle.

| Estrategia de replicación | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Los datos se replican entre varios centros de datos. |No |Sí |Sí |Sí |
| Datos se pueden leer desde una ubicación secundaria, así como la ubicación principal Hola. |No |No |No |Sí |
| Cantidad de copias de datos mantenidas en nodos independientes |3 |3 |6 |6 |

Vea [precios de almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/) para obtener más información para opciones de redundancia diferentes de Hola.

> [!NOTE]
> Premium Storage solo admite almacenamiento con redundancia local (LRS). Para más información sobre Premium Storage, consulte [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](storage-premium-storage.md).
>

> [!NOTE]
> Azure File Storage solo admite cuentas de almacenamiento con redundancia local o de almacenamiento con redundancia geográfica. Para obtener información sobre Azure File Storage, consulte el artículo de [introducción a Azure File Storage](storage-files-introduction.md).
>

## <a name="locally-redundant-storage"></a>Almacenamiento con redundancia local
Almacenamiento con redundancia local (LRS) replica los datos tres veces dentro de una unidad de escala de almacenamiento, que se hospeda en un centro de datos en la región de hello en el que creó la cuenta de almacenamiento. Una solicitud de escritura se devuelve correctamente únicamente cuando ha sido escrito tooall tres réplicas. Cada una de estas tres réplicas reside en dominios de error y dominios de actualización independientes dentro de una unidad de escalado de almacenamiento.

Una unidad de escalado de almacenamiento es una colección de estanterías de nodos de almacenamiento. Un dominio de error (FD) es un grupo de nodos que representan una unidad física de error y se pueden considerar como nodos que pertenecen toohello mismo bastidor físico. Un dominio de actualización (UD) es un grupo de nodos que se actualizan en conjunto durante el proceso de Hola de una actualización de servicio (lanzamiento). Hola tres réplicas se reparten entre ud y FD dentro tooensure de unidad de escala de un almacenamiento que los datos están disponibles incluso si un error de hardware afecta a un único bastidor o cuando se actualizan los nodos durante una implementación.

LRS es la opción de costo más bajo de Hola y ofrece opciones de tooother de menor en comparación con la durabilidad. En caso de hello de un desastre de nivel de centro de datos (incendios, inundaciones etc.) las tres réplicas posible pierde o irrecuperable. toomitigate este riesgo, almacenamiento con redundancia geográfica (GRS) se recomienda para la mayoría de las aplicaciones.

El almacenamiento con redundancia local puede ser conveniente en algunos escenarios:

* Proporciona el ancho de banda máximo más elevado de las opciones de replicación de Azure Storage.
* Si su aplicación almacena datos que se pueden reconstruir fácilmente, puede optar por LRS.
* Algunas aplicaciones son datos tooreplicating restringido solo dentro de un país debido a los requisitos de gobierno toodata. Podría ser una región emparejada en otro país. Para obtener más información, consulte [Regiones de Azure](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Almacenamiento con redundancia de zona
Almacenamiento con redundancia de zona (ZRS) replica los datos de forma asincrónica en centros de datos dentro de uno o dos de las regiones en suma toostoring tres réplicas similar tooLRS, lo que proporciona mayor durabilidad que el LRS. Datos almacenados en ZRS están duraderos incluso si Hola centro de datos principal no está disponible o no recuperable.
Los clientes que planean toouse ZRS deben tenerse en cuenta que:

* ZRS solo está disponible para blobs en bloques en cuentas de almacenamiento de fin general, y solo se admite en versiones del servicio de almacenamiento del 14-02- 2014 y posteriores.
* Puesto que la replicación asincrónica implica un retraso, en caso de hello de un desastre local es posible que los cambios que aún no se han replicado toohello secundaria se perderá si no se puede recuperar datos de Hola de hello principal.
* réplica de Hello no estén disponible hasta que Microsoft inicia la conmutación por error toohello secundaria.
* No se puede convertir cuentas ZRS tooLRS o GRS posterior. De forma similar, una cuenta LRS o GRS existente no se puede convertir la cuenta ZRS tooa.
* Las cuentas ZRS no tienen métricas ni funcionalidad de registro.

## <a name="geo-redundant-storage"></a>Almacenamiento con redundancia geográfica
Almacenamiento con redundancia geográfica (GRS) replica la región secundaria de tooa de datos que se encuentra a cientos de millas fuera de la región principal de Hola. Si la cuenta de almacenamiento tiene GRS habilitado, los datos sean duraderos incluso en caso de hello de una interrupción regional completa o un desastre en qué Hola región principal no es recuperable.

Para una cuenta de almacenamiento con GRS habilitado, una actualización es la primera región principal de toohello confirmado, donde se replica tres veces. A continuación, la actualización de Hola se replica de forma asincrónica toohello región secundaria, donde también se replica tres veces.

Con GRS, ambas regiones principal y secundaria de hello administración réplicas a través de dominios de error independientes y dominios dentro de una unidad de escala de almacenamiento tal como se describe con LRS de actualización.

Consideraciones:

* Puesto que la replicación asincrónica implica un retraso, en caso de hello de un desastre regional es posible que los cambios que no se ha replicado región secundaria toohello se perderán si no se puede recuperar datos de hello de la región principal de Hola.
* Hola réplica no está disponible a menos que Microsoft inicia la región secundaria toohello de conmutación por error. Si Microsoft inició una región secundaria de toohello de conmutación por error, una vez completada la conmutación por error de hello tendrá datos toothat acceso de lectura y escritura. Para más información, consulte la [guía de recuperación ante desastres](storage-disaster-recovery-guidance.md). 
* Si una aplicación desea tooread de región secundaria de hello, usuario Hola debería habilitar RA-GRS.

Cuando se crea una cuenta de almacenamiento, seleccione región principal de hello para la cuenta de hello. región secundaria Hola se determina basándose en la región principal de hello y no se puede cambiar. Hello en la tabla siguiente muestra los emparejamientos de las regiones principal y secundaria Hola.

| Principal | Secundario |
| --- | --- |
| Centro-Norte de EE. UU |Centro-Sur de EE. UU |
| Centro-Sur de EE. UU |Centro-Norte de EE. UU |
| Este de EE. UU. |Oeste de EE. UU. |
| Oeste de EE. UU. |Este de EE. UU. |
| Este de EE. UU. - 2 |Central EE. UU.: |
| Central EE. UU.: |Este de EE. UU. - 2 |
| Europa del Norte |Europa occidental |
| Europa occidental |Europa del Norte |
| Sudeste de Asia |Asia oriental |
| Asia oriental |Sudeste de Asia |
| Este de China |Norte de China |
| Norte de China |Este de China |
| Este de Japón |Oeste de Japón |
| Oeste de Japón |Este de Japón |
| Sur de Brasil |Centro-Sur de EE. UU |
| Australia Oriental |Sudeste de Australia |
| Sudeste de Australia |Australia Oriental |
| Sur de India |India central |
| India central |Sur de India |
| India occidental |Sur de India |
| Gobierno de EE. UU. - Iowa |Gobierno de EE. UU. - Virginia |
| Gobierno de EE. UU. - Virginia |Gobierno de EE. UU.: Texas |
| Gobierno de EE. UU.: Texas |Gobierno de EE. UU.: Arizona |
| Gobierno de EE. UU.: Arizona |Gobierno de EE. UU.: Texas |
| Centro de Canadá |Este de Canadá |
| Este de Canadá |Centro de Canadá |
| Oeste de Reino Unido |Sur del Reino Unido |
| Sur del Reino Unido 2 |Oeste de Reino Unido |
| Centro de Alemania |Noreste de Alemania |
| Noreste de Alemania |Centro de Alemania |
| Oeste de EE. UU. 2 |Centro occidental de EE.UU. |
| Centro occidental de EE.UU. |Oeste de EE. UU. 2 |

Para obtener información actualizada sobre las regiones compatibles con Azure, consulte [Regiones de Azure](https://azure.microsoft.com/regions/).

>[!NOTE]  
> La región secundaria de Virginia Gob. EE. UU. es Texas Gob. EE. UU. Anteriormente, Virginia Gob. EE. UU. utilizaba Iowa Gob. EE. UU. como región secundaria. Las cuentas de almacenamiento aprovechando a nos Gov Iowa como una región secundaria se va a migran tooUS Texas Gov como una región de seconday. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Almacenamiento con redundancia geográfica con acceso de lectura
Almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS) maximiza la disponibilidad de la cuenta de almacenamiento, proporcionando datos de toohello de acceso de solo lectura en la ubicación secundaria de hello, además toohello replicación entre dos regiones proporcionada por GRS.

Cuando habilita los datos de tooyour de acceso de solo lectura en la región secundaria de hello, sus datos están disponibles en un punto de conexión secundaria, suma toohello principal punto de conexión para la cuenta de almacenamiento. extremo secundario de Hello es similar toohello de punto de conexión principal, pero incorpora un sufijo de hello `–secondary` toohello nombre de la cuenta. Por ejemplo, si el extremo principal Hola servicio Blob es `myaccount.blob.core.windows.net`, a continuación, el extremo secundario es `myaccount-secondary.blob.core.windows.net`. teclas de acceso de Hello para la cuenta de almacenamiento se Hola mismo para ambos Hola extremos principal y secundario.

Consideraciones:

* La aplicación tiene toomanage qué extremo está interactuando con cuando se usa RA-GRS.
* Puesto que la replicación asincrónica implica un retraso, en caso de hello de un desastre regional es posible que los cambios que no se ha replicado región secundaria toohello se perderán si no se puede recuperar datos de hello de la región principal de Hola.
* Si Microsoft inicia la región secundaria toohello de conmutación por error, tendrá acceso de lectura y escritura datos toothat una vez completada la conmutación por error de Hola. Para más información, consulte la [guía de recuperación ante desastres](storage-disaster-recovery-guidance.md). 
* RA-GRS está pensado para fines de alta disponibilidad. Para obtener instrucciones de escalabilidad, revise hello [lista de comprobación de rendimiento](storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-hello-geo-replication-type-of-my-storage-account"></a>1. ¿Cómo se puede cambiar el tipo de replicación geográfica de Hola de mi cuenta de almacenamiento?

   Puede cambiar el tipo de replicación geográfica de hello de la cuenta de almacenamiento entre LRS, GRS, y con RA-GRS Hola [portal de Azure](https://portal.azure.com/), [Azure Powershell](storage-powershell-guide-full.md) o mediante programación con uno de nuestros muchos cliente de almacenamiento Bibliotecas. Tenga en cuenta que las cuentas ZRS no se pueden convertir a LRS ni GRS. De forma similar, una cuenta LRS o GRS existente no se puede convertir la cuenta ZRS tooa.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-hello-replication-type-of-my-storage-account"></a>2. ¿Habrá tiempo improductivo al cambiar el tipo de replicación de Hola de mi cuenta de almacenamiento?

   No, no habrá ningún período de inactividad.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-hello-replication-type-of-my-storage-account"></a>3. ¿Habrá ningún coste adicional al cambiar el tipo de replicación de Hola de mi cuenta de almacenamiento?

   Sí. Si cambia de LRS tooGRS (o RA-GRS) para la cuenta de almacenamiento, se incurre en un cargo adicional para la salida de implicados en la copia de datos existentes desde la ubicación secundaria toohello de ubicación principal. Una vez que se copian los datos iniciales de hello es ningún otro cargo de salida adicionales para geográfica replicar datos de Hola de ubicación de hello toosecondary principal. detalles de Hola de cargos de ancho de banda se pueden encontrar en hello [página de precios de almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/blobs/). Si cambia de tooLRS GRS, no hay ningún costo adicional, pero los datos se eliminarán de la ubicación secundaria Hola.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. ¿Cómo puede ayudarme RA-GRS?
   
   Almacenamiento GRS proporciona la replicación de los datos de una región secundaria tooa principal que se encuentra a cientos de millas fuera de la región principal de Hola. En este caso, los datos sean duraderos incluso en caso de hello de una interrupción regional completa o un desastre en qué Hola región principal no es recuperable. Esto incluye el almacenamiento de RA-GRS y agrega datos de saludo de hello capacidad tooread desde la ubicación secundaria Hola. Para algunas ideas acerca de cómo tooleverage esta capacidad, consulte demasiado[diseñar aplicaciones altamente disponible utilizando almacenamiento RA-GRS](storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-toofigure-out-how-long-it-takes-tooreplicate-my-data-from-hello-primary-toohello-secondary-region"></a>5. ¿Hay una manera para mí toofigure espera el tiempo que tarda tooreplicate Mis datos de la región secundaria de hello toohello principal?
   
   Si usa el almacenamiento de RA-GRS, puede comprobar Hola hora de última sincronización de la cuenta de almacenamiento. Última hora de sincronización es un valor de fecha y hora GMT; todas las escrituras principales antes de hello hora de última sincronización se han escrito correctamente toohello ubicación secundaria, lo que significa que estén disponible toobe leer desde la ubicación secundaria Hola. Hora de última sincronización puede o no estén disponible para las lecturas todavía las escrituras principales después de hello. Puede consultar este valor mediante hello [portal de Azure](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md), o mediante programación con Hola API de REST o uno de hello bibliotecas de cliente de almacenamiento. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-toohello-secondary-region-if-there-is-an-outage-in-hello-primary-region"></a>6. ¿Cómo puedo cambiar región secundaria toohello si se produce una interrupción en la región principal de hello?
   
   Consulte el artículo de toohello [qué toodo si se produce una interrupción de almacenamiento de Azure](storage-disaster-recovery-guidance.md) para obtener más detalles.

<a id="rpo-rto"></a>
#### <a name="7-what-is-hello-rpo-and-rto-with-grs"></a>7. ¿Qué es Hola RPO y RTO con GRS?
   
   Objetivo de punto de recuperación (RPO): En GRS y RA-GRS, almacenamiento de hello servicio asincrónicamente geográfica replica los datos de Hola desde la ubicación secundaria de hello toohello principal. Si hay un desastre regional importante y una conmutación por error tiene toobe realiza, podrían perderse los cambios delta recientes que no se han replicado geográficamente. número de Hola de minutos de pérdida potencial de datos es que se hace referencia tooas Hola RPO (lo que significa que se puede recuperar el punto de hello en los datos de toowhich temporal). Normalmente, tenemos un RPO inferior a 15 minutos, aunque actualmente no hay ningún SLA sobre cuánto tiempo toma la replicación geográfica.

   Objetivo de tiempo de recuperación (RTO): Se trata de una medida de cuánto tiempo tarda conmutación por error de toodo hello y regresar cuenta de almacenamiento de hello en línea si tenemos toodo una conmutación por error. conmutación por error de Hello tiempo toodo Hola incluye siguiente de hello:
    * hora de Hello toma nos tooinvestigate y determinar si podemos recuperar datos de hello en la ubicación principal de Hola o si se necesita toodo una conmutación por error.
    * Cuenta de hello de conmutación por error cambiando Hola principal DNS entradas toopoint toohello ubicación secundaria.

   Se asumir la responsabilidad de Hola de mantener los datos muy en serio, así si hay cualquier posibilidad de recuperación de datos de hello, que se a esperar antes de realizar conmutación por error de Hola y centrarse en la recuperación de datos de hello en la ubicación principal Hola. Hola futura, tenemos previsto tooprovide una API tooallow tootrigger una conmutación por error en el nivel de cuenta, que, a continuación, le permitiría toocontrol Hola RTO usted mismo, pero aún no está disponible.
   
## <a name="next-steps"></a>Pasos siguientes
* [Diseño de aplicaciones de alta disponibilidad mediante RA-GRS](storage-designing-ha-apps-with-ragrs.md)
* [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Acerca de las cuentas de almacenamiento de Azure](storage-create-storage-account.md)
* [Objetivos de escalabilidad y rendimiento de Azure Storage](storage-scalability-targets.md)
* [Opciones de redundancia de Microsoft Azure Storage y almacenamiento con redundancia geográfica con acceso de lectura ](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [Documento de SOSP: Azure Storage, un servicio de almacenamiento en nube altamente disponible con gran coherencia](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

