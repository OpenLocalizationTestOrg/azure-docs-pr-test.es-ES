---
title: "base de datos de recuperación ante desastres aaaSQL | Documentos de Microsoft"
description: "Obtenga información acerca de instrucciones y procedimientos recomendados para el uso de mantenimiento de base de datos de SQL Azure tooperform ante desastres recuperación aumenta toohelp su misión crítica para el negocio aplicaciones resistentes toofailures y las interrupciones."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a>Obtención de detalles de la recuperación ante desastres
Se recomienda validar periódicamente el flujo de trabajo de preparación de la aplicación para la recuperación. Comportamiento de la aplicación hello comprobación e implicaciones de interrupción de Hola o de pérdida de datos que conmutan por error implica es una buena práctica de ingeniería. También es un requisito de la mayoría de estándares del sector como parte de la certificación de continuidad del negocio.

Obtener los detalles de una recuperación ante desastres implica lo siguiente:

* Simular la interrupción del nivel de datos.
* Realizar la recuperación.
* Validar la integridad de la aplicación tras la recuperación.

Dependiendo de cómo se [diseñado la aplicación para la continuidad del negocio](sql-database-business-continuity.md), obtención de detalles hello tooexecute de flujo de trabajo de hello puede variar. A continuación se describen los procedimientos recomendados de hello llevar a cabo una exploración de recuperación ante desastres en el contexto de Hola de base de datos de SQL Azure.

## <a name="geo-restore"></a>Restauración geográfica
tooprevent Hola posible pérdida de datos al realizar una exploración de recuperación ante desastres, se recomienda realizar utilizando un entorno de prueba mediante la creación de una copia del entorno de producción de hello y el uso de obtención de detalles de hello flujo de trabajo de conmutación por error de la aplicación de tooverify Hola.

#### <a name="outage-simulation"></a>Simulación de interrupción
toosimulate Hola interrupción, puede eliminar o cambiar el nombre de base de datos de origen de Hola. Tenga en cuenta que esto puede producir un error de conectividad de la aplicación.

#### <a name="recovery"></a>Recuperación
* Realizar la restauración geográfica de Hola de base de datos de hello en un servidor diferente como se describe [aquí](sql-database-disaster-recovery.md).
* Cambio Hola aplicación configuración tooconnect toohello recuperada base de datos y seguir Hola [configurar una base de datos después de la recuperación](sql-database-disaster-recovery.md) Guía de recuperación de hello toocomplete.

#### <a name="validation"></a>Validación
* Obtención de detalles de hello completa mediante la comprobación de la recuperación de post Hola aplicaciones integridad (incluidas las cadenas de conexión, los inicios de sesión, pruebas de funcionalidad básica u otra parte de validaciones de procedimientos de firmas de aplicación estándar).

## <a name="geo-replication"></a>Replicación geográfica
Para una base de datos que está protegido mediante la obtención de detalles de replicación geográfica Hola ejercicio implica la base de datos secundaria toohello de conmutación por error planeada. Hello conmutación por error planeada garantiza que Hola principal y bases de datos secundarias de hello permanezcan sincronizados cuando cambian los roles de Hola. A diferencia de Hola de conmutación por error no planeada, esta operación no se produce pérdida de datos, por lo que la obtención de detalles de Hola se pueden realizar en el entorno de producción de hello.

#### <a name="outage-simulation"></a>Simulación de interrupción
interrupción de hello toosimulate, puede deshabilitar la aplicación web de Hola o base de datos de máquina virtual conectada toohello. Esto da como resultado errores de conectividad de Hola para los clientes web de Hola.

#### <a name="recovery"></a>Recuperación
* Asegúrese de seguro de configuración de la aplicación hello en hello DR región puntos toohello primero secundaria que se convierte en hello totalmente accesible nuevo elemento principal.
* Realizar [conmutación por error planeada](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) un nuevo elemento principal de base de datos secundaria de hello toomake
* Siga hello [configurar una base de datos después de la recuperación](sql-database-disaster-recovery.md) Guía de recuperación de hello toocomplete.

#### <a name="validation"></a>Validación
* Obtención de detalles de hello completa mediante la comprobación de la recuperación de post Hola aplicaciones integridad (incluidas las cadenas de conexión, los inicios de sesión, pruebas de funcionalidad básica u otra parte de validaciones de procedimientos de firmas de aplicación estándar).

## <a name="next-steps"></a>Pasos siguientes
* toolearn sobre escenarios de continuidad de negocio, vea [escenarios de continuidad](sql-database-business-continuity.md)
* toolearn acerca de las copias de seguridad de base de datos de SQL de Azure automatizada, vea [copias de seguridad automáticas de base de datos SQL](sql-database-automated-backups.md)
* toolearn sobre el uso de copias de seguridad automatizadas para la recuperación, vea [restaurar una base de datos de copias de seguridad de hello iniciadas por el servicio](sql-database-recovery-using-backups.md)
* toolearn acerca de las opciones de recuperación más rápidos, consulte [replicación geográfica activa](sql-database-geo-replication-overview.md)  
