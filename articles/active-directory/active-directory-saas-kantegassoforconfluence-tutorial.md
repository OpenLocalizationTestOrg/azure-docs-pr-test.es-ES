---
title: "Tutorial: Integración de Azure Active Directory con Kantega SSO para Confluence | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Kantega SSO para confluencia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d0d99c14-a6ca-45f2-bb84-633126095e7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: b35eb8757e41e86228a3a9ee10869086cc801c9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-confluence"></a><span data-ttu-id="31661-103">Tutorial: Integración de Azure Active Directory con Kantega SSO para Confluence</span><span class="sxs-lookup"><span data-stu-id="31661-103">Tutorial: Azure Active Directory integration with Kantega SSO for Confluence</span></span>

<span data-ttu-id="31661-104">En este tutorial, aprenderá cómo toointegrate Kantega SSO para confluencia con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31661-104">In this tutorial, you learn how toointegrate Kantega SSO for Confluence with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31661-105">Integración Kantega SSO para confluencia con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="31661-105">Integrating Kantega SSO for Confluence with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="31661-106">Puede controlar en Azure AD que tenga acceso tooKantega SSO para confluencia</span><span class="sxs-lookup"><span data-stu-id="31661-106">You can control in Azure AD who has access tooKantega SSO for Confluence</span></span>
- <span data-ttu-id="31661-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooKantega SSO para confluencia (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31661-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Confluence (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31661-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="31661-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="31661-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31661-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31661-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="31661-110">Prerequisites</span></span>

<span data-ttu-id="31661-111">integración de Azure AD con Kantega SSO para confluencia tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="31661-111">tooconfigure Azure AD integration with Kantega SSO for Confluence, you need hello following items:</span></span>

- <span data-ttu-id="31661-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31661-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31661-113">Una suscripción habilitada para el inicio de sesión único de Kantega SSO para Confluence</span><span class="sxs-lookup"><span data-stu-id="31661-113">A Kantega SSO for Confluence single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31661-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="31661-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31661-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="31661-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31661-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="31661-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31661-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31661-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31661-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="31661-118">Scenario description</span></span>
<span data-ttu-id="31661-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="31661-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31661-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="31661-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31661-121">Agregar Kantega SSO para confluencia desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="31661-121">Adding Kantega SSO for Confluence from hello gallery</span></span>
2. <span data-ttu-id="31661-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31661-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-confluence-from-hello-gallery"></a><span data-ttu-id="31661-123">Agregar Kantega SSO para confluencia desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="31661-123">Adding Kantega SSO for Confluence from hello gallery</span></span>
<span data-ttu-id="31661-124">integración de hello tooconfigure de Kantega SSO para confluencia en Azure AD, necesitará tooadd Kantega SSO confluencia de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="31661-124">tooconfigure hello integration of Kantega SSO for Confluence into Azure AD, you need tooadd Kantega SSO for Confluence from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="31661-125">**tooadd Kantega SSO para confluencia de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31661-125">**tooadd Kantega SSO for Confluence from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="31661-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="31661-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31661-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="31661-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="31661-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="31661-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="31661-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31661-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="31661-133">En el cuadro de búsqueda de hello, escriba **Kantega SSO para confluencia**.</span><span class="sxs-lookup"><span data-stu-id="31661-133">In hello search box, type **Kantega SSO for Confluence**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_search.png)

5. <span data-ttu-id="31661-135">En el panel de resultados de hello, seleccione **Kantega SSO para confluencia**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="31661-135">In hello results panel, select **Kantega SSO for Confluence**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31661-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31661-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31661-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Kantega SSO para Confluence con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="31661-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Confluence based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="31661-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Kantega SSO para confluencia es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31661-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Confluence is tooa user in Azure AD.</span></span> <span data-ttu-id="31661-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Kantega SSO para confluencia debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="31661-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Confluence needs toobe established.</span></span>

<span data-ttu-id="31661-141">En Kantega SSO para confluencia, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="31661-141">In Kantega SSO for Confluence, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="31661-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Kantega SSO para confluencia, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="31661-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Confluence, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="31661-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="31661-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="31661-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31661-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31661-145">**[Crear un SSO Kantega de usuario de prueba de confluencia](#creating-a-kantega-sso-for-confluence-test-user)**  -toohave un equivalente de Britta Simon en Kantega SSO para confluencia que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="31661-145">**[Creating a Kantega SSO for Confluence test user](#creating-a-kantega-sso-for-confluence-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Confluence that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="31661-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="31661-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31661-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="31661-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31661-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31661-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31661-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el SSO Kantega para aplicación confluencia.</span><span class="sxs-lookup"><span data-stu-id="31661-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Confluence application.</span></span>

<span data-ttu-id="31661-150">**tooconfigure inicio de sesión único en Azure AD con Kantega SSO para confluencia, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31661-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Confluence, perform hello following steps:**</span></span>

1. <span data-ttu-id="31661-151">En el portal de Azure, en Hola Hola **Kantega SSO para confluencia** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="31661-151">In hello Azure portal, on hello **Kantega SSO for Confluence** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="31661-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="31661-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_samlbase.png)

