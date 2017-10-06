---
title: "Tutorial: Integración de Azure Active Directory con SAP Business Object Cloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y la nube de objeto de negocios de SAP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a>Tutorial: Integración de Azure Active Directory con SAP Business Object Cloud

En este tutorial, aprenderá cómo toointegrate SAP Business objeto en la nube con Azure Active Directory (Azure AD).

Obtener hello las siguientes ventajas cuando se integre SAP Business objeto en la nube con Azure AD:

- En Azure AD, puede controlar quién tiene acceso tooSAP nube del objeto de negocios.
- Puede firmar automáticamente en su tooSAP de los usuarios empresariales objeto nube mediante el inicio de sesión único y una cuenta de usuario Azure AD.
- Puede administrar las cuentas en una ubicación central, Hola portal de Azure.

toolearn más información acerca del software como una integración de aplicaciones de servicio (SaaS) con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooset la integración de Azure AD con la nube de objeto de negocios de SAP, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una instancia de SAP Business Object Cloud con el inicio de sesión único habilitado

> [!NOTE]
> Si prueba a pasos de hello en este tutorial, se recomienda que no probarlas en un entorno de producción.

Recomendaciones para probar los pasos de hello en este tutorial:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba gratuita durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. 

escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar objeto nube de SAP Business de hello Galería.
2. Configuración y prueba del inicio de sesión único en Azure AD.

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a>Agregar objeto nube de SAP Business de galería de Hola
tooset la integración de Hola de SAP Business objeto en la nube con Azure AD, en la Galería de hello, agregue la lista de tooyour de SAP Business objeto nube de las aplicaciones administradas de SaaS.

en la nube SAP Business objeto desde la Galería de Hola tooadd:

