---
title: aaaAzure IoT Suite y Azure Active Directory | Documentos de Microsoft
description: "Describe cómo el conjunto de IoT de Azure utiliza permisos toomanage de Azure Active Directory."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a>Permisos en el sitio de hello azureiotsuite.com

## <a name="what-happens-when-you-sign-in"></a>Qué ocurre al iniciar sesión

Hola la primera vez que inicie sesión en [azureiotsuite.com][lnk-azureiotsuite], sitio de hello determina seleccionados los niveles de permiso de hello tener en función de hello actualmente el inquilino de Azure Active Directory (AAD) y Azure suscripción.

1. En primer lugar, lista de hello toopopulate del nombre de usuario de los inquilinos vistos siguiente tooyour, sitio Hola averigua de Azure que los inquilinos AAD que pertenece. Actualmente, el sitio de hello solo puede obtener tokens de usuario para un solo inquilino a la vez. Por lo tanto, cuando se cambia de inquilinos mediante la lista desplegable de hello en la esquina superior derecha de hello, sitio Hola la sesión en tokens de toothat inquilino tooobtain Hola para ese inquilino.

2. A continuación, el sitio de hello averigua de las suscripciones que tienen asociados con hello seleccionado inquilino de Azure. Vea las suscripciones disponibles de hello cuando se crea una nueva solución preconfigurada.

3. Por último, sitio Hola recupera todos los recursos de hello en suscripciones de Hola y grupos de recursos etiquetados como soluciones preconfiguradas y rellena los iconos de hello en la página de inicio de Hola.

Hola siguientes secciones describe los roles de Hola que controlan el acceso toohello preconfigurado soluciones.

## <a name="aad-roles"></a>Roles de AAD

roles AAD de Hola Hola capacidad aprovisionar preconfigurado soluciones de control y administración de usuarios en una solución preconfigurada.

Puede encontrar más información sobre los roles del administrador en AAD en [Asignación de roles de administrador en Azure Active Directory][lnk-aad-admin]. artículo actual de Hola se centra en hello **administrador Global** hello y **usuario** roles de directorio, como se hace Hola soluciones preconfiguradas.

### <a name="global-administrator"></a>Administrador global

Puede haber muchos administradores globales por inquilino de AAD:

* Cuando se crea un inquilino de AAD, eres por un administrador global de hello predeterminado de ese inquilino.
* Administrador global de Hello puede aprovisionar una solución preconfigurada y se le asigna un **administración** rol de aplicación Hola dentro de su inquilino AAD.
* Si otro usuario de Hola mismo inquilino AAD crea una aplicación, rol predeterminado de hello es concedido de administrador global de toohello **ReadOnly**.
* Un administrador global puede asignar usuarios tooroles para las aplicaciones que usan hello [portal de Azure][lnk-portal].

### <a name="domain-user"></a>Usuario de dominio

Puede haber muchos usuarios de dominio por inquilino de AAD:

* Un usuario de dominio puede proporcionar una solución preconfigurada a través de hello [azureiotsuite.com] [ lnk-azureiotsuite] sitio. De forma predeterminada, se concede a los usuario de dominio de Hola Hola **administración** rol Hola aprovisiona la aplicación.
* Un usuario de dominio puede crear una aplicación con script build.cmd de Hola Hola [-iot-remoto-supervisión de azure][lnk-rm-github-repo], [azure iot-predictivo mantenimiento] [ lnk-pm-github-repo], o [-iot-conectado-factory de azure] [ lnk-cf-github-repo] repositorio. Sin embargo, rol predeterminado de hello concedido es de usuario del dominio toohello **ReadOnly**, ya que un usuario de dominio no tiene permiso tooassign roles.
* Si otro usuario de inquilino de AAD Hola crea una aplicación, usuario de dominio de Hola se asigna hello **ReadOnly** función predeterminada para esa aplicación.
* El usuario de dominio no puede asignar roles para aplicaciones; por consiguiente, no puede agregar usuarios o roles a usuarios para una aplicación, aunque la haya aprovisionado.

### <a name="guest-user"></a>Usuario invitado

Puede haber muchos usuarios invitados por inquilino de AAD. Usuarios invitados tienen un conjunto limitado de derechos en el inquilino de AAD Hola. Como resultado, los usuarios invitados no pueden proporcionar una solución preconfigurada en el inquilino de AAD Hola.

Para obtener más información sobre los usuarios y roles en AAD, consulte Hola recursos siguientes:

* [Creación de usuarios en Azure AD][lnk-create-edit-users]
* [Asignar usuarios tooapps][lnk-assign-app-roles]

## <a name="azure-subscription-administrator-roles"></a>Roles de administrador de suscripciones de Azure

las funciones de administración de Azure Hola controlan Hola capacidad toomap un inquilino de tooan AD de suscripción de Azure.

Obtener más información acerca de los roles de administrador de Azure de hello en el artículo hello [cómo tooadd o cambiar la cuenta de administrador, Administrador de servicios y Coadministrador de Azure][lnk-admin-roles].

## <a name="application-roles"></a>Roles de la aplicación

roles de aplicación Hola controlan toodevices de acceso de la solución preconfigurada.

Hay dos roles definidos y una función implícita definida en una aplicación aprovisionada:

* **Administrador:** tiene control total tooadd, administrar, quite los dispositivos y modificar la configuración.
* **ReadOnly:** puede ver dispositivos, reglas, acciones, trabajos y telemetría.

