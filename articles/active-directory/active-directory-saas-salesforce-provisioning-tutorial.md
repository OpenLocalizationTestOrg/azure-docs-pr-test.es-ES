---
title: "Tutorial: Integración de Azure Active Directory con Salesforce | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a>Tutorial: Configuración de Salesforce para aprovisionar a los usuarios automáticamente

objetivo de Hola de este tutorial es tooshow Hola pasos necesarios tooperform en Salesforce y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooSalesforce.

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory.
*   Debe tener un inquilino válido para Salesforce for Work o Salesforce for Education. Puede usar una cuenta de prueba gratuita de cualquiera de los servicios.
*   Una cuenta de usuario de Salesforce con permisos de administrador de equipo

## <a name="assigning-users-toosalesforce"></a>Asignar usuarios tooSalesforce

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos de usuarios de Azure AD representan Hola que necesitan tener acceso a la aplicación de Salesforce tooyour. Una vez decidido, puede asignar estos usuarios de la aplicación de Salesforce tooyour siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a>Sugerencias importantes para asignar usuarios tooSalesforce

*   Se recomienda que un único usuario de Azure AD se asigna tooSalesforce tootest Hola aprovisionamiento de configuración. Más tarde, se pueden asignar otros usuarios o grupos.

*  Al asignar una tooSalesforce de usuario, debe seleccionar un rol de usuario válido. rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento

    > [!NOTE]
    > Esta aplicación importa roles personalizados de Salesforce como parte del proceso, el cliente que Hola puede tooselect al asignar a los usuarios de aprovisionamiento de Hola

## <a name="enable-automated-user-provisioning"></a>Habilitación del aprovisionamiento automático de usuarios

Esta sección le guía a través de conexión de API de aprovisionamiento de cuentas de usuario de su tooSalesforce de Azure AD y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en Salesforce en función de asignación de usuario y de grupo en Azure AD .

>[!Tip]
>También puede elegir tooenabled basado en SAML Single Sign-On para Salesforce, siguiendo las instrucciones de hello proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure aprovisionamiento de cuentas de usuario automática:

objetivo de Hola de esta sección es toooutline cómo tooenable el aprovisionamiento de usuarios de usuario de Active Directory cuentas tooSalesforce.

1. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

2. Si ya has configurado Salesforce para inicio de sesión único, busque la instancia de Salesforce con el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **Salesforce** en Galería de aplicaciones de Hola. Seleccione Salesforce en resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

3. Seleccione la instancia de Salesforce, a continuación, seleccione hello **Provisioning** ficha.

4. Conjunto hello **modo de aprovisionamiento** demasiado**automática**. 
![Aprovisionamiento](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)

5. En hello **las credenciales de administrador** sección, proporcione Hola siguientes opciones de configuración:
   
    a. Hola **nombre de usuario administrador** cuadro de texto, tipo de una división de ventas de nombre de cuenta que ha Hola **administrador del sistema** perfil asignado en Salesforce.com.
   
    b. Hola **contraseña de administrador** cuadro de texto, escriba la contraseña de Hola para esta cuenta.

6. tooget su token de seguridad de Salesforce, abra una nueva pestaña e inicie sesión en hello misma cuenta de administrador de Salesforce. En hello esquina superior derecha de la página de hello, haga clic en su nombre y, a continuación, haga clic en **My Settings**.

     ![Habilitar el aprovisionamiento automático de usuarios](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Habilitar aprovisionamiento automático de usuarios")
7. En el panel de navegación izquierdo de hello, haga clic en **Personal** tooexpand Hola sección relacionada y, a continuación, haga clic en **restablecer mi Token de seguridad**.
  
    ![Habilitar el aprovisionamiento automático de usuarios](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Habilitar aprovisionamiento automático de usuarios")
8. En hello **restablecer mi Token de seguridad** página, haga clic en **restablecer Token de seguridad** botón.

    ![Habilitar el aprovisionamiento automático de usuarios](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Habilitar aprovisionamiento automático de usuarios")
9. Compruebe la Bandeja de entrada de correo electrónico de hello asociado con esta cuenta de administrador. Busque un correo electrónico de Salesforce.com que contiene el token de seguridad nuevo Hola.
10. Copiar Hola token, vaya tooyour ventana de Azure AD y pegarlos en hello **Socket Token** campo.

11. Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectarse a la aplicación de Salesforce tooyour.

12. Hola **correo electrónico de notificación** , escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir notificaciones de error de aprovisionamiento y comprobar Hola casilla incluida a continuación.

13. Haga clic en **Guardar**.  
    
14.  En la sección asignaciones de hello, seleccione **tooSalesforce sincronizar Azure usuarios de Active Directory.**

15. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooSalesforce de Azure AD. Tenga en cuenta que Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en Salesforce para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

16. tooenable Hola servicio de aprovisionamiento de Azure AD para Salesforce, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración

17. Haga clic en **Guardar**.

Esto inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooSalesforce Hola a los usuarios y la sección de grupos. Tenga en cuenta que la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de Salesforce.

Ahora puede crear una cuenta de prueba. Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooSalesforce.

## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del inicio de sesión único](active-directory-saas-salesforce-tutorial.md)