---
title: "Tutorial: Integración de Azure Active Directory con Freshdesk | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a>Tutorial: Integración de Azure Active Directory con Freshdesk

En este tutorial, aprenderá cómo toointegrate FreshDesk con Azure Active Directory (Azure AD).

Integración FreshDesk con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooFreshDesk
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFreshDesk (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con FreshDesk tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en FreshDesk

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar FreshDesk desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-freshdesk-from-hello-gallery"></a>Agregar FreshDesk desde la Galería de Hola
integración de hello tooconfigure de FreshDesk en Azure AD, deberá tooadd FreshDesk de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd FreshDesk de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **FreshDesk**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. En el panel de resultados de hello, seleccione **FreshDesk**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con FreshDesk con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en FreshDesk es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en FreshDesk debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en FreshDesk.

tooconfigure y prueba de inicio de sesión único en Azure AD con FreshDesk, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de FreshDesk](#creating-a-freshdesk-test-user)**  -toohave un equivalente de Britta Simon en FreshDesk que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Freshservice.

**inicio de sesión único en tooconfigure Azure AD con FreshDesk, siga Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **FreshDesk** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. En hello **FreshDesk dominio y las direcciones URL** sección, escriba Hola **dirección URL de inicio de sesión** como: `https://<tenant-name>.freshdesk.com` o cualquier otro valor que le sugiere Freshdesk.

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > Tenga en cuenta que este no es el valor real. Tiene que actualizar este valor con la dirección URL de inicio de sesión real. Póngase en contacto con el [equipo de soporte técnico de FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) para obtener este valor.  

4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado** y, a continuación, guarde el certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. En hello **configuración de FreshDesk** sección, haga clic en **FreshDesk configurar** ventana tooopen configurar inicio de sesión. Copiar Hola SAML Single Sign-On dirección URL del servicio y la dirección URL de cierre de sesión de hello **referencia rápida** sección.

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Freshdesk como administrador.

8. En el menú de hello en la parte superior de hello, haga clic en **administración**.
   
   ![Administración](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Administración")

9. Hola **configuración General** , haga clic en **seguridad**.
   
   ![Seguridad](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Seguridad")

10. Hola **seguridad** sección, lleve a cabo Hola pasos:
   
    ![Inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "inicio de sesión único")
   
    a. En **Inicio de sesión único (SSO)**, seleccione **Activado**.

    b. Seleccione **Inicio de sesión único de SAML**.

    c. Hola de tipo **SAML Single Sign-On dirección URL del servicio** copió desde el portal de Azure en hello **dirección URL de inicio de sesión de SAML** cuadro de texto.

    d. Hola de tipo **dirección URL de cierre de sesión** copió desde el portal de Azure en hello **Logout URL** cuadro de texto.

    e. Hola copia **huella digital** valor de certificado de hello descargado del portal de Azure y péguelo en hello **huella digital de certificado de seguridad** cuadro de texto.  
 
    >[!TIP]
    >Para obtener más información, consulte [cómo tooretrieve valor de huella digital del certificado](http://youtu.be/YKQF266SAxI). 
    
    f. Haga clic en **Guardar**.


### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-freshdesk-test-user"></a>Creación de un usuario de prueba de FreshDesk

En orden tooenable toolog de los usuarios de Azure AD en FreshDesk, se les deben aprovisionar en FreshDesk.  
En caso de hello de FreshDesk, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**

1. Inicie sesión en tooyour **Freshdesk** inquilino.
2. En el menú de hello en la parte superior de hello, haga clic en **administración**.
   
   ![Administración](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Administración")

3. Hola **configuración General** , haga clic en **agentes**.
   
   ![Agentes](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agentes")

4. Haga clic en **Nuevo agente**.
   
    ![Nuevo agente](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "Nuevo agente")

5. En el cuadro de diálogo de información de agentes de hello, realizar Hola pasos:
   
   ![Información sobre agentes](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Información sobre agentes")
   
   a. Hola **nombre completo** cuadro de texto, nombre de cuenta de hello Azure AD que desee tooprovision Hola de tipo.

   b. Hola **correo electrónico** cuadro de texto, hello Azure AD de tipo dirección de correo electrónico de cuenta de hello Azure AD que desea tooprovision.

   c. Hola **título** cuadro de texto, escriba el título de cuenta de hello Azure AD que desea tooprovision Hola.

   d. Seleccione **Agents role** (Rol de agentes) y luego haga clic en **Asignar**.
       
   e. Haga clic en **Guardar**.     
   
    >[!NOTE]
    >titular de cuenta de Hello Azure AD recibirá un correo electrónico que incluye una cuenta de hello tooconfirm vínculo antes de activarse. 
    > 
    
    >[!NOTE]
    >Puede usar cualquier otra Freshdesk usuario cuenta herramienta de creación o las API proporcionadas por Freshdesk tooprovision cuentas de usuario AAD. tooFreshDesk.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su cuadro de herramientas de acceso.

![Asignar usuario][200] 

**tooassign Britta Simon tooFreshDesk, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **FreshDesk**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de FreshDesk Hola Hola Panel de acceso, deberá obtener inicio de sesión página tooget ha iniciado sesión tooyour aplicación Freshservice.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