1. Hola [portal de Azure](https://portal.azure.com), en el menú de la izquierda de Hola, seleccione **Azure Active Directory**. 

    ![botón de Hello Azure Active Directory][1]

2. Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.

    ![página de aplicaciones de empresa de Hola][2]
    
3. tooadd una nueva aplicación, seleccione **nueva aplicación**.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **SAP Business objeto nube**.

    ![cuadro de búsqueda de Hola](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. En el panel de resultados de hello, seleccione **SAP Business objeto nube**y, a continuación, seleccione **agregar**.

    ![Lista de resultados de la nube de objeto de negocios SAP en hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, configurará y probará el inicio de sesión único de Azure AD con SAP Business Object Cloud mediante un usuario de prueba llamado *Britta Simon*.

Para toowork de inicio de sesión único, Azure AD necesita usuario de equivalente de Azure AD tooknow hello en la nube de objeto de negocios de SAP. Se debe establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en la nube de objeto de negocios de SAP.

Hola tooestablish vincular relación, en la nube de objeto de negocios de SAP, para **nombre de usuario**, asignar un valor de Hola de hello **nombre de usuario** en Azure AD.

tooconfigure y prueba de inicio de sesión único en Azure AD con SAP Business objeto nube, Hola completa después de tareas:

1. [Configuración del inicio de sesión único de Azure AD](#set-up-azure-ad-single-sign-on). Configura un toouse de usuario de esta característica.
2. [Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user). Pruebas AD Azure inicio de sesión único con usuario hello Britta Simon.
3. [Creación de un usuario de prueba de SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user). Crea a un equivalente de Britta Simon en nube de objeto de negocios de SAP que está vinculado toohello representación de Azure AD del usuario de Hola.
4. [Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user). Configura Britta Simon toouse inicio de sesión único en Azure AD.
5. [Prueba de inicio de sesión único](#test-single-sign-on). Comprueba que la configuración de hello funciona.

### <a name="set-up-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, activar Azure AD único inicio de sesión en hello portal de Azure. A continuación, configura el inicio de sesión único en la aplicación SAP Business Object Cloud.

tooset de inicio de sesión único en Azure AD con SAP Business objeto nube:

1. En el portal de Azure, en Hola Hola **SAP Business objeto nube** página de integración de aplicaciones, seleccione **inicio de sesión único**.

    ![Seleccionar Inicio de sesión único][4]

2. En hello **inicio de sesión único** página, para **modo**, seleccione **sesión basado en SAML**.
 
    ![Seleccionar Inicio de sesión basado en SAML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. En **dominio de nube de objeto de negocio de SAP y las direcciones URL**completa Hola lo siguiente:

    1. Hola **dirección URL de inicio de sesión** cuadro, escriba una dirección URL con hello siguiente patrón: 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. Hola **identificador** cuadro, escriba una dirección URL con hello siguiente patrón:
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![Direcciones URL de la página Dominio y direcciones URL de SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > los valores de Hello en estas direcciones URL son únicamente como demostración. Actualizar valores de hello con hello real sesión dirección URL y el identificador de dirección URL. tooget Hola inicio de sesión dirección URL, póngase en contacto con hello [equipo de soporte técnico de SAP Business objeto nube Client](https://www.sap.com/product/analytics/cloud-analytics.support.html). Puede obtener la dirección URL de identificación de hello mediante la descarga de metadatos de la nube de objeto de negocios de SAP Hola desde la consola de administración de Hola. Esto se explica más adelante en el tutorial Hola. 

4. En **Certificado de firma de SAML**, seleccione **XML de metadatos**. A continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Seleccionar XML de metadatos](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. Seleccione **Guardar**.

    ![Seleccionar Guardar](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de SAP Business objeto nube tooyour como administrador.

7. Seleccione **Menu** > **System** > **Administration** (Menú > Sistema > Administración).
    
    ![Seleccionar Menu (Menú), System (Sistema) y, luego, Administration (Administración)](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. En hello **seguridad** ficha, seleccione hello **editar** el icono de (lápiz PC).
    
    ![En la pestaña de seguridad de hello, seleccione el icono de edición de Hola](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. Como **Authentication Method** (Método de autenticación), seleccione **SAML Single Sign-On (SSO)** (Inicio de sesión único [SSO] de SAML).

    ![Seleccione SAML Single Sign-On para el método de autenticación de Hola](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. toodownload Hola proveedor metadatos del servicio (paso 1), seleccione **descargar**. En el archivo de metadatos de hello, busque y copie hello **entityID** valor. Hola Azure portal, en **dominio de nube de objeto de negocio de SAP y las direcciones URL**, pegue el valor de Hola Hola **identificador** cuadro.

    ![Copie y pegue el valor entityID de Hola](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. tooupload Hola proveedor metadatos del servicio (paso 2) en el archivo hello que descargó desde Hola portal de Azure, en **metadatos cargar el proveedor de identidades**, seleccione **cargar**.  

    ![En Upload Identity Provider metadata (Cargar metadatos del proveedor de identidades), seleccionar Upload (Cargar)](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. Hola **usuario atributo** lista, los atributos de usuario de hello seleccione (paso 3) que desea toouse para su implementación. Este atributo de usuario asigna toohello proveedor de identidades. un atributo personalizado en la página del usuario de hello, use hello tooenter **personalizado SAML asignación** opción. O bien, puede seleccionar **correo electrónico** o **Id. de usuario** como atributo de usuario de Hola. En nuestro ejemplo, hemos seleccionado **correo electrónico** porque asignamos Hola notificación de identificador de usuario con hello **userprincipalname** atributo Hola **atributos de usuario** sección Hola Portal de Azure. Esto proporciona un correo electrónico de usuario único, que se envía toohello aplicación en la nube de objeto de negocios de SAP en cada respuesta SAML correcta.

    ![Seleccionar Atributos de usuario](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. cuenta de hello tooverify con el proveedor de identidades de hello (paso 4), en hello **credenciales de inicio de sesión (correo electrónico)** cuadro, escriba la dirección de correo electrónico del usuario de Hola. A continuación, seleccione **Verify Account** (Comprobar cuenta). sistema de Hello agrega la cuenta de usuario de las credenciales de inicio de sesión toohello.

    ![Escribir Email (Correo electrónico) y seleccionar Verify Account (Comprobar cuenta)](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. Seleccione hello **guardar** icono.

    ![Icono Save (Guardar)](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> Puede leer una versión concisa de estas instrucciones en hello [portal de Azure](https://portal.azure.com), mientras que va a configurar la aplicación. Después de agregar la aplicación hello seleccionando **Active Directory** > **aplicaciones empresariales**, seleccione hello **Single Sign-On** ficha. Puede tener acceso a la documentación de hello incrustado en hello **configuración** sección final Hola de página Hola. Para más información, consulte la [documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
En esta sección, creará un usuario de prueba denominado a Britta Simon Hola portal de Azure.

toocreate un usuario de prueba en Azure AD:

1. En el portal de Azure, en el menú de la izquierda, Hola Hola seleccione **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, seleccionados **usuarios y grupos**y, a continuación, seleccione **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, seleccione **agregar**.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. Hola **usuario** cuadro de diálogo, Hola completa pasos:
 
    1. Hola **nombre** cuadro, escriba **BrittaSimon**.

    2. Hola **nombre de usuario** cuadro, escriba la dirección de correo electrónico de saludo del usuario de hello Britta Simon.

    3. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    4. Seleccione **Crear**.

        ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Creación de un usuario de Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a>Creación de un usuario de prueba de SAP Business Object Cloud

Usuarios de Azure AD deben estar aprovisionados en la nube de objeto de negocios de SAP antes de poder iniciar sesión tooSAP nube del objeto de negocios. En SAP Business Object Cloud, el aprovisionamiento es una tarea manual.

tooprovision una cuenta de usuario:

1. Inicie sesión en tooyour sitio SAP Business objeto nube de su compañía como administrador.

2. Seleccione **Menu** > **Security** > **Users** (Menú > Seguridad > Usuarios).

    ![Agregar empleado](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. En hello **usuarios** , tooadd nuevos detalles del usuario, seleccione  **+** . 

    ![Página Add Users (Agregar usuarios)](./media/active-directory-saas-sapboc-tutorial/user4.png)

    A continuación, complete Hola pasos:

    1. Hola **Id. de usuario** cuadro, escriba Hola identificador de usuario de hello, como **Bárbara**.

    2. Hola **nombre** cuadro, escriba Hola nombre de usuario de hello, como **Bárbara**.

    3. Hola **LAST NAME** cuadro, escriba el apellido del nombre de usuario de hello, hello como **Simon**.

    4. Hola **nombre para mostrar** cuadro, escriba el nombre completo de saludo del usuario de hello, como **Britta Simon**.

    5. Hola **correo electrónico** cuadro, escriba la dirección de correo electrónico de saludo del usuario de hello, como  **brittasimon@contoso.com** .

    6. En hello **seleccionar Roles de** , seleccione el rol adecuado de hello para el usuario de hello y, a continuación, seleccione **Aceptar**.

      ![Seleccionar rol](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. Seleccione hello **guardar** icono.  


### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, que permita que a Hola usuario Britta Simon toouse Azure AD inicio de sesión único mediante la concesión de hello usuario cuenta acceso tooSAP nube del objeto de negocios.

tooassign Britta Simon tooSAP nube del objeto de negocios:

1. Hola portal de Azure, abrir vista de aplicaciones de hello y, haga clic en la vista de directorio toohello. Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **SAP Business objeto nube**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. En el menú de la izquierda hello, seleccione **usuarios y grupos**.

    ![Seleccionar Usuarios y grupos][202] 

4. Seleccione **Agregar**. A continuación, en hello **Agregar asignación** página, seleccione **usuarios y grupos**.

    ![página Agregar asignación de Hola][203]

5. En hello **usuarios y grupos** página, en la lista de Hola de usuarios, seleccionados **Britta Simon**.

6. En hello **usuarios y grupos** página, seleccione **seleccione**.

7. En hello **Agregar asignación** página, seleccione **asignar**.

![Asigne el rol de usuario de Hola][200] 
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, probará la configuración de inicio de sesión única de Azure AD mediante el panel de acceso de Hola.

Cuando se selecciona mosaico de nube de objeto de negocios de SAP de hello en el panel de acceso hello, se debe sesión automáticamente en tooyour aplicación en la nube de objeto de negocios de SAP.

Para obtener más información acerca del panel de acceso de hello, consulte [panel de acceso de introducción toohello](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

