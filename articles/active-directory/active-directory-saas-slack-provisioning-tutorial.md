---
title: "Tutorial: Configuración de Slack para aprovisionar automáticamente usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario tooSlack."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a>Tutorial: Configuración de Slack para aprovisionar automáticamente usuarios


Hola objetivo de este tutorial es tooshow Hola pasos que debe tooperform en Slack y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooSlack. 

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de directorio de Azure Active Directory
*   Una demora de inquilinos con hello [Plus plan](https://aadsyncfabric.slack.com/pricing) o mejor habilitado 
*   Una cuenta de usuario de Slack con permisos de administrador de equipo 

Nota: Hola aprovisionamiento de integración de Azure AD se basa en hello [Slack SCIM API](https://api.slack.com/scim) que son los equipos de tooSlack disponible en hello además de plan o superior.

## <a name="assigning-users-tooslack"></a>Asignar usuarios tooSlack

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincronizarán sólo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD. 

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesitará toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan acceder a la aplicación de demora de tooyour. Una vez decidido, puede asignar estas aplicaciones de demora de tooyour de usuarios siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a>Sugerencias importantes para asignar usuarios tooSlack

*   Se recomienda que un único usuario de Azure AD asignarse tooSlack tootest Hola aprovisionamiento de configuración. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar una tooSlack de usuario, debe seleccionar hello **usuario** o el rol de "Grupo" en el cuadro de diálogo de hello asignación. rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.


## <a name="configuring-user-provisioning-tooslack"></a>Configurar tooSlack de aprovisionamiento de usuarios 

Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooSlack de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en demora en función de asignación de usuario y de grupo en Azure AD.

**Sugerencia:** también puede elegir tooenabled basado en SAML Single Sign-On para Slack, siguiendo instrucciones de hello proporcionadas en (portal de Azure) [https://portal.azure.com]. El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a>cuenta de usuario automática de tooconfigure tooSlack de aprovisionamiento en Azure AD:


1)  Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

2) Si ya ha configurado la demora de inicio de sesión único, busque la instancia de demora mediante el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **Slack** en Galería de aplicaciones de Hola. Seleccione demora en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

3)  Seleccione la instancia de demora, a continuación, seleccione hello **Provisioning** ficha.

4)  Conjunto hello **modo de aprovisionamiento** demasiado**automática**.

![Aprovisionamiento de Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  En hello **las credenciales de administrador** sección, haga clic en **Authorize**. Se abrirá un cuadro de diálogo de autorización de Slack en una nueva ventana del explorador. 

6) En la ventana nueva hello, inicie sesión en Slack con su cuenta de administrador de equipo. cuadro de diálogo de autorización resultante hello, seleccione Hola demora equipo que desea tooenable aprovisionamiento para y, a continuación, seleccione **Authorize**. Hola de Azure toocomplete portal toohello una vez finalizado, vuelva aprovisionamiento de configuración.

![Cuadro de diálogo de autorización](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectar la aplicación de demora de tooyour. Si se produce un error en la conexión de hello, asegúrese de que su cuenta de demora tiene permisos de administrador de equipo e intente Hola "Autorizar" vuelva a intentarlo.

8) Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y comprobar Hola casilla incluida a continuación.

9) Haga clic en **Guardar**. 

10) En la sección asignaciones de hello, seleccione **tooSlack sincronizar Azure Active Directory Users**.

11) Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizarán desde tooSlack de Azure AD. Tenga en cuenta que Hola atributos seleccionados como **coincidencia** propiedades estarán toomatch usa cuentas de usuario de hello en Slack para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

12) tooenable Hola servicio de aprovisionamiento de Azure AD para Slack, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección

13) Haga clic en **Guardar**. 

Esto iniciará la sincronización inicial de Hola de todos los usuarios y grupos asignados tooSlack Hola a los usuarios y la sección de grupos. Tenga en cuenta que la sincronización inicial de hello surtirá tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 10 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de la demora.

## <a name="optional-configuring-group-object-provisioning-tooslack"></a>[Opcional] Configuración de aprovisionamiento tooSlack un objeto de grupo 

Si lo desea, puede habilitar Hola de aprovisionamiento de objetos de grupo de tooSlack de Azure AD. Esto es diferente de "asignación de grupos de usuarios", en ese objeto de grupo real de hello además tooits miembros se replicarán desde tooSlack de Azure AD. Por ejemplo, si tiene un grupo denominado "Mi grupo" en Azure AD, se creará un grupo idéntico denominado "Mi grupo" en Slack.

### <a name="tooenable-provisioning-of-group-objects"></a>tooenable el aprovisionamiento de objetos de grupo:

1) En la sección asignaciones de hello, seleccione **tooSlack sincronizar Azure grupos de Active Directory**.

2) En la hoja de la asignación de atributos de hello, establezca tooYes habilitado.

3) Hola **asignaciones de atributos** sección, revise los atributos de grupo de Hola que se sincronizarán desde tooSlack de Azure AD. Tenga en cuenta que Hola atributos seleccionados como **coincidencia** propiedades estarán toomatch usa grupos de hello en Slack para las operaciones de actualización. 

4) Haga clic en **Guardar**.

Este resultado en cualquier tooSlack de objetos asignados del grupo en hello **usuarios y grupos** sección completa que se sincronizan desde tooSlack de Azure AD. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de la demora.


## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-enterprise-apps-manage-provisioning.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
