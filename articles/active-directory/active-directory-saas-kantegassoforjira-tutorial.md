---
title: "Tutorial: Integración de Azure Active Directory con Kantega SSO for JIRA | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Kantega SSO para JIRA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2af4891-e3c8-43b3-bdcb-0500c493e9b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 67894cc55ef91d0991c62e0e4f1be712723cb474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-jira"></a><span data-ttu-id="56256-103">Tutorial: Integración de Azure Active Directory con Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="56256-103">Tutorial: Azure Active Directory integration with Kantega SSO for JIRA</span></span>

<span data-ttu-id="56256-104">En este tutorial, aprenderá cómo toointegrate Kantega SSO para JIRA con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56256-104">In this tutorial, you learn how toointegrate Kantega SSO for JIRA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56256-105">Integración Kantega SSO para JIRA con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="56256-105">Integrating Kantega SSO for JIRA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="56256-106">Puede controlar en Azure AD que tenga acceso tooKantega SSO para JIRA</span><span class="sxs-lookup"><span data-stu-id="56256-106">You can control in Azure AD who has access tooKantega SSO for JIRA</span></span>
- <span data-ttu-id="56256-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooKantega SSO para JIRA (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56256-107">You can enable your users tooautomatically get signed-on tooKantega SSO for JIRA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56256-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="56256-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="56256-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56256-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56256-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="56256-110">Prerequisites</span></span>

<span data-ttu-id="56256-111">integración de Azure AD con Kantega SSO para JIRA tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="56256-111">tooconfigure Azure AD integration with Kantega SSO for JIRA, you need hello following items:</span></span>

- <span data-ttu-id="56256-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56256-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56256-113">Una suscripción habilitada para el inicio de sesión único de Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="56256-113">A Kantega SSO for JIRA single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56256-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="56256-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56256-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="56256-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56256-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="56256-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56256-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56256-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56256-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="56256-118">Scenario description</span></span>
<span data-ttu-id="56256-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="56256-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56256-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="56256-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56256-121">Agregar Kantega SSO para JIRA desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="56256-121">Adding Kantega SSO for JIRA from hello gallery</span></span>
2. <span data-ttu-id="56256-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56256-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-jira-from-hello-gallery"></a><span data-ttu-id="56256-123">Agregar Kantega SSO para JIRA desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="56256-123">Adding Kantega SSO for JIRA from hello gallery</span></span>
<span data-ttu-id="56256-124">integración de hello tooconfigure de Kantega SSO para JIRA en Azure AD, necesitará tooadd Kantega SSO para JIRA de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="56256-124">tooconfigure hello integration of Kantega SSO for JIRA into Azure AD, you need tooadd Kantega SSO for JIRA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="56256-125">**tooadd Kantega SSO para JIRA de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="56256-125">**tooadd Kantega SSO for JIRA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="56256-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="56256-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="56256-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="56256-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="56256-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="56256-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="56256-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56256-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="56256-133">En el cuadro de búsqueda de hello, escriba **Kantega SSO para JIRA**.</span><span class="sxs-lookup"><span data-stu-id="56256-133">In hello search box, type **Kantega SSO for JIRA**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_search.png)

5. <span data-ttu-id="56256-135">En el panel de resultados de hello, seleccione **Kantega SSO para JIRA**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="56256-135">In hello results panel, select **Kantega SSO for JIRA**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56256-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56256-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56256-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Kantega SSO for JIRA con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="56256-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for JIRA based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56256-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Kantega SSO para JIRA es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56256-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for JIRA is tooa user in Azure AD.</span></span> <span data-ttu-id="56256-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Kantega SSO para JIRA debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="56256-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for JIRA needs toobe established.</span></span>

<span data-ttu-id="56256-141">En Kantega SSO para JIRA, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="56256-141">In Kantega SSO for JIRA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="56256-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Kantega SSO para JIRA, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="56256-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for JIRA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="56256-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="56256-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="56256-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56256-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56256-145">**[Crear un SSO Kantega de usuario de prueba JIRA](#creating-a-kantega-sso-for-jira-test-user)**  -toohave un equivalente de Britta Simon en Kantega SSO para JIRA que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="56256-145">**[Creating a Kantega SSO for JIRA test user](#creating-a-kantega-sso-for-jira-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for JIRA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="56256-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="56256-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56256-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="56256-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56256-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56256-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="56256-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el SSO Kantega para aplicaciones de JIRA.</span><span class="sxs-lookup"><span data-stu-id="56256-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for JIRA application.</span></span>

<span data-ttu-id="56256-150">**tooconfigure inicio de sesión único en Azure AD con Kantega SSO para JIRA, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="56256-150">**tooconfigure Azure AD single sign-on with Kantega SSO for JIRA, perform hello following steps:**</span></span>

1. <span data-ttu-id="56256-151">En el portal de Azure, en Hola Hola **Kantega SSO para JIRA** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="56256-151">In hello Azure portal, on hello **Kantega SSO for JIRA** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="56256-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="56256-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_samlbase.png)

