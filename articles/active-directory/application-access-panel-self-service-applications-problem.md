---
title: "aaaProblem con acceso a la aplicación de autoservicio | Documentos de Microsoft"
description: "Solucionar problemas de acceso de la aplicación de servicio de tooself relacionada de problemas"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a>Problemas al usar el acceso de autoservicio a las aplicaciones

Acceso a la aplicación de autoservicio es una tooself de los usuarios de manera estupenda tooallow-detectar las aplicaciones, si lo desea permitir el acceso de tooapprove de grupo de negocios de hello toothose aplicaciones. Puede permitir credenciales de Hola de hello business grupo toomanage asignan a usuarios toothose para derecho de inicio de sesión único en aplicaciones de contraseña de sus paneles de acceso.

Antes de que los usuarios pueden detectar automáticamente las aplicaciones de su panel de acceso, deberá tooenable **acceso a la aplicación de autoservicio** aplicaciones tooany que desea tooallow usuarios tooself-detectar y solicitar acceso a.

## <a name="general-issues-toocheck-first"></a>General emite toocheck primero

-   Asegúrese de que el acceso de autoservicio a las aplicaciones está configurado correctamente. Consulte "Cómo acceder aplicaciones de autoservicio de tooconfigure".

-   Asegúrese de que Hola usuario o grupo se ha habilitado el acceso de toorequest aplicación self-service.

-   Asegúrese de que el usuario Hola está visitando el lugar correcto de hello para el acceso a aplicaciones de autoservicio. los usuarios pueden navegar tootheir [Panel de acceso de la aplicación](https://myapps.microsoft.com/) y haga clic en hello **+ agregar** botón toofind Hola aplicaciones toowhich ha habilitado el acceso de autoservicio.

-   Si recientemente se ha configurado el acceso a la aplicación de autoservicio, toosign de entrada y salida vuelva a intentarlo en el Panel de acceso del usuario de hello después de unos toosee minutos si han aparecido cambios de acceso de autoservicio de Hola.

## <a name="how-tooconfigure-self-service-application-access"></a>Cómo tener acceso aplicaciones de autoservicio de tooconfigure

aplicación de tooan de acceso de tooenable aplicación self-service, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooenable acceso de autoservicio toofrom Hola lista.

7.  Una vez que se carga la aplicación hello, haga clic en **self-service** del menú de navegación izquierdo de la aplicación hello.

8.  tooenable acceso a la aplicación de autoservicio para esta aplicación, activar hello **permitir que los usuarios de aplicación de toorequest access toothis?** alternar demasiado**sí.**

9.  A continuación, tooselect Hola grupo toowhich los usuarios que solicitan acceso toothis aplicación debe agregarse, haga clic en siguiente toohello etiqueta de selector de hello **toowhich grupo debería asignar se agregan usuarios?** y seleccione un grupo.

10. **Opcional:** si desea que toorequire la aprobación de un negocio antes de que los usuarios tienen permiso de acceso, establezca hello **requieren aprobación antes de conceder acceso toothis aplicación?** alternar demasiado**Sí**.

11. **Opcional: para aplicaciones que utilizan la contraseña de inicio de sesión único en solo,** si desea que tooallow esas contraseñas hello toospecify de aprobadores empresariales que se envían toothis aplicación para los usuarios aprobados, establezca hello **permitir aprobadores tooset ¿contraseñas de usuario para esta aplicación?**  alternar demasiado**Sí**.

12. **Opcional:** toospecify Hola business aprobadores se permiten la aplicación de toothis de tooapprove access, haga clic en siguiente toohello etiqueta de selector de hello **que se permite la aplicación de tooapprove access toothis?** tooselect seguridad too10 aprobadores de negocios individuales.

 >[!NOTE]
 > No se admiten grupos.
 >
 >

13. **Opcional:** **para las aplicaciones que exponen funciones**, si desea que el rol de tooa de tooassign usuarios aprobados de autoservicio, haga clic en hello selector siguiente toohello **toowhich rol deben asignarse a los usuarios en este ¿aplicación?**  tooselect Hola rol toowhich se deben asignar estos usuarios.

14. Haga clic en hello **guardar** situado en la parte superior de Hola de hello hoja toofinish.

Cuando se haya completado la configuración de la aplicación de autoservicio, los usuarios pueden navegar tootheir [Panel de acceso de la aplicación](https://myapps.microsoft.com/) y haga clic en hello **+ agregar** botón toofind Hola aplicaciones toowhich ha habilitado Acceso de autoservicio. Los aprobadores de la empresa pueden también ver una notificación en sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/). Puede habilitar un correo electrónico que les informa de cuándo un usuario ha solicitado la aplicación de tooan de acceso que requiere su aprobación. 

Estas aprobaciones admiten una aprobación única sólo flujos de trabajo, lo que significa que si especifica varios aprobadores, cualquier aprobador único puede aprobar aplicación toohello de access.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Si estos pasos no resuelven el problema de Hola 

Abra una incidencia de soporte técnico con hello siguiente información si está disponible:

-   Id. de error de correlación

-   UPN (dirección de correo electrónico del usuario)

-   TenantID

-   Tipo de explorador

-   Zona horaria y hora/período de tiempo durante el que se produce el error

-   Seguimientos de Fiddler

## <a name="next-steps"></a>Pasos siguientes
[Configuración de Azure Active Directory para la administración de grupos de autoservicio](active-directory-accessmanagement-self-service-group-management.md)
