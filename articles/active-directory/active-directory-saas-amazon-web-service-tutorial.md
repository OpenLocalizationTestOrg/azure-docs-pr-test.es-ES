---
title: "Tutorial: Integración de Azure Active Directory con Amazon Web Services (AWS) | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Amazon Web Services (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a>Tutorial: integración de Azure Active Directory con Amazon Web Service (AWS)

En este tutorial, aprenderá cómo toointegrate Amazon Web Services (AWS) con Azure Active Directory (Azure AD).

Integración de Amazon Web Services (AWS) con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooAmazon Web Services (AWS)
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAmazon Web Services (AWS) (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con Amazon Web Services (AWS), necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Suscripción habilitada para el inicio de sesión único en Amazon Web Services (AWS)

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Adición de Amazon Web Services (AWS) desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a>Adición de Amazon Web Services (AWS) desde la Galería de Hola
integración de hello tooconfigure de Amazon Web Services (AWS) en Azure AD, deberá tooadd Amazon Web Services (AWS) de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Amazon Web Services (AWS) desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[Portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Amazon Web Services (AWS)**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. En el panel de resultados de hello, seleccione **Amazon Web Services (AWS)**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Amazon Web Services (AWS) con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Amazon Web Services (AWS) es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Amazon Web Services (AWS) debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Amazon Web Services (AWS).

tooconfigure y prueba de inicio de sesión único en Azure AD con Amazon Web Services (AWS), deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Creación de un usuario de prueba de Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave un equivalente de Britta Simon en Amazon Web Services (AWS) que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Amazon Web Services (AWS).

**tooconfigure inicio de sesión único en Azure AD con Amazon Web Services (AWS), lleve a cabo Hola pasos:**

1. Hola Portal de Azure, en hello **Amazon Web Services (AWS)** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. En hello **Amazon Web Services (AWS) dominio y las direcciones URL** sección, hello usuario no tiene tooperform todos los pasos tal y como aplicación hello ya está integrado previamente con Azure.

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. Hola aplicación de Software de Amazon Web Services (AWS) espera las aserciones de SAML de hello en un formato concreto. Configure Hola después de notificaciones para esta aplicación. Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones. Hola siguiente captura de pantalla muestra un ejemplo de esto.

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:
    
    | Nombre del atributo  | Valor de atributo | Espacio de nombres |
    | --------------- | --------------- | --------------- |
    | RoleSessionName | user.userprincipalname | https://aws.amazon.com/SAML/Attributes |
    | Rol            | user.assignedroles |  https://aws.amazon.com/SAML/Attributes |
    
    >[!TIP]
    >Necesita tooconfigure Hola aprovisionamiento de usuarios en Azure AD toofetch todos los roles de Hola desde la consola de AWS. Consulte Hola pasos de aprovisionamiento.

    a. Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    b. Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    c. De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila. Agregue el valor de Namespace de hello tal como se indica anteriormente.
    
    d. Haga clic en **Aceptar**.

7. Haga clic en **guardar** botón Configuración de hello toosave en Azure.

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. En otra ventana del explorador, sitio de empresa de Amazon Web Services (AWS) tooyour de inicio de sesión como administrador.

9. Haga clic en **Página principal de la consola**.
   
    ![Configurar inicio de sesión único][11]

10. Haga clic en **IAM** en el servicio **Security, Identity & Compliance** (Seguridad, identidad y cumplimiento).
   
    ![Configurar inicio de sesión único][12]

11. Haga clic en **Proveedores de identidades** y, después, en **Create Provider** (Crear proveedor).
   
    ![Configurar inicio de sesión único][13]

12. En hello **Configurar proveedor** cuadro de diálogo, siga los pasos de hello:
   
    ![Configurar inicio de sesión único][14]
 
    a. En **Tipo de proveedor**, seleccione **SAML**.

    b. Hola **nombre de proveedor** cuadro de texto, escriba un nombre de proveedor (p. ej.: *WAAD*).

    c. tooupload el archivo de metadatos descargado, haga clic en **Elegir archivo**.

    d. Haga clic en **Siguiente paso**.

13. En hello **Compruebe la información de proveedor** página del cuadro de diálogo, haga clic en **crear**. 
    
    ![Configurar inicio de sesión único][15]

14. Haga clic en **Roles** y, después, en **Crear nuevo rol**. 
    
    ![Configurar inicio de sesión único][16]

15. En hello **establecer el nombre de rol** cuadro de diálogo, realizar Hola pasos: 
    
    ![Configurar inicio de sesión único][17] 

    a. Hola **nombre de la función** cuadro de texto, escriba un nombre de rol (p. ej.: *TestUser*). 

    b. Haga clic en **Siguiente paso**.

16. En hello **Seleccionar tipo de rol** cuadro de diálogo, realizar Hola pasos: 
    
    ![Configurar inicio de sesión único][18] 

    a. Seleccione **Rol de acceso del proveedor de identidades**. 

    b. Hola **Grant Web Single Sign-On (WebSSO) tooSAML proveedores de acceso a** sección, haga clic en **seleccione**.

17. En hello **establecer confianza** cuadro de diálogo, realizar Hola pasos:  
    
    ![Configurar inicio de sesión único][19] 

    a. Como proveedor SAML, seleccione el proveedor SAML de Hola que haya creado previamente (p. ej.: *WAAD*)
  
    b. Haga clic en **Siguiente paso**.

18. En hello **comprobar confiar en rol** cuadro de diálogo, haga clic en **siguiente paso**.
    
    ![Configurar inicio de sesión único][32]

19. En hello **asociar directiva** cuadro de diálogo, haga clic en **siguiente paso**.
    
    ![Configurar inicio de sesión único][33]

20. En hello **revisión** cuadro de diálogo, realizar Hola pasos:
    
    ![Configurar inicio de sesión único][34]
 
    a. Haga clic en **Crear rol**.

    b. Cree tantos roles según sea necesario y asignarlos toohello proveedor de identidades.

21. Configurar todos los roles de Hola de AWS toofetch el aprovisionamiento de usuario de Hola

    a. En el inicio de sesión de consola de AWS de Hola con la cuenta raíz

    b. En hello esquina superior derecha, haga clic en su nombre y, a continuación, haga clic en hello **mis credenciales de seguridad** opción. Se abrirá una pantalla como un mensaje de advertencia. Haga clic en el botón de hello **las credenciales de seguridad** toopass botón Hola pantalla.
        
       ![Configurar inicio de sesión único][36]

       ![Configurar inicio de sesión único][37]

    c. Hola claves de acceso de sección, haga clic en hello **crear una nueva clave de acceso** botón. Esto genera hello Id. de clave de acceso y un valor de token.
    
       ![Configurar inicio de sesión único][38]

    d. Copie estos dos valores y descárguelos para no perderlos.

    e. Hola Portal de Azure, en la página de integración de aplicaciones de Amazon Web Services (AWS) hello, haga clic en **Provisioning**.
        
       ![Configurar inicio de sesión único][35]

    f. Establecer el modo de aprovisionamiento de hello demasiado**automática**
        
       ![Configurar inicio de sesión único][39]

    g. Ahora en hello **clientsecret** y **secreto Token** pegue los valores correspondientes de hello, que han copiado desde la consola de AWS.
    
    h. Puede hacer clic en hello **Probar conexión** botón conectividad de hello tootest. Una vez que es correcta, a continuación, puede empezar a Hola aprovisionamiento conector.
       
       ![Configurar inicio de sesión único][40]

    i. Ahora habilitar Hola estado de aprovisionamiento demasiado**en**. Esto inicia capturar roles Hola de aplicación hello.

       ![Configurar inicio de sesión único][41]

    > [!NOTE]
    > Azure se ejecuta el servicio AD aprovisionamiento cada después de algunos roles de hello toosync de tiempo de AWS. Debería ver Hola todos los proveedor de identidades adjunta roles AWS en Azure AD y se puede utilizar al asignar Hola aplicación toousers o grupos.

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-an-amazon-web-services-test-user"></a>Creación de un usuario de prueba de Amazon Web Services

En orden tooenable toolog de los usuarios de Azure AD en tooAmazon Web Services (AWS), se les deben aprovisionar en Amazon Web Services (AWS). En caso de hello de Amazon Web Services (AWS), el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour **Amazon Web Services (AWS)** como administrador.

2. Haga clic en hello **inicial de la consola** icono. 
   
    ![Configurar inicio de sesión único][11]

3. Haga clic en Administración de identidades y acceso. 
   
    ![Configurar inicio de sesión único][28]

4. Hola panel, haga clic en **usuarios**y, a continuación, haga clic en **crear nuevos usuarios**. 
   
    ![Configurar inicio de sesión único][29]

5. En el cuadro de diálogo de hello Create User, realizar Hola pasos: 
   
    ![Configurar inicio de sesión único][30]   
    
    a. Hola **escriba los nombres de usuario** cuadros de texto, escriba el nombre de usuario de Brita Simon (userprincipalname) en Azure AD.

    b. Haga clic en **Create** (Crear).
        
### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooAmazon de acceso Web Services (AWS).

![Asignar usuario][200] 

**tooassign Britta Simon tooAmazon Web Services (AWS), lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Amazon Web Services (AWS)**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. En **Seleccionar rol** ficha, seleccione Hola un rol adecuado para el usuario de Hola. Todas estas funciones se muestran con el nombre de la función de Hola y el nombre del proveedor de identidad. De esta forma que puede identificar fácilmente los roles de Hola de AWS.

8. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello Amazon Web Services (AWS) el icono Panel de acceso de hello, deberá obtener tooyour automáticamente firmado en aplicaciones de Amazon Web Services (AWS). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
