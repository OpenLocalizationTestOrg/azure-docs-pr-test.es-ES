---
title: las actualizaciones de aplicaciones de aaaRolling - base de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse replicación geográfica de base de datos de SQL Azure toosupport actualizaciones en línea de la aplicación en la nube."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 58f42859-1e37-463c-a3d8-a3ca2e867148
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/16/2016
ms.author: sashan
ms.openlocfilehash: 18c56300916d129bff141624cc5c416b500408d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-rolling-upgrades-of-cloud-applications-using-sql-database-active-geo-replication"></a>Administración de actualizaciones graduales de aplicaciones en la nube mediante la replicación geográfica activa de SQL Database
> [!NOTE]
> La [replicación geográfica activa](sql-database-geo-replication-overview.md) ahora está disponible para todas las bases de datos en todos los niveles.
> 

Obtenga información acerca de cómo toouse [georreplicación](sql-database-geo-replication-overview.md) en la base de datos SQL tooenable actualizaciones sucesivas de la aplicación en la nube. Como la actualización es una operación problemática, pues debe ser parte del diseño y planeamiento de continuidad. En este artículo que veremos dos métodos diferentes de organización hello proceso de actualización y describe las ventajas de Hola y ventajas y desventajas de cada opción. Hola de este artículo se utilizará una aplicación sencilla que consta de una base de datos solo de sitio web tooa conectado como su capa de datos. Nuestro objetivo es tooupgrade versión 1 de hello aplicación tooversion 2 sin ningún impacto significativo en la experiencia del usuario final Hola. 

Al evaluar las opciones de actualización de hello debe considerar Hola siguientes factores:

* El impacto sobre la disponibilidad de las aplicaciones durante las actualizaciones. ¿Durante cuánto tiempo función de la aplicación hello podría estar limitado o degradado.
* Capacidad tooroll atrás en el caso de un error de actualización.
* Vulnerabilidad de aplicación de hello si se produce un error grave no relacionado durante la actualización de Hola.
* El costo total en dólares.  Esto incluye la redundancia adicional y costes incrementales de componentes de hello temporal utilizados por el proceso de actualización de Hola. 

## <a name="upgrading-applications-that-rely-on-database-backups-for-disaster-recovery"></a>La actualización de las aplicaciones que dependen de las copias de seguridad de base de datos para recuperación ante desastres.
Si la aplicación se basa en las copias de seguridad automáticas de la base de datos y usa la restauración geográfica para la recuperación ante desastres, es normalmente implementado tooa sola región de Azure. En este caso el proceso de actualización de hello implica crear una implementación de todos los componentes de aplicación de copia de seguridad implicados en la actualización de Hola. interrupción de toominimize hello para el usuario final aprovecharán Azure Traffic Manager (WATM) con el perfil de conmutación por error de Hola.  Hola siguiente diagrama ilustra el proceso de actualización de toohello anteriores de entorno operativo de Hola. Hola extremo <i>1.azurewebsites.net contoso</i> representa una zona de producción de la aplicación hello que necesita toobe actualizado. tooenable Hola capacidad tooroll volver Hola actualización, necesita crear un espacio de fase con una copia de la aplicación hello totalmente sincronizada. Hello pasos siguientes son de la aplicación hello tooprepare necesarios para la actualización de hello:

1. Crear un espacio de la fase de actualización de Hola. toodo que crear una base de datos secundaria (1) e implementar un sitio web idéntico en hello misma región de Azure. Supervisar Hola secundaria toosee si Hola la propagación de proceso se ha completado.
2. Cree un perfil de conmutación por error en WATM con <i>contoso-1.azurewebsites.net</i> como punto de conexión en línea y <i>contoso 2.azurewebsites.net</i> como punto de conexión desconectado. 

> [!NOTE]
> Tenga en cuenta los pasos de preparación hello no afectará a la aplicación hello en la ranura de producción de hello y puede funcionar en modo de acceso completa.
>  

