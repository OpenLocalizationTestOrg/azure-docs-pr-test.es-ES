---
title: "aaaOnline de copia de seguridad y restauración con la base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooperform automática de copia de seguridad y restauración en una base de datos de la base de datos de Azure Cosmos."
keywords: "copias de seguridad y restauración, copia de seguridad en línea"
services: cosmos-db
documentationcenter: 
author: RahulPrasad16
manager: jhubbard
editor: monicar
ms.assetid: 98eade4a-7ef4-4667-b167-6603ecd80b79
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/11/2017
ms.author: raprasa
ms.openlocfilehash: a0b464c95681dfc7b5462b02bf04c2c43d6bc16f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-online-backup-and-restore-with-azure-cosmos-db"></a>Copias de seguridad y restauración automáticas en línea con Azure Cosmos DB
Azure Cosmos DB crea automáticamente copias de seguridad de todos los datos a intervalos regulares. se realizan copias de seguridad automáticas de Hello sin afectar al rendimiento de Hola o la disponibilidad de las operaciones de base de datos. Todas las copias de seguridad se almacenan por separado en otro servicio de almacenamiento y se replican globalmente para lograr resistencia frente a desastres regionales. copias de seguridad automáticas de Hello están pensadas para escenarios cuando se elimina el contenedor de la base de datos de Comos y versiones posteriores requiere la recuperación de datos o una solución de recuperación ante desastres.  

En este artículo se inicia con un resumen rápido de redundancia de datos de Hola y la disponibilidad de base de datos de Cosmos y, a continuación, se describe las copias de seguridad. 

## <a name="high-availability-with-cosmos-db---a-recap"></a>Resumen de la alta disponibilidad con Cosmos DB
COSMOS DB está diseñado toobe [distribuidos globalmente](distribute-data-globally.md) : permite la capacidad tooscale en varias regiones de Azure junto con la directiva controlada por la API de hospedaje múltiple transparentes y conmutación por error. Como una oferta de sistema de base de datos [disponibilidad del 99,99% SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db), todas las escrituras de hello en DB Cosmos son discos de toolocal duradera por un quórum de las réplicas en un centro de datos local antes de confirmar toohello cliente. Tenga en cuenta que Hola alta disponibilidad de base de datos de Cosmos se basa en el almacenamiento local y no depende de las tecnologías de almacenamiento externo. Además, si la cuenta de base de datos está asociada con más de una región de Azure, las escrituras se replicarán también en otras regiones. tooscale los datos de rendimiento y acceso en las latencias de bajas, puede tener muchas leen regiones asociadas a su cuenta de base de datos como sea necesario. En cada región de lectura, los datos de hello (Replicada) se guardan manera duradera a través de un conjunto de réplicas.  

Como se muestra en hello siguiente diagrama, un único contenedor de base de datos de Cosmos es [con particiones horizontales](partition-data.md). Una partición de"" se indica mediante un círculo en hello siguiente diagrama, y cada partición ofrezca alta disponibilidad a través de un conjunto de réplicas. Se trata de distribución local de hello en una única región de Azure (indicada por el eje X de hello). Además, cada partición (con su conjunto de réplicas correspondiente), a continuación, se distribuye globalmente en varias regiones asociadas a su cuenta de base de datos (por ejemplo, en esta ilustración Hola tres regiones: este de EE., oeste de Estados Unidos y de la India Central). Hola "conjunto de particiones" es distribuidos globalmente entidad compuestas por varias copias de los datos en cada región (se indica con eje de Hola Y). Puede asignar prioridad regiones toohello asociadas con su cuenta de base de datos y base de datos de Cosmos transparente conmutarán toohello siguiente región de conmutación por error en caso de desastre. Puede simular manualmente la disponibilidad de conmutación por error tootest Hola-to-end de la aplicación.  

Hello siguiente imagen ilustra alto grado de redundancia con DB Cosmos de Hola.

![Alto grado de redundancia con Cosmos DB](./media/online-backup-and-restore/redundancy.png)

![Alto grado de redundancia con Cosmos DB](./media/online-backup-and-restore/global-distribution.png)

