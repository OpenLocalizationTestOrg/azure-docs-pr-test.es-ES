---
title: "los flujos de trabajo de aprobación de administración de identidad con privilegios de aaaAzure | Documentos de Microsoft"
description: "Obtenga información sobre los flujos de trabajo de aprobación de Privileged Identity Management (PIM)"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a>Aprobaciones (versión preliminar)

## <a name="overview"></a>Información general

Con aprobaciones de Privileged Identity Management, puede configurar la aprobación de toorequire de roles para la activación y elija uno o varios usuarios o grupos de aprobadores como delegados. Sigan leyendo toolearn cómo tooconfigure roles y seleccione aprobadores.

>[!NOTE]
Tenga en cuenta que esta característica está aún en desarrollo, por lo que puede encontrar errores. funcionalidad de Hello, incluyendo el texto y convenciones de nomenclatura están sujetos a cambios y no deben considerarse finales.


## <a name="key-terminology"></a>Terminología clave

*Elegibles de rol de usuario* : un rol elegibles trata de un usuario dentro de su organización que se ha asignado el rol de Azure AD tooan como derecho (rol requiere activación).

*Aprobador delegado*: se trata de una o varias personas o grupos de Azure AD responsables de la aprobación de las solicitudes de activación de roles.

## <a name="scenarios"></a>Escenarios

vista previa privada de Hello admite Hola los escenarios siguientes:

**Como administrador de rol con privilegios (PRA), puede:**

