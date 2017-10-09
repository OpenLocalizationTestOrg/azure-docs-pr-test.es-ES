---
title: "Tutorial: Configuración de LucidChart para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario tooLucidChart."
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
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a>Tutorial: Configuración de LucidChart para aprovisionar a los usuarios automáticamente


objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en LucidChart y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooLucidChart. 

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory
*   Un inquilino de LucidChart con hello [plan empresarial](https://www.lucidchart.com/user/117598685#/subscriptionLevel) o mejor habilitado 
*   Una cuenta de usuario de LucidChart con permisos de administrador 

## <a name="assigning-users-toolucidchart"></a>Asignar usuarios tooLucidChart

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD. 

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan tener acceso a la aplicación de LucidChart tooyour. Una vez decidido, puede asignar estas aplicaciones de LucidChart tooyour de usuarios siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a>Sugerencias importantes para asignar usuarios tooLucidChart

*   Se recomienda que un único usuario de Azure AD se asigna tooLucidChart tootest Hola aprovisionamiento de configuración. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar una tooLucidChart de usuario, debe seleccionar cualquier hello **usuario** u otra válida específica de la aplicación rol (si está disponible) en el cuadro de diálogo de hello asignación. Hola **acceso predeterminado** rol no funciona para el aprovisionamiento y se omiten estos usuarios.


## <a name="configuring-user-provisioning-toolucidchart"></a>Configurar tooLucidChart de aprovisionamiento de usuarios 

Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooLucidChart de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en LucidChart en función de asignación de usuario y de grupo en Azure AD .

> [!TIP]
> También puede elegir tooenabled basado en SAML Single Sign-On para LucidChart, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a>Configurar aprovisionamiento tooLucidChart en Azure AD de la cuenta de usuario automática


1. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

2. Si ya ha configurado LucidChart para el inicio de sesión único, busque la instancia de LucidChart con el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **LucidChart** en Galería de aplicaciones de Hola. Seleccione LucidChart en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

3. Seleccione la instancia de LucidChart, a continuación, seleccione hello **Provisioning** ficha.

4. Conjunto hello **modo de aprovisionamiento** demasiado**automática**.

    ![Aprovisionamiento de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. En hello **credenciales de administrador** entrada hello, en una sección **secreto del Token** generados por cuenta de su LucidChart (puede encontrar el token de hello en su cuenta: **equipo**  >  **Integración de aplicaciones** > **SCIM**). 

    ![Aprovisionamiento de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de LucidChart de tooyour. Si se produce un error en la conexión de hello, asegúrese de que su cuenta de LucidChart tiene permisos de administrador e inténtelo de nuevo el paso 5.

7. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y la casilla de verificación Hola "envían una notificación por correo electrónico cuando se produce un error."

8. Haga clic en **Guardar**. 

9. En la sección asignaciones de hello, seleccione **tooLucidChart sincronizar Azure Active Directory Users**.

10. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooLucidChart de Azure AD. Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del Hola toomatch utilizados en LucidChart para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

11. tooenable Hola servicio de aprovisionamiento de Azure AD para LucidChart, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección

12. Haga clic en **Guardar**. 

Esta operación inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooLucidChart Hola a los usuarios y la sección de grupos. la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio.

Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-enterprise-apps-manage-provisioning.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Pasos siguientes

* [Obtenga información acerca de cómo se registra tooreview y obtener informes sobre el aprovisionamiento de actividad](active-directory-saas-provisioning-reporting.md)