3. <span data-ttu-id="56256-155">En **IDP** inicia el modo, hello **Kantega SSO de dominio JIRA y direcciones URL** sección realizar Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="56256-155">In **IDP** initiated mode, on hello **Kantega SSO for JIRA Domain and URLs** section perform hello following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url1.png)

    <span data-ttu-id="56256-157">a.</span><span class="sxs-lookup"><span data-stu-id="56256-157">a.</span></span> <span data-ttu-id="56256-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="56256-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="56256-159">b.</span><span class="sxs-lookup"><span data-stu-id="56256-159">b.</span></span> <span data-ttu-id="56256-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="56256-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="56256-161">En **SP** modo iniciado, verificación **mostrar avanzadas de configuración de la URL** y realizar Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="56256-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url2.png)

    <span data-ttu-id="56256-163">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="56256-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56256-164">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="56256-164">These values are not real.</span></span> <span data-ttu-id="56256-165">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="56256-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="56256-166">Estos valores se reciben durante la configuración de Hola de complemento de Jira, que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="56256-166">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="56256-167">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="56256-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_certificate.png) 

6. <span data-ttu-id="56256-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="56256-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="56256-171">En una ventana del explorador web diferente, inicie sesión en tooyour JIRA en el servidor local como administrador.</span><span class="sxs-lookup"><span data-stu-id="56256-171">In a different web browser window, log in tooyour JIRA on premise server as an administrator.</span></span>

8. <span data-ttu-id="56256-172">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **complementos**.</span><span class="sxs-lookup"><span data-stu-id="56256-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon1.png)

9. <span data-ttu-id="56256-174">En la sección de la pestaña Complementos, haga clic en **Find new add-ons** (Buscar nuevos complementos).</span><span class="sxs-lookup"><span data-stu-id="56256-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="56256-175">Búsqueda **Kantega SSO para JIRA (SAML & Kerberos)** y haga clic en **instalar** tooinstall botón Hola nuevo complemento SAML.</span><span class="sxs-lookup"><span data-stu-id="56256-175">Search **Kantega SSO for JIRA (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon2.png)

10. <span data-ttu-id="56256-177">se inicia la instalación del complemento Hola.</span><span class="sxs-lookup"><span data-stu-id="56256-177">hello plugin installation starts.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon3.png)

11. <span data-ttu-id="56256-179">Una vez completada la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="56256-179">Once hello installation is complete.</span></span> <span data-ttu-id="56256-180">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="56256-180">Click **Close**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon33.png)

12. <span data-ttu-id="56256-182">Haga clic en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="56256-182">Click **Manage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon34.png)
    
13. <span data-ttu-id="56256-184">El nuevo complemento aparece en **INTEGRACIONES**.</span><span class="sxs-lookup"><span data-stu-id="56256-184">New plugin is listed under **INTEGRATIONS**.</span></span> <span data-ttu-id="56256-185">Haga clic en **configurar** tooconfigure Hola nuevo complemento.</span><span class="sxs-lookup"><span data-stu-id="56256-185">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon35.png)

14. <span data-ttu-id="56256-187">Hola **SAML** sección.</span><span class="sxs-lookup"><span data-stu-id="56256-187">In hello **SAML** section.</span></span> <span data-ttu-id="56256-188">Seleccione **Azure Active Directory (Azure AD)** de hello **Agregar proveedor de identidades** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="56256-188">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon4.png)

15. <span data-ttu-id="56256-190">Seleccione el nivel de suscripción **Básica**.</span><span class="sxs-lookup"><span data-stu-id="56256-190">Select subscription level as **Basic**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon5.png)     

