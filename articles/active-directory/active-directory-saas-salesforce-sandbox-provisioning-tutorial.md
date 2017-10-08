---
title: "Tutorial: Integración de Azure Active Directory con Salesforce Sandbox | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el espacio aislado de Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a>Tutorial: Configuración de Salesforce Sandbox para el aprovisionamiento automático de usuarios

objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en espacio aislado de Salesforce y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooSalesforce espacio aislado.

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory.
*   Debe tener un inquilino válido para Salesforce Sandbox for Work o Salesforce Sandbox for Education. Puede usar una cuenta de prueba gratuita de cualquiera de los servicios.
*   Una cuenta de usuario de Salesforce Sandbox con permisos de administrador de equipos.

## <a name="assigning-users-toosalesforce-sandbox"></a>Asignar usuarios tooSalesforce espacio aislado

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincronizan sólo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso a tooyour aplicación de espacio aislado de Salesforce. Una vez decidido, puede asignar estas tooyour usuarios aplicación Salesforce Sandbox siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a>Sugerencias importantes para asignar usuarios tooSalesforce espacio aislado

* Se recomienda que un único usuario de Azure AD se asigna hello tootest tooSalesforce espacio aislado que configuración de aprovisionamiento. Más tarde, se pueden asignar otros usuarios o grupos.

* Al asignar un espacio aislado de usuario tooSalesforce, debe seleccionar un rol de usuario válido. rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento.

> [!NOTE]
> Esta aplicación importa roles personalizados del espacio aislado de Salesforce como parte del proceso, el cliente que Hola puede tooselect al asignar a los usuarios de aprovisionamiento de Hola.

## <a name="enable-automated-user-provisioning"></a>Habilitación del aprovisionamiento automático de usuarios

Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario del espacio aislado de la tooSalesforce Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas en espacio aislado de Salesforce en función de usuario y de grupo de usuario asignado asignación de Azure AD.

>[!Tip]
>También puede elegir tooenabled basado en SAML Single Sign-On espacio aislado de Salesforce, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure aprovisionamiento de cuentas de usuario automática:

objetivo de Hola de esta sección es toooutline cómo tooenable el aprovisionamiento de usuarios de usuario de Active Directory cuentas tooSalesforce espacio aislado.

1. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

2. Si ya ha configurado el espacio aislado de Salesforce para inicio de sesión único, busque la instancia de Salesforce Sandbox usando el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **Salesforce Sandbox** en Galería de aplicaciones de Hola. Seleccionar espacio aislado de Salesforce en resultados de búsqueda de Hola y agregar tooyour lista de aplicaciones.

3. Seleccione la instancia de Salesforce Sandbox, a continuación, seleccione hello **Provisioning** ficha.

4. Conjunto hello **modo de aprovisionamiento** demasiado**automática**. 
    ![Aprovisionamiento](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)

5. En hello **las credenciales de administrador** sección, proporcione Hola siguientes opciones de configuración:
   
    a. Hola **nombre de usuario administrador** cuadro de texto, escriba un espacio aislado de Salesforce de cuenta de nombre que ha Hola **administrador del sistema** perfil asignado en Salesforce.com.
   
    b. Hola **contraseña de administrador** cuadro de texto, escriba la contraseña de Hola para esta cuenta.

6. tooget su token de seguridad de espacio aislado de Salesforce, abra una nueva pestaña e inicie sesión en hello misma cuenta de administrador de espacio aislado de Salesforce. En hello esquina superior derecha de la página de hello, haga clic en su nombre y, a continuación, haga clic en **My Settings**.

     ![Habilitar el aprovisionamiento automático de usuarios](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Habilitar aprovisionamiento automático de usuarios")
7. En el panel de navegación izquierdo de hello, haga clic en **Personal** tooexpand Hola sección relacionada y, a continuación, haga clic en **restablecer mi Token de seguridad**.
  
    ![Habilitar el aprovisionamiento automático de usuarios](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Habilitar aprovisionamiento automático de usuarios")
8. En hello **restablecer mi Token de seguridad** página, haga clic en hello **restablecer Token de seguridad** botón.

    ![Habilitar el aprovisionamiento automático de usuarios](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Habilitar aprovisionamiento automático de usuarios")
9. Compruebe la Bandeja de entrada de correo electrónico de hello asociado con esta cuenta de administrador. Busque un correo electrónico desde Salesforce Sandbox.com que contiene el token de seguridad nuevo Hola.
10. Copiar Hola token, vaya tooyour ventana de Azure AD y pegarlos en hello **Socket Token** campo.

11. Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectarse tooyour aplicación de espacio aislado de Salesforce.

12. Hola **correo electrónico de notificación** , escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir notificaciones de error de aprovisionamiento y active casilla Hola.

13. Haga clic en **Guardar**.  
    
14.  En la sección asignaciones de hello, seleccione **sincronizar Azure Active Directory Users tooSalesforce espacio aislado.**

15. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde Azure AD tooSalesforce espacio aislado. Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en espacio aislado de Salesforce para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

16. tooenable Hola servicio de aprovisionamiento de Azure AD para Salesforce Sandbox, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración

17. Haga clic en **Guardar**.


Inicia la sincronización inicial de Hola de los usuarios o grupos asignados tooSalesforce espacio aislado en la sección usuarios y grupos de Hola. la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de espacio aislado de Salesforce.

Ahora puede crear una cuenta de prueba. Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado toosalesforce.

## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del inicio de sesión único](active-directory-saas-salesforcesandbox-tutorial.md)