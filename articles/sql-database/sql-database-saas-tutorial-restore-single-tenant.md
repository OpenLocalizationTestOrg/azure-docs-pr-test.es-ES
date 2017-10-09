---
title: "aaaRestore una base de datos de SQL Azure en una aplicación de varios inquilinos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorestore un único a los inquilinos SQL base de datos después de la eliminación accidental de datos"
keywords: tutorial de SQL Database
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: billgib;sstein
ms.openlocfilehash: 8507ecec2424c135f1859b88ebf2bb4e17538a58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a>Restaurar una base de datos SQL de inquilinos de SaaS Wingtip

aplicación de SaaS Wingtip Hello se basa en un modelo de base de datos por inquilino, donde cada inquilino tiene su propia base de datos. Una de las ventajas de Hola de este modelo es que es fácil toorestore datos de un solo inquilino de forma aislada sin afectar a otros inquilinos.

En este tutorial, conocerá dos patrones de recuperación de datos:

> [!div class="checklist"]

> * Restauración de una base de datos en una base de datos en paralelo (lado a lado)
> * Restauración de una base de datos en contexto


|||
|:--|:--|
| **Restaurar inquilino tooa anterior punto en el tiempo, en una base de datos paralelo** | Este patrón se puede usar por inquilino Hola para revisión, auditoría, cumplimiento de normas, base de datos etc. Hola original permanece en línea y sin cambios. |
| **Restauración de inquilino en contexto** | Este patrón es toorecover normalmente se usan un punto previo tooa de inquilino en el tiempo, después de un inquilino elimina accidentalmente los datos. base de datos original de Hola se deja sin conexión y reemplazado por base de datos restaurada Hola. |
|||

toocomplete se ha completado este tutorial, asegúrese de hello seguro después de requisitos previos:

