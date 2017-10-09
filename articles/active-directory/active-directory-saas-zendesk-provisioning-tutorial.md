---
title: "Tutorial: Configuración de ZenDesk para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario tooZenDesk."
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a>Tutorial: Configuración de ZenDesk para aprovisionar automáticamente usuarios


objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en ZenDesk y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooZenDesk. 

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory
*   Un inquilino de ZenDesk con hello [plan empresarial](https://www.zendesk.com/product/pricing/) o mejor habilitado 
*   Una cuenta de usuario de ZenDesk con permisos de administrador 

> [!NOTE]
> Hello Azure AD aprovisionamiento integración se basa en hello [API de REST de ZenDesk](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), que son los equipos de tooZenDesk disponible en plan esenciales de Hola o superior.

## <a name="assigning-users-toozendesk"></a>Asignar usuarios tooZenDesk

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincronizan sólo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD. 

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan tener acceso a la aplicación de ZenDesk tooyour. Una vez decidido, puede asignar estas aplicaciones de ZenDesk de tooyour de usuarios siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a>Sugerencias importantes para asignar usuarios tooZenDesk

*   Se recomienda que un único usuario de Azure AD se asigna tooZenDesk tootest Hola aprovisionamiento de configuración. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar una tooZenDesk de usuario, debe seleccionar cualquier hello **usuario** u otra válida específica de la aplicación rol (si está disponible) en el cuadro de diálogo de hello asignación. Hola **acceso predeterminado** rol no funciona para el aprovisionamiento y se omiten estos usuarios.

> [!NOTE]
> Como una característica agregada, Hola aprovisionamiento del servicio lee los roles personalizados definidos en Zendesk y las importa en Azure AD donde se pueden seleccionar en el cuadro de diálogo de hello Seleccionar rol. Estos roles se verán en hello portal de Azure después de hello aprovisionamiento del servicio está habilitado y ha completado un ciclo de sincronización.

## <a name="configuring-user-provisioning-toozendesk"></a>Configurar tooZenDesk de aprovisionamiento de usuarios 

Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooZenDesk de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en ZenDesk en función de asignación de usuario y de grupo en Azure AD.

> [!TIP] 
> También puede elegir tooenabled basado en SAML Single Sign-On para ZenDesk, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a>Configurar aprovisionamiento tooZenDesk en Azure AD de la cuenta de usuario automática


1. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

2. Si ya ha configurado ZenDesk para el inicio de sesión único, busque la instancia de ZenDesk con el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **ZenDesk** en Galería de aplicaciones de Hola. Seleccione ZenDesk de resultados de la búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

3. Seleccione la instancia de ZenDesk, a continuación, seleccione hello **Provisioning** ficha.

4. Conjunto hello **modo de aprovisionamiento** demasiado**automática**.

    ![Aprovisionamiento de ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. En hello **credenciales de administrador de** Hola de entrada, en una sección **administrador Username, tokenkey & dominio** generados por cuenta de su ZenDesk (puede encontrar el token de hello en su cuenta: **Admin**   >  **API** > **configuración**). 

    ![Aprovisionamiento de ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de ZenDesk de tooyour. Si se produce un error en la conexión de hello, asegúrese de que su cuenta de ZenDesk tiene permisos de administrador e inténtelo de nuevo el paso 5.

7. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y la casilla de verificación Hola "envían una notificación por correo electrónico cuando se produce un error."

8. Haga clic en **Guardar**. 

9. En la sección asignaciones de hello, seleccione **tooZenDesk sincronizar Azure Active Directory Users**.

10. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooZenDesk de Azure AD. Hola atributos seleccionados como **coincidencia** propiedades son toomatch usado hello las cuentas de usuario en ZenDesk para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

11. tooenable Hola servicio de aprovisionamiento de Azure AD para ZenDesk, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección

12. Haga clic en **Guardar**. 

Esta operación inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooZenDesk Hola a los usuarios y la sección de grupos. la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio.

Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-enterprise-apps-manage-provisioning.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Pasos siguientes

* [Obtenga información acerca de cómo se registra tooreview y obtener informes sobre el aprovisionamiento de actividad](active-directory-saas-provisioning-reporting.md)
