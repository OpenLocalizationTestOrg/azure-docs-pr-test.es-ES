---
title: "Tutorial: Configuración de Cerner Central para el aprovisionamiento automático de usuarios con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure Azure Active Directory tooautomatically aprovisionar lista tooa de usuarios en el centro de Cerner."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a>Tutorial: configuración de Cerner Central para el aprovisionamiento automático de usuarios

objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform Cerner Central y Azure AD tooautomatically aprovisionar y eliminación de aprovisionamiento en cuentas de usuario de la lista de usuarios de Azure AD tooa en Cerner Central. 


## <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

*   Un inquilino de Azure Active Directory
*   Un inquilino de Cerner Central 

> [!NOTE]
> Azure Active Directory se integra con el centro de Cerner con hello [SCIM](http://www.simplecloud.info/) protocolo.

## <a name="assigning-users-toocerner-central"></a>Asignar usuarios tooCerner Central

Azure Active Directory utiliza un concepto que se denomina toodetermine "asignaciones" que los usuarios deben recibir acceso tooselected aplicaciones. En el contexto de Hola de aprovisionamiento de cuentas de usuario automática, se sincronizan sólo los usuarios de Hola y grupos que se han "asignados" tooan aplicación en Azure AD. 

Antes de configurar y habilitar el aprovisionamiento del servicio de hello, debe decidir qué usuarios o grupos en Azure AD representan a usuarios de Hola que necesitan tener acceso a tooCerner Central. Una vez decidido, puede asignar estas tooCerner centro de usuarios siguiendo las instrucciones de hello aquí:

[Asignar un usuario o grupo tooan su aplicación empresarial](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a>Sugerencias importantes para asignar usuarios tooCerner Central

*   Se recomienda que un único usuario de Azure AD asignarse tooCerner tootest Central Hola aprovisionamiento de configuración. Más tarde, se pueden asignar otros usuarios o grupos.

* Una vez completada para un solo usuario la comprobación inicial, Cerner Central recomienda asignar Hola toda la lista de usuarios crea tooaccess lista de usuarios de la tooCerner de cualquier toobe aprovisionado de soluciones (no solo Cerner Central) Cerner.  Otras soluciones de Cerner aprovechan esta lista de usuarios en la lista de usuarios de Hola.

*   Al asignar un centro de tooCerner de usuario, debe seleccionar hello **usuario** rol en el cuadro de diálogo de hello asignación. Los usuarios con el rol de "Acceso predeterminado" Hola se excluyen de aprovisionamiento.


## <a name="configuring-user-provisioning-toocerner-central"></a>Configuración de aprovisionamiento tooCerner centro de usuarios

Esta sección le guía a través de conexión de lista de usuarios de su Azure AD tooCerner Central mediante la API de aprovisionamiento de cuentas de usuario del Cerner SCIM y configurar hello toocreate de servicio de aprovisionamiento, actualizar y deshabilitar cuentas en el centro de Cerner en función de usuario asignado en la asignación de usuario y de grupo en Azure AD.

> [!TIP]
> También puede elegir tooenabled basado en SAML Single Sign-On para Cerner Central, siguiendo instrucciones de hello proporcionadas en [portal de Azure (https://portal.azure.com). El inicio de sesión único puede configurarse independientemente del aprovisionamiento automático, aunque estas dos características se complementan entre sí. Para obtener más información, vea hello [tutorial de inicio de sesión único de centro de Cerner](active-directory-saas-cernercentral-tutorial.md).


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a>cuenta de usuario automática de tooconfigure tooCerner Central de aprovisionamiento en Azure AD:


En orden tooprovision usuario cuentas tooCerner Central, podrá necesita una cuenta de sistema Cerner centro de Cerner toorequest y generar un token de portador de OAuth que Azure AD puede utilizar el punto de conexión del tooconnect tooCerner SCIM. También se recomienda que la integración de Hola se realizan en un entorno de espacio aislado de Cerner antes de implementar tooproduction.

1.  Hola primer paso es personas de hello tooensure administrar Hola Cerner e integración de Azure AD tiene una cuenta de CernerCare, que es necesario tooaccess Hola documentación necesarios toocomplete Hola instrucciones. Si es necesario, usar direcciones URL de hello debajo toocreate CernerCare cuentas en cada entorno es aplicable.

   * Espacio aislado: https://sandboxcernercare.com/accounts/create

   * Producción: https://cernercare.com/accounts/create  

2.  A continuación, se debe crear una cuenta de sistema para Azure AD. Use las instrucciones de hello debajo toorequest una cuenta de sistema para los entornos de producción y de espacio aislado.

   * Instrucciones: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account

   * Espacio aislado: https://sandboxcernercentral.com/system-accounts/

   * Producción: https://cernercentral.com/system-accounts/

3.  A continuación, genere un token de portador de OAuth para cada una de las cuentas del sistema. toodo this, follow Hola estas instrucciones.

   * Instrucciones: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token

   * Espacio aislado: https://sandboxcernercentral.com/system-accounts/

   * Producción: https://cernercentral.com/system-accounts/

4. Por último, debe tooacquire usuario lista territorio identificadores para ambos entornos de espacio aislado y de producción de hello en la configuración de Cerner toocomplete Hola. Para obtener información acerca de cómo tooacquire, vea: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM. 

5. Ahora puede configurar tooCerner de cuentas de usuario de Azure AD tooprovision. Inicie sesión en toohello [portal de Azure](https://portal.azure.com)y examinar toohello **Azure Active Directory > aplicaciones empresariales > todas las aplicaciones** sección.

6. Si ya has configurado Cerner Central para el inicio de sesión único, busque la instancia del centro de Cerner mediante el campo de búsqueda de Hola. En caso contrario, seleccione **agregar** y busque **Cerner Central** en Galería de aplicaciones de Hola. Seleccione Cerner Central en los resultados de búsqueda de Hola y agregarlo a tooyour lista de aplicaciones.

7.  Seleccione la instancia del centro de Cerner, a continuación, seleccione hello **Provisioning** ficha.

8.  Conjunto hello **modo de aprovisionamiento** demasiado**automática**.

   ![Aprovisionamiento de Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  Rellene Hola después de campos en **las credenciales de administrador**:

   * Hola **dirección URL del inquilino** , a continuación, escriba una dirección URL en formato de hello siguiente, reemplazando "User-lista-dominio-ID" con el Id. de dominio Kerberos de hello adquiridos en el paso 4 de #.

> Espacio aislado: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

> Producción: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

   * Hola **secreto Token** campo, escriba el token de portador de OAuth de Hola que generó en el paso 3 de # y haga clic en **Probar conexión**.

   * Verá una notificación de éxito en el lado superior derecho de hello del portal.

10. Escriba la dirección de correo electrónico de Hola de una persona o grupo que debe recibir las notificaciones de error aprovisionamiento en hello **correo electrónico de notificación** campo y comprobar Hola casilla incluida a continuación.

11. Haga clic en **Guardar**. 

12. Hola **asignaciones de atributos** sección, revise el usuario de Hola y toobe de atributos de grupo sincronizado desde Azure AD tooCerner Central. Hola atributos seleccionados como **coincidencia** propiedades son cuentas de usuario de hello toomatch utilizado y los grupos en Cerner Central para las operaciones de actualización. Seleccione toocommit de botón de hello guardar los cambios.

13. tooenable Hola servicio de aprovisionamiento de Azure AD para Cerner Central, cambio hello **estado de aprovisionamiento** demasiado**en** en hello **configuración** sección

14. Haga clic en **Guardar**. 

Esto inicia la sincronización inicial de Hola de los usuarios o grupos asignados tooCerner Central en la sección usuarios y grupos de Hola. la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se esté ejecutando Hola servicio de aprovisionamiento de Azure AD. Puede usar hello **detalles de sincronización** sección toomonitor progreso y siga los informes de actividad del tooprovisioning vínculos, que describen todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación de centro de Cerner.

Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

## <a name="additional-resources"></a>Recursos adicionales

* [Cerner Central: Publishing identity data using Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD) (Cerner Central: Publicación de datos de identidad mediante Azure AD)
* [Tutorial: configuración de Cerner Central para el inicio de sesión único con Azure Active Directory](active-directory-saas-cernercentral-tutorial.md)
* [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](active-directory-enterprise-apps-manage-provisioning.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Pasos siguientes
* [Obtenga información acerca de cómo se registra tooreview y get informa sobre el aprovisionamiento de actividad](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).
