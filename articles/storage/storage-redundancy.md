---
title: "Replicación de datos en Azure Storage | Microsoft Docs"
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
ms.openlocfilehash: b9354484ff5b81e2561d017d039bf2c07a21a423
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-storage-replication"></a>Replicación de almacenamiento de Azure

Los datos de su cuenta de almacenamiento de Microsoft Azure se replican siempre para garantizar la durabilidad y la alta disponibilidad. La replicación copia los datos, dentro del mismo centro de datos o a otro, en función de la opción de replicación que elija. La replicación protege los datos y conserva el tiempo de actividad de la aplicación en el caso de errores transitorios del hardware. Si los datos se replican en un segundo centro de datos, los protege frente a un error catastrófico en la ubicación principal.

La replicación garantiza que la cuenta de almacenamiento cumpla el [contrato de nivel de servicio (SLA) para Storage](https://azure.microsoft.com/support/legal/sla/storage/), incluso en caso de errores. Consulte en el SLA información acerca de las garantías de durabilidad y disponibilidad de Azure Storage.

Cuando cree una cuenta de almacenamiento, puede seleccionar una de las siguientes opciones de replicación:

* [Almacenamiento con redundancia local (LRS)](#locally-redundant-storage)
* [Almacenamiento con redundancia de zona (ZRS)](#zone-redundant-storage)
* [Almacenamiento con redundancia geográfica (GRS)](#geo-redundant-storage)
* [Almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS).](#read-access-geo-redundant-storage)

El almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS) es la opción predeterminada cuando crea una cuenta de almacenamiento.

La siguiente tabla proporciona una breve descripción de las diferencias entre LRS, ZRS, GRS y RA-GRS, mientras que secciones subsiguientes abordan con más detalle cada tipo de replicación.

| Estrategia de replicación | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Los datos se replican entre varios centros de datos. |No |Sí |Sí |Sí |
| Los datos se pueden leer desde la ubicación secundaria al igual que desde la ubicación principal. |No |No |No |Sí |
| Cantidad de copias de datos mantenidas en nodos independientes |3 |3 |6 |6 |

Consulte [Precios de Almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/) para más información sobre las diferentes opciones de redundancia.

> [!NOTE]
> Premium Storage solo admite almacenamiento con redundancia local (LRS). Para más información sobre Premium Storage, consulte [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](storage-premium-storage.md).
>

> [!NOTE]
> Azure File Storage solo admite cuentas de almacenamiento con redundancia local o de almacenamiento con redundancia geográfica. Para obtener información sobre Azure File Storage, consulte el artículo de [introducción a Azure File Storage](storage-files-introduction.md).
>

## <a name="locally-redundant-storage"></a>Almacenamiento con redundancia local
El almacenamiento con redundancia local (LRS) replica los datos tres veces dentro de una unidad de escalado de almacenamiento que se hospeda en un centro de datos de la región en la que se creó su cuenta de almacenamiento. Una solicitud de escritura se devuelve correctamente solo una vez que se ha escrito en las tres réplicas. Cada una de estas tres réplicas reside en dominios de error y dominios de actualización independientes dentro de una unidad de escalado de almacenamiento.

Una unidad de escalado de almacenamiento es una colección de estanterías de nodos de almacenamiento. Un dominio de error (FD) es un grupo de nodos que representan una unidad física de error y se pueden considerar como nodos pertenecientes a la misma estantería. Un dominio de actualización (UD) es un grupo de nodos que se actualizan en conjunto durante el proceso de actualización de un servicio (implementación). Las tres réplicas se distribuyen entre dominios UD y FD dentro de una unidad de escalado de almacenamiento para garantizar que los datos se encuentran disponibles incluso si un error de hardware afecta a una sola estantería y cuando los nodos se actualizan durante una implementación.

LRS es la opción de costo más bajo y ofrece menos durabilidad en comparación con otras opciones. En caso de un desastre en el nivel de centro de datos (incendio, inundación etc.), las tres réplicas podrían perderse o volverse irrecuperables. Para mitigar este riesgo, se recomienda almacenamiento con redundancia geográfica (GRS) para la mayoría de las aplicaciones.

El almacenamiento con redundancia local puede ser conveniente en algunos escenarios:

* Proporciona el ancho de banda máximo más elevado de las opciones de replicación de Azure Storage.
* Si su aplicación almacena datos que se pueden reconstruir fácilmente, puede optar por LRS.
* Algunas aplicaciones están restringidas a la replicación de datos solo dentro de un país debido a requisitos de gobernanza de datos. Podría ser una región emparejada en otro país. Para obtener más información, consulte [Regiones de Azure](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Almacenamiento con redundancia de zona
El almacenamiento con redundancia de zona (ZRS) replica los datos de manera asincrónica entre centros de datos dentro de una o dos regiones, además de almacenar tres réplicas de forma parecida a LRS, pero con una mayor durabilidad. Los datos almacenados en ZRS son duraderos incluso si el centro de datos principal no está disponible o se ha vuelto irrecuperable.
Los clientes que planeen usar ZRS deben tener en cuenta lo siguiente:

* ZRS solo está disponible para blobs en bloques en cuentas de almacenamiento de fin general, y solo se admite en versiones del servicio de almacenamiento del 14-02- 2014 y posteriores.
* Como la replicación asincrónica implica un retraso, ante la eventualidad de un desastre regional es posible que los cambios que todavía no se hayan replicado en la región secundaria se pierdan si no es posible recuperar los datos de la región primaria.
* Es posible que la réplica no esté disponible hasta que Microsoft inicie la conmutación por error al secundario.
* Las cuentas ZRS no se pueden convertir posteriormente a LRS o GRS. Igualmente, una cuenta LRS o GRS existente no se puede convertir a una cuenta ZRS.
* Las cuentas ZRS no tienen métricas ni funcionalidad de registro.

## <a name="geo-redundant-storage"></a>Almacenamiento con redundancia geográfica
El almacenamiento con redundancia geográfica (GRS) replica sus datos a una región secundaria que se encuentra a cientos de kilómetros de distancia de la región primaria. Si la cuenta de almacenamiento tiene habilitado GRS, sus datos se mantienen incluso ante un apagón regional completo o un desastre del cual la región principal no se puede recuperar.

En el caso de una cuenta de almacenamiento con GRS habilitado, una actualización primero se envía a la región principal, donde se replica tres veces. A continuación, la actualización se replica de manera asincrónica en la región secundaria, donde también se replica tres veces.

Con GRS, las regiones primarias y secundarias administran las réplicas entre dominios de error y de actualización diferentes dentro de una unidad de escalado de almacenamiento, como se describe con LRS.

Consideraciones:

* Como la replicación asincrónica implica un retraso, ante la eventualidad de un desastre regional es posible que los cambios que todavía no se hayan replicado en la región secundaria se pierdan si no es posible recuperar los datos de la región primaria.
* La réplica no está disponible a menos que Microsoft inicie la conmutación por error para la región secundaria. Si Microsoft inicia una conmutación por error en la región secundaria, tendrá acceso de lectura y escritura a esos datos una vez completada la conmutación por error. Para más información, consulte la [guía de recuperación ante desastres](storage-disaster-recovery-guidance.md). 
* Si una aplicación desea leer desde la región secundaria, el usuario debe habilitar RA-GRS.

Cuando crea una cuenta de almacenamiento, selecciona la región principal de la cuenta. La región secundaria se determina según la región principal y no es posible cambiarla. La siguiente tabla muestra los emparejamientos de la región principal y la secundaria.

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
> La región secundaria de Virginia Gob. EE. UU. es Texas Gob. EE. UU. Anteriormente, Virginia Gob. EE. UU. utilizaba Iowa Gob. EE. UU. como región secundaria. Las cuentas de almacenamiento que aún aprovechan Iowa Gob. EE. UU. como región secundaria se están migrando a Texas Gob. EE. UU. como región secundaria. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Almacenamiento con redundancia geográfica con acceso de lectura
El almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS) maximiza la disponibilidad para la cuenta de almacenamiento al proporcionar acceso de solo lectura a los datos de la ubicación secundaria, además de la replicación entre dos regiones que proporciona GRS.

Cuando habilita el acceso de solo lectura a los datos en la región secundaria, los datos quedan disponibles en un extremo secundario, además del extremo principal para la cuenta de almacenamiento. El punto de conexión secundario es similar al punto de conexión principal, pero anexa el sufijo `–secondary` al nombre de la cuenta. Por ejemplo, si el punto de conexión principal del servicio BLOB es `myaccount.blob.core.windows.net`, el punto de conexión secundario es `myaccount-secondary.blob.core.windows.net`. Las claves de acceso de la cuenta de almacenamiento son iguales para los extremos principal y secundario.

Consideraciones:

* La aplicación tiene que administrar el punto de conexión con el que interactúa al usar RA-GRS.
* Como la replicación asincrónica implica un retraso, ante la eventualidad de un desastre regional es posible que los cambios que todavía no se hayan replicado en la región secundaria se pierdan si no es posible recuperar los datos de la región primaria.
* Si Microsoft inicia la conmutación por error en la región secundaria, tendrá acceso de lectura y escritura a esos datos una vez completada la conmutación por error. Para más información, consulte la [guía de recuperación ante desastres](storage-disaster-recovery-guidance.md). 
* RA-GRS está pensado para fines de alta disponibilidad. Para instrucciones sobre escalabilidad, revise la [lista de comprobación de rendimiento](storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-the-geo-replication-type-of-my-storage-account"></a>1. ¿Cómo se puede cambiar el tipo de replicación geográfica de mi cuenta de almacenamiento?

   Puede cambiar el tipo de replicación geográfica de la cuenta de almacenamiento entre LRS, GRS y RA-GRS mediante [Azure Portal](https://portal.azure.com/), [Azure Powershell](storage-powershell-guide-full.md) o mediante programación con uno de nuestras muchas bibliotecas de cliente de almacenamiento. Tenga en cuenta que las cuentas ZRS no se pueden convertir a LRS ni GRS. Igualmente, una cuenta LRS o GRS existente no se puede convertir a una cuenta ZRS.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-the-replication-type-of-my-storage-account"></a>2. ¿Habrá tiempo improductivo si se cambia el tipo de replicación de mi cuenta de almacenamiento?

   No, no habrá ningún período de inactividad.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-the-replication-type-of-my-storage-account"></a>3. ¿Habrá algún costo adicional si se cambia el tipo de replicación de mi cuenta de almacenamiento?

   Sí. Si cambia la cuenta de almacenamiento de LRS a GRS (o RA-GRS), se incurre en un costo adicional por las salidas relativas a la copia de los datos existentes desde la ubicación primaria a la ubicación secundaria. Una vez copiados los datos iniciales no hay cargos adicionales por salidas por la replicación geográfica de los datos desde la ubicación primaria a la secundaria. Los detalles de los cargos por ancho de banda se pueden encontrar en la [Página de precios de Azure Storage](https://azure.microsoft.com/pricing/details/storage/blobs/). Si cambia de GRS a LRS no hay ningún costo adicional, pero los datos se eliminarán de la ubicación secundaria.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. ¿Cómo puede ayudarme RA-GRS?
   
   El almacenamiento GRS proporciona replicación de los datos desde una región primaria a una secundaria que se encuentra a cientos de kilómetros de distancia de la región primaria. En ese caso, los datos se mantienen incluso en caso de un apagón regional completo o un desastre del cual la región primaria no se puede recuperar. El almacenamiento RA-GRS incluye esto y agrega la funcionalidad de leer los datos desde la región secundaria. Para algunas ideas sobre cómo aprovechar esta funcionalidad, consulte [Diseño de aplicaciones de alta disponibilidad utilizando almacenamiento RA-GRS](storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-to-figure-out-how-long-it-takes-to-replicate-my-data-from-the-primary-to-the-secondary-region"></a>5. ¿Hay alguna forma para averiguar cuánto tiempo se tarda en replicar los datos desde la región primaria a la secundaria?
   
   Si utiliza un almacenamiento RA-GRS puede comprobar la hora de última sincronización de la cuenta de almacenamiento. La hora de última sincronización es un valor de fecha y hora GMT; todas las escrituras primarias anteriores a la hora de última sincronización se han escrito correctamente en la ubicación secundaria, lo que significa que están disponibles para leerse desde la ubicación secundaria. Las escrituras primarias posteriores a la hora de última sincronización pueden o no estar disponibles para lecturas todavía. Puede consultar este valor utilizando [Azure Portal](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md), o mediante programación con la API de REST o una de las bibliotecas de cliente de almacenamiento. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-to-the-secondary-region-if-there-is-an-outage-in-the-primary-region"></a>6. ¿Cómo puedo cambiar a la región secundaria si se produce una interrupción en la región primaria?
   
   Consulte el artículo [Qué hacer si se produce una interrupción de Azure Storage](storage-disaster-recovery-guidance.md) para más información.

<a id="rpo-rto"></a>
#### <a name="7-what-is-the-rpo-and-rto-with-grs"></a>7. ¿Qué es el RPO y el RTO en GRS?
   
   Objetivo de punto de recuperación (RPO): en GRS y RA-GRS, el servicio de almacenamiento realiza un replicación geográfica asincrónica de los datos desde la ubicación primaria a la secundaria. Si hay un desastre regional importante y debe realizarse una conmutación por error, se pueden perder los cambios diferenciales recientes que no se han replicado geográficamente. El número de minutos de pérdida potencial de datos se conoce como el RPO (lo que significa que el punto en el tiempo al que se pueden recuperar datos). Normalmente, tenemos un RPO inferior a 15 minutos, aunque actualmente no hay ningún SLA sobre cuánto tiempo toma la replicación geográfica.

   Objetivo de tiempo de recuperación (RTO): se trata de una medida de cuánto tiempo tarda en realizarse la conmutación por error y tener la cuenta de almacenamiento de nuevo en línea si es necesario realizar una conmutación por error. El tiempo para realizar la conmutación por error incluye lo siguiente:
    * El tiempo que lleva investigar y determinar si es posible recuperar los datos de la ubicación primaria o bien si es necesario realizar una conmutación por error.
    * Realizar la conmutación por error de la cuenta mediante el cambio de las entradas DNS hacia la ubicación secundaria.

   Nos tomamos muy en serio la responsabilidad de proteger sus datos, por lo que si existe alguna posibilidad de recuperar los datos, mantendremos a la espera la conmutación por error y nos centraremos en la recuperación de los datos de la ubicación primaria. En el futuro, tenemos previsto proporcionar una API para desencadenar una conmutación por error a nivel de cuenta, lo que permitiría controlar el RTO usted mismo, pero aún no está disponible.
   
## <a name="next-steps"></a>Pasos siguientes
* [Diseño de aplicaciones de alta disponibilidad mediante RA-GRS](storage-designing-ha-apps-with-ragrs.md)
* [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Acerca de las cuentas de almacenamiento de Azure](storage-create-storage-account.md)
* [Objetivos de escalabilidad y rendimiento de Azure Storage](storage-scalability-targets.md)
* [Opciones de redundancia de Microsoft Azure Storage y almacenamiento con redundancia geográfica con acceso de lectura ](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [Documento de SOSP: Azure Storage, un servicio de almacenamiento en nube altamente disponible con gran coherencia](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

