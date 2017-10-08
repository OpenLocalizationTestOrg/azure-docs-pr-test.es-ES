---
title: "Tutorial: Integración de Azure Active Directory con Questetra BPM Suite | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>Tutorial: Integración de Azure Active Directory con Questetra BPM Suite
objetivo de Hola de este tutorial es tooshow, cómo toointegrate Questetra BPM Suite con Azure Active Directory (Azure AD).  
Integración Questetra BPM Suite con Azure AD proporciona Hola siguientes ventajas: 

* Puede controlar en Azure AD que tenga acceso tooQuestetra conjunto de BPM 
* Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooQuestetra BPM Suite (Single Sign-On) con sus cuentas de Azure AD
* Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos
integración de Azure AD con Questetra BPM Suite tooconfigure, necesita Hola siguientes elementos:

* Una suscripción de Azure AD
* Una suscripción habilitada para el inicio de sesión único en [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/)

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.
> 
> 

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

* No debe usar el entorno de producción, a menos que sea necesario.
* Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descripción del escenario
objetivo de Hola de este tutorial es tooenable tootest inicio de sesión único en Azure AD en un entorno de prueba.  
escenario de Hello descrito en este tutorial consta de tres pilares principales:

1. Agregar conjunto de BPM Questetra desde galería Hola 
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a>Agregar conjunto de BPM Questetra desde galería Hola
integración de hello tooconfigure de Questetra BPM Suite en Azure AD, deberá tooadd Questetra BPM Suite de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Questetra BPM Suite de galería de hello, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**. 
   
    ![Active Directory][1]

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Aplicaciones][2]

4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Aplicaciones][3]

5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Aplicaciones][4]

6. En el cuadro de búsqueda de hello, escriba **Questetra BPM Suite**.
   
    ![Aplicaciones][5]

7. En el panel de resultados de hello, seleccione **Questetra BPM Suite**y, a continuación, haga clic en **completar** aplicación de hello tooadd.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de inicio de sesión único en Azure AD con Questetra BPM Suite a partir de un usuario de prueba denominado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow es qué usuario equivalente de hello en usuario de tooan Questetra BPM Suite en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el conjunto de BPM Questetra debe toobe establecido.  
Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Questetra BPM Suite.

tooconfigure y prueba de inicio de sesión único en Azure AD con Questetra BPM Suite, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba del conjunto de BPM Questetra](#creating-a-questetra-bpm-suite-test-user)**  -toohave un equivalente de Britta Simon Questetra BPM conjunto de representación toohello vinculado Azure AD de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD
objetivo de Hola de esta sección es tooenable Azure AD single sign-on en hello portal de Azure clásico y tooconfigure inicio de sesión único en la aplicación Questetra BPM Suite.

**tooconfigure inicio de sesión único en Azure AD con Questetra BPM Suite, lleve a cabo Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **Questetra BPM Suite** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**  cuadro de diálogo.
   
    ![Configurar inicio de sesión único][8]

2. En hello **¿cómo desea que los usuarios toosign en tooQuestetra BPM Suite** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Inicio de sesión único de Azure AD ][9]

3. En otra ventana del explorador web, inicie sesión en el sitio de la compañía de **Questetra BPM Suite** como administrador.

4. En el menú de hello en la parte superior de hello, haga clic en **configuración del sistema**. 
   
    ![Inicio de sesión único de Azure AD ][10]

5. Hola tooopen **SingleSignOnSAML** página, haga clic en **SSO (SAML)**. 
   
    ![Inicio de sesión único de Azure AD ][11]

6. En el portal de Azure clásico en Hola Hola **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello: 
   
    ![Configurar las opciones de la aplicación][13]
   
    a. Depende de usted **Questetra BPM Suite** sitio de la empresa, en la sección de información de SP hello, Hola copia **dirección URL de ACS**y, a continuación, péguelo en hello **dirección URL de inicio de sesión** cuadro de texto.
   
    b. Depende de usted **Questetra BPM Suite** sitio de la empresa, en la sección de información de SP hello, Hola copia **Id. de entidad**y, a continuación, péguelo en hello **dirección URL del emisor** cuadro de texto.
   
    c. Depende de usted **Questetra BPM Suite** sitio de la empresa, en la sección de información de SP hello, Hola copia **dirección URL de ACS**y, a continuación, péguelo en hello **dirección URL de respuesta** cuadro de texto.
   
    d. Haga clic en **Siguiente**.

7. En hello **configurar inicio de sesión único en el conjunto de BPM Questetra** página, haga clic en **Descargar certificado**y, a continuación, guarde el archivo de certificado de hello localmente en el equipo.
   
    ![Configurar inicio de sesión único][14]

