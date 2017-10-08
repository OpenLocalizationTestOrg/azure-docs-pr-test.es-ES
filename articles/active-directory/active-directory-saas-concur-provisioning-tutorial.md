---
title: "Tutorial: integración de Azure Active Directory con Concur | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a>Tutorial: Configuración de Concur para el aprovisionamiento de usuarios

objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en Concur y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooConcur.

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory.
*   Una suscripción habilitada para el inicio de sesión único en Concur.
*   Una cuenta de usuario de Concur con permisos de administrador de equipo.

## <a name="assigning-users-tooconcur"></a>Asignar usuarios tooConcur

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan acceder a la aplicación de Concur de tooyour. Una vez decidido, puede asignar estas aplicaciones de Concur de tooyour de usuarios siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a>Sugerencias importantes para asignar usuarios tooConcur

*   Se recomienda que un único usuario de Azure AD asignarse tooConcur tootest Hola aprovisionamiento de configuración. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar una tooConcur de usuario, debe seleccionar un rol de usuario válido. rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.

## <a name="enable-user-provisioning"></a>Habilitación del aprovisionamiento de usuarios

Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooConcur de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en Concur en función de asignación de usuario y de grupo en Azure AD.

> [!Tip] 
> También puede elegir tooenabled basado en SAML Single Sign-On para Concur, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure aprovisionamiento de cuentas de usuario:

objetivo de Hola de esta sección es toooutline cómo tooenable aprovisionamiento de usuario de Active Directory de cuentas de tooConcur.

aplicaciones de tooenable en Hola servicio de gastos, tiene la configuración correcta de toobe y el uso de un perfil de administrador de servicios Web. No agregue Hola administrador WS rol tooyour perfil de administrador existente que usa para las funciones administrativas de T & E.

Asesores de concur o administrador de clientes de hello debe crear un perfil de administrador de servicios Web distintos y Administrador de clientes de hello debe utilizar este perfil para las funciones de administrador de servicios Web de hello (por ejemplo, al habilitar aplicaciones). Estos perfiles deben estar separados de diaria T & Usar perfil de administrador del administrador del cliente de hello (Hola T & perfil de administrador E no deben tener asignado el rol de hello WSAdmin).

Cuando creas Hola perfil toobe utilizado para habilitar la aplicación hello, escriba nombre del administrador del cliente de hello en campos de perfil de usuario de Hola. Esto asigna perfil toohello de propiedad. Una vez que se crea uno o varios perfiles, cliente hello debe iniciar sesión con esta hello tooclick de perfil "*habilitar*" botón para una aplicación asociada en el menú de servicios Web de Hola.

Para hello después de motivos, esta acción no debería realizarse con perfil de Hola que utiliza para la administración de T & E normal.

* Hello cliente tiene toobe Hola que hace clic en "*Sí*" en la ventana de cuadro de diálogo de Hola que aparece después de habilita una aplicación. Haga clic en confirma cliente Hola considera para tooaccess de aplicación de socio comercial de hello sus datos, por lo que usted u Hola asociado no puede hacer clic que el botón Sí.

* Si un administrador de cliente que ha habilitado una aplicación con hello T & perfil de administrador E deja empresa hello (lo que se desactiva el perfil de hello), las aplicaciones habilitadas con ese perfil no funcionará hasta que se habilite la aplicación hello con otro administrador WS activo perfil. Este es el motivo por el que se supone toocreate distintos perfiles de administrador de WS.

* Si un administrador deja la empresa de hello, nombre de hello asociado toohello perfil de administrador WS puede ser administrador de reemplazo de toohello modificadas si lo desea, sin afectar a Hola habilitado, aplicación porque no es necesario que ese perfil no activado.

**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**

1. Inicie sesión en tooyour **Concur** inquilino.

2. De hello **administración** menú, seleccione **servicios Web**.
   
    ![Inquilino de Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Inquilino de Concur")

3. En hello lado izquierdo, de hello **servicios Web** panel, seleccione **habilitar aplicación de socio**.
   
    ![Habilitar aplicación de asociado](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Habilitar aplicación de asociado")

4. De hello **habilitar aplicación** lista, seleccione **Azure Active Directory**y, a continuación, haga clic en **habilitar**.
   
    ![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")

5. Haga clic en **Sí** tooclose hello **Confirmar acción** cuadro de diálogo.
   
    ![Confirmar acción](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirmar acción")

6. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

7. Si ya ha configurado Concur para el inicio de sesión único, busque la instancia de Concur con el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **Concur** en Galería de aplicaciones de Hola. Seleccione Concur en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

8. Seleccione la instancia de Concur, a continuación, seleccione hello **Provisioning** ficha.

9. Conjunto hello **modo de aprovisionamiento** demasiado**automática**. 
 
    ![Aprovisionamiento](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. En hello **las credenciales de administrador** sección, escriba Hola **nombre de usuario** hello y **contraseña** de su administrador de Concur.

11. Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de Concur de tooyour. Si se produce un error en la conexión de hello, asegúrese de que la cuenta de Concur tiene permisos de administrador de equipo.

12. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y active casilla Hola.

13. Haga clic en **Guardar**.

14. En la sección asignaciones de hello, seleccione **tooConcur sincronizar Azure usuarios de Active Directory.**

15. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooConcur de Azure AD. Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch utilizados en Concur para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

16. tooenable Hola servicio de aprovisionamiento de Azure AD para Concur, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección

17. Haga clic en **Guardar**.

Ahora puede crear una cuenta de prueba. Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooConcur.

## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del inicio de sesión único](active-directory-saas-concur-tutorial.md)

