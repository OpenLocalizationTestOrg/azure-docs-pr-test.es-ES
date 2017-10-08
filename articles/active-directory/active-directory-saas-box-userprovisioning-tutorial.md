---
title: "Tutorial: Integración de Azure Active Directory con Box | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e92baabb174642c22c99e2a30bc9c71845b3b75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a>Tutorial: Configuración de Box para aprovisionar automáticamente usuarios

objetivo de Hola de este tutorial es tooshow Hola pasos tooperform en cuadro y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario del cuadro de herramientas de Azure AD.

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory.
*   Una suscripción a Box habilitada para el inicio de sesión único.
*   Una cuenta de usuario de Box con permisos de administrador de equipo.

## <a name="assigning-users-toobox"></a>Asignación de cuadro de herramientas de los usuarios 

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan tener acceso a la aplicación de Box tooyour. Una vez decidido, puede asignar estas aplicaciones de cuadro de tooyour de usuarios siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a>Asignación de usuarios y grupos
Hola **cuadro > usuarios y grupos** ficha Hola portal de Azure permite toospecify qué usuarios y grupos se debe conceder acceso a cuadro de herramientas. Asignación de un usuario o grupo hace Hola después toooccur cosas:

* Azure AD permite que el cuadro de herramientas de hello asignado usuario (ya sea mediante la asignación directa o pertenencia al grupo) tooauthenticate. Si no se asigna un usuario, Azure AD no permitir toosign en el cuadro de herramientas y devuelve un error en la página de inicio de sesión de Azure AD de Hola.
* El icono de una aplicación de cuadro se agrega del usuario toohello [iniciador de la aplicación](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).
* Si está habilitado el aprovisionamiento automático, Hola asigna usuarios o grupos se agregan toohello toobe cola aprovisionada automáticamente el aprovisionamiento.
  
  * Si solo objetos de usuario configurado toobe aprovisionado, a continuación, todos los usuarios directamente asignados se colocan en cola de aprovisionamiento de Hola y todos los usuarios que son miembros de los grupos asignados se colocan en hello aprovisionamiento de cola. 
  * Si los objetos de grupo estaban configurado toobe aprovisionado, todos los objetos de grupo asignado son aprovisionado de cuadro de herramientas y todos los usuarios que son miembros de esos grupos. pertenencia a grupos y usuarios de Hola se conserva cuando se escribe el cuadro de herramientas.

Puede usar hello **atributos > Single Sign-On** ficha tooconfigure qué atributos de usuario (o notificaciones) se presenta cuadro de herramientas durante la autenticación basada en SAML y hello **atributos > aprovisionamiento** pestaña tooconfigure cómo fluyen de atributos de usuario y grupo de cuadro de herramientas de Azure AD durante el aprovisionamiento de las operaciones.

### <a name="important-tips-for-assigning-users-toobox"></a>Sugerencias importantes para la asignación de cuadro de herramientas de los usuarios 

*   Se recomienda que un anuncio de Azure solo configuración de aprovisionamiento de usuario asignado cuadro de herramientas tootest Hola. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar un cuadro de herramientas de usuario, debe seleccionar un rol de usuario válido. rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.

## <a name="enable-automated-user-provisioning"></a>Habilitación del aprovisionamiento automático de usuarios

En esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su cuadro de herramientas AD de Azure y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en el cuadro en función de asignación de usuario y de grupo en Azure AD.

Si está habilitado el aprovisionamiento automático, Hola asigna usuarios o grupos se agregan toohello toobe cola aprovisionada automáticamente el aprovisionamiento.
    
 * Si solo los objetos de usuario son toobe configurado aprovisionado asignados directamente a los usuarios se colocan en cola de aprovisionamiento de Hola y todos los usuarios que son miembros de los grupos asignados se colocan en hello aprovisionamiento de cola. 
    
 * Si los objetos de grupo estaban configurado toobe aprovisionado, todos los objetos de grupo asignado son aprovisionado de cuadro de herramientas y todos los usuarios que son miembros de esos grupos. pertenencia a grupos y usuarios de Hola se conserva cuando se escribe el cuadro de herramientas.

> [!TIP] 
> También puede elegir tooenabled basado en SAML Single Sign-On para cuadro, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure aprovisionamiento de cuentas de usuario automática:

objetivo de Hola de esta sección es toooutline cómo tooenable aprovisionamiento de usuario de Active Directory de cuentas de cuadro de herramientas.

1. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

2. Si ya ha configurado el cuadro de inicio de sesión único, busque la instancia del cuadro con el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **cuadro** en Galería de aplicaciones de Hola. Active la casilla de resultados de la búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

3. Seleccione la instancia del cuadro y haga clic hello **Provisioning** ficha.

4. Conjunto hello **modo de aprovisionamiento** demasiado**automática**. 

    ![Aprovisionamiento](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. En hello **las credenciales de administrador** sección, haga clic en **Authorize** tooopen un cuadro de diálogo de inicio de sesión en una nueva ventana del explorador.

6. En hello **cuadro de herramientas de acceso de inicio de sesión toogrant** página, proporcione las credenciales de hello necesario y, a continuación, haga clic en **Authorize**. 
   
    ![Habilitar el aprovisionamiento automático de usuarios](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Habilitar aprovisionamiento automático de usuarios")

7. Haga clic en **el cuadro de herramientas de conceder acceso** tooauthorize esta operación y tooreturn toohello portal de Azure. 
   
    ![Habilitar el aprovisionamiento automático de usuarios](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Habilitar aprovisionamiento automático de usuarios")

8. Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectarse tooyour cuadro aplicación. Si se produce un error en la conexión de hello, asegúrese de que su cuenta Box tiene permisos de administrador de equipo e inténtelo de hello **"Autorizar"** vuelva a intentarlo.

9. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y active casilla Hola.

10. Haga clic en **Guardar**.

11. En la sección asignaciones de hello, seleccione **cuadro de herramientas de sincronizar Azure usuarios de Active Directory.**

12. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde el cuadro de herramientas de Azure AD. Hola atributos seleccionados como **coincidencia** propiedades son toomatch usado hello las cuentas de usuario en el cuadro de las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

13. tooenable Hola servicio de aprovisionamiento de Azure AD para cuadro, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración

14. Haga clic en **Guardar**.

Que inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados de cuadro de herramientas en los usuarios de Hola y sección de grupos. la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de cuadro.

Ahora puede crear una cuenta de prueba. Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado el cuadro de herramientas.

En el inquilino de Box, los usuarios sincronizados se enumeran debajo **usuarios administrados** en hello **consola de administración de**.

![Estado de integración](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Estado de integración")


## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del inicio de sesión único](active-directory-saas-box-tutorial.md)