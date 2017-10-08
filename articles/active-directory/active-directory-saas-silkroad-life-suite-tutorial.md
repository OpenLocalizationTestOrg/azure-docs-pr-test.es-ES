---
title: "Tutorial: Integración de Azure Active Directory con SilkRoad Life Suite | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SilkRoad vida Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a>Tutorial: Integración de Azure Active Directory con SilkRoad Life Suite
objetivo de Hola de este tutorial es tooshow, cómo toointegrate SilkRoad vida Suite con Azure Active Directory (Azure AD). 

Integración SilkRoad vida Suite con Azure AD proporciona Hola siguientes ventajas: 

* Puede controlar en Azure AD que tenga acceso tooSilkRoad Suite de vida 
* Puede habilitar la get ha iniciado sesión tooSilkRoad de usuarios tooautomatically vida Suite inicio de sesión único (SSO) con sus cuentas de Azure AD

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos
integración de Azure AD con Suite de vida de SilkRoad tooconfigure, necesita Hola siguientes elementos:

* Una suscripción de Azure AD
* Una suscripción habilitada para el SSO en SilkRoad Life Suite

>[!NOTE]
>Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción. 
> 

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

* No debe usar el entorno de producción, a menos que sea necesario.
* Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descripción del escenario
objetivo de Hola de este tutorial es tooenable tootest Azure AD SSO en un entorno de prueba.

escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar conjunto de vida de SilkRoad de galería de Hola 
2. Configuración y prueba del inicio de sesión único de Azure AD

## <a name="add-silkroad-life-suite-from-hello-gallery"></a>Agregar conjunto de vida de SilkRoad de galería de Hola
integración de hello tooconfigure del conjunto de vida SilkRoad en Azure AD, deberá tooadd SilkRoad vida Suite de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd SilkRoad Suite de vida de la Galería de hello, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**. 
   
    ![Active Directory][1]

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Aplicaciones][2]

4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Aplicaciones][3]

5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Aplicaciones][4]

6. En el cuadro de búsqueda de hello, escriba **SilkRoad vida Suite**.
   
    ![Aplicaciones][5]

