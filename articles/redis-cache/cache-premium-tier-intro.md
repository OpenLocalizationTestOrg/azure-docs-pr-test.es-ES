---
title: "nivel de aaaIntroduction toohello Premium de caché de Redis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y administrar Redis persistencia, agrupación en clústeres de Redis y soporte técnico de red virtual para las instancias de caché en Redis de Azure de nivel Premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 5b58a03647fbf1198509ac6f1acd04f1b682ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-redis-cache-premium-tier"></a>Nivel de introducción toohello Premium de caché de Redis de Azure
Caché en Redis de Azure es una memoria caché distribuida, administrada que le ayuda a crear aplicaciones sensibles y altamente escalables, proporcionando datos de tooyour un acceso muy rápido. 

Hola de que nuevo nivel Premium es una capa listo Enterprise, que incluye todas las características de nivel Standard hello y obtener más información, por ejemplo, un mejor rendimiento, las cargas de trabajo más grandes, recuperación ante desastres, importación y exportación y una seguridad mejorada. Continuar toolearn leer más acerca de las características adicionales de Hola de nivel de caché Premium Hola.

## <a name="better-performance-compared-toostandard-or-basic-tier"></a>Mejorar el rendimiento en comparación con tooStandard o nivel básico
**Mejor rendimiento respecto a los niveles Standard o Basic.** Las memorias caché de nivel Premium de Hola se implementan en un hardware que cuenta con procesadores rápidos disponibles actualmente y le ofrece una mejor toohello de rendimiento en comparación con Basic o nivel estándar. Las cachés de nivel Premium tienen un mayor rendimiento y latencias más bajas. 

**Rendimiento de hello misma caché con tamaño es más alto en Premium como nivel tooStandard comparados.** Por ejemplo, el rendimiento de Hola de un 53 GB P4 caché (Premium) es 250K solicitudes por segundo como too150K comparados para C6 (estándar).

