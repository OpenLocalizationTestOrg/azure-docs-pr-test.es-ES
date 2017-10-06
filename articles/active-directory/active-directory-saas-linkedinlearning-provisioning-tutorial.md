---
title: "Tutorial: Configuración de LinkedIn Learning para el aprovisionamiento automático de usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario tooLinkedIn de aprendizaje."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: e0503e09ab384723ffb73d6ef1df8be6abfc9294
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-learning-for-automatic-user-provisioning"></a>Tutorial: Configuración de LinkedIn Learning para el aprovisionamiento automático de usuarios


Hola objetivo de este tutorial es tooshow Hola pasos que debe tooperform en LinkedIn aprendizaje y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooLinkedIn de aprendizaje. 

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory
*   Un inquilino de LinkedIn Learning 
*   Una cuenta de administrador en el aprendizaje de LinkedIn con acceso toohello centro de cuentas de LinkedIn

> [!NOTE]
> Azure Active Directory se integra con el aprendizaje de LinkedIn con hello [SCIM](http://www.simplecloud.info/) protocolo.

## <a name="assigning-users-toolinkedin-learning"></a>Asignar usuarios tooLinkedIn de aprendizaje

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincronizarán sólo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD. 

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesitará toodecide lo que los usuarios o grupos en Azure AD representan a usuarios de Hola que necesitan tener acceso a tooLinkedIn de aprendizaje. Una vez decidido, puede asignar estas tooLinkedIn usuarios aprendizaje siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-learning"></a>Sugerencias importantes para asignar usuarios tooLinkedIn de aprendizaje

*   Se recomienda que un único usuario de Azure AD asignarse hello tootest tooLinkedIn aprendizaje que configuración de aprovisionamiento. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar un usuario tooLinkedIn de aprendizaje, debe seleccionar hello **usuario** rol en el cuadro de diálogo de hello asignación. rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.


## <a name="configuring-user-provisioning-toolinkedin-learning"></a>Usuario que realiza configuración tooLinkedIn el aprovisionamiento de aprendizaje

Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario del su aprendizaje tooLinkedIn de Azure AD SCIM y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en el aprendizaje de LinkedIn en función de usuario y de grupo asignación de Azure AD.

> [!TIP]
> También puede elegir tooenabled basado en SAML Single Sign-On para el aprendizaje de LinkedIn, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-learning-in-azure-ad"></a>cuenta de usuario automática de tooconfigure tooLinkedIn de aprovisionamiento de aprendizaje de Azure AD:


primer paso de Hello es tooretrieve el token de acceso de LinkedIn. Si es administrador de organización, puede aprovisionar automáticamente un token de acceso. En el centro de cuentas, vaya demasiado**configuración &gt; configuración Global** hello abierto y **el programa de instalación de SCIM** panel.

> [!NOTE]
> Si se obtiene acceso a centro de cuentas de hello directamente en lugar de a través de un vínculo, puede llegar a él mediante Hola pasos.

1)  Inicie sesión en el centro de tooAccount.

2)  Seleccione **Administración &gt; Configuración de administración**.

3)  Haga clic en **avanzada integraciones** en barra lateral izquierdo de Hola. Está dirigido toohello centro de cuentas.

4)  Haga clic en **+ agregar una nueva configuración de SCIM** y siga el procedimiento de hello rellenando en cada campo.

> Si no está habilitada la asignación de licencias automática, solo se sincronizan los datos de usuario.

![Aprovisionamiento de LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_1.PNG)

> Cuando se habilita la asignación de autolicense, necesita toonote la instancia de aplicación y tipo de licencia. Se asignan licencias primero en llegar, primero actúan base hasta que se realizan todas las licencias de Hola.

![Aprovisionamiento de LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_2.PNG)

5)  Haga clic en **Generar token**. Debería ver la pantalla de token de acceso en hello **token de acceso** campo.

6)  Guarde el Portapapeles de tooyour de token de acceso o el equipo antes de abandonar la página de Hola.

7) A continuación, inicie sesión en toohello [portal de Azure](https://portal.azure.com)y examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

8) Si ya has configurado LinkedIn aprendizaje para el inicio de sesión único, busque la instancia de aprendizaje de LinkedIn con el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **LinkedIn aprendizaje** en Galería de aplicaciones de Hola. Seleccione LinkedIn aprendizaje en resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

9)  Seleccione la instancia de aprendizaje de LinkedIn, a continuación, seleccione hello **Provisioning** ficha.

10) Conjunto hello **modo de aprovisionamiento** demasiado**automática**.

![Aprovisionamiento de LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_3.PNG)

11)  Rellene Hola después de campos en **las credenciales de administrador** :

* Hola **dirección URL del inquilino** , escriba https://api.linkedin.com.

* Hola **secreto Token** campo, escriba el token de acceso de Hola que generó en el paso 1 y haga clic en **Probar conexión** .

* Verá una notificación de éxito en el lado superior derecho de hello del portal.

12) Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y comprobar Hola casilla incluida a continuación.

13) Haga clic en **Guardar**. 

14) Hola **asignaciones de atributos** sección, revise los atributos de usuario y grupo de Hola que se sincronizarán desde Azure AD tooLinkedIn de aprendizaje. Tenga en cuenta que Hola atributos seleccionados como **coincidencia** propiedades será toomatch usado hello las cuentas de usuario y grupos en el aprendizaje de LinkedIn para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

![Aprovisionamiento de LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_4.PNG)

15) tooenable Hola servicio de aprovisionamiento de Azure AD para el aprendizaje de LinkedIn, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección

16) Haga clic en **Guardar**. 

Esto iniciará la sincronización inicial de Hola de los usuarios o grupos asignados tooLinkedIn de aprendizaje en la sección usuarios y grupos de Hola. Tenga en cuenta que la sincronización inicial de hello surtirá tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de aprendizaje de LinkedIn.


## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-enterprise-apps-manage-provisioning.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