![Configuración de la replicación geográfica de la Base de datos SQL. Recuperación ante desastres en la nube.](media/sql-database-manage-application-rolling-upgrade/Option1-1.png)

Cuando haya realizado los pasos de preparación de hello aplicación hello está listo para la actualización real de Hola. Hola siguiente diagrama muestra Hola pasos implicados en el proceso de actualización de Hola. 

1. Establecer base de datos principal de Hola Hola ranura solo tooread en modo de producción (3). Esto garantizará que Hola permanecerá instancia de producción de la aplicación hello (V1) de solo lectura durante la actualización de hello evitando divergencia de datos de hello entre Hola V1 y V2 instancias de base de datos.  
2. Desconectar Hola base de datos secundaria utilizando el modo de finalización planeada hello (4). Creará una copia independiente totalmente sincronizada de la base de datos principal de Hola. Esta base de datos se actualizará.
3. Activar el modo de escritura tooread de base de datos principal de Hola y ejecute el script de actualización de hello en la ranura de fase de hello (5).     

![Configuración de replicación geográfica de SQL Database. Recuperación ante desastres en la nube.](media/sql-database-manage-application-rolling-upgrade/Option1-2.png)

Ahora está aplicación de hello tooswitch listo Hola a los usuarios finales toohello provisionalmente copia si Hola actualización se completó correctamente. Ranura de producción de hello de aplicación hello estará ahora.  Esto supone unos pocos pasos más tal como se muestra en hello siguiente diagrama.

1. Cambiar punto de conexión en línea hello en perfil WATM de hello demasiado<i>2.azurewebsites.net contoso</i>, qué versión de toohello V2 puntos del sitio web de hello (6). Ahora se convierte en zona de producción de hello con hello aplicación V2 y tráfico de usuario final de hello es tooit dirigido.  
2. Si ya no necesita los componentes de la aplicación hello V1 para poder sin ningún riesgo quitarlos (7).   

![Configuración de replicación geográfica de SQL Database. Recuperación ante desastres en la nube.](media/sql-database-manage-application-rolling-upgrade/Option1-3.png)

Si el proceso de actualización de hello es correcta, por ejemplo debido a error de tooan en el script de actualización de hello, ranura de la fase de hello debe considerarse en peligro. tooroll hacer una copia de hello toohello previas a la actualización estado de la aplicación simplemente Revertir aplicación hello en el acceso de toofull de ranura de producción de hello. pasos de Hola se muestran en el diagrama siguiente Hola.    

1. Establecer modo de escritura de tooread de copia de base de datos de hello (8). Esto restaurará Hola completa V1 funcionalmente en la ranura de producción de hello.
2. Realizar análisis de causa raíz de Hola y quitar componentes de hello en peligro en la ranura de fase de hello (9). 

En este momento aplicación hello es totalmente funcional y se pueden repetir los pasos de actualización de Hola.

> [!NOTE]
> Hello rollback no requiere cambios en el perfil WATM como ya puntos demasiado<i>1.azurewebsites.net contoso</i> como Hola extremo activo.
> 
> 

![Configuración de replicación geográfica de SQL Database. Recuperación ante desastres en la nube.](media/sql-database-manage-application-rolling-upgrade/Option1-4.png)

clave de Hello **ventaja** de esta opción es que puede actualizar una aplicación en una sola región con un conjunto de pasos sencillos. costo de dólar Hola de actualización de hello es relativamente baja. Hola principal **contrapartida** es que si se produce un error grave durante el estado previo a la actualización de Hola Hola actualización recuperación toohello implicará la reimplementación de la aplicación hello en una región distinta y Hola base de datos de copia de seguridad mediante la restauración geográfica. Este proceso dará como resultado un tiempo de inactividad considerable.   

