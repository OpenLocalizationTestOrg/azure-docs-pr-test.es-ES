---
title: "Tutorial: Integración de Azure Active Directory con LearnUpon | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a>Tutorial: Integración de Azure Active Directory con LearnUpon

En este tutorial, aprenderá cómo toointegrate LearnUpon con Azure Active Directory (Azure AD).

Integración LearnUpon con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooLearnUpon
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLearnUpon (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con LearnUpon tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en LearnUpon

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar LearnUpon desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-learnupon-from-hello-gallery"></a>Agregar LearnUpon desde la Galería de Hola
integración de hello tooconfigure de LearnUpon en Azure AD, deberá tooadd LearnUpon de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd LearnUpon de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **LearnUpon**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. En el panel de resultados de hello, seleccione **LearnUpon**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con LearnUpon con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en LearnUpon es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en LearnUpon debe toobe establecido.

En LearnUpon, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con LearnUpon, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba LearnUpon](#creating-a-learnupon-test-user)**  -toohave un equivalente de Britta Simon en LearnUpon que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación LearnUpon.

**inicio de sesión único en Azure AD tooconfigure con LearnUpon, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **LearnUpon** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. En hello **LearnUpon dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.learnupon.com/saml/consumer`

    > [!NOTE] 
    > Tenga en cuenta que esto no es un valor real Hola. tiene este valor con la dirección URL de respuesta real hello tooupdate. tooget este valor póngase en contacto con [equipo de soporte técnico de LearnUpon](https://www.learnupon.com/features/support/).



4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Raw)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. En hello **LearnUpon configuración** sección, haga clic en **configurar LearnUpon** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. Abra otra instancia del explorador e inicie sesión en LearnUpon con una cuenta de administrador. 

8. Haga clic en hello **configuración** ficha.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. Haga clic en **Single Sign On - SAML**y, a continuación, haga clic en **configuración General** tooconfigure configuración de SAML.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. Hola **configuración General** sección, lleve a cabo Hola pasos:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    a. Seleccione **Habilitado**.

    b. Seleccione la **versión** **2.0**.

    c. En **Skip conditions** (Omitir condiciones), haga clic en **No**.

    d. Hola **publicar Token de SAML param nombre** cuadro de texto Nombre de solicitud post parámetro toohello dirección URL del consumidor SAML indicada anteriormente que contiene toobe de aserción de SAML de hello comprueban y autentican - por ejemplo hello de tipo  **SAMLResponse**.

    e. Hola **formato de nombre de identificador** cuadro de texto, valor de Hola de tipo que indica dónde en los usuarios de Hola de aserción de SAML identificador (dirección de correo electrónico) reside - por ejemplo **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: emailAddress**.
  
    f. Hola **identificar la ubicación del proveedor** cuadro de texto, valor de Hola de tipo que indica dónde hello se envían tooif a los usuarios hagan clic en el icono cargada desde la pantalla de inicio de sesión de portal Azure.
  
    g. Hola **cerrar sesión URL** cuadro de texto, pegue hello **dirección URL de cierre de sesión** que haya copiado desde Hola portal de Azure.
    
    h. Haga clic en **administrar huellas dactilares**y, a continuación, cargar la huella dactilar de Hola del certificado descargado.

11. Haga clic en **configuración de usuario**y, a continuación, realizar Hola pasos:
   
     ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    a. Hola **formato del identificador de nombre** cuadro de texto, valor de tipo de Hola que nos indica cuando, en su firstname de los usuarios de aserción de SAML Hola reside - por ejemplo: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.
  
    b. Hola **formato de identificador de nombre de último** cuadro de texto, valor de tipo de Hola que nos indica cuando, en su lastname de los usuarios de aserción de SAML Hola reside - por ejemplo: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-learnupon-test-user"></a>Creación de un usuario de prueba de LearnUpon

objetivo de Hola de esta sección es un usuario llamado a Britta Simon en LearnUpon toocreate. LearnUpon admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.

No hay ningún elemento de acción para usted en esta sección. Si no existe todavía, se creará un nuevo usuario durante un tooaccess intento LearnUpon. [Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-single-sign-on).

>[!NOTE]
>Si necesita un usuario toocreate manualmente, necesita toocontact [equipo de soporte técnico de LearnUpon](https://www.learnupon.com/features/support/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLearnUpon.

![Asignar usuario][200] 

**tooassign Britta Simon tooLearnUpon, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **LearnUpon**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de LearnUpon Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour LearnUpon aplicación.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

