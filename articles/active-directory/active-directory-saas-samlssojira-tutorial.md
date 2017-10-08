---
title: "Tutorial: Integración de Azure Active Directory con SAML SSO for Jira by resolution GmbH | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SSO de SAML para Jira mediante la resolución GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="87e03-103">Tutorial: Integración de Azure Active Directory con SAML SSO for Jira by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="87e03-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="87e03-104">En este tutorial, aprenderá cómo toointegrate SSO de SAML para Jira mediante la resolución GmbH con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87e03-104">In this tutorial, you learn how toointegrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87e03-105">Integración de SSO de SAML para Jira mediante la resolución GmbH con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="87e03-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="87e03-106">Puede controlar en Azure AD que tenga acceso tooSAML SSO para Jira mediante la resolución GmbH</span><span class="sxs-lookup"><span data-stu-id="87e03-106">You can control in Azure AD who has access tooSAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="87e03-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSAML SSO para Jira mediante la resolución GmbH (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87e03-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="87e03-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="87e03-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="87e03-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="87e03-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87e03-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="87e03-110">Prerequisites</span></span>

<span data-ttu-id="87e03-111">integración de Azure AD con SSO de SAML para Jira mediante la resolución GmbH tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="87e03-111">tooconfigure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="87e03-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87e03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87e03-113">Una suscripción habilitada para el inicio de sesión único de SAML SSO for Jira by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="87e03-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87e03-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="87e03-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87e03-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="87e03-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87e03-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="87e03-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87e03-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87e03-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87e03-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="87e03-118">Scenario description</span></span>
<span data-ttu-id="87e03-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="87e03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87e03-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="87e03-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87e03-121">Adición de SSO de SAML para Jira resolución GmbH desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="87e03-121">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="87e03-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87e03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="87e03-123">Adición de SSO de SAML para Jira resolución GmbH desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="87e03-123">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
<span data-ttu-id="87e03-124">tooconfigure Hola integración de SSO de SAML para Jira mediante la resolución GmbH en Azure AD, necesitará tooadd SSO de SAML para Jira mediante la resolución GmbH de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="87e03-124">tooconfigure hello integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need tooadd SAML SSO for Jira by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="87e03-125">**tooadd SSO de SAML para Jira mediante la resolución GmbH de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="87e03-125">**tooadd SAML SSO for Jira by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="87e03-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="87e03-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="87e03-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="87e03-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="87e03-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="87e03-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="87e03-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="87e03-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="87e03-133">En el cuadro de búsqueda de hello, escriba **SSO de SAML para Jira mediante la resolución GmbH**.</span><span class="sxs-lookup"><span data-stu-id="87e03-133">In hello search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="87e03-135">En el panel de resultados de hello, seleccione **SSO de SAML para Jira mediante la resolución GmbH**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="87e03-135">In hello results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="87e03-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87e03-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="87e03-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con SAML SSO for Jira by resolution GmbH con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="87e03-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="87e03-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario homólogo hello en SSO de SAML para Jira resolución GmbH es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87e03-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Jira by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="87e03-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado hello en SSO de SAML para Jira mediante la resolución GmbH debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="87e03-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Jira by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="87e03-141">En SSO de SAML para Jira mediante la resolución GmbH, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="87e03-141">In SAML SSO for Jira by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="87e03-142">tooconfigure y prueba de inicio de sesión único en Azure AD con SSO de SAML para Jira mediante la resolución GmbH, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="87e03-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="87e03-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="87e03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="87e03-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87e03-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87e03-145">**[Crear un SSO de SAML para Jira por usuario de prueba de resolución GmbH](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave un equivalente de Britta Simon en SSO de SAML para Jira mediante la resolución GmbH que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="87e03-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="87e03-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="87e03-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87e03-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="87e03-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="87e03-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87e03-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="87e03-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el SSO de SAML para Jira mediante la resolución de aplicación GmbH.</span><span class="sxs-lookup"><span data-stu-id="87e03-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="87e03-150">**tooconfigure inicio de sesión único en Azure AD con SSO de SAML para Jira mediante la resolución GmbH, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="87e03-150">**tooconfigure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="87e03-151">En el portal de Azure, en Hola Hola **SSO de SAML para Jira mediante la resolución GmbH** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="87e03-151">In hello Azure portal, on hello **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="87e03-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="87e03-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="87e03-155">En hello **SSO de SAML para las direcciones URL y Jira mediante la resolución de dominio GmbH** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="87e03-155">On hello **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="87e03-157">a.</span><span class="sxs-lookup"><span data-stu-id="87e03-157">a.</span></span> <span data-ttu-id="87e03-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="87e03-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="87e03-159">b.</span><span class="sxs-lookup"><span data-stu-id="87e03-159">b.</span></span> <span data-ttu-id="87e03-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="87e03-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="87e03-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="87e03-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="87e03-162">Si desea que aplicación de hello tooconfigure en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="87e03-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="87e03-164">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="87e03-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="87e03-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="87e03-165">These values are not real.</span></span> <span data-ttu-id="87e03-166">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="87e03-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="87e03-167">Póngase en contacto con [equipo de soporte técnico de SSO de SAML para Jira mediante la resolución de cliente GmbH](https://www.resolution.de/go/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="87e03-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="87e03-168">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="87e03-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="87e03-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="87e03-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="87e03-172">En una ventana del explorador web diferente, inicie sesión en tooyour **SSO de SAML para Jira mediante el portal de administración de resolución GmbH** como administrador.</span><span class="sxs-lookup"><span data-stu-id="87e03-172">In a different web browser window, log in tooyour **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="87e03-173">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **complementos**.</span><span class="sxs-lookup"><span data-stu-id="87e03-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="87e03-175">Está página de acceso a tooAdministrator redirigida.</span><span class="sxs-lookup"><span data-stu-id="87e03-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="87e03-176">Escriba hello **contraseña** y haga clic en **confirmar** botón.</span><span class="sxs-lookup"><span data-stu-id="87e03-176">Enter hello **Password** and click **Confirm** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="87e03-178">En la sección de la pestaña Complementos, haga clic en **Find new add-ons** (Buscar nuevos complementos).</span><span class="sxs-lookup"><span data-stu-id="87e03-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="87e03-179">Búsqueda **SAML único inicio de sesión (SSO) para JIRA** y haga clic en **instalar** tooinstall botón Hola nuevo complemento SAML.</span><span class="sxs-lookup"><span data-stu-id="87e03-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="87e03-181">se iniciará la instalación del complemento Hola.</span><span class="sxs-lookup"><span data-stu-id="87e03-181">hello plugin installation will start.</span></span> <span data-ttu-id="87e03-182">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="87e03-182">Click **Close**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="87e03-185">Haga clic en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="87e03-185">Click **Manage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="87e03-187">Haga clic en **configurar** tooconfigure Hola nuevo complemento.</span><span class="sxs-lookup"><span data-stu-id="87e03-187">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="87e03-189">En **configuración del complemento SAML SingleSignOn** página, haga clic en **Agregar proveedor de identidad adicional** botón Configuración de hello tooconfigure de proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="87e03-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="87e03-191">Siga los pasos indicados en esta página:</span><span class="sxs-lookup"><span data-stu-id="87e03-191">Perform following steps on this page:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="87e03-193">a.</span><span class="sxs-lookup"><span data-stu-id="87e03-193">a.</span></span> <span data-ttu-id="87e03-194">Agregar **nombre** de hello proveedor de identidades (por ejemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87e03-194">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="87e03-195">b.</span><span class="sxs-lookup"><span data-stu-id="87e03-195">b.</span></span> <span data-ttu-id="87e03-196">Agregar **descripción** de hello proveedor de identidades (por ejemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87e03-196">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="87e03-197">c.</span><span class="sxs-lookup"><span data-stu-id="87e03-197">c.</span></span> <span data-ttu-id="87e03-198">Haga clic en **XML** y seleccione hello **metadatos** archivo, que ha descargado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="87e03-198">Click **XML** and select hello **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="87e03-199">d.</span><span class="sxs-lookup"><span data-stu-id="87e03-199">d.</span></span> <span data-ttu-id="87e03-200">Haga clic en el botón **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="87e03-200">Click **Load** button.</span></span>

    <span data-ttu-id="87e03-201">e.</span><span class="sxs-lookup"><span data-stu-id="87e03-201">e.</span></span> <span data-ttu-id="87e03-202">Lee los metadatos de IdP de Hola y rellena los campos de hello como se resalta en la captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="87e03-202">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   

16. <span data-ttu-id="87e03-203">Haga clic en **Guardar configuración** botón Configuración de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="87e03-203">Click **Save settings** button toosave hello settings.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="87e03-205">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="87e03-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="87e03-206">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="87e03-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="87e03-207">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="87e03-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="87e03-208">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87e03-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="87e03-209">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="87e03-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="87e03-211">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="87e03-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="87e03-212">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="87e03-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="87e03-214">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="87e03-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="87e03-216">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="87e03-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="87e03-218">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="87e03-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="87e03-220">a.</span><span class="sxs-lookup"><span data-stu-id="87e03-220">a.</span></span> <span data-ttu-id="87e03-221">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87e03-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87e03-222">b.</span><span class="sxs-lookup"><span data-stu-id="87e03-222">b.</span></span> <span data-ttu-id="87e03-223">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="87e03-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="87e03-224">c.</span><span class="sxs-lookup"><span data-stu-id="87e03-224">c.</span></span> <span data-ttu-id="87e03-225">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="87e03-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="87e03-226">d.</span><span class="sxs-lookup"><span data-stu-id="87e03-226">d.</span></span> <span data-ttu-id="87e03-227">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="87e03-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="87e03-228">Creación del usuario de prueba de SAML SSO for Jira by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="87e03-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="87e03-229">toolog de los usuarios de Azure AD tooenable en tooSAML SSO para Jira mediante la resolución GmbH, se les deben aprovisionar en SSO de SAML para Jira mediante la resolución GmbH.</span><span class="sxs-lookup"><span data-stu-id="87e03-229">tooenable Azure AD users toolog in tooSAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="87e03-230">En SAML SSO for Jira by resolution GmbH, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="87e03-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="87e03-231">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="87e03-231">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="87e03-232">Inicie sesión en tooyour SSO de SAML para Jira por sitio de la compañía de resolución GmbH como administrador.</span><span class="sxs-lookup"><span data-stu-id="87e03-232">Log in tooyour SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="87e03-233">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="87e03-233">Hover on cog and click hello **User management**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="87e03-235">Son tooenter de página de acceso redirigida tooAdministrator **contraseña** y haga clic en **confirmar** botón.</span><span class="sxs-lookup"><span data-stu-id="87e03-235">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Agregar empleado](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="87e03-237">En la sección de la pestaña **Administración de usuarios**, haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="87e03-237">Under **User management** tab section, click **create user**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="87e03-239">En hello **"Crear nuevo usuario"** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="87e03-239">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Agregar empleado](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="87e03-241">a.</span><span class="sxs-lookup"><span data-stu-id="87e03-241">a.</span></span> <span data-ttu-id="87e03-242">Hola **dirección de correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="87e03-242">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="87e03-243">b.</span><span class="sxs-lookup"><span data-stu-id="87e03-243">b.</span></span> <span data-ttu-id="87e03-244">Hola **nombre completo** cuadro de texto, nombre completo del tipo de usuario de hello como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87e03-244">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="87e03-245">c.</span><span class="sxs-lookup"><span data-stu-id="87e03-245">c.</span></span> <span data-ttu-id="87e03-246">Hola **nombre de usuario** Hola de tipo de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="87e03-246">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="87e03-247">d.</span><span class="sxs-lookup"><span data-stu-id="87e03-247">d.</span></span> <span data-ttu-id="87e03-248">Hola **contraseña** cuadro de texto, escriba la contraseña de saludo del usuario.</span><span class="sxs-lookup"><span data-stu-id="87e03-248">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="87e03-249">e.</span><span class="sxs-lookup"><span data-stu-id="87e03-249">e.</span></span> <span data-ttu-id="87e03-250">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="87e03-250">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="87e03-251">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="87e03-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="87e03-252">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSAML SSO para Jira mediante la resolución GmbH.</span><span class="sxs-lookup"><span data-stu-id="87e03-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Jira by resolution GmbH.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="87e03-254">**tooassign Britta Simon tooSAML SSO para Jira mediante la resolución GmbH, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="87e03-254">**tooassign Britta Simon tooSAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="87e03-255">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="87e03-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="87e03-257">En la lista de aplicaciones de hello, seleccione **SSO de SAML para Jira mediante la resolución GmbH**.</span><span class="sxs-lookup"><span data-stu-id="87e03-257">In hello applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="87e03-259">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="87e03-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="87e03-261">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="87e03-261">Click **Add** button.</span></span> <span data-ttu-id="87e03-262">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="87e03-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="87e03-264">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="87e03-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="87e03-265">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="87e03-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="87e03-266">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="87e03-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="87e03-267">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="87e03-267">Testing single sign-on</span></span>

<span data-ttu-id="87e03-268">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="87e03-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="87e03-269">Al hacer clic en hello SSO de SAML para Jira por mosaico GmbH de resolución en el Panel de acceso de hello, deberá obtener automáticamente ha iniciado sesión tooyour SSO de SAML para Jira mediante la resolución de aplicación GmbH.</span><span class="sxs-lookup"><span data-stu-id="87e03-269">When you click hello SAML SSO for Jira by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="87e03-270">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="87e03-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="87e03-271">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="87e03-271">Additional resources</span></span>

* [<span data-ttu-id="87e03-272">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87e03-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87e03-273">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87e03-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

