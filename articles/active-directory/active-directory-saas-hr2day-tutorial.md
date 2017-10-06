---
title: "Tutorial: integración de Azure Active Directory con HR2day by Merces | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y HR2day por Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>Tutorial: Integración de Azure Active Directory con HR2day by Merces

En este tutorial, aprenderá cómo toointegrate HR2day por Merces con Azure Active Directory (Azure AD).

Integración HR2day por Merces con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooHR2day por Merces.
- Puede permitir a los usuarios tooautomatically obtener inicia sesión en tooHR2day Merces con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con HR2day por Merces tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD.
- Una suscripción habilitada para el inicio de sesión único en HR2day by Merces.

> [!NOTE]
> No se recomienda usar un Hola de tootest del entorno de producción de los pasos en este tutorial.

pasos de hello tootest en este tutorial, siga estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Puede obtener [un versión de evaluación gratuita de un mes de Azure AD](https://azure.microsoft.com/pricing/free-trial/) si aún no la tiene.  

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hola que se detallan en este documento consta de dos bloques principales:

1. Agregar HR2day por Merces desde la Galería de Hola.
2. Configuración y prueba del inicio de sesión único de Azure AD

## <a name="add-hr2day-by-merces-from-hello-gallery"></a>Agregar HR2day por Merces de galería de Hola
integración de hello tooconfigure de HR2day por Merces en Azure AD, agregue HR2day por Merces de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd HR2day por Merces de galería de hello, tomar Hola pasos:**

1. Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, seleccione hello **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Vaya demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd una nueva aplicación, seleccione hello **nueva aplicación** botón en la parte superior de Hola Hola del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **HR2day por Merces**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. En el panel de resultados de hello, seleccione **HR2day por Merces**y, a continuación, seleccione hello **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con HR2day by Merces con un usuario de prueba llamado "Britta Simon."

Para toowork de inicio de sesión único, Azure AD necesita tooknow quién Hola homólogo usuario en HR2day por Merces tooa usuario en Azure AD. En otras palabras, necesita tooestablish un vínculo entre un usuario de Azure AD y el usuario relacionado de hello en HR2day por Merces.

En HR2day por Merces, asigne hello **nombre de usuario** en Azure AD demasiado **nombre de usuario** relación de hello tooestablish.

tooconfigure y prueba de inicio de sesión único en Azure AD con HR2day por Merces, deberá hello toocomplete después de bloques de creación:

1. [Configurar inicio de sesión único en Azure AD](#configuring-azure-ad-single-sign-on): habilitar el toouse de los usuarios de esta característica.
2. [Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user): pruebe el inicio de sesión único de Azure AD con Britta Simon.
3. [Crear un HR2day por usuario de prueba de Merces](#creating-an-hr2day-by-merces-test-user): crear un equivalente de Britta Simon en HR2day por Merces que es la representación toohello vinculado Azure AD del usuario.
4. [Asignar el usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user): habilitar Britta Simon toouse inicio de sesión único en Azure AD.
5. [Probar el inicio de sesión único](#testing-single-sign-on): comprobar si la configuración de hello funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en su HR2day Merces aplicación.

**inicio de sesión único en Azure AD tooconfigure con HR2day por Merces, tomar Hola pasos:**

1. En el portal de Azure, en Hola Hola **HR2day por Merces** página de integración de aplicaciones, seleccione **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. tooenable inicio de sesión único, Hola **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML**.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. Hola **HR2day Merces dominio y las direcciones URL** sección, llevar Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro, escriba una dirección URL mediante el uso de hello siguiente patrón: `https://<tenantname>.force.com/<instancename>`.

    b. Hola **identificador** cuadro, escriba una dirección URL mediante el uso de hello siguiente patrón: `https://hr2day.force.com/<companyname>`.

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con URL de inicio de sesión real de Hola y el identificador. Póngase en contacto con hello [HR2day equipo de soporte técnico de cliente de Merces](mailto:servicedesk@merces.nl) tooget estos valores. 
 


4. En hello **el certificado de firma de SAML** sección, seleccione **Certificate(Base64)**y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. Esta sección se describe cómo tooenable usuarios tooauthenticate tooHR2day por Merces con su cuenta en Azure AD. Para hacerlo mediante el uso de federación que se basa en hello protocolo SAML.

    Su HR2day Merces aplicación espera las aserciones de SAML de hello en un formato específico, que requiere el token SAML de tooyour de asignaciones de atributo personalizado de tooadd. Hola siguiente captura de pantalla muestra un ejemplo de esto. 

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    Para poder configurar la aserción de SAML de hello, debe ponerse en contacto con hello [HR2day equipo de soporte técnico de Merces cliente](mailto:servicedesk@merces.nl) y solicite el valor de Hola de atributo del identificador único de hello para el inquilino. Necesita esta valor toocomplete Hola se analiza en la sección siguiente Hola. 

6. Hola **inicio de sesión único** cuadro de diálogo hello **atributos de usuario** sección, configure el atributo de token de SAML de hello como se muestra en hello después de la imagen. A continuación, tomar Hola pasos.
    
      | Nombre del atributo    |   Valor de atributo |  
    | ------------------- | -------------------- |    
    | ATTR_LOGINCLAIM | join([mail],"102938475Z","@" |
    
      a. Hola tooopen **Agregar atributo** cuadro de diálogo, seleccione **Agregar atributo**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    b. Hola **nombre** , escriba **ATTR_LOGINCLAIM**.

    c. De hello **valor** lista, seleccione **Join()**.

    d. De hello **String1** lista, seleccione **user.mail**.

    e. Para **String2**, escriba Hola identificador único proporcionado por el equipo de HR2day.

    f. Hola **separador** , escriba  **@** .
    
    g. Seleccione **Aceptar**.

7. Seleccione hello **guardar** botón.

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. Hola **HR2day por la configuración de Merces** sección, seleccione **HR2day configurar por Merces** tooopen hello **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión**, **Id. de entidad SAML**, y **SAML Single Sign-On dirección URL del servicio** de hello **referencia rápida** sección.

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. tooconfigure SSO para su aplicación, póngase en contacto con hello [HR2day Merces equipo de soporte técnico de cliente](mailTo:servicedesk@merces.nl). Adjuntar Hola descargado **Certificate(Base64)** correo electrónico tooyour de archivos. También proporcionan hello **dirección URL de cierre de sesión**, **Id. de entidad SAML**, y **SAML Single Sign-On dirección URL del servicio** para que se pueden configurar para la integración de SSO.

    > [!NOTE]
    >Indique el equipo de Merces toohello que esta integración debe Hola toobe de Id. de entidad establecida con el patrón de hello **https://hr2day.force.com/INSTANCENAME**.

    > [!TIP]
    >Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory** > **aplicaciones empresariales** sección, seleccione hello **Single Sign-On** ficha. Hola acceso incrusta documentación a través de hello **configuración** sección final Hola. Puede leer más acerca de la característica de documentación de embedded Hola Hola [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, tomar Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, seleccione hello **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, seleccione **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, seleccione **agregar** en la parte superior de Hola Hola del cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. Hola **usuario** cuadro de diálogo, Hola toman pasos:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro, Hola de tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña**a continuación, anote la contraseña de Hola.

    d. Seleccione **Crear**.
 
### <a name="create-an-hr2day-by-merces-test-user"></a>Creación de un usuario de prueba de HR2day by Merces

objetivo de Hola de esta sección es un usuario llamado a Britta Simon en HR2day Merces toocreate. los usuarios de hello tooadd en la cuenta de hello HR2day, trabajar con hello [HR2day Merces equipo de soporte técnico de cliente](mailto:servicedesk@merces.nl). 

> [!NOTE]
> Si necesita un usuario toocreate manualmente, póngase en contacto con hello [HR2day Merces equipo de soporte técnico de cliente](mailto:servicedesk@merces.nl).

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooHR2day acceso por Merces.

![Asignar usuario][200] 

**tooassign Britta Simon tooHR2day por Merces, tome Hola pasos:**

1. Hola Azure ver aplicaciones de portal, abra Hola, vaya toohello vista del directorio y, a continuación, vaya demasiado**aplicaciones empresariales**. A continuación, seleccione **Todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **HR2day por Merces**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. En el menú de Hola Hola izquierda, seleccione **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Seleccione hello **agregar** botón. A continuación, en hello **Agregar asignación** cuadro de diálogo, seleccione **usuarios y grupos**.

    ![Asignar usuario][203]

5. Hola **usuarios y grupos** cuadro de diálogo hello **usuarios** lista, seleccione **Britta Simon**.

6. Haga clic en hello **seleccione** botón.

7. Hola **Agregar asignación** cuadro de diálogo, seleccione **asignar**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

Hola objetivo de esta sección es tootest su único inicio de sesión en configuración de Azure AD mediante el uso de Hola Panel de acceso.  

Al seleccionar hello HR2day Merces icono en el Panel de acceso de hello, que automáticamente obtener iniciado sesión en tooyour HR2day Merces aplicación.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