Consulte el artículo [P+F de Azure Redis Cache](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

## <a name="redis-data-persistence"></a>Persistencia de datos de Redis
nivel de Hello Premium permite toopersist datos de la caché de hello en una cuenta de almacenamiento de Azure. En una caché básico o estándar todos los datos de Hola se almacena en memoria. En caso de problemas con la infraestructura subyacente, podría producirse una pérdida de los datos. Se recomienda usar la característica de persistencia de datos de Redis hello en resistencia de hello Premium capa tooincrease contra la pérdida de datos. Caché en Redis de Azure ofrece las opciones RDB y AOF (próximamente) en la [persistencia de Redis](http://redis.io/topics/persistence). 

Para obtener instrucciones acerca de cómo configurar la persistencia, consulte [cómo persistencia tooconfigure para una caché de Redis de Azure Premium](cache-how-to-premium-persistence.md).

## <a name="redis-cluster"></a>Clúster Redis
Si desea toocreate cachés mayores de GB 53 o quiere tooshard datos en varios nodos de Redis, puede usar Redis que está disponible en el nivel Premium de Hola de agrupación en clústeres. Cada nodo consta de un par de cachés principal-réplica administrado por Azure para ofrecer una alta disponibilidad. 

**La agrupación en clústeres de Redis proporciona una escalabilidad y un rendimiento máximos.** El rendimiento aumenta linealmente a medida que aumente el número de Hola de particiones (nodos) en clúster de Hola. P. ej. Si crea un clúster P4 de 10 particiones, el rendimiento disponible hello es 250K * 10 = 2,5 millones de solicitudes por segundo. Vea hello [preguntas más frecuentes de caché de Redis Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) para obtener más detalles sobre el tamaño, el rendimiento y el ancho de banda con las cachés premium.

tooget a trabajar con la agrupación en clústeres, consulte [cómo tooconfigure agrupación en clústeres para una caché en Redis de Azure Premium](cache-how-to-premium-clustering.md).

## <a name="enhanced-security-and-isolation"></a>Aislamiento y seguridad mejorados
Son accesibles en memorias caché que creó en el nivel básico o estándar de Hola Hola internet pública. Acceso toohello de que caché está restringida en función de la clave de acceso de Hola. Con nivel de hello Premium que puede asegurarse de que solo los clientes dentro de una red determinada pueden tener acceso a Hola caché. Puede implementar la Caché en Redis en una [Red Virtual de Azure (VNet)](https://azure.microsoft.com/services/virtual-network/). Puede usar todas las características de Hola de red virtual, como subredes, las directivas de control de acceso y otra características toofurther restringen acceso tooRedis.

Para obtener más información, consulte [cómo son compatibles con tooconfigure red Virtual para una caché de Redis de Azure Premium](cache-how-to-premium-vnet.md).

## <a name="importexport"></a>Importación/Exportación
Importación y exportación es una operación de administración de datos de caché en Redis de Azure que permite tooimport datos en caché en Redis de Azure o exportar los datos de caché en Redis de Azure mediante la importación y exportación de una instantánea de base de datos de caché de Redis (RDB) de un blob en páginas tooa caché premium en un Azure Cuenta de almacenamiento. Esto le permite toomigrate entre distintas instancias de caché en Redis de Azure o rellenar Hola caché con los datos antes de su uso.

Importación puede ser toobring usado Redis compatible RDB archivos desde cualquier servidor de Redis que se ejecute en cualquier nube o el entorno, incluidos Redis que se ejecutan en Linux, Windows o cualquier proveedor de nube, como Amazon Web Services y otros. Importación de datos es un toocreate fácilmente una memoria caché con datos rellenadas previamente. Durante el proceso de importación de hello, caché en Redis de Azure carga archivos RDB Hola del almacenamiento de Azure en la memoria y, a continuación, inserta las claves de hello en memoria caché de Hola.

Exportación permite datos de hello tooexport almacenados en caché en Redis de Azure tooRedis compatible RDB archivos. Puede usar estos datos de toomove característica de una caché en Redis de Azure instancia tooanother o un servidor de Redis tooanother. Durante el proceso de exportación de hello, se crea un archivo temporal en hello VM que hosts Hola instancia del servidor de caché en Redis de Azure y archivo hello toohello cargado designado de la cuenta de almacenamiento. Cuando se completa la operación de exportación de hello con estado de éxito o error, se elimina el archivo temporal de Hola.

Para obtener más información, consulte [cómo tooimport datos en y exporte los datos de caché en Redis de Azure](cache-how-to-import-export-data.md).

## <a name="reboot"></a>Reboot
nivel de Hello premium le permite tooreboot uno o varios nodos de la memoria caché a petición. Esto le permite tootest la aplicación para proporcionar resistencia en caso de hello de un error. Puede reiniciar Hola después de nodos.

* Nodo maestro de la memoria caché
* Nodo subordinado de la memoria caché
* Nodos maestro y subordinado de la memoria caché
* Cuando se utiliza una caché premium con agrupación en clústeres, puede reiniciar Hola maestra, esclavo o ambos nodos para las particiones individuales en memoria caché de Hola

Para más información, consulte [Reboot](cache-administration.md#reboot) y [Preguntas más frecuentes sobre el reinicio](cache-administration.md#reboot-faq).

>[!NOTE]
>La funcionalidad de inicio ahora está habilitada para todos los niveles de Azure Redis Cache.
>
>

## <a name="schedule-updates"></a>Programar actualizaciones
característica de actualizaciones programadas de Hello permite toodesignate una ventana de mantenimiento de la memoria caché. Cuando se especifica la ventana de mantenimiento de hello, se realizan las actualizaciones de servidor Redis durante este período. toodesignate una ventana de mantenimiento, seleccione los días de hello deseado y especificar hora de inicio de ventana de mantenimiento de Hola para cada día. Tenga en cuenta que es hora de ventana de mantenimiento de hello en UTC. 

Para más información, consulte [Programación de actualizaciones](cache-administration.md#schedule-updates) y [Preguntas más frecuentes sobre la programación de actualizaciones](cache-administration.md#schedule-updates-faq).

> [!NOTE]
> Redis solo servidor se realizan las actualizaciones durante la ventana de mantenimiento programada Hola. ventana de mantenimiento de Hello no aplica la actualización de tooAzure o actualiza el sistema operativo de la VM de toohello.
> 
> 

## <a name="geo-replication"></a>Replicación geográfica

La **replicación geográfica** proporciona un mecanismo para vincular dos instancias de Azure Redis Cache de nivel Premium. Una memoria caché se designa como caché primaria vinculada de Hola y Hola otro como caché secundaria vinculado de Hola. caché secundaria vinculado de Hello pasa a ser de solo lectura, y datos de caché principal toohello escrito es replican toohello secundario vinculado caché. Esta funcionalidad puede ser tooreplicate usa una memoria caché en regiones de Azure.

Para obtener más información, consulte [cómo tooconfigure replicación geográfica para caché en Redis de Azure](cache-how-to-geo-replication.md).


## <a name="tooscale-toohello-premium-tier"></a>nivel de tooscale toohello premium
nivel de tooscale toohello premium, basta con elegir uno de los niveles premium Hola Hola **cambio de nivel de precios** hoja. También puede escalar el nivel de caché toohello premium con PowerShell y CLI. Para obtener instrucciones detalladas, consulte [cómo tooScale Redis de Azure almacenan en caché](cache-how-to-scale.md) y [cómo tooautomate una operación de escalado](cache-how-to-scale.md#how-to-automate-a-scaling-operation).

## <a name="next-steps"></a>Pasos siguientes
Crear una memoria caché y explore las nuevas características de nivel premium Hola.

* [La persistencia de tooconfigure para una caché en Redis de Azure Premium](cache-how-to-premium-persistence.md)
* [¿Cómo admiten tooconfigure red Virtual para una caché de Redis de Azure Premium](cache-how-to-premium-vnet.md)
* [¿Cómo tooconfigure agrupación en clústeres para una caché en Redis de Azure Premium](cache-how-to-premium-clustering.md)
* [¿Cómo tooimport datos en y exporte los datos de caché en Redis de Azure](cache-how-to-import-export-data.md)
* [Cómo tooadminister Redis de Azure almacenan en caché](cache-administration.md)