## <a name="full-automatic-online-backups"></a>Copias de seguridad completas, automáticas y en línea
¡Vaya! Eliminé mi contenedor o base de datos. Con la base de datos de Cosmos, no solo los datos, pero las copias de seguridad de Hola de los datos se realizan también frente a desastres tooregional altamente resistente y redundantes. Actualmente, estas copias de seguridad automatizadas se crean aproximadamente cada cuatro horas y se almacenan las dos copias de seguridad más recientes en todo momento. Si accidentalmente los datos de Hola quita o daña, por favor, [póngase en contacto con soporte técnico de Azure](https://azure.microsoft.com/support/options/) 8 horas. 

se realizan copias de seguridad de Hello sin afectar al rendimiento de Hola o la disponibilidad de las operaciones de base de datos. COSMOS DB realiza copia de seguridad de hello en segundo plano de hello sin consumir sus aprovisionamiento RUs o afectar al rendimiento de Hola y sin afectar a la disponibilidad de saludo de la base de datos. 

A diferencia de los datos que se almacenan dentro de la base de datos de Cosmos, copias de seguridad automáticas de Hola se almacenan en el servicio de almacenamiento de blobs de Azure. carga de latencia baja y eficaz de hello tooguarantee, instantánea de saludo de la copia de seguridad es instancia de tooan cargado de almacenamiento de blobs de Azure en Hola misma región que la actual región de escritura hello de la cuenta de base de datos de base de datos de Cosmos. Para lograr resistencia frente a desastres regionales, cada instantánea de los datos de copia de seguridad en almacenamiento de blobs de Azure nuevo se replica a través de la región de tooanother de almacenamiento con redundancia geográfica (GRS). Hello siguiente diagrama muestra que todo contenedor de base de datos de Cosmos hello (con todas las tres particiones primarias zona horaria del Pacífico occidental, en este ejemplo) se copia en una cuenta de almacenamiento de blobs de Azure remota zona horaria del Pacífico occidental y, a continuación, GRS replica tooEast nosotros. 

Hello siguiente imagen ilustra copias de seguridad completas periódicas de todas las entidades de base de datos de Cosmos GRS en almacenamiento de Azure.

![Copias de seguridad completas y periódicas de todas las entidades de Cosmos DB en Azure Storage de GRS](./media/online-backup-and-restore/automatic-backup.png)

## <a name="backup-retention-period"></a>Período de retención de copia de seguridad
Como se describió anteriormente, base de datos de Azure Cosmos toma instantáneas de los datos cada cuatro horas y conserva la última dos instantáneas de Hola de cada partición durante 30 días. Siguiendo nuestras normas de cumplimiento, las instantáneas se purgan después de 90 días.

Si desea toomaintain sus propias instantáneas, puede utilizar la opción de tooJSON de exportación de hello en la base de datos de Azure Cosmos hello [herramienta de migración de datos](import-data.md#export-to-json-file) tooschedule copias de seguridad adicionales. 

## <a name="restoring-a-database-from-an-online-backup"></a>Restauración de una base de datos desde una copia de seguridad en línea
Si elimina accidentalmente la base de datos o una colección, puede [una incidencia de soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) o [llame al soporte técnico de Azure](https://azure.microsoft.com/support/options/) toorestore datos de saludo de copia de seguridad automática Hola último. Si necesita toorestore la base de datos debido a problemas de corrupción de datos, consulte [daños en los datos de control](#handling-data-corruption) según sea necesario tootake adicional pasos tooprevent Hola dañado datos de copias de seguridad de hello penetrar. Para obtener una instantánea concreta de la copia de seguridad toobe restaurar, Cosmos DB requiere que había disponibles datos de Hola durante Hola del ciclo de copia de seguridad de Hola para esa instantánea.

## <a name="handling-data-corruption"></a>Control de los datos dañados
Base de datos de Azure Cosmos conserva copias de dos últimas seguridad de Hola de cada partición en el sistema de Hola. Este modelo funciona muy bien cuando un contenedor (colección de documentos, gráfico y tabla) o una base de datos se elimina accidentalmente porque una de las últimas versiones de Hola se puede restaurar. Sin embargo, en hello caso cuando cuando los usuarios pueden introducir un problema de daños en los datos, base de datos de Azure Cosmos puede ser consciente de daños en los datos hello y es posible que Hola daños pueda haber entrado en las copias de seguridad de Hola. En cuanto se detectan daños, debe eliminar el contenedor Hola dañado (colección/gráfico y tabla) para que las copias de seguridad estén protegidos contra sobrescritura con datos dañados. Puesto que la última copia de seguridad de hello podría ser cuatro horas de antigüedad, puede emplear el usuario hello [Cambiar fuente](change-feed.md) toocapture y almacén Hola últimas cuatro horas que vale la pena de datos antes de eliminar el contenedor de Hola.

## <a name="next-steps"></a>Pasos siguientes

la base de datos en varios centros de datos, vea a tooreplicate [distribuir los datos globales con la base de datos de Cosmos](distribute-data-globally.md). 

toofile póngase en contacto con soporte técnico de Azure, [una incidencia de hello portal de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

