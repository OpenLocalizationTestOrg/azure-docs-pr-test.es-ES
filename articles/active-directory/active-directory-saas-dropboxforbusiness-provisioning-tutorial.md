---
title: "Tutorial: Integración de Azure Active Directory con Dropbox for Business | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Dropbox para empresas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a>Tutorial: Configuración de Dropbox for Business para el aprovisionamiento automático de usuarios

objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform en Dropbox para negocios y Azure AD tooautomatically aprovisionar y eliminación de aprovisionar cuentas de usuario de Azure AD tooDropbox para la empresa.

## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory.
*   Una suscripción a Dropbox for Business con inicio de sesión único habilitado.
*   Una cuenta de usuario de Dropbox for Business con permisos de administrador de equipo.

## <a name="assigning-users-toodropbox-for-business"></a>Asignar usuarios tooDropbox para la empresa

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincroniza solo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD.

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, necesita toodecide qué usuarios o grupos en Azure AD que representan a usuarios de Hola que necesitan tener acceso a tooyour Dropbox para empresas. Una vez decidido, puede asignar estas tooyour usuarios Dropbox para empresas siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a>Sugerencias importantes para asignar usuarios tooDropbox para la empresa

*   Se recomienda que un único usuario de Azure AD se asigna tooDropbox para hello tootest de negocios aprovisionamiento de configuración. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar una tooDropbox de usuario para la empresa, debe seleccionar un rol de usuario válido. rol de "Acceso predeterminado" Hello no funciona para el aprovisionamiento de...

## <a name="enable-automated-user-provisioning"></a>Habilitación del aprovisionamiento automático de usuarios

Esta sección le guía a través de conectar su tooDropbox de Azure AD para la API de aprovisionamiento de cuentas de usuario de la empresa y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas de usuario asignado en Dropbox para empresas en función de usuario y de grupo asignación de Azure AD.

>[!Tip]
>También puede elegir tooenabled basado en SAML Single Sign-On para Dropbox para empresas, siguiendo las instrucciones Hola proporcionadas en [portal de Azure](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure aprovisionamiento de cuentas de usuario automática:

1. Hola [portal de Azure](https://portal.azure.com), examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

2. Si ya has configurado Dropbox para empresas para el inicio de sesión único, busque la instancia de Dropbox para empresas mediante el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **Dropbox para empresas** en Galería de aplicaciones de Hola. Seleccione Dropbox para empresas en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

3. Seleccione la instancia de Dropbox para empresas, a continuación, seleccione hello **Provisioning** ficha.

4. Conjunto hello **modo de aprovisionamiento** demasiado**automática**. 

    ![Aprovisionamiento](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. En hello **las credenciales de administrador** sección, haga clic en **Authorize**. Se abre un cuadro de diálogo de inicio de sesión de Dropbox for Business en una nueva ventana del explorador.

6. En hello **toolink inicio de sesión tooDropbox con Azure AD** cuadro de diálogo de inicio de sesión tooyour Dropbox para el inquilino de negocios.

     ![Aprovisionamiento de usuarios](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Aprovisionamiento de usuarios")

7. Confirme que desea toogive Azure Active Directory permiso toomake cambios tooyour Dropbox para el inquilino de negocios. Haga clic en **Permitir**.
    
      ![Aprovisionamiento de usuarios](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Aprovisionamiento de usuarios")

8. Hola portal de Azure, haga clic en **Probar conexión** tooensure Azure AD puede conectarse tooyour Dropbox para empresas. Si se produce un error en la conexión de hello, asegúrese de la lista desplegable para la cuenta de empresa tiene permisos de administrador de equipo e inténtelo de hello **"Autorizar"** vuelva a intentarlo.

9. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y active casilla Hola.

10. Haga clic en **Guardar**.

11. En la sección asignaciones de hello, seleccione **tooDropbox sincronizar Azure usuarios de Active Directory para la empresa.**

12. Hola **asignaciones de atributos** sección, revise los atributos de usuario de Hola que se sincronizan desde tooDropbox de Azure AD para la empresa. Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario del hello toomatch usado en Dropbox para empresas para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

13. tooenable Hola servicio de aprovisionamiento de Azure AD para Dropbox para empresas, cambio hello **estado de aprovisionamiento** demasiado**en** en hello sección de configuración

14. Haga clic en **Guardar**.

Inicia la sincronización inicial de Hola de todos los usuarios y grupos asignados tooDropbox para la empresa en los usuarios de Hola y sección de grupos. la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la lista desplegable para aplicaciones de negocio.

Ahora puede crear una cuenta de prueba. Espere a que los minutos de too20 tooverify que cuenta Hola se ha había sincronizado tooDropbox para la empresa.

Un ciclo de aprovisionamiento de usuarios completado correctamente se indica con un estado relacionado:

![Asignar usuarios](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Asignar usuarios")


## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del inicio de sesión único](active-directory-saas-dropboxforbusiness-tutorial.md)