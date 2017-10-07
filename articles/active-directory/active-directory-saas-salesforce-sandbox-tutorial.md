---
title: "Tutorial: Integración de Azure Active Directory con Salesforce Sandbox | Microsoft Docs"
description: "Obtenga información acerca de cómo toouse espacio aislado de Salesforce con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Tutorial: Integración de Azure Active Directory con Salesforce Sandbox

objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Salesforce Sandbox.  

>[!TIP]
>Para enviar comentarios, vea hello [página de soporte técnico de Azure](http://go.microsoft.com/fwlink/?LinkId=521878). 
> 

Dé de espacios aislados Hola capacidad toocreate varias copias de su organización en entornos independientes para una serie de propósitos, como desarrollo, prueba y entrenamiento, sin comprometer los datos de Hola y las aplicaciones de la producción de Salesforce organización.  

Para obtener más información, vea [Información general del espacio aislado](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

* Una suscripción de Azure válida
* Un espacio aislado en Salesforce.com

Si aún no tiene un espacio aislado válido en Salesforce.com, deberá toocontact Salesforce.

escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:

1. Habilitar la integración de aplicación Hola para Salesforce Sandbox
2. Configuración del inicio de sesión único (SSO)
3. Habilitación de su dominio
4. Configuración del aprovisionamiento de usuario
5. Asignación de usuarios

![Escenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Escenario")

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a>Habilitar la integración de aplicación Hola para Salesforce Sandbox
objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Salesforce sandbox.

**integración de aplicaciones de hello tooenable para Salesforce sandbox, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
   ![Aplicaciones](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Aplicaciones")
4. Hola tooopen **Galería de aplicaciones**, haga clic en **agregar una aplicación**y, a continuación, haga clic en **agregar una aplicación que mi organización toouse**.
   
   ![¿Especifique qué desea toodo? ¿ ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Especifique qué desea toodo?")
5. Hola **cuadro de búsqueda**, tipo **Salesforce Sandbox**.
   
   ![Galería de aplicaciones](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Galería de aplicaciones")
6. En el panel de resultados de hello, seleccione **Salesforce Sandbox**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")
   
## <a name="configur-single-sign-on-sso"></a>Configuración del inicio de sesión único (SSO)

objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooSalesforce con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.

**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **Salesforce Sandbox** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configurar inicio de sesión único")
2. En hello **¿cómo desea que los usuarios toosign en espacio aislado tooSalesforce** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")
3. En hello **configurar URL de aplicación** página Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL usando Hola sigue el patrón `http://company.my.salesforce.com`y, a continuación, haga clic en **siguiente**.
   
   ![Configurar dirección URL de la aplicación](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configurar dirección URL de la aplicación")
4. Si ya ha configurado un inicio de sesión único para otra instancia de Salesforce Sandbox de su directorio, también debe configurar hello **identificador** toohave Hola el mismo valor que hello **dirección URL de inicio de sesión**. 
 * Hola **identificador** campo puede encontrarse mediante la comprobación de hello **Mostrar configuración avanzada** casilla de verificación de hello **configurar URL de aplicación** página del cuadro de diálogo de Hola.
5. En hello **configurar inicio de sesión único en Salesforce Sandbox** página, haga clic en **Descargar certificado**y, a continuación, guarde el archivo de certificado de hello en el equipo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configurar inicio de sesión único")
6. En otra ventana del explorador web, inicie sesión en su sitio de la compañía del espacio aislado de Salesforce como administrador.
7. En el menú de hello en la parte superior de hello, haga clic en **el programa de instalación**.
   
   ![Instalación](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Instalación")
8. En el panel de navegación de Hola Hola izquierda, haga clic en **controles de seguridad**y, a continuación, haga clic en **configuración de inicio de sesión único**.
   
   ![Configuración de inicio de sesión único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Configuración de inicio de sesión único")
9. En la sección de configuración de inicio de sesión único de hello, realizar Hola pasos:
   
   ![Configuración de inicio de sesión único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Configuración de inicio de sesión único")  
 1.  Seleccione **SAML habilitado**. 
 2.  Haga clic en **Nuevo**.
10. En la sección de configuración de inicio de sesión único de SAML de hello, realizar Hola pasos:
    
    ![Configuración de inicio de sesión único de SAML](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "Configuración de inicio de sesión único de SAML")  
 1. En el cuadro de texto de nombre de hello, escriba el nombre de Hola de configuración de hello (p. ej.: *SPSSOWAAD\_prueba*). 
 2. En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Salesforce Sandbox** página de diálogo, Hola copia **dirección URL del emisor** valor y, a continuación, péguelo en hello **emisor**cuadro de texto.
 3. Hola **Id. de entidad** cuadro de texto, tipo **https://test.salesforce.com** si se trata la primera instancia de Salesforce Sandbox Hola que va a Agregar directorio tooyour. Si ya ha agregado una instancia de Salesforce Sandbox, después de hello **Id. de entidad** tipo Hola **dirección URL de inicio de sesión**, que debe tener este formato:`http://company.my.salesforce.com`   
 4. Haga clic en **examinar** hello tooupload descargado el certificado.  
 5. Como **tipo de identidad SAML**, seleccione **la aserción contiene Hola Id. de federación del objeto de usuario de hello**. 
 6. Como **ubicación de identidad SAML**, seleccione **identidad está en el elemento NameIdentifier de Hola de hello instrucción Subject**.
 7. En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Salesforce Sandbox** página de diálogo, Hola copia **dirección URL de inicio de sesión remoto** valor y, a continuación, péguelo en hello **proveedor de identidades Dirección URL de inicio de sesión** cuadro de texto. 
 8. SFDC no admite el cierre de sesión SAML.  Como alternativa, pegue 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' en hello **URL de cierre de sesión del proveedor de identidades** cuadro de texto.
 9. Para **Service Provider Initiated Request Binding** (Enlace de solicitud iniciada por el proveedor de servicio), seleccione **HTTP POST** (Método HTTP POST). 
 10. Haga clic en **Guardar**.
11. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configurar inicio de sesión único")

## <a name="enable-your-domain"></a>Habilitación del dominio
En esta sección se supone que ya ha creado un dominio.  Para obtener más información, vea [Definición de su nombre de dominio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable su dominio, realizar Hola pasos:**

1. En el panel de navegación izquierdo de hello, haga clic en **Domain Management**y, a continuación, haga clic en **mi dominio.**
   
   ![Mi dominio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "Mi dominio")
   
   >[!NOTE]
   >Asegúrese de que su dominio se ha configurado correctamente. 
   > 
2. Hola **configuración de la página de inicio de sesión** sección, haga clic en **editar**, a continuación, como **servicio de autenticación**, seleccione nombre de Hola de hello configuración de inicio de sesión único de SAML de hello anterior sección y, por último, haga clic en **guardar**.
   
   ![Mi dominio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "Mi dominio")

Tan pronto como tiene configurado un dominio, los usuarios deben usar toohello Salesforce sandbox de hello dominio URL toologin.  

valor de hello tooget de dirección URL de hello, haga clic en perfil SSO de Hola que haya creado en la sección anterior de Hola.

## <a name="configure-user-provisioning"></a>Configurar aprovisionamiento de usuarios
objetivo de Hola de esta sección es toooutline cómo tooenable el aprovisionamiento de usuarios de usuario de Active Directory cuentas tooSalesforce espacio aislado.

**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**

1. En el portal de Salesforce hello, en la barra de navegación superior de hello, seleccione su nombre tooexpand el menú del usuario:
   
   ![Mi configuración](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Mi configuración")
2. En el menú del usuario, seleccione **My Settings** tooopen su **My Settings** página.
3. En el panel izquierdo de hello, haga clic en **Personal** tooexpand Hola sección Personal y, a continuación, haga clic en **restablecer mi Token de seguridad**:
   
   ![Mi configuración](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Mi configuración")
4. En hello **restablecer mi Token de seguridad** página, haga clic en **restablecer Token de seguridad** toorequest un correo electrónico que contiene el token de seguridad de Salesforce.com.
   
   ![Nuevo token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "Nuevo token")
5. Compruebe en su bandeja de entrada de correo electrónico si le ha llegado un correo electrónico de Salesforce.com con el asunto "**salesforce.com.com security confirmation**" (confirmación de seguridad de salesforce.com.com).
6. Revise este correo electrónico y copie Hola seguridad valor de token.
7. En el portal de Azure clásico en Hola Hola **espacio aislado de salesforce** página de integración de aplicaciones, haga clic en **configurar aprovisionamiento de usuario** tooopen hello **configurar el aprovisionamiento de usuarios**cuadro de diálogo.
   
   ![Configurar aprovisionamiento de usuarios](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configurar aprovisionamiento de usuarios")
8. En hello **escriba el aprovisionamiento automático de usuarios de Salesforce Sandbox credenciales tooenable** , proporcione Hola siguientes opciones de configuración:
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")   
 1. Hola **nombre de usuario de administrador de espacio aislado de Salesforce** cuadro de texto, escriba un espacio aislado de Salesforce de cuenta de nombre que ha Hola **administrador del sistema** perfil asignado en Salesforce.com.
 2. Hola **contraseña de administrador de espacio aislado de Salesforce** cuadro de texto, escriba la contraseña de Hola para esta cuenta.
 3. Hola **el Token de seguridad de usuario** cuadro de texto, valor de token de seguridad de Hola de pegar.
 4. Haga clic en **validar** tooverify su configuración.
 5. Haga clic en hello **siguiente** Hola de botón tooopen **confirmación** página.
9. En hello **confirmación** página, haga clic en **completar** toosave su configuración.
   
## <a name="assigning-users"></a>Asignación de usuarios

tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.

**tooassign usuarios tooSalesforce espacio aislado, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, cree una cuenta de prueba.
2. En Hola ** Salesforce Sandbox ** página de integración de aplicaciones, haga clic en **asignar usuarios**.
   
   ![Asignar usuarios](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Asignar usuarios")
3. Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.
   
   ![Sí](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Sí")

Ahora debe esperar 10 minutos y comprobar si la cuenta de hello se ha sincronizado tooSalesforce espacio aislado.

Si desea tootest la configuración de SSO, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](https://msdn.microsoft.com/library/dn308586).

