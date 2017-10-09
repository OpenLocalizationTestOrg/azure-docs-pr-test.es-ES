---
title: "Tutorial: integración de Azure Active Directory con TOPdesk - Secure | Microsoft Docs"
description: "Obtenga información acerca de cómo toouse TOPdesk - Secure con Azure Active Directory tooenable inicio de sesión único, aprovisionamiento automático y mucho más!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a>Tutorial: integración de Azure Active Directory con TOPdesk - Secure
objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y TOPdesk - Secure.  
escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

* Una suscripción de Azure válida
* Una suscripción habilitada para el inicio de sesión único en TOPdesk - Secure

Después de completar este tutorial, los usuarios de hello Azure AD que haya asignado tooTOPdesk - will segura puede toosingle capaz de inicio de sesión en la aplicación hello en TOPdesk - sitio de la compañía seguros (servicio iniciado por el proveedor inicio de sesión), o mediante hello [Introducción Panel de acceso de toohello](active-directory-saas-access-panel-introduction.md).

escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:

1. Habilitar la integración de aplicación Hola para TOPdesk - Secure
2. Configuración del inicio de sesión único
3. Configuración del aprovisionamiento de usuario
4. Asignación de usuarios

![Escenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Escenario")

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a>Habilitar la integración de aplicación Hola para TOPdesk - Secure
objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para TOPdesk - Secure.

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a>integración de aplicaciones de hello tooenable para TOPdesk - Secure, lleve a cabo Hola pasos:
1. Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Aplicaciones](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Aplicaciones")

4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Agregar aplicaciones](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Agregar aplicaciones")

5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Agregar una aplicación de la galería](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Agregar una aplicación de la galería")

6. Hola **cuadro de búsqueda**, tipo **TOPdesk - Secure**.
   
    ![Galería de aplicaciones](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Galería de aplicaciones")

7. En el panel de resultados de hello, seleccione **TOPdesk - Secure**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
    ![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")

## <a name="configuring-single-sign-on"></a>Configuración del inicio de sesión único
objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooTOPdesk - Secure con su cuenta de Azure AD utilizando federación basada en hello protocolo SAML.  
Configurar inicio de sesión único para TOPdesk - Secure requiere tooupload un archivo de icono de logotipo. archivo de icono de hello tooget, equipo de soporte técnico de TOPdesk Hola contacto.

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a>tooconfigure inicio de sesión único, lleve a cabo Hola pasos:
1. Inicio de sesión tooyour **TOPdesk - Secure** sitio de la empresa como administrador.
2. Hola **TOPdesk** menú, haga clic en **configuración**.
   
    ![Configuración](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configuración")

3. Haga clic en **Login Settings**(Configuración de inicio de sesión).
   
    ![Configuración de inicio de sesión](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configuración de inicio de sesión")

4. Expanda hello **configuración de inicio de sesión** menú y, a continuación, haga clic en **General**.
   
    ![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")

5. Hola **seguro** sección de hello **inicio de sesión SAML** configuración sección, lleve a cabo Hola pasos:
   
    ![Configuración técnica](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Configuración técnica")
   
    a. Haga clic en **descargar** toodownload Hola archivo de metadatos públicos y, a continuación, guardarlo localmente en el equipo.
   
    b. Abra el archivo de metadatos de hello y, a continuación, busque hello **AssertionConsumerService** nodo.
    
    ![Servicio de consumidor de aserciones](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Servicio de consumidor de aserciones")
   
    c. Hola copia **AssertionConsumerService** valor.  
      
    > [!NOTE]
    > Se necesita Hola valor Hola **configurar URL de aplicación** sección más adelante en este tutorial.
    > 
    > 

6. En otra ventana del explorador web, inicie sesión en su **Portal de Azure clásico** como administrador.

7. En hello **TOPdesk - Secure** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen Hola ** configurar inicio de sesión único ** cuadro de diálogo.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurar inicio de sesión único")

8. En hello **¿cómo quiere como usuarios toosign en tooTOPdesk - Secure** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurar inicio de sesión único")

9. En hello **configurar URL de aplicación** , siga los pasos de hello:
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurar dirección URL de la aplicación")
   
    a. Hola **TOPdesk - Secure URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por su toosign a los usuarios en la aplicación TOPdesk - Secure (p. ej.: "*https://qssolutions.topdesk.net*").
   
    b. Hola **TOPdesk – Public Reply URL** cuadro de texto, pegue hello **TOPdesk - Secure AssertionConsumerService URL** (p. ej.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")
   
    c. Haga clic en **Siguiente**.

10. En hello **configurar inicio de sesión único en TOPdesk - Secure** page, toodownload el archivo de metadatos, haga clic en **descargar metadatos**y, a continuación, guardar archivo hello localmente en el equipo.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurar inicio de sesión único")

11. toocreate un archivo de certificado, lleve a cabo Hola pasos:
    
    ![Certificado](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificado")
    
    a. Archivo de metadatos descargado Hola abierto.
    b. Expanda hello **RoleDescriptor** nodo que tenga un **xsi: Type** de **fed: ApplicationServiceType**.
    c. Copiar valor de Hola de hello **X509Certificate** nodo.
    d. Hola Guardar copia **X509Certificate** valor localmente en el equipo en un archivo.

12. En TOPdesk - Secure sitio de la empresa, en hello **TOPdesk** menú, haga clic en **configuración**.
    
    ![Configuración](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configuración")

13. Haga clic en **Login Settings**(Configuración de inicio de sesión).
    
    ![Configuración de inicio de sesión](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configuración de inicio de sesión")

14. Expanda hello **configuración de inicio de sesión** menú y, a continuación, haga clic en **General**.
    
    ![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")

15. Hola **público** sección, haga clic en **agregar**.
    
    ![Agregar](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Agregar")

16. En hello **Asistente de configuración de SAML** cuadro de diálogo, siga los pasos de hello:
    
    ![Asistente para configuración de SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Asistente de configuración de SAML")
    
    a. tooupload en los metadatos descargados archivo **metadatos de federación**, haga clic en **examinar**.

    b. tooupload archivo su certificado, en **certificado (RSA)**, haga clic en **examinar**.

    c. que se obtuvo al equipo de soporte técnico de TOPdesk hello, en el archivo de logotipo de hello tooupload **icono del logotipo de**, haga clic en **examinar**.

    d. Hola **atributo de nombre de usuario** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    e. Hola **nombre para mostrar** cuadro de texto, escriba un nombre para la configuración.

    f. Haga clic en **Guardar**.

17. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurar inicio de sesión único")

## <a name="configuring-user-provisioning"></a>Configuración del aprovisionamiento de usuario
En orden tooenable Azure AD a los usuarios toolog en TOPdesk - Secure, debe aprovisionar en TOPdesk - Secure.  
En caso de hello de TOPdesk - Secure, el aprovisionamiento es una tarea manual.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprovisionamiento de usuario, realizar Hola pasos:
1. Inicio de sesión tooyour **TOPdesk - Secure** como administrador.
2. En el menú de hello en la parte superior de hello, haga clic en **TOPdesk \> New \> archivos auxiliares \> operador**.
   
    ![Operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operador")

3. En hello **New (operador)** cuadro de diálogo, realizar Hola pasos:
   
    ![New operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "Nuevo operador")
   
    a. Haga clic en la ficha General de Hola.
   
    b. Hola **apellido** cuadro de texto de hello **General** sección, escriba Hola apellidos de una cuenta válida de Azure Active Directory que desee tooprovision.
   
    c. Seleccione un **sitio** de cuenta de hello en hello **ubicación** sección.
   
    d. Hola **nombre de inicio de sesión** cuadro de texto de hello **inicio de sesión de TOPdesk** sección, escriba un nombre de inicio de sesión para el usuario.
   
    e. Haga clic en **Guardar**.

> [!NOTE]
> Puede usar cualquier otra TOPdesk - cuenta de usuario segura herramientas de creación o las API proporcionadas por TOPdesk - Secure tooprovision cuentas de usuario AAD.
> 
> 

## <a name="assigning-users"></a>Asignación de usuarios
tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a>tooassign usuarios tooTOPdesk - Secure, realizar Hola pasos:
1. Hola portal de Azure clásico, cree una cuenta de prueba.
2. En Hola ** TOPdesk - Secure ** página de integración de aplicaciones, haga clic en **asignar usuarios**.
   
    ![Asignar usuarios](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Asignar usuarios")

3. Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.
   
    ![Sí](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Sí")

Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

