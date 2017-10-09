---
title: "registro de auditoría aaaHow toouse hello en Azure AD Privileged Identity Management | Documentos de Microsoft"
description: "Obtenga información acerca de cómo registro de auditoría de Hola de toouse en extensión de hello Privileged Identity Management de Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a>Mediante el registro de auditoría de hello en PIM
Puede usar toosee de registro de auditoría de hello Privileged Identity Management (PIM) todas las asignaciones de usuario de Hola y las activaciones dentro de un período de tiempo determinado. Si desea historial de auditoría completo de hello toosee de actividad en su inquilino, incluidos administrador, el usuario final y la actividad de sincronización, puede usar hello [informes de acceso y uso de Azure Active Directory.](active-directory-view-access-usage-reports.md)

## <a name="navigate-toohello-audit-log"></a>Navegar por el registro de auditoría toohello
De hello [portal de Azure](https://portal.azure.com) panel, seleccione hello **Azure AD Privileged Identity Management** aplicación. Desde allí, tener acceso a registro de auditoría de hello haciendo clic en **administrar roles con privilegios** > **historial de auditoría** en el panel PIM Hola.

## <a name="hello-audit-log-graph"></a>gráfico de registro de auditoría de Hola
Puede usar Hola auditoría registro tooview Hola total de activaciones, max activaciones al día y las activaciones medias por día en un gráfico de líneas.  También puede filtrar datos de Hola por rol si hay más de un rol en el historial de auditoría de Hola.

Hola de uso **tiempo**, **acción**, y **rol** botones toosort Hola registro.

## <a name="hello-audit-log-list"></a>lista de registro de auditoría de Hola
Hola columnas en la lista de registro de auditoría de hello son:

* **Solicitante** -usuario Hola que solicitó la activación de rol de Hola o cambiar.  Si el valor de hello es "Sistema de Azure", compruebe el registro de auditoría de Azure de Hola para obtener más información.
* **Usuario** -usuario Hola que se está activando o asignado tooa rol.
* **Rol** -rol Hola asignados o activados por usuario de Hola.
* **Acción** : acciones de hello realizadas por el solicitante de Hola. Esto puede incluir asignación, desasignación, activación o desactivación.
* **Tiempo** : cuando se produjo la acción de Hola.
* **Razonamiento** -si se especificó ningún texto en el campo motivo de Hola durante la activación, se mostrará aquí.
* **Caducidad** : solo es importante para la activación de los roles.

## <a name="filter-hello-audit-log"></a>Registro de auditoría de filtro Hola
Puede filtrar información de Hola que aparezca en el registro de auditoría de hello haciendo clic en hello **filtro** botón.  Hola **hoja de parámetros del gráfico de actualización** aparecerá.

Después de establecer filtros de hello, haga clic en **actualización** toofilter datos de hello en el registro de hello.  Si los datos de hello no aparecen inmediatamente, actualice la página de Hola.

### <a name="change-hello-date-range"></a>Cambiar el intervalo de fechas de Hola
Hola de uso **hoy**, **última semana**, **mes pasado**, o **personalizado** botones de intervalo de tiempo de hello toochange del registro de auditoría de Hola.

Cuando eliges hello **personalizado** botón, se le ofrecerá una **de** campo de fecha y un **a** toospecify un intervalo de fechas para el registro de hello de campo de fecha.  Puede escribir las fechas de hello en formato MM/DD/AAAA o haga clic en hello **calendario** icono y elija una fecha de Hola de un calendario.

### <a name="change-hello-roles-included-in-hello-log"></a>Cambiar los roles de Hola que se incluyen en el registro de hello
Active o desactive hello **rol** casilla de verificación siguiente tooeach rol tooinclude o excluir del registro de hello.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