3. <span data-ttu-id="31661-155">En **IDP** inicia el modo, hello **Kantega SSO de dominio confluencia y direcciones URL** sección realizar Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="31661-155">In **IDP** initiated mode, on hello **Kantega SSO for Confluence Domain and URLs** section perform hello following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url1.png)

    <span data-ttu-id="31661-157">a.</span><span class="sxs-lookup"><span data-stu-id="31661-157">a.</span></span> <span data-ttu-id="31661-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="31661-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="31661-159">b.</span><span class="sxs-lookup"><span data-stu-id="31661-159">b.</span></span> <span data-ttu-id="31661-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="31661-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="31661-161">En **SP** modo iniciado, verificación **mostrar avanzadas de configuración de la URL** y realizar Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="31661-161">In **SP** initiated mode, check **Show advanced URL settings** and perform hello following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url2.png)

    <span data-ttu-id="31661-163">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="31661-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="31661-164">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="31661-164">These values are not real.</span></span> <span data-ttu-id="31661-165">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="31661-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="31661-166">Estos valores se reciben durante la configuración de Hola de complemento de confluencia, que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="31661-166">These values are received during hello configuration of Confluence plugin, which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="31661-167">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="31661-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_certificate.png) 

6. <span data-ttu-id="31661-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="31661-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="31661-171">En una ventana del explorador web diferente, inicie sesión en tooyour **portal de administración de confluencia** como administrador.</span><span class="sxs-lookup"><span data-stu-id="31661-171">In a different web browser window, log in tooyour **Confluence admin portal** as an administrator.</span></span>

8. <span data-ttu-id="31661-172">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **complementos**.</span><span class="sxs-lookup"><span data-stu-id="31661-172">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon1.png)

9. <span data-ttu-id="31661-174">En la pestaña **ATLASSIAN MARKETPLACE** (MARKETPLACE DE ATLASSIAN), haga clic en **Find new add-ons** (Buscar nuevos complementos).</span><span class="sxs-lookup"><span data-stu-id="31661-174">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon.png)

10. <span data-ttu-id="31661-176">Búsqueda **Kantega SSO para confluencia SAML Kerberos** y haga clic en **instalar** tooinstall botón Hola nuevo complemento SAML.</span><span class="sxs-lookup"><span data-stu-id="31661-176">Search **Kantega SSO for Confluence SAML Kerberos** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon2.png)

11. <span data-ttu-id="31661-178">se inicia la instalación del complemento Hola.</span><span class="sxs-lookup"><span data-stu-id="31661-178">hello plugin installation starts.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon3.png)

12. <span data-ttu-id="31661-180">Una vez completada la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="31661-180">Once hello installation is complete.</span></span> <span data-ttu-id="31661-181">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="31661-181">Click **Close**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon33.png)

13. <span data-ttu-id="31661-183">Haga clic en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="31661-183">Click **Manage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon34.png)
    
14. <span data-ttu-id="31661-185">Haga clic en **configurar** tooconfigure Hola nuevo complemento.</span><span class="sxs-lookup"><span data-stu-id="31661-185">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon35.png)

15. <span data-ttu-id="31661-187">Este nuevo complemento también puede encontrarse en la pestaña **USERS & SECURITY** (USUARIOS Y SEGURIDAD).</span><span class="sxs-lookup"><span data-stu-id="31661-187">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon36.png)
    
16. <span data-ttu-id="31661-189">Hola **SAML** sección.</span><span class="sxs-lookup"><span data-stu-id="31661-189">In hello **SAML** section.</span></span> <span data-ttu-id="31661-190">Seleccione **Azure Active Directory (Azure AD)** de hello **Agregar proveedor de identidades** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="31661-190">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon4.png)

17. <span data-ttu-id="31661-192">Seleccione el nivel de suscripción **Básica**.</span><span class="sxs-lookup"><span data-stu-id="31661-192">Select subscription level as **Basic**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon5.png)       

