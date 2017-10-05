---
title: "Tutorial: Integración de Azure Active Directory con Box | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9f061f3f5a0a4825854b893150ceccc8951487de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a>Tutorial: Configuración de Box para aprovisionar automáticamente usuarios

El objetivo de este tutorial es explicar los pasos que debe realizar en Box y Azure AD para aprovisionar y cancelar automáticamente el aprovisionamiento de cuentas de usuario de Azure AD para Box.

## <a name="prerequisites"></a>Requisitos previos

En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:

*   Un inquilino de Azure Active Directory.
*   Una suscripción a Box habilitada para el inicio de sesión único.
*   Una cuenta de usuario de Box con permisos de administrador de equipo.

## <a name="assigning-users-to-box"></a>Asignación de usuarios a Box 

Azure Active Directory usa un concepto que se denomina "asignaciones" para determinar qué usuarios deben recibir acceso a determinadas aplicaciones. En el contexto del aprovisionamiento automático de cuentas de usuario, solo se sincronizarán los usuarios y grupos que se han "asignado" a una aplicación de Azure AD.

Antes de configurar y habilitar el servicio de aprovisionamiento, debe decidir qué usuarios o grupos de Azure AD representan a los usuarios que necesitan acceso a la aplicación Box. Una vez decidido, puede asignar estos usuarios a la aplicación de Box siguiendo estas instrucciones:

