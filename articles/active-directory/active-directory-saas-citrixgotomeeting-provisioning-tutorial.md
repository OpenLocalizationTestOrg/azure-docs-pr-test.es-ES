---
title: "Tutorial: Integración de Azure Active Directory con Citrix GoToMeeting | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a>Tutorial: Configuración de Citrix GoToMeeting para el aprovisionamiento automático de usuarios

objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en Citrix GoToMeeting y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooCitrix GoToMeeting.

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory.
*   Una suscripción habilitada para el inicio de sesión único en Citrix GoToMeeting.
*   Una cuenta de usuario de Citrix GoToMeeting con permisos de administrador de equipo.

## <a name="assigning-users-toocitrix-gotomeeting"></a>Asignar usuarios tooCitrix GoToMeeting

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso a tooyour aplicación Citrix GoToMeeting. Una vez decidido, puede asignar estas aplicaciones de Citrix GoToMeeting tooyour de usuarios siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a>Sugerencias importantes para asignar usuarios tooCitrix GoToMeeting

*   Se recomienda que un único usuario de Azure AD se asigna tooCitrix GoToMeeting tootest Hola aprovisionamiento de configuración. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar un tooCitrix usuario GoToMeeting, debe seleccionar un rol de usuario válido. rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.

## <a name="enable-automated-user-provisioning"></a>Habilitación del aprovisionamiento automático de usuarios

Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de Azure AD tooCitrix GoToMeeting y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas en Citrix GoToMeeting en función de usuario y de grupo de usuario asignado asignación de Azure AD.

> [!TIP]
> También puede elegir tooenabled basado en SAML Single Sign-On para Citrix GoToMeeting, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure aprovisionamiento de cuentas de usuario automática:

1. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

2. Si ya has configurado Citrix GoToMeeting para inicio de sesión único, busque la instancia de Citrix GoToMeeting con el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **Citrix GoToMeeting** en Galería de aplicaciones de Hola. Seleccione Citrix GoToMeeting en resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

3. Seleccione la instancia de Citrix GoToMeeting, a continuación, seleccione hello **Provisioning** ficha.

4. Conjunto hello **Provisioning** modo demasiado**automática**. 

    ![Aprovisionamiento](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. En la sección credenciales de administrador de hello, realizar Hola pasos:
   
    a. Hola **nombre de usuario de administrador de Citrix GoToMeeting** cuadro de texto, escriba el nombre de usuario de Hola de un administrador.

    b. Hola **contraseña de administrador de Citrix GoToMeeting** cuadro de texto de contraseña del Administrador de Hola.

6. Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectarse tooyour aplicación Citrix GoToMeeting. Si se produce un error en la conexión de hello, asegúrese de que su cuenta de Citrix GoToMeeting tiene permisos de administrador de equipo e inténtelo de hello **"Credenciales de administrador"** vuelva a intentarlo.

7. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y active casilla Hola.

8. Haga clic en **Guardar**.

9. En la sección asignaciones de hello, seleccione **sincronizar Azure Active Directory Users tooCitrix GoToMeeting.**

10. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde Azure AD tooCitrix GoToMeeting. Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en Citrix GoToMeeting para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

11. tooenable Hola servicio de aprovisionamiento de Azure AD para Citrix GoToMeeting, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración

12. Haga clic en **Guardar**.

Inicia la sincronización inicial de Hola de los usuarios o grupos asignados tooCitrix GoToMeeting en la sección usuarios y grupos de Hola. la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de Citrix GoToMeeting.

## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del inicio de sesión único](active-directory-saas-citrix-gotomeeting-tutorial.md)


