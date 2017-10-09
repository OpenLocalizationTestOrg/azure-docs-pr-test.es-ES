---
title: "Tutorial: Configuración de GitHub para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario tooGitHub."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a>Tutorial: Configuración de GitHub para aprovisionar automáticamente usuarios


objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en GitHub y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooGitHub. 

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory
*   Un inquilino de Github con hello [plan de negocio](https://help.github.com/articles/organization-billing-plans/#business-plan) o mejor habilitado 
*   Una cuenta de usuario de GitHub con permisos de administrador 

> [!NOTE]
> Hello Azure AD aprovisionamiento integración se basa en hello [GitHub SCIM API](https://developer.github.com/v3/scim/), que son los equipos de tooGithub disponible en el plan de negocio de Hola o superior.

## <a name="assigning-users-toogithub"></a>Asignar usuarios tooGitHub

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD. 

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan tener acceso a la aplicación de GitHub de tooyour. Una vez decidido, puede asignar estas aplicaciones de GitHub de tooyour de usuarios siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a>Sugerencias importantes para asignar usuarios tooGitHub

*   Se recomienda que un único usuario de Azure AD se asigna tooGitHub tootest Hola aprovisionamiento de configuración. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar una tooGitHub de usuario, debe seleccionar cualquier hello **usuario** u otra válida específica de la aplicación rol (si está disponible) en el cuadro de diálogo de hello asignación. Hola **acceso predeterminado** rol no funciona para el aprovisionamiento y se omiten estos usuarios.


## <a name="configuring-user-provisioning-toogithub"></a>Configurar tooGitHub de aprovisionamiento de usuarios 

Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooGitHub de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en GitHub en función de asignación de usuario y de grupo en Azure AD.

> [!TIP]
> También puede elegir tooenabled basado en SAML Single Sign-On para GitHub, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a>Configurar aprovisionamiento tooGitHub en Azure AD de la cuenta de usuario automática


1. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

2. Si ya ha configurado GitHub para el inicio de sesión único, busque la instancia de GitHub con el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **GitHub** en Galería de aplicaciones de Hola. Seleccione GitHub de resultados de la búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

3. Seleccione la instancia de GitHub, a continuación, seleccione hello **Provisioning** ficha.

4. Conjunto hello **modo de aprovisionamiento** demasiado**automática**.

    ![Aprovisionamiento de GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. En hello **las credenciales de administrador** sección, haga clic en **Authorize**. Con esta operación se abre un cuadro de diálogo de autorización de GitHub en una nueva ventana del explorador. 

6. En la ventana nueva hello, inicie sesión en GitHub con su cuenta de administrador. Cuadro de diálogo de autorización resultante hello, seleccione el equipo de GitHub de Hola que desee tooenable aprovisionamiento para y, a continuación, seleccione **Authorize**. Hola de Azure toocomplete portal toohello una vez finalizado, vuelva aprovisionamiento de configuración.

    ![Cuadro de diálogo de autorización](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. En el portal de Azure hello, entrada **dirección URL del inquilino** y haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de GitHub de tooyour. Si se produce un error en la conexión de hello, asegúrese de que la cuenta de GitHub tiene permisos de administrador y **dirección URl del inquilino** se especifica correctamente, a continuación, intente Hola "Autorizar" vuelva a intentarlo (pueden constituir **dirección URL del inquilino** regla: "https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ", puede encontrar su organización en su cuenta de GitHub: **configuración** > **organizaciones**).

    ![Cuadro de diálogo de autorización](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y la casilla de verificación Hola "envían una notificación por correo electrónico cuando se produce un error."

9. Haga clic en **Guardar**. 

10. En la sección asignaciones de hello, seleccione **tooGitHub sincronizar Azure Active Directory Users**.

11. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooGitHub de Azure AD. Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch utilizados en GitHub para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

12. tooenable Hola servicio de aprovisionamiento de Azure AD para GitHub, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección

13. Haga clic en **Guardar**. 

Esta operación inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooGitHub Hola a los usuarios y la sección de grupos. la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio.

Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-enterprise-apps-manage-provisioning.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Pasos siguientes

* [Obtenga información acerca de cómo se registra tooreview y obtener informes sobre el aprovisionamiento de actividad](active-directory-saas-provisioning-reporting.md)
