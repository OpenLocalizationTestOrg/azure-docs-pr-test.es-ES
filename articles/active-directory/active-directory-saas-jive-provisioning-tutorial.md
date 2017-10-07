---
title: "Tutorial: Integración de Azure Active Directory con Jive | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Active Directory de Azure y Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a>Tutorial: Configuración de Jive para el aprovisionamiento de usuarios

objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en Jive y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooJive.

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory.
*   Una suscripción habilitada para inicio de sesión único en Jive.
*   Una cuenta de usuario de Jive con permisos de Team Admin (administrador de equipo).

## <a name="assigning-users-toojive"></a>Asignar usuarios tooJive

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso a la aplicación de Jive tooyour. Una vez decidido, puede asignar estas aplicaciones de Jive tooyour de usuarios siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a>Sugerencias importantes para asignar usuarios tooJive

*   Se recomienda que un único usuario de Azure AD asignarse tooJive tootest Hola aprovisionamiento de configuración. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar una tooJive de usuario, debe seleccionar un rol de usuario válido. rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.

## <a name="enable-user-provisioning"></a>Habilitación del aprovisionamiento de usuarios

Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooJive de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en Jive en función de asignación de usuario y de grupo en Azure AD.

> [!TIP]
> También puede elegir tooenabled basado en SAML Single Sign-On para Jive, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure aprovisionamiento de cuentas de usuario:

objetivo de Hola de esta sección es toooutline cómo tooenable el aprovisionamiento de usuarios de usuario de Active Directory cuentas tooJive.
Como parte de este procedimiento, se le tooprovide requiere un token de seguridad de usuario que deberá toorequest jive.com.

1. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

2. Si ya ha configurado Jive para el inicio de sesión único, busque la instancia de Jive mediante el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **Jive** en Galería de aplicaciones de Hola. Seleccione Jive de resultados de la búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

3. Seleccione la instancia de Jive, a continuación, seleccione hello **Provisioning** ficha.

4. Conjunto hello **modo de aprovisionamiento** demasiado**automática**. 

    ![Aprovisionamiento](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. En hello **las credenciales de administrador** sección, proporcione Hola siguientes opciones de configuración:
   
    a. Hola **nombre de usuario de administrador de Jive** cuadro de texto, tipo de un Jive nombre de cuenta que ha Hola **administrador del sistema** perfil en Jive.com asignado.
   
    b. Hola **contraseña de administrador de Jive** cuadro de texto, escriba la contraseña de Hola para esta cuenta.
   
    c. Hola **URL del inquilino de Jive** cuadro de texto URL de inquilino de Jive de tipo hello.
      
      > [!NOTE]
      > URL del inquilino de Jive Hello es la dirección URL que se usa por su toolog de organización en tooJive.  
      > Normalmente, la dirección URL de hello tiene Hola siguiendo el formato: **www.\< organización\>. jive.com**.          

6. Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de Jive de tooyour.

7. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y comprobar Hola casilla incluida a continuación.

8. Haga clic en **Guardar**.

9. En la sección asignaciones de hello, seleccione **tooJive sincronizar Azure usuarios de Active Directory.**

10. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooJive de Azure AD. Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del Hola toomatch utilizados en Jive para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

11. tooenable Hola servicio de aprovisionamiento de Azure AD para Jive, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración

12. Haga clic en **Guardar**.

Inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooJive Hola a los usuarios y la sección de grupos. la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de Jive.

Ahora puede crear una cuenta de prueba. Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooJive.

## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del inicio de sesión único](active-directory-saas-jive-tutorial.md)