Puede encontrar permisos Hola asignan el rol de tooeach en hello [RolePermissions.cs] [ lnk-resource-cs] archivo de código fuente.

### <a name="changing-application-roles-for-a-user"></a>Cambio de roles de aplicación para un usuario

Puede usar Hola siguiendo el procedimiento toomake un usuario en el Administrador de la solución preconfigurada de Active Directory.

Debe ser un rol de toochange AAD administrador global para un usuario:

1. Vaya toohello [portal de Azure][lnk-portal].
2. Seleccione **Azure Active Directory**.
3. Asegúrese de que está usando directorio Hola elegido en azureiotsuite.com al aprovisionar la solución. Si tiene varios directorios asociados a su suscripción, puede cambiar entre ellos si hace clic en el nombre de su cuenta en hello superior derecha del portal de Hola.
4. Haga clic en **Aplicaciones empresariales** y en **Todas las aplicaciones**.
4. Muestre **Todas las aplicaciones** con **Cualquier** estado. A continuación, busque una aplicación con el nombre de la solución preconfigurada.
5. Haga clic en el nombre de Hola de aplicación Hola que coincida con el nombre de la solución preconfigurada.
6. Haga clic en **Usuarios y grupos**.
7. Seleccione usuario Hola desea tooswitch roles.
8. Haga clic en **asignar** y seleccione Hola rol (como **administración**) le gustaría tooassign toohello usuario, haga clic en la marca de verificación de Hola.

## <a name="faq"></a>P+F

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a>Soy un administrador de servicios y me gustaría que la asignación de directorio de hello toochange entre mi suscripción y un inquilino AAD específico. ¿Cómo completo esta tarea?

1. Vaya toohello [portal de Azure clásico][lnk-classic-portal], haga clic en **configuración** en lista de hello de servicios en el lado izquierdo de Hola.
2. Seleccione la suscripción de Hola que desea que la asignación de directorio de hello toochange a.
3. Haga clic en **Editar directorio**.
4. Seleccione hello **Directory** le gustaría toouse en la lista desplegable de Hola. Haga clic en la flecha hacia adelante Hola.
5. Confirmar la asignación de directorio de Hola y afectados coadministradores. Si va a mover de otro directorio, se quitan todos los Hola coadministradores de directorio original Hola.

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a>Soy un usuario o miembro del dominio en el inquilino de AAD de Hola y he creado una solución preconfigurada. ¿Cómo se asigna un rol en mi aplicación?

Solicitar un toomake administrador global que un administrador global en hello AAD de inquilinos y, a continuación, asigna roles toousers. O bien, pida un tooassign administrador global es un rol directamente. Si desea que el inquilino de AAD de hello toochange en que se ha implementado la solución preconfigurada, vea la siguiente pregunta de Hola.

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a>¿Cómo se puede cambiar el inquilino de AAD Hola a que mi solución preconfigurada de supervisión y la aplicación se asignan?

Puede ejecutar una implementación en la nube desde <https://github.com/Azure/azure-iot-remote-monitoring> e implementar de nuevo con un inquilino de ADD recién creado. Dado que son, de forma predeterminada, un administrador global cuando se crea un inquilino de AAD, que tiene permisos tooadd usuarios y asigna roles a los usuarios de toothose.

1. Crear un directorio AAD en hello [portal de Azure][lnk-portal].
2. Vaya demasiado<https://github.com/Azure/azure-iot-remote-monitoring>.
3. Ejecute `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (por ejemplo, `build.cmd cloud debug myRMSolution`)
4. Cuando se le pida, establezca hello **tenantid** toobe el inquilino recién creado en lugar de su inquilino anterior.

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a>Desea toochange un administrador de servicios o Coadministrador cuando inicia sesión con una cuenta organizativa

Vea el artículo de soporte técnico de hello [cambiar el Administrador de servicios y Coadministrador cuando inicia sesión con una cuenta organizativa][lnk-service-admins].

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a>¿Por qué veo este error? "Su cuenta no tiene toocreate de los permisos adecuados de hello una solución. Póngase en contacto con el administrador de cuentas o inténtelo con otra cuenta."

Mire Hola siguiente diagrama para obtener instrucciones:

![][img-flowchart]

> [!NOTE]
> Si continúa el error de hello toosee después de validar un administrador global de inquilino de AAD de Hola y Coadministrador de suscripción de hello, pida al administrador de cuenta quitar usuario hello y volver a asignar los permisos necesarios en este orden. En primer lugar, agregar usuario hello como administrador global y, a continuación, agregar el usuario como Coadministrador en hello suscripción de Azure. Si los problemas persisten, póngase en contacto con [Ayuda y soporte técnico][lnk-help-support].

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a>¿Por qué veo este error cuando tengo una suscripción de Azure? "Una suscripción de Azure es necesario toocreate preconfigurado y soluciones. Puede crear una cuenta de evaluación gratuita en pocos minutos".

Si está seguro de que tiene una suscripción de Azure, validar la asignación de su suscripción de inquilinos de Hola e inquilino correcto de hello está seleccionado en la lista desplegable de Hola. Si ha validado Hola deseado inquilino es correcto, siga Hola anterior diagrama y validar la asignación de Hola de su suscripción y este inquilino AAD.

## <a name="next-steps"></a>Pasos siguientes
toocontinue de aprendizaje sobre los conjuntos de IoT, vea cómo puede [personalizar una solución preconfigurada][lnk-customize].

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