8. Depende de usted **Questetra BPM Suite** sitio de la compañía, lleve a cabo Hola pasos: 
   
    ![Configurar inicio de sesión único][15]
   
    a. Seleccione **Enable Single Sign-On**(Habilitar inicio de sesión único).
   
    b. En el portal de Azure clásico hello, copie hello **dirección URL del emisor** valor y, a continuación, péguelo en hello **Id. de entidad** cuadro de texto.
   
    c. En el portal de Azure clásico hello, copie hello **URL de servicio de inicio de sesión único** valor y, a continuación, péguelo en hello **URL de la página de inicio de sesión** cuadro de texto.
   
    d. En el portal de Azure clásico hello, copie hello **dirección URL del servicio de cierre de sesión único** valor y, a continuación, péguelo en hello **URL de la página de cierre de sesión** cuadro de texto.
   
    e. Hola **formato de NameID** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: emailAddress**.

    f. Cree un archivo codificado en base 64 a partir del certificado descargado. 

    >[!TIP] 
    >Para obtener más información, consulte [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o).

    g. Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo en hello **certificado de validación** cuadro de texto. 

    h. Haga clic en **Guardar**.

1. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**. 
   
    ![Qué es Azure AD Connect][17]

2. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.  
   
    ![Qué es Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de Azure clásico que se llama a Britta Simon hello toocreate.

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Creación de un usuario de prueba de Azure AD][100] 

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.
   
    ![Creación de un usuario de prueba de Azure AD][101] 

4. Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**. 
   
    ![Creación de un usuario de prueba de Azure AD][102] 

5. En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD][103]
   
    a. En **Tipo de usuario**, seleccione **Nuevo usuario de la organización**.
   
    b. En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.
   
    c. Haga clic en Siguiente.

6. En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello: 
   
    ![Creación de un usuario de prueba de Azure AD][104] 
   
    a. Hola **nombre** cuadro de texto, tipo **Bárbara**. 
   
    b. Hola **Last Name** cuadro de texto, tipo, **Simon**.
   
    c. Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.
   
    d. Hola **rol** lista, seleccione **usuario**.
   
    e. Haga clic en **Siguiente**.

7. En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.
   
    ![Creación de un usuario de prueba de Azure AD][105]  

8. En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD][106]   
   
    a. Anote el valor de Hola de hello **nueva contraseña**.
   
    b. Haga clic en **Completo**.   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Creación de un usuario de prueba de Questetra BPM Suite
objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en Questetra BPM Suite.

**toocreate un usuario llamado Britta Simon en Questetra BPM Suite, lleve a cabo Hola pasos:**

1. Sitio de empresa de Questetra BPM Suite tooyour inicio de sesión como administrador.
2. Vaya demasiado**configuración del sistema > lista de usuarios > nuevo usuario**. 
3. Cuadro de diálogo nuevo usuario de hello, realizar Hola pasos: 
   
    ![Creación de un usuario de prueba][300] 
   
    a. Hola **nombre** cuadro de texto, escriba el nombre de usuario de Bárbara en Azure AD.
   
    b. Hola **correo electrónico** cuadro de texto, escriba el nombre de usuario de Bárbara en Azure AD.
   
    c. Hola **contraseña** cuadro de texto, escriba una contraseña.

4. Haga clic en **Add new user**(Agregar nuevo usuario).

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD
objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure inicio de sesión único mediante la concesión de su conjunto de BPM tooQuestetra de acceso.

![Qué es Azure AD Connect][200]

**tooassign Britta Simon tooQuestetra BPM Suite, lleve a cabo Hola pasos:**

1. En hello Azure portal clásico, vista de aplicaciones de hello tooopen, en la vista de directorio de hello, haga clic en **aplicaciones** en el menú superior Hola.
   
    ![Qué es Azure AD Connect][201]
2. En la lista de aplicaciones de hello, seleccione **Questetra BPM Suite**.
   
    ![Qué es Azure AD Connect][205]
3. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.
   
    ![Qué es Azure AD Connect][202]
4. En la lista de usuarios de hello, seleccione **Britta Simon**.
   
    ![Qué es Azure AD Connect][203]
5. En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.
   
    ![Qué es Azure AD Connect][204]

### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 
objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.  
Al hacer clic en icono de conjunto de BPM Questetra Hola Hola Panel de acceso, deberá obtener la aplicación de conjunto de BPM Questetra tooyour automáticamente ha iniciado sesión.

## <a name="additional-resources"></a>Recursos adicionales
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