16. <span data-ttu-id="56256-192">En hello **propiedades de la aplicación** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="56256-192">On hello **App properties** section, perform following steps:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon6.png)

    <span data-ttu-id="56256-194">a.</span><span class="sxs-lookup"><span data-stu-id="56256-194">a.</span></span> <span data-ttu-id="56256-195">Hola copia **App ID URI** valor y utilizarlo como **identificador, dirección URL de respuesta y dirección URL de inicio de sesión** en hello **Kantega SSO de dominio JIRA y direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="56256-195">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for JIRA Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="56256-196">b.</span><span class="sxs-lookup"><span data-stu-id="56256-196">b.</span></span> <span data-ttu-id="56256-197">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="56256-197">Click **Next**.</span></span>

17. <span data-ttu-id="56256-198">En hello **importación de metadatos** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="56256-198">On hello **Metadata import** section, perform following steps:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon7.png)

    <span data-ttu-id="56256-200">a.</span><span class="sxs-lookup"><span data-stu-id="56256-200">a.</span></span> <span data-ttu-id="56256-201">Seleccione **Archivo de metadatos en el equipo** y cargue el archivo de metadatos que descargó desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="56256-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="56256-202">b.</span><span class="sxs-lookup"><span data-stu-id="56256-202">b.</span></span> <span data-ttu-id="56256-203">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="56256-203">Click **Next**.</span></span>

18. <span data-ttu-id="56256-204">En hello **nombre y SSO ubicación** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="56256-204">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon8.png)
    
    <span data-ttu-id="56256-206">a.</span><span class="sxs-lookup"><span data-stu-id="56256-206">a.</span></span> <span data-ttu-id="56256-207">Agregar nombre de proveedor de identidades de hello en **el nombre del proveedor de identidad** cuadro de texto (por ejemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56256-207">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="56256-208">b.</span><span class="sxs-lookup"><span data-stu-id="56256-208">b.</span></span> <span data-ttu-id="56256-209">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="56256-209">Click **Next**.</span></span>

19. <span data-ttu-id="56256-210">Comprobar el certificado de firma de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="56256-210">Verify hello Signing certificate and click **Next**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon9.png)

20. <span data-ttu-id="56256-212">En hello **cuentas de usuario JIRA** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="56256-212">On hello **JIRA user accounts** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon10.png)

    <span data-ttu-id="56256-214">a.</span><span class="sxs-lookup"><span data-stu-id="56256-214">a.</span></span> <span data-ttu-id="56256-215">Seleccione **crear usuarios en el directorio interno del JIRA si es necesario** y escriba nombre adecuado Hola del grupo de Hola para los usuarios (puede ser no varios.</span><span class="sxs-lookup"><span data-stu-id="56256-215">Select **Create users in JIRA's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="56256-216">de grupos separados por coma).</span><span class="sxs-lookup"><span data-stu-id="56256-216">of groups separated by comma).</span></span>

    <span data-ttu-id="56256-217">b.</span><span class="sxs-lookup"><span data-stu-id="56256-217">b.</span></span> <span data-ttu-id="56256-218">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="56256-218">Click **Next**.</span></span>

21. <span data-ttu-id="56256-219">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="56256-219">Click **Finish**.</span></span>   

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon11.png)

22. <span data-ttu-id="56256-221">En hello **conoce dominios para Azure AD** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="56256-221">On hello **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon12.png)

    <span data-ttu-id="56256-223">a.</span><span class="sxs-lookup"><span data-stu-id="56256-223">a.</span></span> <span data-ttu-id="56256-224">Seleccione **conoce dominios** desde el panel izquierdo de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="56256-224">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="56256-225">b.</span><span class="sxs-lookup"><span data-stu-id="56256-225">b.</span></span> <span data-ttu-id="56256-226">Escriba el nombre de dominio en hello **conoce dominios** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="56256-226">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="56256-227">c.</span><span class="sxs-lookup"><span data-stu-id="56256-227">c.</span></span> <span data-ttu-id="56256-228">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="56256-228">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="56256-229">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="56256-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="56256-230">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="56256-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="56256-231">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56256-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56256-232">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56256-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="56256-233">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="56256-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="56256-235">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="56256-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="56256-236">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="56256-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="56256-238">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="56256-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="56256-240">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="56256-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="56256-242">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="56256-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56256-244">a.</span><span class="sxs-lookup"><span data-stu-id="56256-244">a.</span></span> <span data-ttu-id="56256-245">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56256-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56256-246">b.</span><span class="sxs-lookup"><span data-stu-id="56256-246">b.</span></span> <span data-ttu-id="56256-247">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="56256-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56256-248">c.</span><span class="sxs-lookup"><span data-stu-id="56256-248">c.</span></span> <span data-ttu-id="56256-249">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="56256-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="56256-250">d.</span><span class="sxs-lookup"><span data-stu-id="56256-250">d.</span></span> <span data-ttu-id="56256-251">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="56256-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-jira-test-user"></a><span data-ttu-id="56256-252">Crear un usuario de prueba de Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="56256-252">Creating a Kantega SSO for JIRA test user</span></span>

