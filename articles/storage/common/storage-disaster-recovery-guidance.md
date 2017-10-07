---
title: "aaaWhat toodo en caso de hello de una interrupción de almacenamiento de Azure | Documentos de Microsoft"
description: "¿Qué toodo en caso de hello de una interrupción de almacenamiento de Azure"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: 93e1e831c35b96b8bf190fa2b56ab89350bbac13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-if-an-azure-storage-outage-occurs"></a>¿Qué toodo si se produce una interrupción de almacenamiento de Azure
En Microsoft, trabajamos duro toomake seguro de que nuestros servicios están siempre disponibles. A veces, debido a factores externos que escapan de nuestro control, se producen interrupciones de servicio no planeadas en una o varias regiones. toohelp controlar estos rara vez, proporcionamos Hola después de orientación de alto nivel para servicios de almacenamiento de Azure.

## <a name="how-tooprepare"></a>Cómo tooprepare
Es fundamental para cada cliente tooprepare su propio plan de recuperación ante desastres. Hola toorecover de esfuerzo de una interrupción de almacenamiento suele implica personal de operaciones y procedimientos automatizados en orden tooreactivate las aplicaciones en un estado de funcionamiento. Consulte toohello documentación de Azure a continuación toobuild su propio plan de recuperación ante desastres:

