---
title: "Tutorial: Integración de Azure Active Directory con Workplace by Facebook | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y un área de trabajo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Tutorial: integración de Azure Active Directory con Workplace by Facebook

En este tutorial, aprenderá cómo toointegrate al área de trabajo Facebook con Azure Active Directory (Azure AD).

Integración al área de trabajo Facebook con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooWorkplace Facebook
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWorkplace Facebook (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con un área de trabajo Facebook tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único de Workplace by Facebook

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar un área de trabajo Facebook desde galería Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a>Agregar un área de trabajo Facebook desde galería Hola
integración de hello tooconfigure del área de trabajo Facebook en Azure AD, deberá tooadd al área de trabajo Facebook de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd al área de trabajo Facebook desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **al área de trabajo Facebook**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. En el panel de resultados de hello, seleccione **al área de trabajo Facebook**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección podrá configurar y probar el inicio de sesión único de Azure AD con Workplace by Facebook con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en lugar de trabajo Facebook es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en lugar de trabajo Facebook debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en lugar de trabajo Facebook.

tooconfigure y prueba de inicio de sesión único en Azure AD con un área de trabajo Facebook, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Configurar la frecuencia de la reautenticación](#configuring-reauthentication-frequency) ** -tooconfigure tooprompt de área de trabajo para una comprobación SAML.
3. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
4. **[Crear un área de trabajo por usuario de prueba de Facebook](#creating-a-workplace-by-facebook-test-user) ** -toohave un equivalente de Britta Simon en lugar de trabajo Facebook que es la representación toohello vinculado Azure AD del usuario.
5. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
6. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el área de trabajo por la aplicación de Facebook.

**inicio de sesión único en tooconfigure Azure AD con un área de trabajo Facebook, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **al área de trabajo Facebook** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. En hello **al área de trabajo por dominio de Facebook y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instancename>.facebook.com`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.facebook.com/company/<instancename>`

    > [!NOTE] 
    > Estos valores no son Hola real. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [al área de trabajo al equipo de soporte técnico de cliente de Facebook](https://workplace.fb.com/faq/) tooget estos valores. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. En hello **al área de trabajo por la configuración de Facebook** sección, haga clic en **al área de trabajo configurar Facebook** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. En una ventana del explorador web diferente, tooyour de inicio de sesión al área de trabajo por sitio de la compañía de Facebook como administrador.
  
   > [!NOTE] 
   > Como parte del proceso de autenticación de SAML de hello, al área de trabajo puede usar las cadenas de consulta de seguridad too2.5 kilobytes de tamaño en orden toopass parámetros tooAzure AD.

8. Hola **empresa panel**, vaya toohello **autenticación** ficha.

9. En **autenticación SAML**, seleccione **SSO sólo** desde la lista desplegable de Hola.

10. Los valores de entrada Hola copiados desde **al área de trabajo por la configuración de Facebook** sección del portal de Azure en los campos correspondientes de Hola Hola:

    *   En **dirección URL SAML** cuadro de texto, pegue Hola valo **URL de servicio de inicio de sesión único**, que haya copiado desde el portal de Azure.
    *   En **cuadro de texto de dirección URL del emisor de SAML**, pegue el valor de Hola de **Id. de entidad SAML**, que haya copiado desde el portal de Azure.
    *   En **redireccionamiento de cierre de sesión de SAML** (opcional), pegue el valor de Hola de **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.
    *   Abra su **certificado codificado en base 64** en el Bloc de notas descargado del portal de Azure, copie el contenido de hello del mismo en el Portapapeles y péguelo toothe **certificado SAML** cuadro de texto.

11. Puede que necesite tooenter Hola dirección URL de la audiencia, dirección URL del destinatario, y dirección URL de ACS (servicio de consumidor de aserción) aparece en hello **configuración de SAML** sección.

12. Desplácese toohello inferior de la sección de Hola y haga clic en hello **prueba SSO** botón. Como resultado aparece una ventana emergente en la que se muestra la página de inicio de sesión de Azure AD. Escriba sus credenciales en como tooauthenticate normal. 

    **Solución de problemas:** dirección de correo electrónico de hello Asegúrese de que se devuelve desde Azure AD es Hola igual Hola cuenta de empresa que haya iniciado sesión.

13. Una vez que se ha completado correctamente la prueba de hello, desplácese toohello inferior de la página de Hola y haga clic en hello **guardar** botón.

14. Ahora se presentará a todos los usuarios de Workplace la página de inicio de sesión de Azure AD para la autenticación.

15. **Redirigir el cierre de sesión de SAML (opcional)** - 

    Puede elegir toooptionally configurar una dirección de Url de cierre de sesión de SAML, que puede ser toopoint utilizado en la página de cierre de sesión de Azure AD. Cuando esta opción está habilitada y configurada, usuario de hello ya no será la página de cierre de sesión de toohello dirigida al área de trabajo. En su lugar, el usuario de hello será redirigido toohello url que se agregó en la configuración de redireccionamiento de cierre de sesión de SAML de Hola.


> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="configuring-reauthentication-frequency"></a>Configuración de la frecuencia de reautenticación

Puede configurar tooprompt al área de trabajo para una comprobación SAML cada día, tres días, semanas, dos semanas, mes o nunca.

> [!NOTE] 
>Hello valor mínimo para la comprobación SAML de hello en aplicaciones móviles se establece tooone semana.

También puede forzar un SAML restablecer para todos los usuarios con el botón de hello: autenticación de SAML requiere para todos los usuarios ahora.


### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-workplace-by-facebook-test-user"></a>Creación de un usuario de prueba de Workplace by Facebook

En esta sección se crea un usuario llamado Britta Simon en Workplace by Facebook. Workplace by Facebook admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.

El usuario no tiene que hacer nada en esta sección. Si un usuario no existe en el área de trabajo Facebook, una nueva se crea cuando intente tooaccess al área de trabajo Facebook.

>[!Note]
>Si necesita toocreate manualmente, póngase en contacto con en un usuario [al área de trabajo al equipo de soporte técnico de cliente de Facebook](https://workplace.fb.com/faq/)

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWorkplace Facebook.

![Asignar usuario][200] 

**tooassign tooWorkplace Britta Simon Facebook, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **al área de trabajo Facebook**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del aprovisionamiento de usuarios](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

