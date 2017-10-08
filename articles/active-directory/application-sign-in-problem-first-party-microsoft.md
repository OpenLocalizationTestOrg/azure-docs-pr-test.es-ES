---
title: "aaaProblems iniciar sesión en aplicaciones de Microsoft tooa | Documentos de Microsoft"
description: "Solucionar problemas comunes que se enfrentan al iniciar sesión en Applications de Microsoft toofirst terceros mediante Azure AD (por ejemplo, Office 365)"
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a>Problemas para iniciar sesión en tooa aplicaciones de Microsoft

Las aplicaciones de Microsoft (como Office 365 Exchange, SharePoint, Yammer, etc.) se asignan y administran de manera algo diferente que las aplicaciones SaaS de terceros u otras aplicaciones que integra con Azure AD para el inicio de sesión único.

Hay tres maneras principales que un usuario puede obtener acceso tooa aplicación publicada por Microsoft.

-   Para las aplicaciones de Office 365 de Hola o de otros conjuntos de pagadas, los usuarios tienen acceso a través de **asignación de licencias** ya sea directamente tootheir cuenta de usuario o a través de un grupo con nuestra capacidad de asignación basado en el grupo de licencias.

-   Para las aplicaciones que Microsoft o una tercera entidad publica libremente para todo aquel que toouse, se podrá otorgar a los usuarios acceso a través de **consentimiento del usuario**. This0 significa que inicie sesión en la aplicación de toohello con su cuenta de Azure AD empresa o centro educativo y permitir toohave conjunto de toosome limitado de acceso de datos en su cuenta.

-   Para las aplicaciones que Microsoft o una entidad 3rd publica libremente para todo aquel que toouse, los usuarios también se podrá otorgar acceso a través de **consentimiento del administrador**. Esto significa que un administrador ha determinado la aplicación hello pueden utilizar todas las personas de la organización de hello, para que inicie sesión en la aplicación de toohello con una cuenta de administrador Global y conceder acceso tooeveryone de organización de Hola.

