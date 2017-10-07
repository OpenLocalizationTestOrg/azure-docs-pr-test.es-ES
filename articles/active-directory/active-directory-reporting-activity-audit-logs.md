---
title: los informes de actividad aaaAudit de portal de Azure Active Directory Hola | Documentos de Microsoft
description: "Informes de actividad en el portal de Azure Active Directory de Hola de auditoría de toohello de introducción"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a>Informes de actividad en el portal de Azure Active Directory Hola de auditoría 

Con los informes en Azure Active Directory (Azure AD), puede obtener información de hello necesita toodetermine cómo está haciendo su entorno.

arquitectura de los informes en Azure AD de Hello consta de Hola de los componentes siguientes:

- **Actividad** 
    - **Las actividades de inicio de sesión** : información sobre el uso de Hola de las aplicaciones administradas y las actividades de inicio de sesión de usuario
    - **Registros de auditoría**: información de la actividad del sistema sobre los usuarios y la administración de grupos, sus aplicaciones administradas y actividades de directorio.
- **Seguridad** 
    - **Inicios de sesión arriesgados** -un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que es posible que se han realizado por alguien que no es propietario legítimo de Hola de una cuenta de usuario. Para más información, consulte Inicios de no seguros.
    - **Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro. Para más información, consulte la sección Usuarios marcados en riesgo.

Este tema ofrece una visión general de las actividades de auditoría de Hola.
 
## <a name="who-can-access-hello-data"></a>¿Quién puede tener acceso a datos de hello?
* Usuarios de rol de administrador de seguridad o seguridad lector Hola
* Administradores globales
* Los usuarios individuales (no administradores) pueden ver sus propias actividades


## <a name="audit-logs"></a>Registros de auditoría

registros de auditoría de Hello en Azure Active Directory proporcionan registros de las actividades del sistema para el cumplimiento.  
Es el primer tooall de punto de entrada datos de auditoría **registros de auditoría** en hello **actividad** sección de **Azure Active Directory**.

![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/61.png "Registros de auditoría")

Un registro de auditoría tiene una vista de lista predeterminada que muestra:

- Hola fecha y hora de aparición de Hola
- Hola iniciador / actor (*que*) de una actividad 
- Hola actividad (*qué*) 
- destino de Hola

![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/18.png "Registros de auditoría")

Puede personalizar la vista de lista Hola haciendo clic en **columnas** en la barra de herramientas de Hola.

![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/19.png "Registros de auditoría")

Esto permite los campos adicionales de toodisplay o quitar los campos que ya se muestran.

![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/21.png "Registros de auditoría")


Si hace clic en un elemento en la vista de lista de hello, obtener todos los detalles disponibles sobre él.

![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/22.png "Registros de auditoría")


## <a name="filtering-audit-logs"></a>Filtrado de registros de auditoría

toonarrow hacia abajo Hola informó de un nivel de tooa de datos que funciona para usted, puede filtrar datos de auditoría de hello mediante Hola siguientes campos:

- Intervalo de fechas
- Iniciado por (actor)
- Categoría
- Tipo de recurso de actividad
- Actividad

![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/23.png "Registros de auditoría")


Hola **intervalo de fechas** filtro permite tooyou toodefine un período de tiempo para hello devolvió datos.  
Los valores posibles son:

- 1 mes
- 7 días
- 24 horas
- Personalizado

Cuando se selecciona un intervalo de tiempo personalizado, puede configurar una hora de inicio y una hora de finalización.

Hola **iniciadas por** filtro permite toodefine nombre de un actor o su nombre principal universal (UPN).

Hola **categoría** filtro le permite tooselect de hello siguiente filtro:

- Todo
- Core category (Categoría principal)
- Core Directory (Directorio principal)
- Self-service Password Management (Administración de contraseñas de autorservicio)
- Self-service group management (Administración de grupos de autoservicio)
- Account provisioning- Automated password rollover (Aprovisionamiento de cuentas: sustitución automática de contraseñas)
- Invited users (Usuarios invitados)
- MIM service (Servicio MIM)
- Identity Protection
- B2C

Hola **tipo de recurso de la actividad** filtro le permite tooselect uno de los siguientes Hola filtros:

- Todo 
- Grupo
- Directorio
- Usuario
- Application
- Directiva
- Dispositivo
- Otros

Cuando se selecciona **grupo** como **tipo de recurso de la actividad**, obtendrá una categoría de filtro adicional que le permite tooalso proporcionan un **origen**:

- Azure AD
- O365


Hola **actividad** filtro se basa en la categoría de Hola y selección de tipo de recurso de actividad que realice. Puede seleccionar una actividad específica que desee toosee o elegir todos. 

Puede obtener lista de Hola de todas las actividades de auditoría mediante Hola API Graph https://graph.windows.net/$ tenantdomain/actividades/auditActivityTypes? api-version = beta, donde $tenantdomain = el nombre de dominio o consulte el artículo toohello [informe de auditoría eventos](active-directory-reporting-audit-events.md).


## <a name="audit-logs-shortcuts"></a>Métodos abreviados de los registros de auditoría

Además demasiado**Azure Active Directory**, hello portal de Azure proporciona dos puntos de entrada adicionales tooaudit datos:

- Usuarios y grupos
- Aplicaciones empresariales

### <a name="users-and-groups-audit-logs"></a>Registros de auditoría de los usuarios y grupos

Con informes de auditoría basadas en el grupo y usuario, puede obtener respuestas tooquestions como:

- ¿Qué tipos de actualizaciones han sido usuarios Hola aplicado?

- ¿Cuántos usuarios han cambiado?

- ¿Cuántas contraseñas han cambiado?

- ¿Qué ha hecho un administrador en un directorio?

- ¿Cuáles son los grupos de Hola que se han agregado?

- ¿Hay grupos con cambios de pertenencia?

- ¿Se cambiaron los propietarios de Hola de grupo?

- ¿Qué licencias se han asignado un usuario o grupo de tooa?

Si su intención es tooreview datos toousers relacionados y grupos de la auditoría, puede encontrar una vista filtrada en **registros de auditoría** en hello **actividad** sección de hello **usuarios y grupos**. Este punto de entrada tiene **Usuarios y grupos** como **Tipo de recurso de actividad** preseleccionado.

![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/93.png "Registros de auditoría")

### <a name="enterprise-applications-audit-logs"></a>Registros de auditoría de aplicaciones empresariales

Informes de auditoría basado en la aplicación, puede obtener respuestas tooquestions como:

* ¿Cuáles son las aplicaciones de Hola que se han agregado o actualizado?
* ¿Cuáles son las aplicaciones de Hola que se han quitado?
* ¿Ha cambiado el principal de servicio para una aplicación?
* ¿Se cambiaron los nombres de Hola de las aplicaciones?
* ¿Que dio consentimiento tooan aplicación?

Si su intención es tooreview datos que está relacionado tooyour aplicaciones de la auditoría, puede encontrar una vista filtrada en **registros de auditoría** en hello **actividad** sección de hello **aplicaciones empresariales**  hoja. Este punto de entrada tiene **Aplicaciones empresariales** como **Tipo de recurso de actividad** preseleccionado.

![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/134.png "Registros de auditoría")

Puede filtrar aún más esta vista hacia abajo toojust **grupos** o simplemente **usuarios**.

![Registros de auditoría](./media/active-directory-reporting-activity-audit-logs/25.png "Registros de auditoría")


## <a name="next-steps"></a>Pasos siguientes

Para obtener información general de informes, vea hello [reporting de Azure Active Directory](active-directory-reporting-azure-portal.md).

