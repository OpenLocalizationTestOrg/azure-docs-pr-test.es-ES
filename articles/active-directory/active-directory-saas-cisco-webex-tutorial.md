---
title: "Tutorial: Integración de Azure Active Directory con Cisco Webex | Microsoft Azure"
description: "¡Obtenga información acerca de cómo toouse Cisco Webex con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>Tutorial: integración de Azure Active Directory con Cisco Webex
objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Cisco Webex.  
escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

* Una suscripción de Azure válida
* Un inquilino de Cisco Webex

Después de completar este tutorial, Hola usuarios de Azure AD que haya asignado tooCisco Webex será capaz de toosingle inicio de sesión en la aplicación hello en el sitio de la compañía de Cisco Webex (servicio iniciado por el proveedor inicio de sesión), o mediante hello [toohello de introducción Obtener acceso al Panel](active-directory-saas-access-panel-introduction.md).

escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:

* Habilitar la integración de aplicación Hola para Cisco Webex
* Configuración del inicio de sesión único (SSO)
* Configuración del aprovisionamiento de usuario
* Asignación de usuarios

![Escenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Escenario")

## <a name="enable-hello-application-integration-for-cisco-webex"></a>Habilitar la integración de aplicación Hola para Cisco Webex
objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Cisco Webex.

**integración de aplicaciones de hello tooenable para Cisco Webex, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
   ![Aplicaciones](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Aplicaciones")
4. Haga clic en **agregar** final Hola de página Hola.
   
   ![Agregar aplicaciones](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Agregar aplicaciones")
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
   ![Agregar una aplicación de la galería](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Agregar una aplicación de la galería")
6. Hola **cuadro de búsqueda**, tipo **Cisco Webex**.
   
   ![Galería de aplicaciones](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Galería de aplicaciones")
7. En el panel de resultados de hello, seleccione **Cisco Webex**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
   ![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")
   
## <a name="configure-single-sign-on"></a>Configurar inicio de sesión único

objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooCisco Webex con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.  

Como parte de este procedimiento, se le toocreate requiere un certificado codificado en base 64. Si no está familiarizado con este procedimiento, vea [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **Cisco Webex** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurar inicio de sesión único")
2. En hello **¿cómo desea que los usuarios toosign en tooCisco Webex** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurar inicio de sesión único")
3. En hello **configurar URL de aplicación** página realizar pasos de Hola y, a continuación, haga clic en **siguiente**.
   
   ![Configurar dirección URL de la aplicación](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurar dirección URL de la aplicación")   
   1. Hola **cantar URL** cuadro de texto, escriba la dirección URL de inquilino de Cisco Webex (p. ej.: *http://contoso.webex.com*).
   2. Hola **dirección URL de respuesta de Cisco Webex** cuadro de texto, tipo de su **dirección URL de AssertionConsumerService de Cisco Webex** (p. ej.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).
4. En hello **configurar inicio de sesión único en Cisco Webex** page, toodownload su certificado, haga clic en **Descargar certificado**y, a continuación, guarde el archivo de certificado de hello en el equipo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurar inicio de sesión único")
5. En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Cisco Webex.
6. En el menú de hello en la parte superior de hello, haga clic en **administración de sitios**.
   
   ![Administración de sitios](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Administración de sitios")
7. Hola **Administrar sitio** sección, haga clic en **configuración de SSO**.
   
   ![Configuración de SSO](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "Configuración de SSO")
8. En la sección de configuración de SSO Web federado hello, realizar Hola pasos:
   
   ![Configuración de SSO federado](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Configuración de SSO federado")  
   1. De hello **protocolo Federation** lista, seleccione **SAML 2.0**.
   2. Cree un archivo **codificado en base 64** a partir del certificado descargado.  
    >[!TIP]
    >Para obtener más información, vea [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)
    >  
   3. Abra el certificado codificado en base 64 en el Bloc de notas y, a continuación, Hola copia contenido del mismo.
   4. Haga clic en **Import SAML Metadata**(Importar metadatos de SAML) y, a continuación, pegue el certificado codificado base 64.
   5. En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Cisco Webex** página de diálogo, Hola copia **dirección URL del emisor** valor y, a continuación, péguelo en hello **emisor de SAML (Id. de IdP)** cuadro de texto.
   6. En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Cisco Webex** página de diálogo, Hola copia **dirección URL de inicio de sesión remoto** valor y, a continuación, péguelo en hello **inicio de sesión del servicio de SSO de cliente Dirección URL** cuadro de texto.
   7. De hello **NameID Format** lista, seleccione **dirección de correo electrónico**.
   8. Hola **AuthnContextClassRef** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:2.0:ac:classes:Password**.
   9. En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Cisco Webex** página de diálogo, Hola copia **dirección URL de cierre de sesión remoto** valor y, a continuación, péguelo en hello **cierre de sesión del servicio de SSO de cliente Dirección URL** cuadro de texto.
   10. Haga clic en **Update**(Actualizar).
9. En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Cisco Webex** página del cuadro de diálogo, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar**.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurar inicio de sesión único")
   
## <a name="configure-user-provisioning"></a>Configurar aprovisionamiento de usuarios

En orden tooenable toolog de los usuarios de Azure AD en Cisco Webex, se les deben aprovisionar en Cisco Webex.  

* En caso de hello de Cisco Webex, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**

1. Inicie sesión en tooyour **Cisco Webex** inquilino.
2. Vaya demasiado**administrar usuarios \> Agregar usuario**.
   
   ![Agregar usuarios](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Agregar usuarios")
3. En la sección Agregar usuario hello, realizar Hola pasos:
   
   ![Agregar usuario](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Agregar usuario")   
   1. En **Account Type** (Tipo de cuenta) seleccione **Host**.
   2. Escribir información de Hola de un usuario de Azure AD existente en hello siguientes cuadros de texto: **nombre, apellido**, **nombre de usuario**, **correo electrónico**, **contraseña**, **Confirmar contraseña**.
   3. Haga clic en **Agregar**.

>[!NOTE]
>Puede usar cualquier otra Cisco Webex usuario cuenta herramienta de creación o las API proporcionadas por Cisco Webex tooprovision cuentas de usuario AAD. 
> 

## <a name="assign-users"></a>Asignar usuarios
tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.

**tooassign usuarios tooCisco Webex, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, cree una cuenta de prueba.
2. En hello **Cisco Webex** página de integración de aplicaciones, haga clic en **asignar usuarios**.
   
   ![Asignar usuarios](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Asignar usuarios")
3. Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.
   
   ![Sí](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Sí")

Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

