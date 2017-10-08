---
title: "Tutorial: Integración de Azure Active Directory con Workplace by Facebook | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y un área de trabajo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a>Tutorial: Configuración de Workplace by Facebook para el aprovisionamiento de usuarios

objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en lugar de trabajo por Facebook y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooWorkplace Facebook.

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con un área de trabajo Facebook tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único de Workplace by Facebook

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assigning-users-tooworkplace-by-facebook"></a>Asignar usuarios tooWorkplace Facebook

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso al área de trabajo de tooyour por aplicación de Facebook. Una vez decidido, puede asignar estas tooyour al área de trabajo de usuarios por aplicación de Facebook siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a>Sugerencias importantes para asignar usuarios tooWorkplace Facebook

*   Se recomienda que un único usuario de Azure AD asignada tooWorkplace por Facebook tootest Hola aprovisionamiento de configuración. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar un tooWorkplace usuario Facebook, debe seleccionar un rol de usuario válido. rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.

## <a name="enable-user-provisioning"></a>Habilitación del aprovisionamiento de usuarios

Esta sección le guía a través de conectarse la tooWorkplace de Azure AD mediante la API de aprovisionamiento de cuentas de usuario de Facebook y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en lugar de trabajo en función de usuario y grupo de Facebook asignación de Azure AD.

>[!Tip]
>También puede elegir tooenabled basado en SAML Single Sign-On para Facebook, siguiendo las instrucciones Hola proporcionadas en el área de trabajo [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>cuenta de usuario de tooconfigure tooWorkplace Facebook de aprovisionamiento en Azure AD:

objetivo de Hola de esta sección es toooutline cómo tooenable el aprovisionamiento de usuario de Active Directory cuentas tooWorkplace Facebook.

Azure admite AD Hola capacidad tooautomatically sincronizar los detalles de la cuenta de hello de asigna usuarios tooWorkplace Facebook. Esta sincronización automática permite al área de trabajo mediante datos de Facebook tooget Hola debe tooauthorize a los usuarios para tener acceso, antes de implementarlos intentar toosign en para hello primera vez. También desaprovisiona usuarios de Workplace by Facebook cuando se revoque el acceso en Azure AD.

1. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory** > **aplicaciones empresariales** > **detodaslasaplicaciones** sección.

2. Si ya ha configurado un área de trabajo Facebook para inicio de sesión único, busque la instancia de un área de trabajo mediante el campo de búsqueda de Hola de Facebook. En caso contrario, seleccione **agregar** y busque **al área de trabajo Facebook** en Galería de aplicaciones de Hola. Seleccione un área de trabajo Facebook en resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

3. Seleccione la instancia de un área de trabajo Facebook, a continuación, seleccione hello **Provisioning** ficha.

4. Conjunto hello **modo de aprovisionamiento** demasiado**automática**. 

    ![Aprovisionamiento](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. En hello **las credenciales de administrador** sección, escriba el secreto del Token de Hola y Hola URL de inquilino de su área de trabajo mediante el Administrador de Facebook.

6. Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectarse tooyour al área de trabajo por la aplicación de Facebook. Si se produce un error en la conexión de hello, asegúrese de que el área de trabajo por cuenta de Facebook tiene permisos de administrador de equipo.

7. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y active casilla Hola.

8. Haga clic en **Guardar**.

9. En la sección asignaciones de hello, seleccione **tooWorkplace sincronizar Azure Active Directory Users Facebook.**

10. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde Azure AD tooWorkplace Facebook. Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en lugar de trabajo Facebook para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

11. tooenable Hola servicio de aprovisionamiento de Azure AD para un área de trabajo Facebook, Hola de cambio **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección

12. Haga clic en **Guardar**.

Para obtener más información acerca de cómo tooconfigure automática de aprovisionamiento, vea [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)

Ahora puede crear una cuenta de prueba. Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooWorkplace Facebook.

## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del inicio de sesión único](active-directory-saas-workplacebyfacebook-tutorial.md)