18. <span data-ttu-id="31661-194">En hello **propiedades de la aplicación** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="31661-194">On hello **App properties** section, perform following steps:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon6.png)

    <span data-ttu-id="31661-196">a.</span><span class="sxs-lookup"><span data-stu-id="31661-196">a.</span></span> <span data-ttu-id="31661-197">Hola copia **App ID URI** valor y utilizarlo como **identificador, dirección URL de respuesta y dirección URL de inicio de sesión** en hello **Kantega SSO de dominio confluencia y direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="31661-197">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Confluence Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="31661-198">b.</span><span class="sxs-lookup"><span data-stu-id="31661-198">b.</span></span> <span data-ttu-id="31661-199">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="31661-199">Click **Next**.</span></span>

19. <span data-ttu-id="31661-200">En hello **importación de metadatos** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="31661-200">On hello **Metadata import** section, perform following steps:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon7.png)

    <span data-ttu-id="31661-202">a.</span><span class="sxs-lookup"><span data-stu-id="31661-202">a.</span></span> <span data-ttu-id="31661-203">Seleccione **Archivo de metadatos en el equipo** y cargue el archivo de metadatos que descargó desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="31661-203">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="31661-204">b.</span><span class="sxs-lookup"><span data-stu-id="31661-204">b.</span></span> <span data-ttu-id="31661-205">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="31661-205">Click **Next**.</span></span>

20. <span data-ttu-id="31661-206">En hello **nombre y SSO ubicación** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="31661-206">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon8.png)
    
    <span data-ttu-id="31661-208">a.</span><span class="sxs-lookup"><span data-stu-id="31661-208">a.</span></span> <span data-ttu-id="31661-209">Agregar nombre de proveedor de identidades de hello en **el nombre del proveedor de identidad** cuadro de texto (por ejemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31661-209">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="31661-210">b.</span><span class="sxs-lookup"><span data-stu-id="31661-210">b.</span></span> <span data-ttu-id="31661-211">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="31661-211">Click **Next**.</span></span>

21. <span data-ttu-id="31661-212">Comprobar el certificado de firma de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="31661-212">Verify hello Signing certificate and click **Next**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon9.png)

22. <span data-ttu-id="31661-214">En hello **cuentas de usuario de confluencia** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="31661-214">On hello **Confluence user accounts** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon10.png)

    <span data-ttu-id="31661-216">a.</span><span class="sxs-lookup"><span data-stu-id="31661-216">a.</span></span> <span data-ttu-id="31661-217">Seleccione **crear usuarios en el directorio interno del confluencia si es necesario** y escriba nombre adecuado Hola del grupo de Hola para los usuarios (puede ser no varios.</span><span class="sxs-lookup"><span data-stu-id="31661-217">Select **Create users in Confluence's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="31661-218">de grupos separados por coma).</span><span class="sxs-lookup"><span data-stu-id="31661-218">of groups separated by comma).</span></span>

    <span data-ttu-id="31661-219">b.</span><span class="sxs-lookup"><span data-stu-id="31661-219">b.</span></span> <span data-ttu-id="31661-220">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="31661-220">Click **Next**.</span></span>

23. <span data-ttu-id="31661-221">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="31661-221">Click **Finish**.</span></span>   

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon11.png)

24. <span data-ttu-id="31661-223">En hello **conoce dominios para Azure AD** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="31661-223">On hello **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon12.png)

    <span data-ttu-id="31661-225">a.</span><span class="sxs-lookup"><span data-stu-id="31661-225">a.</span></span> <span data-ttu-id="31661-226">Seleccione **conoce dominios** desde el panel izquierdo de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="31661-226">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="31661-227">b.</span><span class="sxs-lookup"><span data-stu-id="31661-227">b.</span></span> <span data-ttu-id="31661-228">Escriba el nombre de dominio en hello **conoce dominios** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="31661-228">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="31661-229">c.</span><span class="sxs-lookup"><span data-stu-id="31661-229">c.</span></span> <span data-ttu-id="31661-230">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="31661-230">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="31661-231">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="31661-231">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="31661-232">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="31661-232">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="31661-233">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31661-233">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31661-234">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31661-234">Creating an Azure AD test user</span></span>
<span data-ttu-id="31661-235">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="31661-235">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="31661-237">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31661-237">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="31661-238">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="31661-238">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31661-240">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="31661-240">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31661-242">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="31661-242">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31661-244">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="31661-244">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31661-246">a.</span><span class="sxs-lookup"><span data-stu-id="31661-246">a.</span></span> <span data-ttu-id="31661-247">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31661-247">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31661-248">b.</span><span class="sxs-lookup"><span data-stu-id="31661-248">b.</span></span> <span data-ttu-id="31661-249">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="31661-249">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31661-250">c.</span><span class="sxs-lookup"><span data-stu-id="31661-250">c.</span></span> <span data-ttu-id="31661-251">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="31661-251">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="31661-252">d.</span><span class="sxs-lookup"><span data-stu-id="31661-252">d.</span></span> <span data-ttu-id="31661-253">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="31661-253">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-confluence-test-user"></a><span data-ttu-id="31661-254">Creación de un usuario de prueba de Kantega SSO para Confluence</span><span class="sxs-lookup"><span data-stu-id="31661-254">Creating a Kantega SSO for Confluence test user</span></span>

