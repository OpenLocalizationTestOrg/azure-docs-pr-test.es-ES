---
title: "Tutorial: Integración de Azure Active Directory con GitHub | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="ae751-103">Tutorial: Integración de Azure Active Directory con GitHub</span><span class="sxs-lookup"><span data-stu-id="ae751-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="ae751-104">En este tutorial, aprenderá cómo toointegrate GitHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae751-104">In this tutorial, you learn how toointegrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae751-105">Integración de GitHub con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ae751-105">Integrating GitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ae751-106">Puede controlar en Azure AD que tenga acceso tooGitHub</span><span class="sxs-lookup"><span data-stu-id="ae751-106">You can control in Azure AD who has access tooGitHub</span></span>
- <span data-ttu-id="ae751-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooGitHub (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae751-107">You can enable your users tooautomatically get signed-on tooGitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae751-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="ae751-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="ae751-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae751-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae751-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ae751-110">Prerequisites</span></span>

<span data-ttu-id="ae751-111">integración de Azure AD con GitHub tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ae751-111">tooconfigure Azure AD integration with GitHub, you need hello following items:</span></span>

- <span data-ttu-id="ae751-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae751-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae751-113">Una suscripción habilitada para inicio de sesión único en GitHub</span><span class="sxs-lookup"><span data-stu-id="ae751-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="ae751-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ae751-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="ae751-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ae751-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae751-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ae751-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ae751-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae751-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="ae751-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ae751-118">Scenario description</span></span>
<span data-ttu-id="ae751-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ae751-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae751-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="ae751-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae751-121">Adición de GitHub de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ae751-121">Adding GitHub from hello gallery</span></span>
2. <span data-ttu-id="ae751-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae751-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-hello-gallery"></a><span data-ttu-id="ae751-123">Adición de GitHub de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ae751-123">Adding GitHub from hello gallery</span></span>
<span data-ttu-id="ae751-124">integración de hello tooconfigure de GitHub en Azure AD, deberá tooadd GitHub de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="ae751-124">tooconfigure hello integration of GitHub into Azure AD, you need tooadd GitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ae751-125">**tooadd GitHub de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ae751-125">**tooadd GitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae751-126">Hola ** [Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ae751-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae751-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ae751-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ae751-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ae751-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ae751-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae751-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ae751-133">En el cuadro de búsqueda de hello, escriba **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="ae751-133">In hello search box, type **GitHub.com**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="ae751-135">En el panel de resultados de hello, seleccione **GitHub**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ae751-135">In hello results panel, select **GitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae751-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae751-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae751-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con GitHub mediante un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae751-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae751-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en GitHub es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae751-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="ae751-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en GitHub debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="ae751-140">In other words, a link relationship between an Azure AD user and hello related user in GitHub needs toobe established.</span></span>

<span data-ttu-id="ae751-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en GitHub.</span><span class="sxs-lookup"><span data-stu-id="ae751-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in GitHub.</span></span>