7. En el panel de resultados de hello, seleccione **SilkRoad vida Suite**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
    ![Aplicaciones][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de Azure AD SSO con SilkRoad vida Suite a partir de un usuario de prueba denominado "Britta Simon".

Para toowork SSO, Azure AD necesita tooknow es qué usuario equivalente de hello en usuario de tooan SilkRoad vida Suite en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SilkRoad vida Suite debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en SilkRoad vida Suite.

tooconfigure y prueba de inicio de sesión único en Azure AD con SilkRoad vida Suite, deberá hello toocomplete después de bloques de creación:

1. **[Configuración del inicio de sesión único en Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba del conjunto de vida de SilkRoad](#creating-a-silkroad-life-suite-test-user)**  -toohave un equivalente de Britta Simon SilkRoad vida conjunto de representación toohello vinculado Azure AD de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD
objetivo de Hola de esta sección es tooenable Azure AD SSO en el portal de Azure clásico de Hola y tooconfigure SSO en la aplicación SilkRoad vida Suite.

**tooconfigure inicio de sesión único en Azure AD con SilkRoad vida Suite, lleve a cabo Hola pasos:**

1. Sitio de empresa de SilkRoad tooyour de inicio de sesión como administrador. 

  >[!NOTE] 
  > tooobtain acceso toohello autenticación de conjunto de vida de SilkRoad de aplicación para configurar la federación con Microsoft Azure AD, póngase en contacto con soporte técnico de SilkRoad o con su representante de servicios de SilkRoad.
  > 

2. Vaya demasiado**proveedor de servicios**y, a continuación, haga clic en **detalles de la federación**. 
   
    ![Inicio de sesión único de Azure AD ][10] 

3. Haga clic en **descargar metadatos de federación**y, a continuación, guarde el archivo de metadatos de hello en el equipo.
   
    ![Inicio de sesión único de Azure AD ][11] 

4. En el portal de Azure clásico en Hola Hola **SilkRoad vida Suite** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**  cuadro de diálogo.
   
    ![Configurar inicio de sesión único][6] 

5. En hello **¿cómo desea que los usuarios toosign en tooSilkRoad Suite de vida** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Inicio de sesión único de Azure AD ][7] 

6. En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:
   
    ![Inicio de sesión único de Azure AD ][8]   
 1. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por el sitio de los usuarios en toosign tooyour SilkRoad vida Suite (p. ej.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).  
 2. Abra Hola descargado **Silkroad** archivo de metadatos. 
 3. Busque hello **AssertionConsumerService** etiqueta y, a continuación, Hola copia **ubicación** atributo.         
   
    ![Inicio de sesión único de Azure AD ][21] 
 4. Pegue el valor de hello en hello **dirección URL de respuesta** cuadro de texto.  
 5. Haga clic en **Siguiente**.

6. En hello **configurar inicio de sesión único en el conjunto de vida de SilkRoad** , siga los pasos de hello:
   
    ![Inicio de sesión único de Azure AD ][9]  
 1. Haga clic en Descargar certificado y, a continuación, guarde el archivo hello en el equipo.  
 2. Haga clic en **Siguiente**.

7. En la aplicación **SilkRoad**, haga clic en **Authentication Sources** (Orígenes de autenticación).
   
    ![Inicio de sesión único de Azure AD ][12] 

8. Haga clic en **Add Authentication Source**(Agregar origen de autenticación). 
   
    ![Inicio de sesión único de Azure AD ][13] 

9. Hola **agregar origen de autenticación** sección, lleve a cabo Hola pasos: 
   
    ![Inicio de sesión único de Azure AD ][14]  
 1. En **opción 2: archivo de metadatos**, haga clic en **examinar** hello tooupload descargado el archivo de metadatos.  
 2. Haga clic en **Create Identity Provider using File Data**(Crear proveedor de identidades con los datos del archivo).

10. Hola **fuentes de autenticación** sección, haga clic en **editar**. 
    
     ![Inicio de sesión único de Azure AD ][15] 

11. En hello **Editar origen de autenticación** cuadro de diálogo, realizar Hola pasos: 
    
     ![Inicio de sesión único de Azure AD ][16] 
 1. En **Enabled** (Habilitado), seleccione **Yes** (Sí).   
 2. Hola **IdP descripción** cuadro de texto, escriba una descripción para la configuración (p. ej.: *SSO de Azure AD*).  
 3. Hola **nombre IdP** cuadro de texto, escriba un nombre de configuración específico tooyour (p. ej.: *Azure SP*).  
 4. Haga clic en **Guardar**.

12. Deshabilite todos los demás orígenes de autenticación. 
    
     ![Inicio de sesión único de Azure AD ][17]

13. En el portal de Azure clásico en Hola Hola **única confirmación de inicio de sesión** página, haga clic en **siguiente**.  
    
     ![Inicio de sesión único de Azure AD ][18]

14. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.
    
     ![Inicio de sesión único de Azure AD ][19]

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de Azure clásico que se llama a Britta Simon hello toocreate.

![Creación de un usuario de Azure AD][20]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**. 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello: 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. En Tipo de usuario, seleccione Nuevo usuario de la organización.  
 2. En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**. 
 3. Haga clic en **Siguiente**.

6. En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello: 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. Hola **nombre** cuadro de texto, tipo **Bárbara**.    
 2. Hola **Last Name** cuadro de texto, tipo, **Simon**. 
 3. Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**. 
 4. Hola **rol** lista, seleccione **usuario**.
 5. Haga clic en **Siguiente**.

7. En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. Anote el valor de Hola de hello **nueva contraseña**. 
 2. Haga clic en **Completo**.   

### <a name="create-a-silkroad-life-suite-test-user"></a>Creación de un usuario de prueba de SilkRoad Life Suite
objetivo de Hola de esta sección es un usuario llamado a Britta Simon en conjunto de vida de SilkRoad toocreate. Bárbara debe tener un Id. de SSO (a veces denominado tooas una *AuthParam*) que coincide con la de Bárbara **emailaddress** en Azure AD.

**toocreate un usuario llamado Britta Simon en conjunto de vida SilkRoad, lleve a cabo Hola pasos:**

- Solicite a su toocreate de equipo de soporte técnico de SilkRoad vida Suite un usuario que tenga como **Id. de SSO** Hola atributo mismo valor que hello **emailaddress** de Britta Simon en Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD
objetivo de Hola de esta sección es tooenable Britta Simon toouse Azure SSO mediante la concesión de su conjunto de vida de tooSilkRoad de acceso.

![Asignar usuario][200] 

**tooassign Britta Simon tooSilkRoad Suite de vida, lleve a cabo Hola pasos:**

1. En hello Azure portal clásico, vista de aplicaciones de hello tooopen, en la vista de directorio de hello, haga clic en **aplicaciones** en el menú superior Hola.
   
    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **SilkRoad vida Suite**.
   
    ![Asignar usuario][202] 

3. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.
   
    ![Asignar usuario][203] 

4. En la lista de usuarios de hello, seleccione **Britta Simon**.

5. En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.
   
    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único
objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.  

Al hacer clic en icono de conjunto de vida SilkRoad Hola Hola Panel de acceso, deberá obtener la aplicación de conjunto de vida de SilkRoad tooyour automáticamente ha iniciado sesión.

## <a name="additional-resources"></a>Recursos adicionales
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