* se implementa la aplicación de SaaS Wingtip Hello. vea toodeploy en menos de cinco minutos, [implementar y explorar la aplicación de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell está instalado. Para más información, consulte [Introducción a Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

## <a name="introduction-toohello-saas-tenant-restore-pattern"></a>Patrón de restauración de introducción toohello SaaS inquilino

Para el inquilino de hello restaurar patrón, hay dos modelos simples para restaurar datos de un inquilino individual. Debido a que las bases de datos de inquilino están aisladas entre sí, restaurar un inquilino no afecta los datos de los demás inquilinos.

En el primer patrón de hello, los datos se restauran en una base de datos. inquilino Hello, a continuación, se proporciona la base de datos de access toothis junto con sus datos de producción. Este patrón permite a un inquilino de datos de administración tooreview Hola restaurar y potencialmente utilizarla tooselectively sobrescribir los valores de datos actuales. Es una toohello SaaS aplicación diseñador toodetermine solo a la manera sofisticada hello deben ser opciones de recuperación de datos. Basta con que se va a tooreview capaz de datos en estado de Hola que estaba en un momento dado en el tiempo puede ser todo lo que es necesario en algunos escenarios. Si utiliza la base de datos de hello [georreplicación](sql-database-geo-replication-overview.md), se recomienda copiar datos de hello necesario de copia de hello restaurado en la base de datos original de Hola. Si reemplaza la base de datos original de Hola con base de datos de hello restaurar, es necesario tooreconfigure y resincronizar la replicación geográfica.

En patrón segundo hello, que adopta ese inquilino Hola ha sufrido una pérdida o daños de los datos, se restaura la base de datos de producción del inquilino de hello tooa punto anterior en el tiempo. De restauración de hello en lugar patrón inquilino Hola se desconecta durante un breve tiempo mientras la base de datos de Hola se restaure y se vuelve a poner en línea. Hello base de datos original se elimina, pero todavía se puede restaurar desde si necesita toogo atrás tooan incluso anterior punto en el tiempo. Una variación de este modelo podría cambiar el nombre de base de datos de hello en lugar de eliminarlo, aunque la base de datos de cambio de nombre hello no proporciona ninguna ventaja adicional en cuanto a seguridad de los datos.

## <a name="get-hello-wingtip-application-scripts"></a>Obtener scripts de la aplicación hello Wingtip

Hello Wingtip SaaS scripts y código fuente de aplicación están disponibles en hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositorio de github. [Pasos de secuencias de comandos de toodownload Hola Wingtip SaaS](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="simulate-a-tenant-accidentally-deleting-data"></a>Simulación de la eliminación accidental de los datos de un inquilino

toodemonstrate estos escenarios de recuperación, se necesita demasiado*accidentalmente* eliminar algunos datos en una de las bases de datos del inquilino de Hola. Aunque puede eliminar todos los registros, Hola configura paso siguiente Hola demostración toonot bloquearse mediante infracciones de integridad referencial! También agrega algunos datos de compra de vales puede usar más adelante en hello *tutoriales de análisis de SaaS Wingtip*.

Ejecutar secuencia de comandos del generador de vale de Hola y crear datos adicionales. Generador de vale Hola intencionadamente no adquirir vales para cada evento último de los inquilinos.

1. Abra... \\Módulos de aprendizaje\\utilidades\\*demostración TicketGenerator.ps1* en hello *PowerShell ISE*
1. Presione **F5** toorun Hola script y generan los clientes y datos de ventas de vales.


### <a name="open-hello-events-app-tooreview-hello-current-events"></a>Abra Hola aplicación tooreview Hola actuales eventos

1. Abra hello *concentrador de eventos* (http://events.wtp.&lt; usuario&gt;. trafficmanager.net) y haga clic en **Contoso un auditorio**:

   ![events hub](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. Desplácese por hello lista de eventos y tome nota del último evento de hello en lista de hello:

   ![último evento](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-hello-demo-scenario-tooaccidentally-delete-hello-last-event"></a>Ejecutar demo Hola Hola escenario tooaccidentally delete último evento

1. Abra... \\Módulos de aprendizaje\\continuidad del negocio y recuperación ante desastres\\RestoreTenant\\*demostración RestoreTenant.ps1* en hello *PowerShell ISE*, y Hola conjunto siguiente valor:
   * **$DemoScenario** = **1**, establezca demasiado**1** -eliminar eventos sin ventas de vale.
1. Presione **F5** toorun Hola script y eliminar el último evento de Hola. Verá una confirmación mensaje similares toohello a continuación:

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. se abre la página de eventos de Hello Contoso. Desplácese hacia abajo y compruebe el evento Hola ha desaparecido. Si hay eventos de hello en lista de hello, haga clic en actualizar y compruebe que ha desaparecido.

   ![último evento](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-hello-production-database"></a>Restaurar una base de datos de inquilinos en paralelo con la base de datos de producción de hello

Este ejercicio restaura el punto de tooa de base de datos de Contoso un auditorio hello en tiempo antes de que se eliminó el evento de Hola. Después de eliminan eventos de hello en los pasos anteriores de hello, que desee toorecover y ver datos de hello eliminado. No es necesario toorestore la base de datos de producción con registro de hello eliminado, pero necesita toorecover Hola antigua base de datos tooaccess Hola datos antiguos por otros motivos empresariales.

 Hola *restauración TenantInParallel.ps1* secuencia de comandos crea un inquilino paralelo base de datos y una entrada de catálogo paralelo ambas denominada *ContosoConcertHall\_antiguo*. Este patrón de restauración es más adecuado para recuperarse de una pérdida de datos sin importancia o para escenarios de recuperación de cumplimiento y auditoría. También es Hola enfoque recomendado cuando se usa [georreplicación](sql-database-geo-replication-overview.md).

1. Hola completa [simular un usuario que se eliminen accidentalmente los datos](#simulate-a-tenant-accidentally-deleting-data) sección.
1. Abra... \\Módulos de aprendizaje\\continuidad del negocio y recuperación ante desastres\\RestoreTenant\\_demostración RestoreTenant.ps1_ en hello *PowerShell ISE*.
1. Establecer **$DemoScenario** = **2**, establezca esta propiedad demasiado**2** demasiado*inquilino de restauración en paralelo*.
1. Presione **F5** secuencia de comandos de toorun Hola.

script de Hola restaura Hola inquilino database (base de datos paralelos de tooa) tooa punto en el tiempo antes de eliminar eventos de hello en la sección anterior de Hola. Crea una segunda base de datos, quita los metadatos de catálogo existentes que existe en esta base de datos y agrega el catálogo de toohello de base de datos de hello en hello *ContosoConcertHall\_antiguo* entrada.

script de demostración de Hello abre la página de eventos de hello en el explorador. Nota de la dirección URL de hello: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` que esto muestra de Hola Restaurar base de datos donde *_old* se agrega el nombre de toohello.

Eventos de hello desplazamiento incluidos en hello explorador tooconfirm que Hola eliminado en la sección anterior de hello el evento se ha restaurado.

Tenga en cuenta a ese inquilino Hola restaurar exponer como un inquilino adicional, con sus propio vales toobrowse de aplicación de eventos, es poco probable toobe cómo proporcionaría que un inquilino acceder a toorestored los datos, pero actúa tooeasily ilustra el patrón de restauración de Hola.

En realidad, es probable que solo debería retener esta base de datos restaurada durante un período definido. Puede eliminar entrada del inquilino de hello restaura una vez que termine por llamada hello *Remove-RestoredTenant.ps1* secuencia de comandos.

1. Establecer **$DemoScenario** demasiado**4** tooselect hello *quitar restaurar inquilino* escenario.
1. **Ejecute****con****F5**
1. Hola *ContosoConcertHall\_antiguo* entrada ahora se elimina del catálogo de Hola. Continúe y cerrar la página de eventos de Hola para este inquilino en el explorador.


## <a name="restore-a-tenant-in-place-replacing-hello-existing-tenant-database"></a>Restaurar a un inquilino en su lugar, reemplazando la base de datos de inquilinos existente Hola

Este ejercicio restaura el punto de hello Contoso un auditorio inquilino tooa de tiempo antes de que se eliminó el evento de Hola. Hola *TenantInPlace restauración* script restaura Hola actual inquilino tooa nueva base de datos que señala tooa anterior punto en el tiempo y las eliminaciones Hola base de datos original. Este patrón de restauración es más adecuado para recuperarse de daños graves en los datos, ya que puede haber pérdida de datos importantes que Hola inquilino tendría tooaccommodate.

1. Abra el archivo **Demo-RestoreTenant.ps1** en PowerShell ISE
1. Establecer **$DemoScenario** demasiado**5** tooselect hello *restaurar inquilino en el escenario de contexto*.
1. Ejecute con **F5**.

script de Hola restaura el punto de tooa de base de datos de inquilino de hello cinco minutos antes de que se eliminó el evento de Hola. Para ello, primero teniendo Hola Contoso un auditorio inquilino sin conexión por lo que no hay ningún otro actualiza los datos de toohello. A continuación, se crea mediante la restauración desde el punto de restauración de Hola y denominado una base de datos en paralelo con una marca de tiempo nombre de base de datos de hello tooensure no entra en conflicto con el nombre de base de datos de inquilino existente de Hola. A continuación, se elimina la base de datos de inquilino antigua hello y base de datos restaurada hello es el nombre de base de datos original de toohello cuyo nombre ha cambiado. Por último, Contoso un auditorio se pone tooallow en línea hello aplicación toohello Restaurar base de datos.

Restauró correctamente el punto de tooa de base de datos de hello en tiempo antes de que se eliminó el evento de Hola. Hola se abrirá la página de eventos, por lo que se confirme se ha restaurado el último evento de Hola.


## <a name="next-steps"></a>Pasos siguientes

En este tutorial aprendió lo siguiente:

> [!div class="checklist"]

> * Restauración de una base de datos en una base de datos en paralelo (lado a lado)
> * Restauración de una base de datos en contexto

[Administración de un esquema de base de datos de inquilino](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a>Recursos adicionales

* Adicionales [tutoriales que parten Hola aplicación Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Introducción a la continuidad empresarial con Base de datos SQL de Azure](sql-database-business-continuity.md)
* [Más información sobre las copias de seguridad de SQL Database](sql-database-automated-backups.md)