<span data-ttu-id="31661-255">toolog de los usuarios de Azure AD tooenable en tooConfluence, se les deben aprovisionar en confluencia.</span><span class="sxs-lookup"><span data-stu-id="31661-255">tooenable Azure AD users toolog in tooConfluence, they must be provisioned into Confluence.</span></span> <span data-ttu-id="31661-256">En caso de hello de Kantega SSO para confluencia, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="31661-256">In hello case of Kantega SSO for Confluence, provisioning is a manual task.</span></span>

<span data-ttu-id="31661-257">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31661-257">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="31661-258">Inicie sesión en tooyour Kantega SSO para el sitio de empresa confluencia como administrador.</span><span class="sxs-lookup"><span data-stu-id="31661-258">Log in tooyour Kantega SSO for Confluence company site as an administrator.</span></span>

2. <span data-ttu-id="31661-259">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="31661-259">Hover on cog and click hello **User management**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforconfluence-tutorial/user1.png) 

3. <span data-ttu-id="31661-261">En la sección Usuarios, haga clic en la pestaña **Agregar usuarios**. En hello **"Agregar usuarios"** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="31661-261">Under Users section, click **Add Users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforconfluence-tutorial/user2.png) 

    <span data-ttu-id="31661-263">a.</span><span class="sxs-lookup"><span data-stu-id="31661-263">a.</span></span> <span data-ttu-id="31661-264">Hola **nombre de usuario** Hola de tipo de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="31661-264">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="31661-265">b.</span><span class="sxs-lookup"><span data-stu-id="31661-265">b.</span></span> <span data-ttu-id="31661-266">Hola **nombre completo** cuadro de texto, nombre completo de tipo hello del usuario como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31661-266">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="31661-267">c.</span><span class="sxs-lookup"><span data-stu-id="31661-267">c.</span></span> <span data-ttu-id="31661-268">Hola **correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="31661-268">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="31661-269">d.</span><span class="sxs-lookup"><span data-stu-id="31661-269">d.</span></span> <span data-ttu-id="31661-270">Hola **contraseña** cuadro de texto, escriba la contraseña de hello para el usuario.</span><span class="sxs-lookup"><span data-stu-id="31661-270">In hello **Password** textbox, type hello password for user.</span></span>

    <span data-ttu-id="31661-271">e.</span><span class="sxs-lookup"><span data-stu-id="31661-271">e.</span></span> <span data-ttu-id="31661-272">Haga clic en **Confirmar contraseña** introducir la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="31661-272">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="31661-273">f.</span><span class="sxs-lookup"><span data-stu-id="31661-273">f.</span></span> <span data-ttu-id="31661-274">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="31661-274">Click **Add** button.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="31661-275">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="31661-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="31661-276">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooKantega SSO para confluencia.</span><span class="sxs-lookup"><span data-stu-id="31661-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Confluence.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="31661-278">**tooassign Britta Simon tooKantega SSO para confluencia, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31661-278">**tooassign Britta Simon tooKantega SSO for Confluence, perform hello following steps:**</span></span>

1. <span data-ttu-id="31661-279">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="31661-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="31661-281">En la lista de aplicaciones de hello, seleccione **Kantega SSO para confluencia**.</span><span class="sxs-lookup"><span data-stu-id="31661-281">In hello applications list, select **Kantega SSO for Confluence**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_app.png) 

3. <span data-ttu-id="31661-283">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="31661-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="31661-285">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="31661-285">Click **Add** button.</span></span> <span data-ttu-id="31661-286">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="31661-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="31661-288">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="31661-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="31661-289">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="31661-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31661-290">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="31661-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31661-291">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="31661-291">Testing single sign-on</span></span>

<span data-ttu-id="31661-292">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="31661-292">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="31661-293">Al hacer clic en hello Kantega SSO para mosaico confluencia Hola Panel de acceso, obtendrá automáticamente ha iniciado sesión tooyour Kantega SSO para aplicaciones de confluencia.</span><span class="sxs-lookup"><span data-stu-id="31661-293">When you click hello Kantega SSO for Confluence tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Confluence application.</span></span>
<span data-ttu-id="31661-294">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="31661-294">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="31661-295">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="31661-295">Additional resources</span></span>

* [<span data-ttu-id="31661-296">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31661-296">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31661-297">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31661-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_203.png