* [Recuperación ante desastres y alta disponibilidad para aplicaciones de Azure](/azure/architecture/resiliency/disaster-recovery-high-availability-azure-applications.md)
* [Guía técnica sobre resistencia en Azure](/azure/architecture/resiliency.md)
* [Servicio Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)
* [Replicación de almacenamiento de Azure](storage-redundancy.md)
* [Azure Backup](https://azure.microsoft.com/services/backup/)

## <a name="how-toodetect"></a>Cómo toodetect
Hola recomendado Hola de manera toodetermine estado del servicio de Azure es toosubscribe toohello [panel de estado del servicio de Azure](https://azure.microsoft.com/status/).

## <a name="what-toodo-if-a-storage-outage-occurs"></a>¿Qué toodo si se produce una interrupción de almacenamiento
Si uno o más servicios de almacenamiento no están disponibles temporalmente en una o varias regiones, hay dos opciones para tooconsider. Si desea que los datos de tooyour acceder de forma inmediata, considere la posibilidad de opción 2.

### <a name="option-1-wait-for-recovery"></a>Opción 1: esperar a que se recupere el servicio
En este caso, no se requieren acciones por su parte. Estamos trabajando diligentemente disponibilidad de los servicios de Azure toorestore Hola. Puede supervisar el estado del servicio hello en hello [panel de estado del servicio de Azure](https://azure.microsoft.com/status/).

### <a name="option-2-copy-data-from-secondary"></a>Opción 2: copiar los datos de la región secundaria
Si ha elegido [almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (recomendado) para las cuentas de almacenamiento, tendrá acceso de lectura tooyour datos de la región secundaria Hola. Puede usar herramientas como [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), hello y [biblioteca de movimiento de datos de Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/) toocopy datos de la región secundaria de hello en otra cuenta de almacenamiento en una región unimpacted y a continuación, elija el sistema de almacenamiento de toothat de las aplicaciones de la cuenta para leen y escribir la disponibilidad.

## <a name="what-tooexpect-if-a-storage-failover-occurs"></a>¿Qué tooexpect si se produce una conmutación por error de almacenamiento
Si eligió el [almacenamiento con redundancia geográfica (GRS)](storage-redundancy.md#geo-redundant-storage) o el [almacenamiento geográficamente redundante con acceso de lectura (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (recomendado), Almacenamiento de Azure conservará los datos en dos regiones (la principal y la secundaria). En las dos regiones, Almacenamiento de Azure mantendrá constantemente réplicas de los datos.

Cuando un desastre regional afecta a la región principal, se probará primero toorestore servicio de hello en dicha región. Depende de la naturaleza de Hola de desastre de Hola y sus impactos, en algunas ocasiones excepcionales nos será región principal de toorestore capaz de Hola. En ese momento, realizaremos una conmutación por error geográfica. la replicación de datos entre regiones Hello es un proceso asincrónico que puede implicar un retraso, por lo que es posible que los cambios que aún no se han replicado región secundaria toohello podrían perderse. Puede consultar hello ["Hora de última sincronización" de la cuenta de almacenamiento](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/) tooget detalles de estado de replicación de Hola.

Un par de cuestiones con respecto a la experiencia de conmutación por error geográfica de almacenamiento de hello:

* Solo se desencadenará conmutación geográfica de almacenamiento que el equipo de almacenamiento de Azure hello: no es necesaria ninguna acción del usuario.
* El servicio de almacenamiento existente permanecerán extremos para blobs, tablas, colas y archivos Hola igual después de la conmutación por error de hello; Hola entrada DNS será necesario tooswitch toobe actualizado de la región secundaria de hello región principal toohello.
* Antes y durante la conmutación por error Hola geográfica, no tendrá acceso de escritura tooyour cuenta de almacenamiento debido toohello impacto de desastre Hola pero todavía puede leerse de hello secundaria si se ha configurado su cuenta de almacenamiento como RA-GRS.
* Cuando Hola geográfica conmutación por error se ha completado y Hola propaga los cambios de DNS, se reanudará la cuenta de almacenamiento de tooyour de acceso de lectura y escritura; Esto señala toobe toowhat utiliza el extremo secundario. 
* Tenga en cuenta que tendrá acceso de escritura si tiene GRS o RA-GRS configuran para la cuenta de almacenamiento de Hola. 
* Puede consultar ["Tiempo de conmutación por error último de replicación geográfica" de la cuenta de almacenamiento](https://msdn.microsoft.com/library/azure/ee460802.aspx) tooget más detalles.
* Después de la conmutación por error de hello, su cuenta de almacenamiento totalmente funcionará, pero en un estado "Degradado", tal y como se hospeda realmente en una región independiente con no es posible la replicación geográfica. toomitigate este riesgo, se restaurará la región principal original de hello y, a continuación, realice una conmutación geográfica toorestore Hola original estado. Si la región principal original de hello es irrecuperable, se asignará otra región secundaria.
  Para obtener más detalles sobre la infraestructura de Hola de replicación geográfica de almacenamiento de Azure, consulte toohello artículo en el blog del equipo de almacenamiento de hello sobre [opciones de redundancia y RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

## <a name="best-practices-for-protecting-your-data"></a>Prácticas recomendadas para proteger los datos
No hay algunos tooback de enfoques recomendados de seguridad de los datos de almacenamiento de forma regular.

* Discos de máquina virtual: Hola de uso [servicio de copia de seguridad de Azure](https://azure.microsoft.com/services/backup/) tooback los discos de máquina virtual de hello utilizados por máquinas virtuales de Azure.
* Los blobs en bloques: crear un [instantánea](https://msdn.microsoft.com/library/azure/hh488361.aspx) de cada bloque blob o copiar cuenta de almacenamiento de hello blobs tooanother en otra región mediante [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), o hello [ Biblioteca de movimiento de datos de Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/).
* Usar tablas – [AzCopy](storage-use-azcopy.md) datos de la tabla tooexport hello en otra cuenta de almacenamiento en otra región.
* Usar archivos- [AzCopy](storage-use-azcopy.md) o [Azure PowerShell](storage-powershell-guide-full.md) toocopy cuenta el almacenamiento de archivos tooanother en otra región.

Para obtener información sobre cómo crear aplicaciones que aprovechan la característica de hello RA-GRS, consulte la [diseñar aplicaciones altamente disponible utilizando almacenamiento RA-GRS](../storage-designing-ha-apps-with-ragrs.md)

