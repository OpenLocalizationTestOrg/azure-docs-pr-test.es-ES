---
title: acceso a las aplicaciones de autoservicio aaaHow toouse | Documentos de Microsoft
description: "Habilitar aplicación self-service acceso tooallow usuarios toofind sus propias aplicaciones"
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
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a>Cómo tener acceso aplicaciones de autoservicio de toouse

Antes de que los usuarios pueden detectar automáticamente las aplicaciones de su panel de acceso, deberá tooenable **acceso a la aplicación de autoservicio** aplicaciones tooany que desea tooallow usuarios tooself-detectar y solicitar acceso a.

Esta característica es una excelente manera de toosave tiempo y dinero como un grupo de TI y se recomienda encarecidamente como parte de una implementación de aplicaciones modernas con Azure Active Directory.

Con esta característica, puede:

-   Permitir que los usuarios detectar automáticamente las aplicaciones de hello [Panel de acceso de la aplicación](https://myapps.microsoft.com/) sin molestarle Hola TI grupo.

-   Agregue esos grupo preconfigurada de tooa de usuarios para que pueda ver que ha solicitado el acceso, quitar el acceso y administrar roles de hello asignados toothem.

-   Si lo desea permitir que un aprobador empresariales las solicitudes de acceso de aplicación tooapprove para que hello grupo de TI no tiene que.

-   Opcionalmente, configure hasta too10 personas pueden aprobar aplicación toothis de access.

-   Si lo desea permitir un aprobador business contraseñas de hello tooset estos usuarios pueden utilizar toosign en aplicación toohello, directamente desde del aprobador Hola business [Panel de acceso de la aplicación](https://myapps.microsoft.com/).

-   Si lo desea asignar rol de aplicación de los usuarios asignados autoservicio tooan directamente.

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a>Habilitar aplicación self-service acceso tooallow usuarios toofind sus propias aplicaciones

Acceso a la aplicación de autoservicio es una tooself de los usuarios de manera estupenda tooallow-detectar las aplicaciones, si lo desea permitir el acceso de tooapprove de grupo de negocios de hello toothose aplicaciones. Puede permitir credenciales de Hola de hello business grupo toomanage asignan a usuarios toothose para derecho de inicio de sesión único en aplicaciones de contraseña de sus paneles de acceso.

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

   * No se admiten grupos.

13. **Opcional:** **para las aplicaciones que exponen funciones**, si desea que el rol de tooa de tooassign usuarios aprobados de autoservicio, haga clic en hello selector siguiente toohello **toowhich rol deben asignarse a los usuarios en este ¿aplicación?**  tooselect Hola rol toowhich se deben asignar estos usuarios.

14. Haga clic en hello **guardar** situado en la parte superior de Hola de hello hoja toofinish.

Cuando se haya completado la configuración de la aplicación de autoservicio, los usuarios pueden navegar tootheir [Panel de acceso de la aplicación](https://myapps.microsoft.com/) y haga clic en hello **+ agregar** botón toofind Hola aplicaciones toowhich ha habilitado Acceso de autoservicio. Los aprobadores de la empresa pueden también ver una notificación en sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/). Puede habilitar un correo electrónico que les informa de cuándo un usuario ha solicitado la aplicación de tooan de acceso que requiere su aprobación. 

Estas aprobaciones admiten una aprobación única sólo flujos de trabajo, lo que significa que si especifica varios aprobadores, cualquier aprobador único puede aprobar aplicación toohello de access.

## <a name="next-steps"></a>Pasos siguientes
[Configuración de Azure Active Directory para la administración de grupos de autoservicio](active-directory-accessmanagement-self-service-group-management.md)
