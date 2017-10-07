---
title: "Tutorial: Integración de Azure Active Directory con Workplace by Facebook | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y un área de trabajo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Tutorial: integración de Azure Active Directory con Workplace by Facebook

En este tutorial, aprenderá cómo toointegrate al área de trabajo Facebook con Azure Active Directory (Azure AD).

Integración al área de trabajo Facebook con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooWorkplace Facebook.
- Puede permitir a los usuarios tooautomatically obtener firmado en tooWorkplace Facebook (inicio de sesión único) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con un área de trabajo Facebook tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único (SSO) de Workplace by Facebook

pasos de hello tootest en este tutorial, siga estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único (SSO) de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar un área de trabajo Facebook de hello Galería.
2. Configuración y prueba del inicio de sesión único en Azure AD.

## <a name="add-workplace-by-facebook-from-hello-gallery"></a>Agregar un área de trabajo Facebook de galería de Hola
integración de hello tooconfigure del área de trabajo Facebook en Azure AD, agregue al área de trabajo Facebook de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

1. Hola [portal de Azure](https://portal.azure.com), en el panel izquierdo de Hola, seleccione **Azure Active Directory**. 

    ![botón de Hello Azure Active Directory][1]

2. Examinar demasiado**aplicaciones empresariales** > **todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd Hola nueva aplicación, seleccione **nueva aplicación** en la parte superior de Hola Hola del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **al área de trabajo Facebook**y seleccione **al área de trabajo Facebook** de resultados. A continuación, seleccione **agregar**, aplicación de hello tooadd.

    ![Área de trabajo Facebook en la lista de resultados de Hola](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección podrá configurar y probar el SSO de Azure AD con Workplace by Facebook con un usuario de prueba llamado "Britta Simon".

Para toowork SSO, Azure AD necesita tooknow qué usuario equivalente de hello en lugar de trabajo Facebook es tooa usuario en Azure AD. En otras palabras, se debe establecer una relación entre un usuario de Azure AD y el usuario relacionado de hello en lugar de trabajo Facebook vinculada.

Establecer esta relación mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en lugar de trabajo Facebook.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, se habilita el SSO de Azure AD en hello portal de Azure y configurar SSO en el área de trabajo por la aplicación de Facebook.

1. En el portal de Azure, en Hola Hola **al área de trabajo Facebook** página de integración de aplicaciones, seleccione **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. Hola **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable SSO.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. Hola **al área de trabajo por dominio de Facebook y las direcciones URL** sección, Hola siguientes:

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL que utiliza Hola siguiente patrón:`https://<company subdomain>.facebook.com`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL que utiliza Hola siguiente patrón:`https://www.facebook.com/company/<scim company id>`

    > [!NOTE]
    > Estos valores son solo un ejemplo. Actualizar estos valores con URL de inicio de sesión real de Hola y el identificador. Póngase en contacto con hello [al área de trabajo al equipo de soporte técnico de cliente de Facebook](https://workplace.fb.com/faq/) tooget estos valores. 

4. Hola **el certificado de firma de SAML** sección, seleccione **certificado (Base64)**y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Seleccione **Guardar**.

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. Hola **al área de trabajo por la configuración de Facebook** sección, seleccione **al área de trabajo configurar Facebook** tooopen hello **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **referencia rápida** sección.

    ![Configuración de Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. En una ventana del explorador web diferente, inicie sesión en tooyour al área de trabajo por sitio de la compañía de Facebook como administrador.
  
   > [!NOTE] 
   > Como parte del proceso de autenticación de SAML de hello, al área de trabajo puede utilizar cadenas de consulta de seguridad too2.5 kilobytes de tamaño en orden toopass parámetros tooAzure AD.

8. Hola **empresa panel**, vaya toohello **autenticación** ficha.

9. En **autenticación SAML**, seleccione **SSO sólo** desde la lista desplegable de Hola.

10. Escriba los valores de hello copiados de hello **al área de trabajo por la configuración de Facebook** sección del portal de Azure en los campos correspondientes de Hola Hola:

    *   En el **dirección URL SAML** cuadro de texto, pegue Hola valo **URL de servicio de inicio de sesión único**, que haya copiado desde Hola portal de Azure.
    *   En el **dirección URL del emisor de SAML** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde Hola portal de Azure.
    *   En **SAML Logout redirigir (opcional)**, pegue el valor de Hola de **dirección URL de cierre de sesión**, que haya copiado desde Hola portal de Azure.
    *   Abra su **certificado codificado en base 64** en el Bloc de notas, descarga desde Hola portal de Azure. Copie el contenido de hello del mismo en el Portapapeles y, a continuación, péguelo toothe **certificado SAML** cuadro de texto.

11. Es posible que tenga la audiencia de hello tooenter dirección URL, dirección URL de destinatario y ACS (servicio de consumidor de aserción) URL, aparecen en hello **configuración de SAML** sección.

12. Desplácese toohello inferior de la sección de Hola y seleccione **prueba SSO**. Aparece una ventana emergente, página de inicio de sesión de hello Azure AD. tooauthenticate, escriba sus credenciales de forma habitual. Asegúrese de dirección de correo electrónico de hello devuelto desde Azure AD es Hola igual Hola cuenta de empresa que haya iniciado sesión.

13. Si prueba Hola ha finalizado correctamente, desplazar toohello inferior de la página de Hola y seleccione **guardar**.

14. A todo el que use Workplace se le presentará la página de inicio de sesión de Azure AD para la autenticación.

Puede elegir tooconfigure un cierre de sesión SAML dirección URL, que puede ser toopoint utilizado en la página de cierre de sesión de hello Azure AD. Cuando esta opción está habilitada y configurada, el usuario de Hola ya no es página de cierre de sesión de toohello dirigida al área de trabajo. En su lugar, usuario de hello es dirección URL redirigida toohello que se agregó en la configuración de redireccionamiento de cierre de sesión de SAML de Hola.


> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello. Después de agregar esta aplicación de hello **Active Directory** > **aplicaciones empresariales** sección, simplemente seleccione hello **Single Sign-On** hello de acceso y de pestaña incrusta documentación a través de hello **configuración** sección final Hola. Puede leer más acerca de la característica de documentación de embedded Hola Hola [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="configure-reauthentication-frequency"></a>Configuración de la frecuencia de reautenticación

Puede configurar tooprompt al área de trabajo para una comprobación SAML cada día, tres días, una semana, dos semanas, un mes o nunca.

> [!NOTE] 
>Hello valor mínimo para la comprobación SAML de hello en aplicaciones móviles se establece tooone semana.

También puede forzar un restablecimiento de SAML para todos los usuarios. toodo, Hola uso **la autenticación de SAML requiere para todos los usuarios ahora** botón.


### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

1. Hola **portal de Azure**, en el panel izquierdo de Hola, seleccione **Azure Active Directory**.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y seleccione **todos los usuarios**.
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, seleccione **agregar**.
 
    ![botón de agregar Hola](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. Hola **usuario** diálogo cuadro, Hola siguientes:
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anótela.

    d. Seleccione **Crear**.
 
### <a name="create-a-workplace-by-facebook-test-user"></a>Creación de un usuario de prueba de Workplace by Facebook

En esta sección se crea un usuario llamado Britta Simon en Workplace by Facebook. Workplace by Facebook admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.

El usuario no tiene que hacer nada en esta sección. Si un usuario no existe en el área de trabajo Facebook, una nueva se crea cuando intente tooaccess al área de trabajo Facebook.

>[!Note]
>Si necesita un usuario toocreate manualmente, póngase en contacto con hello [al área de trabajo al equipo de soporte técnico de cliente de Facebook](https://workplace.fb.com/faq/).

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure SSO concediendo acceso tooWorkplace Facebook.

![Asignar usuario][200] 

1. Hola Azure ver aplicaciones de portal, abra Hola. Ir a vista del directorio toohello, vaya demasiado**aplicaciones empresariales**y, a continuación, seleccione **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **al área de trabajo Facebook**.

    ![Hola al área de trabajo por el vínculo de Facebook en la lista de aplicaciones de Hola](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. En el menú de Hola Hola izquierda, seleccione **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. Seleccione **Agregar**. A continuación, en hello **Agregar asignación** panel, seleccione **usuarios y grupos**.

    ![panel de agregar asignación de Hola][203]

5. Hola **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Hola **usuarios y grupos** cuadro de diálogo, seleccione **seleccione**.

7. Hola **Agregar asignación** cuadro de diálogo, seleccione **asignar**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

Si desea tootest la configuración de SSO, abra Hola Panel de acceso.
Para obtener más información, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).


## <a name="next-steps"></a>Pasos siguientes

* Vea hello [lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md).
* Consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).
* Más información acerca de cómo demasiado[configurar aprovisionamiento de usuario](active-directory-saas-facebook-at-work-provisioning-tutorial.md).



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