<span data-ttu-id="ae751-142">tooconfigure y prueba de inicio de sesión único en Azure AD con GitHub, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ae751-142">tooconfigure and test Azure AD single sign-on with GitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ae751-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="ae751-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ae751-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae751-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae751-145">**[Crear un usuario de prueba de GitHub](#creating-a-GitHub-test-user) ** -toohave un equivalente de Britta Simon en GitHub que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="ae751-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - toohave a counterpart of Britta Simon in GitHub that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="ae751-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ae751-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae751-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ae751-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae751-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae751-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae751-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación de GitHub.</span><span class="sxs-lookup"><span data-stu-id="ae751-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="ae751-150">**inicio de sesión único en Azure AD tooconfigure con GitHub, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ae751-150">**tooconfigure Azure AD single sign-on with GitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae751-151">En el portal de administración de Azure de hello, en hello **GitHub** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ae751-151">In hello Azure Management portal, on hello **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ae751-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ae751-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="ae751-155">En hello **GitHub dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ae751-155">On hello **GitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="ae751-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae751-157">a.</span></span> <span data-ttu-id="ae751-158">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello como:`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="ae751-158">In hello **Sign-on URL** textbox, type hello value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="ae751-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae751-159">b.</span></span> <span data-ttu-id="ae751-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="ae751-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae751-161">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae751-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="ae751-162">Tener tooupdate estos valores con hello Sign-on dirección URL real y el identificador.</span><span class="sxs-lookup"><span data-stu-id="ae751-162">You have tooupdate these values with hello actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="ae751-163">Aquí le sugerimos toouse Hola único valor de cadena en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="ae751-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="ae751-164">Vaya a tooGitHub administrador sección tooretrieve estos valores.</span><span class="sxs-lookup"><span data-stu-id="ae751-164">Go tooGitHub Admin section tooretrieve these values.</span></span> 

4. <span data-ttu-id="ae751-165">En hello **atributos de usuario** sección, seleccione **identificador de usuario** como user.mail.</span><span class="sxs-lookup"><span data-stu-id="ae751-165">On hello **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="ae751-167">En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="ae751-167">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="ae751-169">En hello **crear nuevo certificado** cuadro de diálogo, haga clic en el icono del calendario de Hola y seleccione un **fecha de expiración**.</span><span class="sxs-lookup"><span data-stu-id="ae751-169">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="ae751-170">Luego haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ae751-170">Then click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="ae751-172">En hello **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado** y haga clic en **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="ae751-172">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="ae751-174">En la ventana emergente de hello **el certificado de sustitución** ventana, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ae751-174">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="ae751-176">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ae751-176">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="ae751-178">En hello **configuración de GitHub** sección, haga clic en **configurar GitHub** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="ae751-178">On hello **GitHub Configuration** section, click **Configure GitHub** tooopen **Configure sign-on** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="ae751-181">En otra ventana del navegador web, inicie sesión en el sitio de la organización de GitHub como administrador.</span><span class="sxs-lookup"><span data-stu-id="ae751-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="ae751-182">Navegue demasiado**configuración** y haga clic en **seguridad**</span><span class="sxs-lookup"><span data-stu-id="ae751-182">Navigate too**Settings** and click **Security**</span></span>

    ![Settings](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="ae751-184">Comprobar hello **Habilitar autenticación SAML** cuadro, revelar campos de hello el inicio de sesión único en la configuración.</span><span class="sxs-lookup"><span data-stu-id="ae751-184">Check hello **Enable SAML authentication** box, revealing hello Single Sign-on configuration fields.</span></span> <span data-ttu-id="ae751-185">A continuación, utilice Hola único inicio de sesión valor tooupdate Hola único inicio de sesión en dirección URL en configuración de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae751-185">Then, use hello single sign-on URL value tooupdate hello Single sign-on URL on Azure AD configuration.</span></span>

    ![Settings](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="ae751-187">Configurar Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="ae751-187">Configure hello following fields:</span></span>

    <span data-ttu-id="ae751-188">a.</span><span class="sxs-lookup"><span data-stu-id="ae751-188">a.</span></span> <span data-ttu-id="ae751-189">**Dirección URL de inicio de sesión**: escriba **el inicio de sesión único de SAML dirección URL del servicio** de hello **configurar GitHub** sección en Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae751-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="ae751-190">b.</span><span class="sxs-lookup"><span data-stu-id="ae751-190">b.</span></span> <span data-ttu-id="ae751-191">**Emisor**: escriba **Id. de entidad SAML** de hello **configurar GitHub** sección en Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae751-191">**Issuer**: Enter **SAML Entity ID** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="ae751-192">c.</span><span class="sxs-lookup"><span data-stu-id="ae751-192">c.</span></span> <span data-ttu-id="ae751-193">**Certificado público**: Hola abierto descarga certificado de Azure AD en un contenido de hello el Bloc de notas y copie incluidos "BEGIN CERTIFICATE" y "END CERTIFICATE"</span><span class="sxs-lookup"><span data-stu-id="ae751-193">**Public Certificate**: Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Settings](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="ae751-195">Haga clic en **configuración de SAML de prueba** tooconfirm que no hay errores de validación o errores durante el SSO.</span><span class="sxs-lookup"><span data-stu-id="ae751-195">Click on **Test SAML configuration** tooconfirm that no validation failures or errors during SSO.</span></span>

    ![Settings](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="ae751-197">Haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="ae751-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae751-198">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae751-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae751-199">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="ae751-199">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ae751-201">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ae751-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae751-202">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ae751-202">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae751-204">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ae751-204">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae751-206">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae751-206">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae751-208">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ae751-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae751-210">a.</span><span class="sxs-lookup"><span data-stu-id="ae751-210">a.</span></span> <span data-ttu-id="ae751-211">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae751-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae751-212">b.</span><span class="sxs-lookup"><span data-stu-id="ae751-212">b.</span></span> <span data-ttu-id="ae751-213">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae751-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae751-214">c.</span><span class="sxs-lookup"><span data-stu-id="ae751-214">c.</span></span> <span data-ttu-id="ae751-215">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ae751-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ae751-216">d.</span><span class="sxs-lookup"><span data-stu-id="ae751-216">d.</span></span> <span data-ttu-id="ae751-217">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ae751-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="ae751-218">Creación de un usuario de prueba de GitHub</span><span class="sxs-lookup"><span data-stu-id="ae751-218">Creating a GitHub test user</span></span>

<span data-ttu-id="ae751-219">En orden tooenable toolog de los usuarios de Azure AD en GitHub, se les deben aprovisionar en GitHub.</span><span class="sxs-lookup"><span data-stu-id="ae751-219">In order tooenable Azure AD users toolog into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="ae751-220">En caso de hello de GitHub, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="ae751-220">In hello case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="ae751-221">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="ae751-221">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae751-222">Inicie sesión en tooyour sitio de GitHub su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="ae751-222">Log in tooyour GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="ae751-223">Haga clic en **Contactos**.</span><span class="sxs-lookup"><span data-stu-id="ae751-223">Click **People**.</span></span>

    <span data-ttu-id="ae751-224">![Personas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="ae751-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="ae751-225">Haga clic en **Invitar a miembros**.</span><span class="sxs-lookup"><span data-stu-id="ae751-225">Click **Invite member**.</span></span>

    <span data-ttu-id="ae751-226">![Invitación de usuarios](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invitación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="ae751-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="ae751-227">En hello **invitar miembros** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ae751-227">On hello **Invite member** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="ae751-228">a.</span><span class="sxs-lookup"><span data-stu-id="ae751-228">a.</span></span> <span data-ttu-id="ae751-229">Hola **correo electrónico** cuadro de texto, dirección de correo electrónico de Hola de tipo de cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae751-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="ae751-230">![Invitar a personas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invitar a personas")</span><span class="sxs-lookup"><span data-stu-id="ae751-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="ae751-231">b.</span><span class="sxs-lookup"><span data-stu-id="ae751-231">b.</span></span> <span data-ttu-id="ae751-232">Haga clic en **Enviar invitación**.</span><span class="sxs-lookup"><span data-stu-id="ae751-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="ae751-233">![Invitar a personas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invitar a personas")</span><span class="sxs-lookup"><span data-stu-id="ae751-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae751-234">titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="ae751-234">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ae751-235">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae751-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ae751-236">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooGitHub de acceso.</span><span class="sxs-lookup"><span data-stu-id="ae751-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooGitHub.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ae751-238">**tooassign Britta Simon tooGitHub, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ae751-238">**tooassign Britta Simon tooGitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae751-239">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ae751-239">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ae751-241">En la lista de aplicaciones de hello, seleccione **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="ae751-241">In hello applications list, select **GitHub.com**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="ae751-243">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae751-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ae751-245">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ae751-245">Click **Add** button.</span></span> <span data-ttu-id="ae751-246">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ae751-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ae751-248">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae751-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ae751-249">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae751-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae751-250">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ae751-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="ae751-251">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ae751-251">Testing single sign-on</span></span>

<span data-ttu-id="ae751-252">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ae751-252">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ae751-253">Al hacer clic en icono de GitHub de Hola Hola Panel de acceso, deberá obtener tooyour iniciado sesión en aplicaciones de GitHub.</span><span class="sxs-lookup"><span data-stu-id="ae751-253">When you click hello GitHub tile in hello Access Panel, you should get signed-on tooyour GitHub application.</span></span> <span data-ttu-id="ae751-254">Con su cuenta personal podrá iniciar la sesión como una cuenta de organización pero, a continuación, la necesidad toolog.</span><span class="sxs-lookup"><span data-stu-id="ae751-254">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ae751-255">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ae751-255">Additional resources</span></span>

* [<span data-ttu-id="ae751-256">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae751-256">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae751-257">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae751-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