-   [Habilitar la aprobación de roles específicos](#enable-approval-for-specific-roles)

-   [Especifique solicitudes de tooapprove de usuarios o grupos de aprobador](#specify-approver-users-and/or-groups-to-approve-requests)

-   [Ver el historial de solicitudes y aprobaciones de todos los roles con privilegios](#view-request-and-approval-history-for-all-privileged-roles)

**Como un aprobador designado, puede:**

-   [Ver aprobaciones o solicitudes pendientes](#view-pending-approvals-requests)

-   [Aprobar o rechazar solicitudes de elevación de rol (de forma individual o masiva)](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [Proporcionar una justificación de la aprobación o el rechazo](#provide-justification-for-my-approval/rejection) 

**Como usuario de rol apto, puede:**

-   [Solicitar la activación de un rol que requiere aprobación](#request-activation-of-a-role-that-requires-approval)

-   [ver el estado de saludo de su tooactivate de solicitud](#view-the-status-of-your-request-to-activate)

-   [Completar la tarea en Azure AD si la activación se ha aprobado](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a>Navegación

Hemos actualizado aprobaciones de hello navegación toosupport

![](media/azure-ad-pim-approval-workflow/image001.png)

página de aterrizaje de Hello predeterminada proporciona un acceso cómodo tooinformation sobre hello y PIM nueva documentación de aprobaciones.

![](media/azure-ad-pim-approval-workflow/image002.png)

También se ha agregado una sección nueva para todos los usuarios de PIM, "My Audit History" (Mi historial de auditoría). Aquí puede encontrar todas las identidades de tooyour relevantes de información Hola. Esto incluye todas las solicitudes pendientes y completadas, ninguna decisión relativa al que haya realizado sobre las solicitudes de Hola para resolver y todas sus activaciones rol pasados en una ubicación conveniente.

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a>Habilitar la aprobación de roles específicos

aprobación de tooenable para un rol específico, primero seleccione Roles del directorio de navegación izquierdo de Hola.

![](media/azure-ad-pim-approval-workflow/image004.png)

Busque y seleccione Configuración Hola de navegación izquierdo de Roles de directorio

![](media/azure-ad-pim-approval-workflow/image006.png)

Seleccione Roles con privilegios:

![](media/azure-ad-pim-approval-workflow/image009.png)

Seleccione "Activar" Hola requieren la sección de aprobación:

![](media/azure-ad-pim-approval-workflow/image011.png)

Una vez habilitada, hoja de hello expandirá hello tooshow detalles siguientes:

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
Si no especifica los aprobadores, hello PRA(s) se convierten en hello aprobadores de forma predeterminada. PRA(s) sería necesario tooapprove activación todas las solicitudes para este rol.

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a>Especifique solicitudes de tooapprove de usuarios o grupos de aprobador

aprobación de toodelegate, haga clic en la opción de hello demasiado "Seleccionar aprobadores":

![](media/azure-ad-pim-approval-workflow/image015.png)

Cuando se carga la hoja de aprobadores seleccione hello, puede buscar un usuario o grupo específico mediante la barra de búsqueda de hello en la parte superior de Hola o seleccionar de lista rellenada previamente hello, a continuación, haga clic en "Seleccionar" cuando finaliza:

![](media/azure-ad-pim-approval-workflow/image017.png)

Nota: puede seleccionar varios usuarios o grupos a la vez.

La selección aparecerá en lista de Hola de aprobadores seleccionados tal como se muestra a continuación:

![](media/azure-ad-pim-approval-workflow/image019.png)

tooremove aprobador, simplemente haga clic en siguiente tootheir nombre del botón Quitar del saludo.

tooadd aprobadores adicionales, el proceso de repetición Hola.

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a>Ver el historial de solicitudes y aprobaciones de todos los roles con privilegios

historial de solicitud y aprobación de tooview para los roles con todos los privilegios, seleccione historial de auditoría desde el panel de hello:

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
Puede ordenar los datos de Hola por acción y busque "Activación"aprobado"

### <a name="view-pending-approvals-requests"></a>Ver aprobaciones o solicitudes pendientes

Como un aprobador delegado, recibirá notificaciones por correo electrónico cuando una solicitud está pendiente de aprobación. tooview estas solicitudes en el portal PIM de hello, desde la ficha Panel (en la nueva navegación hello) seleccione Hola "aprobación solicitudes pendientes" hello la barra de navegación izquierda.

![](media/azure-ad-pim-approval-workflow/image023.png)

Ahí se mostrará una lista de solicitudes pendientes de aprobación:

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a>Aprobar o rechazar solicitudes de elevación de rol (de forma individual o masiva)

Seleccione las solicitudes de hello desea tooapprove o denegar y haga clic en botón hello en la barra de acciones que se corresponde con su decisión:

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a>Proporcionar una justificación de la aprobación o el rechazo

Esto abre una nueva tooapprove hoja o denegar varias solicitudes a la vez. Especificar una justificación para su decisión, y haga clic en Aprobar (o denegar) en parte inferior de Hola u hoja hello:

![](media/azure-ad-pim-approval-workflow/image029.png)

Cuando se completa el proceso de solicitud de hello, símbolo de estado de hello reflejará la decisión adoptada (en este ejemplo, la decisión de hello es aprobar):

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a>Solicitar la activación de un rol que requiere aprobación

Solicitar la activación de un rol que requiere la aprobación se puede iniciar desde navegación PIM antiguo de Hola o navegación nueva hello, como proceso de Hola para sigue siendo de activación de rol Hola igual. Simplemente seleccione un rol de la lista de Hola de roles para activar:

![](media/azure-ad-pim-approval-workflow/image033.png)

Si un rol con privilegios requiere Multi-Factor Authentication, se le pedirá que complete esa tarea en primer lugar:

![](media/azure-ad-pim-approval-workflow/image035.png)

Cuando haya terminado, haga clic en Activar y proporcione una justificación (si es necesario):

![](media/azure-ad-pim-approval-workflow/image037.png)

solicitante de Hello verá una notificación que Hola solicitud está pendiente de aprobación:

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a>Ver el estado de saludo de su tooactivate de solicitud

Ver el estado de saludo de una solicitud pendiente tooactivate debe tener acceso desde el nuevo panel de navegación. Desde la barra de navegación izquierda de hello, seleccione la pestaña de "Mis solicitudes" de hello:

![](media/azure-ad-pim-approval-workflow/image041.png)

estado de la solicitud de saludo predeterminado es demasiado "Pendiente", pero puede alternar toosee todos o solicitudes denegadas.

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a>Completar la tarea en Azure AD si la activación se ha aprobado

Una vez aprobada la solicitud de hello, rol de hello está activo y se puede continuar con cualquier trabajo que requiere este rol.

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a>Pasos siguientes

Sus comentarios son valiosos toous. Póngase tooshare libre ni comentario con nosotros aquí.
