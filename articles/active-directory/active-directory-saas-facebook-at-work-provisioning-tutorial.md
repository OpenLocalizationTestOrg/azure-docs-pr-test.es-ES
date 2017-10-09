---
title: "Tutorial: Configuración de Workplace by Facebook para el aprovisionamiento de usuarios | Microsoft Docs"
description: "Obtenga información acerca de cómo tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooWorkplace Facebook."
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a>Tutorial: Configuración de Workplace by Facebook para el aprovisionamiento de usuarios

Este tutorial muestra Hola tooautomatically necesarios pasos aprovisionar y desaprovisionar cuentas de usuario de Azure Active Directory (Azure AD) tooWorkplace Facebook.

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con un área de trabajo Facebook tooconfigure, necesita siguiente de hello:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único (SSO) de Workplace by Facebook

pasos de hello tootest en este tutorial, siga estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una oferta de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assign-users-tooworkplace-by-facebook"></a>Asignar usuarios tooWorkplace Facebook

Azure AD usa un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincronizan sólo los usuarios de Hola y grupos que se han asignado tooan aplicación en Azure AD.

Antes de configurar y habilitar Hola aprovisionamiento del servicio, decida qué usuarios y grupos en Azure AD representan a usuarios de Hola que necesitan tener acceso al área de trabajo de tooyour por aplicación de Facebook. A continuación, puede asignar estas tooyour al área de trabajo de usuarios por aplicación de Facebook siguiendo Hola instrucciones [asignar una aplicación de empresa de tooan de usuario o grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

>[!IMPORTANT]
>*   Hola prueba configuración de aprovisionamiento mediante la asignación de una sola tooWorkplace de usuario de Azure AD Facebook. Asigne usuarios y grupos adicionales más tarde.
>*   Cuando se asigna un tooWorkplace usuario Facebook, debe seleccionar un rol de usuario válido. rol de acceso predeterminado de Hello no funciona para el aprovisionamiento.

## <a name="enable-automated-user-provisioning"></a>Habilitación del aprovisionamiento automático de usuarios

En esta sección le guiará en el proceso de conexión de su cuenta de usuario de Azure AD toohello aprovisionamiento API del área de trabajo Facebook. También aprenderá cómo tooconfigure Hola aprovisionamiento toocreate de servicio, actualizar y deshabilitar cuentas de usuario asignado en lugar de trabajo Facebook. Esto se basa en la asignación de grupos y usuarios en Azure AD.

>[!Tip]
>También puede elegir tooenabled SSO basado en SAML para Facebook, al área de trabajo por siguiendo las instrucciones de hello proporcionadas en hello [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>Configurar aprovisionamiento tooWorkplace Facebook en Azure AD de la cuenta de usuario

Azure admite AD Hola capacidad tooautomatically sincronizar los detalles de la cuenta de hello de asigna usuarios tooWorkplace Facebook. Esta sincronización automática permite al área de trabajo mediante datos de Facebook tooget Hola debe tooauthorize a los usuarios para tener acceso, antes de implementarlos intentar toosign en para hello primera vez. También desaprovisiona usuarios de Workplace by Facebook cuando se revoque el acceso en Azure AD.

1. Hola [portal de Azure](https://portal.azure.com), seleccione **Azure Active Directory** > **aplicaciones empresariales** > **todas las aplicaciones**.

2. Si ya ha configurado un área de trabajo Facebook para SSO, buscar la instancia de un área de trabajo Facebook mediante el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **al área de trabajo Facebook** en Galería de aplicaciones de Hola. Seleccione **al área de trabajo Facebook** de hello resultados de búsqueda y agregarlo a tooyour lista de aplicaciones.

3. Seleccione la instancia de un área de trabajo Facebook y, a continuación, seleccione hello **Provisioning** ficha.

4. Establecer **modo de aprovisionamiento** demasiado**automática**. 

    ![Captura de pantalla de las opciones de aprovisionamiento de Workplace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. En hello **las credenciales de administrador** sección, escriba Hola **secreto Token** hello y **dirección URL del inquilino** su área de trabajo mediante el Administrador de Facebook.

6. Hola portal de Azure, seleccione **Probar conexión** tooensure Azure AD puede conectarse tooyour al área de trabajo por la aplicación de Facebook. Si se produce un error en la conexión de hello, asegúrese de que el área de trabajo por cuenta de Facebook tiene permisos de administrador de equipo.

7. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y la casilla de verificación de Hola.

8. Seleccione **Guardar**.

9. En la sección asignaciones de hello, seleccione **tooWorkplace sincronizar Azure Active Directory Users Facebook**.

10. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde Azure AD tooWorkplace Facebook. Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en lugar de trabajo Facebook para las operaciones de actualización. toocommit todos los cambios, seleccione **guardar**.

11. tooenable Hola servicio de aprovisionamiento de Azure AD para Facebook, al área de trabajo en hello **configuración** sección, cambie hello **estado de aprovisionamiento** demasiado**en**.

12. Seleccione **Guardar**.

Para obtener más información acerca de cómo tooconfigure automática de aprovisionamiento, vea [Hola documentación de Facebook](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).

Ahora puede crear una cuenta de prueba. Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooWorkplace Facebook.

## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del inicio de sesión único](active-directory-saas-facebook-at-work-tutorial.md)

