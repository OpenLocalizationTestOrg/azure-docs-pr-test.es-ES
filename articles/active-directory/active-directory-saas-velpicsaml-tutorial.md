---
title: "Tutorial: Integración de Azure Active Directory con Velpic SAML | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Velpic SAML."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a>Tutorial: Integración de Azure Active Directory con Velpic SAML

En este tutorial, aprenderá cómo toointegrate Velpic SAML con Azure Active Directory (Azure AD).

Integración Velpic SAML con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooVelpic SAML
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooVelpic SAML (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con Velpic SAML, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Velpic SAML

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Velpic SAML desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-velpic-saml-from-hello-gallery"></a>Agregar Velpic SAML desde la Galería de Hola
integración de hello tooconfigure de Velpic SAML en Azure AD, deberá tooadd Velpic SAML en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Velpic SAML de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Velpic SAML**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. En el panel de resultados de hello, seleccione **Velpic SAML**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Velpic SAML utilizando un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Velpic SAML es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Velpic SAML debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Velpic SAML.

tooconfigure y prueba de inicio de sesión único en Azure AD con Velpic SAML, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave un equivalente de Britta Simon en Velpic SAML que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Velpic SAML.

**inicio de sesión único en Azure AD tooconfigure con Velpic SAML, siga Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **Velpic SAML** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. Escriba los detalles de Hola Hola **Velpic SAML dominio y las direcciones URL** sección:

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello como:`https://<sub-domain>.velpicsaml.net`

    b. Hola **identificador** cuadro de texto, pegue hello **'Solo la dirección URL de inicio de sesión'** valor`https://auth.velpic.com/saml/v2/<entity-id>/login`
    
    > [!NOTE]
    > Tenga en cuenta que Hola equipo Velpic SAML proporcionarán Hola dirección URL de inicio de sesión y el valor de identificador estarán disponible al configurar Hola complemento SSO en el lado de Velpic SAML. Debe toocopy que valor de página de la aplicación Velpic SAML y péguelo aquí.

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. En la sección de configuración de SAML Velpic hello, haga clic en configurar Velpic SAML tooopen configurar inicio de sesión en la ventana. Copie Hola Id. de entidad de SAML de hello sección de referencia rápida.

7. En otra ventana del explorador web, inicie sesión como administrador en su sitio de la compañía de Velpic SAML.

8. Haga clic en **administrar** pestaña e ir demasiado**integración** sección donde se necesitan tooclick en **complementos** botón toocreate nuevo complemento para el inicio de sesión.

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. Haga clic en hello **'Agregar complemento'** botón.
    
    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. Haga clic en hello **SAML** disponer en mosaico en la página Agregar complemento de Hola.
    
    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. Escriba nombre Hola de nuevo complemento SAML hello y haga clic en hello **'Add'** botón.

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. Escriba los detalles de hello como se indica a continuación:

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    a. Hola **nombre** cuadro de texto, nombre de tipo hello de complemento SAML.

    b. Hola **dirección URL del emisor** cuadro de texto, pegue hello **Id. de entidad SAML** que copió de hello **configurar inicio de sesión** ventana de hello portal de Azure.

    c. Hola **configuración de metadatos del proveedor** cargar Hola archivo Metadata XML que descargó desde el portal de Azure.

    d. También puede elegir tooenable SAML aprovisionamiento justo a tiempo habilitando hello **'Creación automática de nuevos usuarios'** casilla de verificación. Si un usuario no existe en Velpic y esta marca no está habilitada, se producirá un error de inicio de sesión de Hola de Azure. Si marca Hola estará habilitado Hola usuario automáticamente aprovisionar en Velpic en tiempo de Hola de inicio de sesión. 

    e. Hola copia **en dirección URL de inicio de sesión único** de cuadro de texto de Hola y lo pega en Hola portal de Azure.
    
    f. Haga clic en **Guardar**.

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-velpic-saml-test-user"></a>Creación de un usuario de prueba de Velpic SAML

Normalmente este paso no es necesario que sea compatible con aplicación hello justo a tiempo el aprovisionamiento de usuarios. Si no está habilitado el aprovisionamiento automático de usuarios de hello creación manual del usuario puede realizarse tal y como se describe a continuación.

Inicie sesión como administrador en su sitio de la compañía de Velpic SAML y realice los pasos siguientes:
    
1. Haga clic en la ficha administrar y vaya sección tooUsers, a continuación, haga clic en nuevo botón tooadd usuarios.

    ![agregar usuario](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. En hello **"Crear nuevo usuario"** cuadro de diálogo, siga los pasos de Hola.

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    a. Hola **nombre** cuadro de texto Nombre tipo hello de Britta Simon.

    b. Hola **Last Name** cuadro de texto, escriba Hola apellidos de Britta Simon.

    c. Hola **nombre de usuario** cuadro de texto, escriba el nombre de usuario de Hola de Britta Simon.

    d. Hola **correo electrónico** cuadro de texto, dirección de correo electrónico de Hola de tipo de cuenta de Britta Simon.

    e. Resto de información de hello es opcional, que puede rellenar si es necesario.
    
    f. Haga clic en **GUARDAR**.  

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooVelpic acceso SAML.

![Asignar usuario][200] 

**tooassign Britta Simon tooVelpic SAML, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Velpic SAML**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

1. Al hacer clic en hello Velpic SAML disponer en mosaico en hello Panel de acceso, deberá obtener la página de inicio de sesión de aplicación Velpic SAML. Debería ver Hola **'Iniciar sesión con Azure AD'** botón de inicio de sesión de hello en la página.

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. Haga clic en hello **'Iniciar sesión con Azure AD'** toolog de botón en tooVelpic con su cuenta de Azure AD.


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