<span data-ttu-id="56256-253">toolog de los usuarios de Azure AD tooenable en tooJIRA, se les deben aprovisionar en JIRA.</span><span class="sxs-lookup"><span data-stu-id="56256-253">tooenable Azure AD users toolog in tooJIRA, they must be provisioned into JIRA.</span></span> <span data-ttu-id="56256-254">En Kantega SSO for JIRA, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="56256-254">In Kantega SSO for JIRA, provisioning is a manual task.</span></span>

<span data-ttu-id="56256-255">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="56256-255">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="56256-256">Inicie sesión en tooyour JIRA en el servidor local como administrador.</span><span class="sxs-lookup"><span data-stu-id="56256-256">Log in tooyour JIRA on premise server as an administrator.</span></span>

2. <span data-ttu-id="56256-257">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="56256-257">Hover on cog and click hello **User management**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforjira-tutorial/user1.png) 

3. <span data-ttu-id="56256-259">En la sección de la pestaña **Administración de usuarios**, haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="56256-259">Under **User management** tab section, click **Create user**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforjira-tutorial/user2.png) 

4. <span data-ttu-id="56256-261">En hello **"Crear nuevo usuario"** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="56256-261">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforjira-tutorial/user3.png) 

    <span data-ttu-id="56256-263">a.</span><span class="sxs-lookup"><span data-stu-id="56256-263">a.</span></span> <span data-ttu-id="56256-264">Hola **dirección de correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="56256-264">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="56256-265">b.</span><span class="sxs-lookup"><span data-stu-id="56256-265">b.</span></span> <span data-ttu-id="56256-266">Hola **nombre completo** cuadro de texto, nombre completo del tipo de usuario de hello como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56256-266">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="56256-267">c.</span><span class="sxs-lookup"><span data-stu-id="56256-267">c.</span></span> <span data-ttu-id="56256-268">Hola **nombre de usuario** Hola de tipo de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="56256-268">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="56256-269">d.</span><span class="sxs-lookup"><span data-stu-id="56256-269">d.</span></span> <span data-ttu-id="56256-270">Hola **contraseña** cuadro de texto, escriba la contraseña de saludo del usuario.</span><span class="sxs-lookup"><span data-stu-id="56256-270">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="56256-271">e.</span><span class="sxs-lookup"><span data-stu-id="56256-271">e.</span></span> <span data-ttu-id="56256-272">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="56256-272">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="56256-273">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="56256-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="56256-274">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooKantega SSO para JIRA.</span><span class="sxs-lookup"><span data-stu-id="56256-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for JIRA.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="56256-276">**tooassign Britta Simon tooKantega SSO para JIRA, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="56256-276">**tooassign Britta Simon tooKantega SSO for JIRA, perform hello following steps:**</span></span>

1. <span data-ttu-id="56256-277">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="56256-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="56256-279">En la lista de aplicaciones de hello, seleccione **Kantega SSO para JIRA**.</span><span class="sxs-lookup"><span data-stu-id="56256-279">In hello applications list, select **Kantega SSO for JIRA**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_app.png) 

3. <span data-ttu-id="56256-281">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="56256-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="56256-283">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="56256-283">Click **Add** button.</span></span> <span data-ttu-id="56256-284">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="56256-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="56256-286">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="56256-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="56256-287">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="56256-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56256-288">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="56256-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="56256-289">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="56256-289">Testing single sign-on</span></span>

<span data-ttu-id="56256-290">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="56256-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="56256-291">Al hacer clic en hello Kantega SSO de icono JIRA Hola Panel de acceso, obtendrá automáticamente ha iniciado sesión tooyour Kantega SSO para aplicaciones de JIRA.</span><span class="sxs-lookup"><span data-stu-id="56256-291">When you click hello Kantega SSO for JIRA tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for JIRA application.</span></span>
<span data-ttu-id="56256-292">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="56256-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="56256-293">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="56256-293">Additional resources</span></span>

* [<span data-ttu-id="56256-294">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56256-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56256-295">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56256-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_203.png