[Asignar un usuario o grupo a una aplicación empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a>Asignación de usuarios y grupos
La pestaña **Box > Usuarios y grupos** de Azure Portal permite especificar qué usuarios y grupos deben tener acceso a Box. La asignación de un usuario o un grupo hace que ocurra lo siguiente:

* Azure AD permite que el usuario asignado (ya sea mediante asignación directa o pertenencia al grupo) se autentique en Box. Si no se asigna un usuario, Azure AD no permitirá que inicie sesión en Box y devolverá un error en la página de inicio de sesión de Azure AD.
* Se agregará un icono de la aplicación de Box al [iniciador de aplicaciones](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)del usuario.
* Si está habilitado el aprovisionamiento automático, se agregan a la cola de aprovisionamiento los usuarios o grupos asignados para aprovisionarlos automáticamente.
  
  * Si solo se ha configurado el aprovisionamiento de objetos de usuario, todos los usuarios asignados directamente se colocan en la cola de aprovisionamiento, y todos los usuarios que son miembros de los grupos asignados se colocarán en la cola de aprovisionamiento. 
  * Si se ha configurado el aprovisionamiento de objetos de grupo, todos los objetos de grupo asignados se aprovisionan en Box, así como todos los usuarios que son miembros de esos grupos. Las pertenencias a grupos y usuarios se conservan una vez que se escriben en Box.

Puede usar la pestaña **Atributos > Inicio de sesión único** para configurar los atributos de usuario (o notificaciones) que se presentan en Box durante la autenticación basada en SAML, y la pestaña **Atributos > Aprovisionamiento** para configurar la forma en que los atributos de usuario y grupo fluyen de Azure AD a Box durante las operaciones de aprovisionamiento.

### <a name="important-tips-for-assigning-users-to-box"></a>Sugerencias importantes para asignar usuarios a Box 

*   Se recomienda asignar un solo usuario de Azure AD a Box para probar la configuración de aprovisionamiento. Más tarde, se pueden asignar otros usuarios o grupos.

*   Al asignar a un usuario a Box, debe seleccionar un rol de usuario válido. El rol "Acceso predeterminado" no funciona para realizar el aprovisionamiento.

## <a name="enable-automated-user-provisioning"></a>Habilitación del aprovisionamiento automático de usuarios

Esta sección lo guía a través de los pasos necesarios para conectar la API de aprovisionamiento de su cuenta de usuario de Box, así como para configurar el servicio de aprovisionamiento con el fin de crear, actualizar y deshabilitar cuentas de usuario asignadas de Box en función de la asignación de grupos y usuarios Azure AD.

Si está habilitado el aprovisionamiento automático, se agregan a la cola de aprovisionamiento los usuarios o grupos asignados para aprovisionarlos automáticamente.
    
 * Si solo se ha configurado el aprovisionamiento de objetos de usuario, los usuarios asignados directamente se colocan en la cola de aprovisionamiento, y todos los usuarios que son miembros de los grupos asignados se colocarán en la cola de aprovisionamiento. 
    
 * Si se ha configurado el aprovisionamiento de objetos de grupo, todos los objetos de grupo asignados se aprovisionan en Box, así como todos los usuarios que son miembros de esos grupos. Las pertenencias a grupos y usuarios se conservan una vez que se escriben en Box.

> [!TIP] 
> También puede habilitar el inicio de sesión único basado en Box para Concur siguiendo las instrucciones de [Azure Portal](https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí.

### <a name="to-configure-automatic-user-account-provisioning"></a>Para configurar el aprovisionamiento automático de cuentas de usuario, siga estos pasos:

El objetivo de esta sección es describir cómo habilitar el aprovisionamiento de las cuentas de usuario de Active Directory en Box.

1. En [Azure Portal](https://portal.azure.com), vaya a la sección **Azure Active Directory > Aplicaciones empresariales > Todas las aplicaciones**.

2. Si ya ha configurado Box para el inicio de sesión único, busque la instancia de Box mediante el campo de búsqueda. En caso contrario, seleccione **Agregar** y busque **Box** en la Galería de aplicaciones. Seleccione Box en los resultados de búsqueda y agrégalo a la lista de aplicaciones.

3. Seleccione la instancia de Box y, después, seleccione la pestaña **Aprovisionamiento**.

4. Establezca el **modo de aprovisionamiento** en **Automático**. 

    ![Aprovisionamiento](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. En la sección **Credenciales de administrador**, haga clic en **Authorize** (Autorizar) para abrir un cuadro de diálogo de inicio de sesión de Box en una nueva ventana del explorador.

6. En la página **Log in to grant access to Box** (Iniciar sesión para otorgar acceso a Box), proporcione las credenciales necesarias y haga clic en **Authorize** (Autorizar). 
   
    ![Habilitar el aprovisionamiento automático de usuarios](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Habilitar aprovisionamiento automático de usuarios")

7. Haga clic en **Grant access to Box** (Otorgar acceso a Box) para autorizar esta operación y volver a Azure Portal. 
   
    ![Habilitar el aprovisionamiento automático de usuarios](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Habilitar aprovisionamiento automático de usuarios")

8. En Azure Portal, haga clic en **Probar conexión** para asegurarse de que Azure AD puede conectarse a la aplicación Box. Si se produce un error de conexión, asegúrese de que su cuenta de Box tiene permisos de administrador de equipo y vuelva a intentar el paso de **Autorizar**.

9. Escriba la dirección de correo electrónico de una persona o grupo que debe recibir las notificaciones de error de aprovisionamiento en el campo **Correo electrónico de notificación** y active la casilla.

10. Haga clic en **Guardar**.

11. En la sección Asignaciones, seleccione **Synchronize Azure Active Directory Users to Box** (Sincronizar usuarios de Azure Active Directory con Box).

12. En la sección **Attribute Mappings** (Asignaciones de atributos), revise los atributos de usuario que se sincronizan entre Azure AD y Box. Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con las cuentas de usuario de Box con el objetivo de realizar operaciones de actualización. Seleccione el botón Guardar para confirmar los cambios.

13. Para habilitar el aprovisionamiento del servicio de aprovisionamiento de Azure AD para Box, cambie el **estado de aprovisionamiento** a **Activado** en la sección Configuración.

14. Haga clic en **Guardar**.

Esta acción inicia la sincronización inicial de todos los usuarios y grupos asignados a Box en la sección Usuarios y grupos. La sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos si se está ejecutando el servicio. Puede usar la sección **Detalles de sincronización** para supervisar el progreso y hacer clic en los vínculos a los informes de actividad de aprovisionamiento, que describen todas las acciones que ha llevado a cabo el servicio de aprovisionamiento en la aplicación Box.

Ahora puede crear una cuenta de prueba. Espere 20 minutos para comprobar que la cuenta se ha sincronizado con Box.

En su inquilino de Box, los usuarios sincronizados se muestran en **Usuarios administrados** en la **Consola de administración**.

![Estado de integración](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Estado de integración")


## <a name="additional-resources"></a>Recursos adicionales

* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del inicio de sesión único](active-directory-saas-box-tutorial.md)