## <a name="upgrading-applications-that-rely-on-database-geo-replication-for-disaster-recovery"></a>Actualización de aplicaciones que dependen de la replicación geográfica para la recuperación ante desastres
Si la aplicación utiliza la replicación geográfica para la continuidad del negocio, está implementada tooat menos dos regiones diferentes con una implementación activa en la región principal y una implementación en espera en la región de copia de seguridad. Además toohello factores se ha mencionado anteriormente, proceso de actualización de hello debe garantizar que:

* aplicación de Hello sigue estando protegida frente a errores catastróficos en todo momento durante el proceso de actualización de Hola
* componentes con redundancia geográfica de Hola de aplicación hello se actualizan en paralelo con componentes active Hola

tooachieve generar perfiles de estos objetivos aprovecharán con conmutación por error de hello Azure Traffic Manager (WATM) con una activa y tres puntos de conexión de copia de seguridad.  Hola siguiente diagrama ilustra el proceso de actualización de toohello anteriores de entorno operativo de Hola. Hola sitios web <i>contoso 1.azurewebsites.net</i> y <i>dr.azurewebsites.net contoso</i> representan una ranura de producción de la aplicación hello con redundancia geográfica completa. tooenable Hola capacidad tooroll volver Hola actualización, necesita crear un espacio de fase con una copia de la aplicación hello totalmente sincronizada. Dado que necesitan tooensure que aplicación hello puede recuperar rápidamente en caso de que se produce un error grave durante el proceso de actualización de hello, ranura de la fase de hello necesita que toobe también con redundancia geográfica. Hello pasos siguientes son de la aplicación hello tooprepare necesarios para la actualización de hello:

1. Crear un espacio de la fase de actualización de Hola. toodo que crea una base de datos secundaria (1) e implementa una copia idéntica del sitio web de Hola Hola misma región de Azure. Supervisar Hola secundaria toosee si Hola la propagación de proceso se ha completado.
2. Crear una base de datos secundaria con redundancia geográfica en la ranura de la fase de hello mediante la replicación geográfica región de copia de seguridad Hola base de datos secundaria toohello (Esto se denomina "encadenadas replicación geográfica"). Supervisar toosee secundaria de copia de seguridad de hello si Hola proceso la propagación está completado (3).
3. Crear una copia en espera del sitio web de hello en la región de copia de seguridad de Hola y vincúlela toohello con redundancia geográfica secundaria (4).  
4. Agregar extremos adicionales de hello <i>contoso 2.azurewebsites.net</i> y <i>3.azurewebsites.net contoso</i> perfil de conmutación por error de toohello en WATM como extremos sin conexión (5). 

> [!NOTE]
> Tenga en cuenta los pasos de preparación hello no afectará a la aplicación hello en la ranura de producción de hello y puede funcionar en modo de acceso completa.
> 
> 

![Configuración de replicación geográfica de SQL Database. Recuperación ante desastres en la nube.](media/sql-database-manage-application-rolling-upgrade/Option2-1.png)

Una vez completados los pasos de preparación de hello, ranura de la fase de hello está listo para actualización de Hola. Hola siguiente diagrama ilustra los pasos de actualización de Hola.

1. Establecer base de datos principal de Hola Hola ranura solo tooread en modo de producción (6). Esto garantizará que Hola permanecerá instancia de producción de la aplicación hello (V1) de solo lectura durante la actualización de hello evitando divergencia de datos de hello entre Hola V1 y V2 instancias de base de datos.  
2. Desconectar la base de datos secundaria de Hola Hola misma región mediante Hola modo la terminación planificada (7). Creará una copia independiente totalmente sincronizada de base de datos principal hello, que se convertirá automáticamente en un elemento principal después de la terminación de Hola. Esta base de datos se actualizará.
3. Activar la base de datos principal de Hola Hola fase ranura tooread-en modo de escritura y ejecutar el script de actualización de hello (8).    

![Configuración de replicación geográfica de SQL Database. Recuperación ante desastres en la nube.](media/sql-database-manage-application-rolling-upgrade/Option2-2.png)