tootroubleshoot su problema, comienzan con hello [áreas con problemas generales con acceso a la aplicación tooconsider](#general-problem-areas-with-application-access-to-consider) y, a continuación, leer hello [Tutorial: pasos tootroubleshoot acceso de Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget en los detalles de Hola.

## <a name="general-problem-areas-with-application-access-tooconsider"></a>Áreas de riesgo general tooconsider de acceso a la aplicación

A continuación se muestra una lista de hello áreas con problemas generales que puede profundizar en si tiene una idea de donde toostart, pero le recomendamos que lea Hola tutorial tooget a trabajar rápidamente: [Tutorial: pasos tootroubleshoot acceso de Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access).

-   [Problemas con la cuenta de usuario de Hola](#problems-with-the-users-account)

-   [Problemas con grupos](#problems-with-groups)

-   [Problemas con las directivas de acceso condicional](#problems-with-conditional-access-policies)

-   [Problemas con el consentimiento de la aplicación](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a>Pasos tootroubleshoot acceso de Microsoft Application

A continuación se ciertos tipos de problemas comunes surgir cuando los usuarios no pueden iniciar sesión en tooa aplicaciones de Microsoft.

-   General emite toocheck primero

  * Asegúrese de que el usuario de hello es iniciar sesión en toohello **corríjala** y no una dirección URL de aplicación local.

  * Asegúrese de que es la cuenta de usuario de hello **no está bloqueada.**

  * Asegúrese de hello seguro **cuenta de usuario existe** en Azure Active Directory. [Comprobar si existe una cuenta de usuario en Azure Active Directory](#problems-with-the-users-account)

  * Asegúrese de que es la cuenta de usuario de hello **habilitado** para inicios de sesión. [Comprobar el estado de la cuenta de un usuario](#problems-with-the-users-account)

  * Asegúrese de que usuario hello **contraseña no se ha caducado o se olvida.** [Restablecer la contraseña del usuario](#reset-a-users-password) o [habilitar el autoservicio de restablecimiento de contraseña](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)

   * Asegurarse de que **Multi-Factor Authentication** no bloquee el acceso del usuario [Comprobar el estado de la autenticación multifactor de un usuario](#check-a-users-multi-factor-authentication-status) o [comprobar la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info)

   * Asegurarse de que una **directiva de acceso condicional** o una directiva de **protección de identidad** no bloquee el acceso del usuario [Comprobar una directiva de acceso condicional específica](#problems-with-conditional-access-policies) o [comprobar la directiva de acceso condicional de una aplicación específica](#check-a-specific-applications-conditional-access-policy) o [deshabilitar una directiva de acceso condicional específica](#disable-a-specific-conditional-access-policy)

   * Asegúrese de que un usuario **información de contacto de autenticación** es hacia arriba toodate tooallow la autenticación multifactor o acceso condicional directivas toobe aplicada. [Comprobar el estado de la autenticación multifactor de un usuario](#check-a-users-multi-factor-authentication-status) o [comprobar la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info)

-   Para **Microsoft** **las aplicaciones que requieren una licencia** (por ejemplo, Office 365), estos son algunos toocheck problemas específicos una vez que haya descartado problemas generales de hello anteriores:

   * Asegúrese de que el usuario de Hola o tiene un **una licencia asignada.** [Comprobar las licencias asignadas de un usuario](#check-a-users-assigned-licenses) o [comprobar licencias asignadas de un grupo](#check-a-groups-assigned-licenses)

   * Si la licencia de hello es **asignado tooa** **grupo estático**, asegúrese de que hello **pertenece un usuario** de ese grupo. [Comprobar la pertenencia a grupos de un usuario](#check-a-users-group-memberships)

   * Si la licencia de hello es **asignado tooa** **grupo dinámico**, asegúrese de que hello **regla de grupo dinámico se ha establecido correctamente**. [Comprobar los criterios de pertenencia de un grupo dinámico](#check-a-dynamic-groups-membership-criteria)

   * Si la licencia de hello es **asignado tooa** **grupo dinámico**, asegúrese de ese grupo dinámico hello tiene **haya terminado de procesar** ese hello y su pertenencia a **usuario es un miembro** (Esto puede tardar algún tiempo). [Comprobar la pertenencia a grupos de un usuario](#check-a-users-group-memberships)

   *  Una vez que asegurarse de que se asignará la licencia de hello, asegúrese de que está licencia hello **no expirado**.

   *  Asegúrese de que está licencia hello **para la aplicación hello** tienen acceso.

-   Para **Microsoft** **aplicaciones que no requieren una licencia**, estos son algunos otro toocheck cosas:

   * Si está solicitando la aplicación hello **permisos de usuario** (por ejemplo "acceso a este buzón de usuario"), asegúrese de que ese usuario Hola ha iniciado sesión en la aplicación toohello y ha realizado un **operación de consentimiento de nivel de usuario**  toolet Hola aplicación acceder a sus datos.

   * Si está solicitando la aplicación hello **permisos de nivel de administrador** (por ejemplo "obtener acceso a los buzones de correo de todos los usuarios"), asegúrese de que un administrador Global ha realizado una **operación de consentimiento de nivel de administrador en nombre de todos los usuarios** de organización de Hola.

## <a name="problems-with-hello-users-account"></a>Problemas con la cuenta de usuario de Hola

Acceso a la aplicación se puede bloquear debido tooa problema con un usuario que tenga asignada la aplicación toohello. A continuación se muestran algunas maneras de solucionar problemas con los usuarios y la configuración de sus cuentas:

-   [Comprobar si existe una cuenta de usuario en Azure Active Directory](#check-if-a-user-account-exists-in-azure-active-directory)

-   [Comprobar el estado de la cuenta de un usuario](#check-a-users-account-status)

-   [Restablecer la contraseña de un usuario](#reset-a-users-password)

-   [Habilitar el autoservicio de restablecimiento de contraseña](#enable-self-service-password-reset)

-   [Comprobar el estado de la autenticación multifactor de un usuario](#check-a-users-multi-factor-authentication-status)

-   [Comprobar la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info)

-   [Comprobar la pertenencia a grupos de un usuario](#check-a-users-group-memberships)

-   [Comprobar las licencias asignadas de un usuario](#check-a-users-assigned-licenses)

-   [Asignar una licencia a un usuario](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Comprobar si existe una cuenta de usuario en Azure Active Directory

toocheck si está presente, una cuenta de usuario siga Hola pasos:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Compruebe las propiedades de Hola de hello usuario objeto toobe seguro de que se muestran como esperaba y no existe ningún dato.

### <a name="check-a-users-account-status"></a>Comprobar el estado de la cuenta de un usuario

toocheck un usuario de estado de la cuenta, siga los pasos de hello siguientes:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **Perfil**.

8.  En **configuración** Asegúrese de que **bloque iniciar sesión en** se establece demasiado**No**.

### <a name="reset-a-users-password"></a>Restablecer la contraseña de un usuario

tooreset contraseña de un usuario, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en hello **de restablecimiento de contraseña** situado en la parte superior de Hola de hoja de usuario de Hola.

8.  Haga clic en hello **de restablecimiento de contraseña** botón en hello **de restablecimiento de contraseña** hoja que aparece.

9.  Hola copia **contraseña temporal** o **escriba una contraseña nueva** para el usuario de Hola.

10. Este nuevo usuario toohello de contraseña se comunican, requiere toochange esta contraseña durante su próximo iniciar sesión en tooAzure Active Directory.

### <a name="enable-self-service-password-reset"></a>Habilitar el autoservicio de restablecimiento de contraseña

contraseña de autoservicio de tooenable restablecer, siga los pasos de implementación de hello siguientes:

-   [Habilitar usuarios tooreset sus contraseñas de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Habilitar usuarios tooreset o cambiar sus contraseñas locales de Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Comprobar el estado de la autenticación multifactor de un usuario

toocheck un usuario de multifactor estado de autenticación, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  Haga clic en hello **la autenticación multifactor** situado en la parte superior de Hola de hoja de Hola.

7.  Una vez Hola **Portal de administración de Multi-factor Authentication** cargas, asegúrese de que esté en hello **usuarios** ficha.

8.  Busque el usuario de hello en lista de Hola de usuarios por búsqueda, el filtrado u ordenación.

9.  Usuario seleccione Hola Hola usuarios de lista y **habilitar**, **deshabilitar**, o **aplicar** la autenticación multifactor según sea necesario.

  * **Tenga en cuenta**: si un usuario pertenece a un **forzado** estado, puede establecerlos demasiado**deshabilitado** temporalmente toolet volverlos a su cuenta. Una vez que estén en, a continuación, puede cambiar su estado demasiado**habilitado** nuevo toorequire les toore su información de contacto durante su próximo iniciar sesión en el registro. Como alternativa, puede seguir los pasos de Hola Hola [Compruebe la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info) tooverify o establecer estos datos para ellos.

### <a name="check-a-users-authentication-contact-info"></a>Comprobar la información de contacto de autenticación de un usuario

toocheck autenticación de un usuario, póngase en contacto con información usada para la autenticación multifactor, acceso condicional, protección de identidad y de restablecimiento de contraseña, siga Hola pasos:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **Perfil**.

8.  Desplácese hacia abajo demasiado**información de contacto de autenticación**.

9.  **Revisión** datos Hola registrado para el usuario de Hola y actualizar según sea necesario.

### <a name="check-a-users-group-memberships"></a>Comprobar la pertenencia a grupos de un usuario

toocheck un usuario de pertenencia a grupos, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **grupos** toosee que agrupa usuario hello es un miembro de.

### <a name="check-a-users-assigned-licenses"></a>Comprobar las licencias asignadas de un usuario

toocheck un usuario había asignado licencias, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.

### <a name="assign-a-user-a-license"></a>Asignar una licencia a un usuario 

tooassign un usuario tooa de licencias, siga Hola pasos:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.

8.  Haga clic en hello **asignar** botón.

9.  Seleccione **uno o más productos** en lista de Hola de productos disponibles.

10. **Opcional** haga clic en hello **opciones de asignación** elemento toogranularly asignar productos. Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.

11. Haga clic en hello **asignar** botón tooassign estos usuario toothis de licencias.

## <a name="problems-with-groups"></a>Problemas con grupos

Acceso a la aplicación se puede bloquear debido tooa problema con un grupo que se asigna la aplicación toohello. A continuación se muestran algunas maneras de solucionar problemas con grupos y pertenencias a grupos:

-   [Comprobar la pertenencia de un grupo](#check-a-groups-membership)

-   [Comprobar los criterios de pertenencia de un grupo dinámico](#check-a-dynamic-groups-membership-criteria)

-   [Comprobar las licencias asignadas de un grupo](#check-a-groups-assigned-licenses)

-   [Volver a procesar las licencias de un grupo](#reprocess-a-groups-licenses)

-   [Asignar una licencia a un grupo](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a>Comprobar la pertenencia de un grupo

toocheck pertenencia de un grupo, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los grupos**.

6.  **Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **miembros** tooreview lista de Hola de usuarios asignados toothis grupo.

### <a name="check-a-dynamic-groups-membership-criteria"></a>Comprobar los criterios de pertenencia de un grupo dinámico 

toocheck criterios de pertenencia de un grupo dinámico, siga los pasos de hello siguientes:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los grupos**.

6.  **Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **Reglas de pertenencia dinámica**.

8.  Hola de revisión **simple** o **avanzadas** definida para este grupo de reglas y asegúrese de que ese usuario Hola desea toobe un miembro de este grupo cumple estos criterios.

### <a name="check-a-groups-assigned-licenses"></a>Comprobar licencias asignadas de un grupo

toocheck un grupo había asignado licencias, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los grupos**.

6.  **Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **licencias** toosee qué grupo de licencias Hola actualmente tiene asignada.

### <a name="reprocess-a-groups-licenses"></a>Volver a procesar las licencias de un grupo

tooreprocess un grupo había asignado licencias, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los grupos**.

6.  **Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **licencias** toosee qué grupo de licencias Hola actualmente tiene asignada.

8.  Haga clic en hello **volver a procesar** tooensure de botón que Hola miembros del grupo de licencias asignadas toothis están actualizados. Esto puede tardar mucho tiempo, en función de hello tamaño y la complejidad del grupo de Hola.

   >[!NOTE]
   >toodo esto con mayor rapidez, considere la posibilidad de temporalmente asignar una licencia toohello usuario directamente. [Asignar una licencia a un usuario](#problems-with-application-consent)
   >
   >

### <a name="assign-a-group-a-license"></a>Asignar una licencia a un grupo

tooassign un grupo de tooa licencias, siga Hola pasos:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los grupos**.

6.  **Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **licencias** toosee qué grupo de licencias Hola actualmente tiene asignada.

8.  Haga clic en hello **asignar** botón.

9.  Seleccione **uno o más productos** en lista de Hola de productos disponibles.

10. **Opcional** haga clic en hello **opciones de asignación** elemento toogranularly asignar productos. Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.

11. Haga clic en hello **asignar** botón tooassign estos toothis de grupo de licencias. Esto puede tardar mucho tiempo, en función de hello tamaño y la complejidad del grupo de Hola.

   >[!NOTE]
   >toodo esto con mayor rapidez, considere la posibilidad de temporalmente asignar una licencia toohello usuario directamente. [Asignar una licencia a un usuario](#problems-with-application-consent)
   > 
   >

## <a name="problems-with-conditional-access-policies"></a>Problemas con las directivas de acceso condicional

### <a name="check-a-specific-conditional-access-policy"></a>Comprobar una directiva de acceso condicional específica

toocheck o validar una directiva de acceso condicional único:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** en el menú de navegación de Hola.

5.  Haga clic en hello **acceso condicional** elemento de navegación.

6.  Haga clic en directiva de hello está interesado en inspeccionar.

7.  Revise que no haya condiciones, asignaciones u otras configuraciones específicas que puedan estar bloqueando el acceso del usuario.

   >[!NOTE]
   >Puede ser conveniente deshabilitar tootemporarily esta tooensure de directiva no afecta a toodo de componentes de inicio de sesión, Hola conjunto **habilitar Directiva de** alternar demasiado**No** y haga clic en hello **guardar** botón .
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a>Comprobar la directiva de acceso condicional de una aplicación específica

toocheck ni validar la directiva de acceso condicional configuradas actualmente un único de la aplicación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** en el menú de navegación de Hola.

5.  A continuación, haga clic en **Todas las aplicaciones**.

6.  Búsqueda de aplicación de hello interesa u Hola usuario está intentando toosign en aplicación tooby mostrar Id. de nombre o de la aplicación.

     >[!NOTE]
     >Si no ve la aplicación hello que está buscando, haga clic en hello **filtro** botón y extiende el ámbito de Hola de lista Hola demasiado**todas las aplicaciones**. Si desea toosee más columnas, haga clic en hello **columnas** botón tooadd detalles adicionales para las aplicaciones.
     >
     >

7.  Haga clic en hello **acceso condicional** elemento de navegación.

8.  Haga clic en directiva de hello está interesado en inspeccionar.

9.  Revise que no haya condiciones, asignaciones u otras configuraciones específicas que puedan estar bloqueando el acceso del usuario.

     >[!NOTE]
     >Puede ser conveniente deshabilitar tootemporarily esta tooensure de directiva no afecta a toodo de componentes de inicio de sesión, Hola conjunto **habilitar Directiva de** alternar demasiado**No** y haga clic en hello **guardar** botón .
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a>Deshabilitar una directiva de acceso condicional específica

toocheck o validar una directiva de acceso condicional único:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** en el menú de navegación de Hola.

5.  Haga clic en hello **acceso condicional** elemento de navegación.

6.  Haga clic en directiva de hello está interesado en inspeccionar.

7.  Deshabilitar directiva Hola Hola establecer **habilitar Directiva de** alternar demasiado**No** y haga clic en hello **guardar** botón.

## <a name="problems-with-application-consent"></a>Problemas con el consentimiento de aplicación

Acceso a la aplicación se puede bloquear porque no se ha producido la operación de consentimiento de los permisos adecuados de Hola. A continuación se muestran algunas maneras en que puede solucionar problemas relacionados con el consentimiento de aplicación:

-   [Realizar una operación de consentimiento de nivel de usuario](#perform-a-user-level-consent-operation)

-   [Realizar la operación de consentimiento de nivel de administrador para cualquier aplicación](#perform-administrator-level-consent-operation-for-any-application)

-   [Realizar el consentimiento de nivel de administrador para una aplicación de un solo inquilino](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [Realizar el consentimiento de nivel de administrador para una aplicación multiinquilino](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a>Realizar una operación de consentimiento de nivel de usuario

-   Para cualquier aplicación habilitada para abrir conectarse de Id. que solicita permisos, navegar por el inicio de sesión de la aplicación toohello en pantalla realiza una aplicación de toohello de nivel de consentimiento de usuario para el usuario que inició sesión Hola.

-   Si desea toodo esto mediante programación, vea [solicitar el consentimiento del usuario](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).

### <a name="perform-administrator-level-consent-operation-for-any-application"></a>Realizar la operación de consentimiento de nivel de administrador para cualquier aplicación

-   Para **sólo las aplicaciones desarrolladas con el modelo de aplicación Hola V1**, puede forzar este toooccur de nivel de consentimiento del administrador mediante la adición de "**? prompt = admin\_consentimiento**" toohello final de un inicio de sesión de la aplicación en la dirección URL.

-   Para **cualquier aplicación desarrollada con el modelo de aplicación Hola V2**, puede aplicar este toooccur de consentimiento de nivel de administrador, siga las instrucciones de hello en hello **solicitar permisos de Hola desde un directorio administración** sección de [con el extremo de consentimiento de administración de hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a>Realizar el consentimiento de nivel de administrador para una aplicación de un único inquilino

-   Para **único inquilino aplicaciones** que solicitan permisos (por ejemplo, aquellas que está desarrollando o el propietario de la organización), puede realizar un **consentimiento de nivel administrativo** operación en nombre de todos los los usuarios iniciar sesión como administrador Global y haciendo clic en hello **conceder permisos** situado en la parte superior de Hola de hello **el registro de aplicación -&gt; todas las aplicaciones -&gt; seleccione una aplicación: &gt; Permisos necesarios** hoja.

-   Para **cualquier aplicación desarrollada con Hola V1 o V2 modelo de aplicación**, puede aplicar este toooccur de consentimiento de nivel de administrador, siga las instrucciones de hello en hello **solicitar permisos de Hola a un Administrador de directorio** sección de [con el extremo de consentimiento de administración de hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a>Realizar el consentimiento de nivel de administrador para una aplicación multiinquilino

-   Para **aplicaciones multiinquilino** que solicitan permisos (como una aplicación que desarrolla un tercero o Microsoft), puede realizar una operación de **consentimiento de nivel administrativo**. Inicie sesión como administrador Global y haga clic en hello **conceder permisos** botón en hello **aplicaciones empresariales -&gt; todas las aplicaciones -&gt; seleccionar una aplicación -&gt; Permisos** hoja (disponible próximamente).

-   También puede aplicar este toooccur de consentimiento de nivel de administrador siguiendo las instrucciones de hello en hello **solicitar permisos de Hola desde un directorio de administrador** sección de [con el extremo de consentimiento de administración de hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

## <a name="next-steps"></a>Pasos siguientes
[Uso de extremo de consentimiento de administración de Hola](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

