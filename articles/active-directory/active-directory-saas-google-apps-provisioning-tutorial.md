---
title: "Tutorial: Configuración de Google Apps para el aprovisionamiento automático de usuarios en Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooGoogle aplicaciones."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>Tutorial: Configuración de Google Apps para aprovisionar a los usuarios automáticamente

objetivo de Hola de este tutorial es tooshow que Hola pasos necesita tooperform en Google Apps y Azure AD tooautomatically el aprovisionamiento y Desaprovisionamiento de cuentas de usuario de Azure AD tooGoogle aplicaciones.

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory.
*   Debe tener un inquilino válido para Google Apps for Work o Google Apps for Education. Puede usar una cuenta de prueba gratuita de cualquiera de los servicios.
*   Una cuenta de usuario de Google Apps con permisos de administrador de equipo.

## <a name="assigning-users-toogoogle-apps"></a>Asignación de usuarios tooGoogle aplicaciones

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso a la aplicación de Google Apps tooyour. Una vez decidido, puede asignar estas aplicaciones de Google Apps tooyour usuarios siguiendo las instrucciones de hello aquí: [asignar una aplicación de empresa de tooan de usuario o grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   Se recomienda que un único usuario de Azure AD asignarse hello tootest tooGoogle aplicaciones que configuración de aprovisionamiento. Más tarde, se pueden asignar otros usuarios o grupos.
>*   Al asignar un usuario tooGoogle aplicaciones, debe seleccionar Hola usuario o rol de "Grupo" en el cuadro de diálogo de hello asignación. rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.

## <a name="enable-automated-user-provisioning"></a>Habilitación del aprovisionamiento automático de usuarios

Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de las aplicaciones tooGoogle de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en Google Apps en función de asignación de usuario y de grupo en Azure AD .

>[!Tip]
>También puede elegir tooenabled basado en SAML Single Sign-On para Google Apps, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.

### <a name="configure-automatic-user-account-provisioning"></a>Configurar el aprovisionamiento automático de cuentas de usuario

> [!NOTE]
> Otra opción viable para automatizar aplicaciones de tooGoogle de aprovisionamiento de usuarios es toouse [sincronización de directorio de aplicaciones de Google (GADS)](https://support.google.com/a/answer/106368?hl=en) que aprovisiona la tooGoogle de identidades de Active Directory local las aplicaciones. En cambio, solución hello en este tutorial proporciona a los usuarios de Azure Active Directory (nube) y los grupos habilitados para correo tooGoogle aplicaciones. 

1. Inicio de sesión en hello [consola de administración de aplicaciones de Google](http://admin.google.com/) con su cuenta de administrador y haga clic en **seguridad**. Si no ve el vínculo de hello, puede estar oculto bajo hello **más controles** menú situado en la parte inferior de Hola de pantalla de bienvenida.
   
    ![Haga clic en Seguridad.][10]

2. En hello **seguridad** página, haga clic en **referencia de la API**.
   
    ![Haga clic en la referencia de la API.][15]

3. Seleccione **Enable API access**.
   
    ![Haga clic en la referencia de la API.][16]

    > [!IMPORTANT]
    > Para cada usuario que piensa tooprovision tooGoogle aplicaciones, su nombre de usuario en Azure Active Directory *debe* ser tooa relacionados de dominio personalizado. Por ejemplo, Google Apps no acepta los nombres de usuario parecidos a bob@contoso.onmicrosoft.com, mientras que bob@contoso.com se acepta. Puede cambiar el dominio de un usuario existente editando sus propiedades en Azure AD. Instrucciones de cómo se incluyen tooset un dominio personalizado para Azure Active Directory y Google Apps en lo siguiente.
      
4. Si no ha agregado todavía un tooyour de nombre de dominio personalizado Azure Active Directory, a continuación, siga Hola pasos:
  
    a. Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**. En la lista de directorios de hello, seleccione el directorio. 

    b. Haga clic en **nombre de los dominios** en Hola panel de navegación izquierdo y, a continuación, haga clic en **agregar**.
     
     ![dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![agregar un dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Escriba el nombre de dominio en hello **nombre de dominio** campo. Este nombre de dominio debe ser Hola mismo nombre de dominio que piensa toouse para Google Apps. Cuando esté listo, haga clic en hello **Agregar dominio** botón.
     
     ![nombre de dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. Haga clic en **siguiente** página de comprobación de toogo toohello. tooverify que posee este dominio, debe editar los registros DNS del dominio de hello según los valores de toohello incluidos en esta página. Puede elegir tooverify mediante **registros MX** o **registros TXT**, en función de lo que seleccione para hello **tipo de registro** opción. Para obtener instrucciones detalladas sobre cómo el nombre de dominio tooverify con Azure AD, consulte [agregar su propios tooAzure de nombre de dominio AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).
     
     ![dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. Repita los pasos para todos los dominios de Hola que piensa tooadd tooyour directory anteriores de Hola.

5. Ahora que ha comprobado todos los dominios con Azure AD, debe comprobarlos de nuevo con Google Apps. Para cada dominio que ya no está registrado con Google Apps, siga Hola pasos:
   
    a. Hola [consola de administración de aplicaciones de Google](http://admin.google.com/), haga clic en **dominios**.
     
     ![Haga clic en Dominios][20]

    b. Haga clic en **Agregar un dominio o un alias de dominio**.
     
     ![Adición de un nuevo dominio][21]

    c. Seleccione **agregar otro dominio**y escriba Hola nombre de dominio de Hola que desearía tooadd.
     
     ![Especificación de un nombre de dominio][22]

    d. Haga clic en **Continuar y comprobar la propiedad del dominio**. A continuación, siga Hola pasos tooverify si su propio nombre de dominio de Hola. Para obtener instrucciones completas sobre cómo tooverify su dominio con Google Apps, vea. [Verificar que eres el propietario del sitio web](https://support.google.com/webmasters/answer/35179).

    e. Repita los pasos para todos los dominios adicionales que piensa tooadd tooGoogle aplicaciones anteriores de Hola.
     
     > [!WARNING]
     > Si cambiar dominio principal de hello para el inquilino de Google Apps, y si ya ha configuran el inicio de sesión único con Azure AD, entonces tiene toorepeat paso 3 de # bajo [paso dos: habilitar Single Sign-On](#step-two-enable-single-sign-on).
       
6. Hola [consola de administración de aplicaciones de Google](http://admin.google.com/), haga clic en **Roles de administrador**.
   
     ![Haga clic en Google Apps][26]

7. Determinar qué Administrador de cuenta le gustaría toomanage toouse el aprovisionamiento de usuarios. Para hello **rol de administrador** de esa cuenta, editar hello **privilegios** para ese rol. Asegúrese de que tiene todos los hello **privilegios de administrador API** habilitado para que esta cuenta puede utilizarse para el aprovisionamiento.
   
     ![Haga clic en Google Apps][27]
   
    > [!NOTE]
    > Si va a configurar un entorno de producción, se recomienda hello es toocreate una cuenta de administrador en Google Apps específicamente para este paso. Estas cuentas deben tener asociado un rol de administrador que tenga privilegios de API necesarias de Hola.
     
8. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

9. Si ya has configurado Google Apps para el inicio de sesión único, busque la instancia de Google Apps con el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **Google Apps** en Galería de aplicaciones de Hola. Seleccionar aplicaciones de Google de resultados de la búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

10. Seleccione la instancia de Google Apps, a continuación, seleccione hello **Provisioning** ficha.

11. Conjunto hello **modo de aprovisionamiento** demasiado**automática**. 

     ![Aprovisionamiento](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. En hello **las credenciales de administrador** sección, haga clic en **Authorize**. Se abrirá un cuadro de diálogo de autorización de Google Apps en una nueva ventana del explorador.

13. Confirme que desea que los cambios de toomake toogive Azure Active Directory permiso de inquilinos tooyour Google Apps. Haga clic en **Aceptar**.
    
     ![Confirme los permisos.][28]

14. Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de Google Apps tooyour. Si se produce un error en la conexión de hello, asegúrese de que su cuenta de Google Apps tiene permisos de administrador de equipo e inténtelo de hello **"Autorizar"** vuelva a intentarlo.

15. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y active casilla Hola.

16. Haga clic en **Guardar**.

17. En la sección asignaciones de hello, seleccione **sincronizar Azure Active Directory Users tooGoogle aplicaciones.**

18. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooGoogle aplicaciones de Azure AD. Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en Google Apps para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

19. tooenable Hola servicio de aprovisionamiento de Azure AD para Google Apps, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración

20. Haga clic en **Guardar**.

Inicia la sincronización inicial de Hola de los usuarios o grupos asignados tooGoogle aplicaciones en la sección usuarios y grupos de Hola. la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de Google Apps.

## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del inicio de sesión único](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png