Si Hola actualización se completó correctamente ahora está versión de toohello V2 de tooswitch listo Hola a los usuarios finales de la aplicación hello. Hola siguiente diagrama ilustra los pasos para saludo.

1. Cambiar punto de conexión activo de hello en perfil WATM de hello demasiado<i>2.azurewebsites.net contoso</i>, que ahora apunta toohello V2 versión del sitio web de hello (9). Ahora se convierte en una ranura de producción con hello aplicación V2 y tráfico de usuario final es tooit dirigido. 
2. Si ya no necesita la aplicación de hello V1 por lo que puede quitar (10 y 11).  

![Configuración de replicación geográfica de SQL Database. Recuperación ante desastres en la nube.](media/sql-database-manage-application-rolling-upgrade/Option2-3.png)

Si el proceso de actualización de hello es correcta, por ejemplo debido a error de tooan en el script de actualización de hello, ranura de la fase de hello debe considerarse en peligro. tooroll hacer una copia de hello toohello previas a la actualización estado de la aplicación simplemente Revertir aplicación de hello toousing en la ranura de producción de hello con acceso completo. pasos de Hola se muestran en el diagrama siguiente Hola.    

1. Conjunto de copia de base de datos principal de hello en modo de tooread y escritura de ranura de producción de hello (12). Esto restaurará Hola completa V1 funcionalmente en la ranura de producción de hello.
2. Realizar análisis de causa raíz de Hola y quitar componentes de hello en peligro en la ranura de fase de hello (13 y 14). 

En este momento aplicación hello es totalmente funcional y se pueden repetir los pasos de actualización de Hola.

> [!NOTE]
> Hello rollback no requiere cambios en el perfil WATM como ya puntos demasiado <i>1.azurewebsites.net contoso</i> como Hola extremo activo.
> 
> 

![Configuración de replicación geográfica de SQL Database. Recuperación ante desastres en la nube.](media/sql-database-manage-application-rolling-upgrade/Option2-4.png)

clave de Hello **ventaja** de esta opción es que puede actualizar aplicación hello y su copia con redundancia geográfica en paralelo sin poner en peligro la continuidad empresarial durante la actualización de Hola. Hola principal **contrapartida** es que requiere doble redundancia de los componentes de aplicaciones y, por tanto, implica mayor costo de dólar. También implica un flujo de trabajo más complicado. 

## <a name="summary"></a>Resumen
métodos de actualización de Hello dos descritos en el artículo Hola difieren en dólares de hello y complejidad de costo, pero se centran en minimizar el tiempo de hello cuando el usuario de final de hello es limitadas operaciones sólo tooread. Duración de Hola de script de actualización de hello directamente define ese tiempo. No depende de tamaño de base de datos de hello, Hola de nivel de servicio seleccione, configuración de sitios web de Hola y otros factores que no se puede controlar fácilmente. Esto es porque todos los pasos de preparación de Hola se desacoplan de pasos de actualización de Hola y pueden realizarse sin afectar a la aplicación de producción de hello. eficacia de Hola de script de actualización de hello es factor clave Hola que determina la experiencia del usuario final de Hola durante las actualizaciones. Por lo que se puede mejorar de mejor manera de hello es centrar los esfuerzos en hacer la secuencia de comandos de actualización de hello tan eficaz como sea posible.  

## <a name="next-steps"></a>Pasos siguientes
* Para obtener una descripción general y los escenarios de la continuidad empresarial, consulte [Información general sobre la continuidad empresarial](sql-database-business-continuity.md).
* toolearn acerca de las copias de seguridad automatizada de base de datos SQL Azure, consulte [copias de seguridad automáticas de base de datos SQL](sql-database-automated-backups.md).
* toolearn sobre el uso de copias de seguridad automatizadas para la recuperación, consulte [restaurar una base de datos de copias de seguridad automatizadas](sql-database-recovery-using-backups.md).
* toolearn acerca de las opciones de recuperación más rápidos, consulte [replicación geográfica activa](sql-database-geo-replication-overview.md).


