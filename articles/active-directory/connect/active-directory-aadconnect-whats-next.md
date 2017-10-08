---
title: "Azure AD Connect: Pasos siguientes y cómo toomanage Azure AD Connect | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooextend Hola tareas operativas y la configuración predeterminada de Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a>Pasos siguientes y cómo toomanage Azure AD Connect
Utilice los procedimientos operativos hello en este toomeet de artículo toocustomize Connect de Azure Active Directory (Azure AD) necesidades y los requisitos de su organización.  

## <a name="add-additional-sync-admins"></a>Pasos para agregar administradores de sincronización adicionales
De forma predeterminada, solo usuario Hola que Hola instalación y administradores locales son toomanage capaz de motor de sincronización de hello instalado. Para otras personas toobe capaz de tooaccess y administrar el motor de sincronización de hello, busque grupo Hola denominada ADSyncAdmins en el servidor local de Hola y agréguelos toothis grupo.

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a>Asignar licencias tooAzure usuarios de AD Premium y Enterprise Mobility Suite
Ahora que los usuarios han estado sincronizado toohello en la nube, necesita tooassign ellos una licencia por lo que pueden empezar a trabajar con aplicaciones de nube, como Office 365.

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a>tooassign una Azure AD Premium o licencia de Enterprise Mobility Suite

1. Inicie sesión en toohello portal de Azure como administrador.
2. Hola izquierda, seleccione **Active Directory**.
3. En hello **Active Directory** página, haga doble clic en el directorio de Hola que tiene usuarios de Hola que desee tooset seguridad.
4. Hola parte superior de página de directorio de hello, seleccione **licencias**.
5. En hello **licencias** página, seleccione **Active Directory Premium** o **Enterprise Mobility Suite**y, a continuación, haga clic en **asignar**.
6. En el cuadro de diálogo de hello, seleccione los usuarios que desee tooassign licencias y, a continuación, haga clic en hello marca de verificación icono toosave Hola cambios de Hola.

## <a name="verify-hello-scheduled-synchronization-task"></a>Comprobar la tarea de sincronización programada de Hola
Utilizar el estado de Hola de hello toocheck portal Azure de una sincronización.

### <a name="tooverify-hello-scheduled-synchronization-task"></a>tarea de sincronización programada de hello tooverify
1. Inicie sesión en toohello portal de Azure como administrador.
2. Hola izquierda, seleccione **Active Directory**.
3. En hello **Active Directory** página, haga doble clic en el directorio de Hola que tiene usuarios de Hola que desee tooset seguridad.
4. Hola parte superior de página de directorio de hello, seleccione **integración de directorios**.
5. En **integración con active directory local**, Hola Nota hora de última sincronización.

<center>![Hora de sincronización de directorios](./media/active-directory-aadconnect-whats-next/verify.png)</center>

## <a name="start-a-scheduled-synchronization-task"></a>Inicio de una tarea de sincronización programada
Si necesita toorun una tarea de sincronización, puede hacerlo ejecutando a través del Asistente de Azure AD Connect de Hola de nuevo.  Debe tooprovide sus credenciales de Azure AD.  En el Asistente de hello, seleccione hello **personalizar las opciones de sincronización** de tareas y haga clic en **siguiente** toomove a través del Asistente de Hola. Al final de hello, asegúrese de que hello **iniciar el proceso de sincronización de hello tan pronto como finalice la configuración inicial de hello** casilla de verificación.

<center>![Inicio de la sincronización](./media/active-directory-aadconnect-whats-next/startsynch.png)</center>

Para obtener más información sobre la sincronización de hello Azure AD Connect programador, consulte [el programador de conectarse de Azure AD](active-directory-aadconnectsync-feature-scheduler.md).

## <a name="additional-tasks-available-in-azure-ad-connect"></a>Tareas adicionales disponibles en Azure AD Connect
Después de la instalación inicial de Azure AD Connect, puede siempre Hola volver a iniciar a Asistente de hello Azure AD Connect página o escritorio acceso directo de inicio.  Observará que pasar por el Asistente de Hola de nuevo proporciona algunas opciones nuevas en forma de Hola de tareas adicionales.  

Hello tabla siguiente proporciona un resumen de estas tareas y una breve descripción de cada tarea.

![Lista de tareas adicionales](./media/active-directory-aadconnect-whats-next/addtasks.png)

| Tarea adicional | Descripción |
| --- | --- |
| **Escenario de vista Hola seleccionado** |Visualice su solución actual de Azure AD Connect.  Incluye la configuración general, los directorios sincronizados y la configuración de sincronización. |
| **Personalizar las opciones de sincronización** |Cambiar la configuración actual de hello como agregar configuración adicional de toohello de bosques de Active Directory, o habilitar las opciones de sincronización como un usuario, grupo, dispositivo o reescritura de contraseña. |
| **Habilitar el modo provisional** |La información de fases que no se sincroniza inmediatamente y no exporta tooAzure AD o en local de Active Directory.  Con esta característica, puede obtener una vista previa sincronizaciones Hola antes de que ocurran. |

## <a name="next-steps"></a>Pasos siguientes
Más información acerca de la [integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
