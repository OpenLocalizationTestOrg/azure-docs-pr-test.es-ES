---
title: "Tutorial: integración de Azure Active Directory con DocuSign | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="6e440-103">Tutorial: Integración de Azure Active Directory con DocuSign</span><span class="sxs-lookup"><span data-stu-id="6e440-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="6e440-104">En este tutorial, aprenderá cómo toointegrate DocuSign con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e440-104">In this tutorial, you learn how toointegrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e440-105">Integración de DocuSign con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6e440-105">Integrating DocuSign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6e440-106">Puede controlar en Azure AD que tenga acceso tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="6e440-106">You can control in Azure AD who has access tooDocuSign</span></span>
- <span data-ttu-id="6e440-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooDocuSign (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e440-107">You can enable your users tooautomatically get signed-on tooDocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e440-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6e440-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6e440-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e440-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e440-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6e440-110">Prerequisites</span></span>

<span data-ttu-id="6e440-111">integración de Azure AD con DocuSign tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6e440-111">tooconfigure Azure AD integration with DocuSign, you need hello following items:</span></span>

- <span data-ttu-id="6e440-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e440-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e440-113">Una suscripción habilitada para el inicio de sesión único en DocuSign</span><span class="sxs-lookup"><span data-stu-id="6e440-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e440-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6e440-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e440-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6e440-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e440-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6e440-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e440-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e440-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e440-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6e440-118">Scenario description</span></span>
<span data-ttu-id="6e440-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6e440-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e440-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="6e440-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e440-121">Agregar DocuSign desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6e440-121">Adding DocuSign from hello gallery</span></span>
2. <span data-ttu-id="6e440-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e440-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-hello-gallery"></a><span data-ttu-id="6e440-123">Agregar DocuSign desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6e440-123">Adding DocuSign from hello gallery</span></span>
<span data-ttu-id="6e440-124">integración de hello tooconfigure de DocuSign en Azure AD, deberá tooadd DocuSign de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="6e440-124">tooconfigure hello integration of DocuSign into Azure AD, you need tooadd DocuSign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6e440-125">**tooadd DocuSign de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6e440-125">**tooadd DocuSign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e440-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6e440-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6e440-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6e440-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6e440-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6e440-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="6e440-131">Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e440-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="6e440-133">En el cuadro de búsqueda de hello, escriba **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="6e440-133">In hello search box, type **DocuSign**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="6e440-135">En el panel de resultados de hello, seleccione **DocuSign**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6e440-135">In hello results panel, select **DocuSign**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e440-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e440-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e440-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con DocuSign con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6e440-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6e440-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en DocuSign es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e440-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DocuSign is tooa user in Azure AD.</span></span> <span data-ttu-id="6e440-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en DocuSign debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="6e440-140">In other words, a link relationship between an Azure AD user and hello related user in DocuSign needs toobe established.</span></span>

<span data-ttu-id="6e440-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en DocuSign.</span><span class="sxs-lookup"><span data-stu-id="6e440-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in DocuSign.</span></span>

<span data-ttu-id="6e440-142">tooconfigure y prueba de inicio de sesión único en Azure AD con DocuSign, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6e440-142">tooconfigure and test Azure AD single sign-on with DocuSign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6e440-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="6e440-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6e440-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e440-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e440-145">**[Crear un usuario de prueba de DocuSign](#creating-a-docusign-test-user) ** -toohave un equivalente de Britta Simon en DocuSign que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="6e440-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - toohave a counterpart of Britta Simon in DocuSign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e440-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6e440-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e440-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="6e440-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e440-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e440-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e440-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de DocuSign.</span><span class="sxs-lookup"><span data-stu-id="6e440-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="6e440-150">**inicio de sesión único en tooconfigure Azure AD con DocuSign, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6e440-150">**tooconfigure Azure AD single sign-on with DocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e440-151">En el portal de Azure, en Hola Hola **DocuSign** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6e440-151">In hello Azure portal, on hello **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="6e440-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6e440-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="6e440-155">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base 64)** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6e440-155">On hello **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="6e440-157">En hello **configuración de DocuSign** sección del portal de Azure, haga clic en **DocuSign configurar** ventana tooopen configurar inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6e440-157">On hello **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** tooopen Configure sign-on window.</span></span> <span data-ttu-id="6e440-158">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="6e440-158">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="6e440-160">En una ventana del explorador web diferente, inicio de sesión tooyour **portal de administración de DocuSign** como administrador.</span><span class="sxs-lookup"><span data-stu-id="6e440-160">In a different web browser window, login tooyour **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="6e440-161">En el menú de navegación de Hola Hola izquierda, haga clic en **dominios**.</span><span class="sxs-lookup"><span data-stu-id="6e440-161">In hello navigation menu on hello left, click **Domains**.</span></span>
   
    ![Configuración del inicio de sesión único][51]

7. <span data-ttu-id="6e440-163">En el panel derecho de hello, haga clic en **notificación dominio**.</span><span class="sxs-lookup"><span data-stu-id="6e440-163">On hello right pane, click **Claim Domain**.</span></span>
   
    ![Configuración del inicio de sesión único][52]

8. <span data-ttu-id="6e440-165">En hello **de notificación de un dominio** cuadro de diálogo, en hello **nombre de dominio** cuadro de texto, escriba el dominio de su empresa y, a continuación, haga clic en **notificación**.</span><span class="sxs-lookup"><span data-stu-id="6e440-165">On hello **Claim a domain** dialog, in hello **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="6e440-166">Asegúrese de comprobar el dominio de Hola y Hola estado está activo.</span><span class="sxs-lookup"><span data-stu-id="6e440-166">Make sure that you verify hello domain and hello status is active.</span></span>
   
    ![Configuración del inicio de sesión único][53]

9. <span data-ttu-id="6e440-168">En el menú en el lado izquierdo de hello, haga clic en **proveedores de identidades**</span><span class="sxs-lookup"><span data-stu-id="6e440-168">In menu on hello left side, click **Identity Providers**</span></span>  
   
    ![Configuración del inicio de sesión único][54]
10. <span data-ttu-id="6e440-170">En el panel derecho de hello, haga clic en **Agregar proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="6e440-170">In hello right pane, click **Add Identity Provider**.</span></span> 
   
    ![Configuración del inicio de sesión único][55]

11. <span data-ttu-id="6e440-172">En hello **configuración del proveedor de identidad** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="6e440-172">On hello **Identity Provider Settings** page, perform hello following steps:</span></span>
   
    ![Configuración del inicio de sesión único][56]

    <span data-ttu-id="6e440-174">a.</span><span class="sxs-lookup"><span data-stu-id="6e440-174">a.</span></span> <span data-ttu-id="6e440-175">Hola **nombre** cuadro de texto, escriba un nombre único para la configuración.</span><span class="sxs-lookup"><span data-stu-id="6e440-175">In hello **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="6e440-176">No utilice espacios.</span><span class="sxs-lookup"><span data-stu-id="6e440-176">Do not use spaces.</span></span>

    <span data-ttu-id="6e440-177">b.</span><span class="sxs-lookup"><span data-stu-id="6e440-177">b.</span></span> <span data-ttu-id="6e440-178">Pegar **Id. de entidad SAML** en hello **emisor del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="6e440-178">Paste **SAML Entity ID** into hello **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="6e440-179">c.</span><span class="sxs-lookup"><span data-stu-id="6e440-179">c.</span></span> <span data-ttu-id="6e440-180">Pegar **SAML Single Sign-On dirección URL del servicio** en hello **URL de inicio de sesión del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="6e440-180">Paste **SAML Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="6e440-181">d.</span><span class="sxs-lookup"><span data-stu-id="6e440-181">d.</span></span> <span data-ttu-id="6e440-182">Pegar **dirección URL de cierre de sesión** en hello **URL de cierre de sesión del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="6e440-182">Paste **Sign-Out URL** into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="6e440-183">e.</span><span class="sxs-lookup"><span data-stu-id="6e440-183">e.</span></span> <span data-ttu-id="6e440-184">Seleccione **Sign AuthN Request**(Firmar solicitud de autenticación).</span><span class="sxs-lookup"><span data-stu-id="6e440-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="6e440-185">f.</span><span class="sxs-lookup"><span data-stu-id="6e440-185">f.</span></span> <span data-ttu-id="6e440-186">En **Send AuthN request by** (Enviar solicitud de autorización por), seleccione **POST**.</span><span class="sxs-lookup"><span data-stu-id="6e440-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="6e440-187">g.</span><span class="sxs-lookup"><span data-stu-id="6e440-187">g.</span></span> <span data-ttu-id="6e440-188">En **Send logout request by** (Enviar solicitud de cierre de sesión por), seleccione **GET**.</span><span class="sxs-lookup"><span data-stu-id="6e440-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="6e440-189">Hola **asignación de atributo personalizado** sección, elija el campo de Hola que desee toomap con notificación de AD de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e440-189">In hello **Custom Attribute Mapping** section, choose hello field you want toomap with Azure AD Claim.</span></span> <span data-ttu-id="6e440-190">En este ejemplo, Hola **emailaddress** notificación se asigna su valor hello **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="6e440-190">In this example, hello **emailaddress** claim is mapped with hello value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="6e440-191">Es nombre de notificación predeterminado de Hola de Azure AD para notificación de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="6e440-191">It is hello default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="6e440-192">Hola de uso adecuado **identificador de usuario** toomap usuario de saludo de la asignación de usuario de Azure AD tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="6e440-192">Use hello appropriate **User identifier** toomap hello user from Azure AD tooDocuSign user mapping.</span></span> <span data-ttu-id="6e440-193">Seleccione Hola campo apropiado y escriba el valor adecuado de hello según la configuración de la organización.</span><span class="sxs-lookup"><span data-stu-id="6e440-193">Select hello proper Field and enter hello appropriate value based on your organization settings.</span></span>
          
    ![Configuración del inicio de sesión único][57]

13. <span data-ttu-id="6e440-195">Hola **certificado del proveedor de identidad** sección, haga clic en **agregar certificado**y, a continuación, cargar el certificado de Hola que ha descargado desde el portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e440-195">In hello **Identity Provider Certificate** section, click **Add Certificate**, and then upload hello certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Configuración del inicio de sesión único][58]

14. <span data-ttu-id="6e440-197">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6e440-197">Click **Save**.</span></span>

15. <span data-ttu-id="6e440-198">Hola **proveedores de identidades** sección, haga clic en **acciones**y, a continuación, haga clic en **extremos**.</span><span class="sxs-lookup"><span data-stu-id="6e440-198">In hello **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Configuración del inicio de sesión único][59]
 
16. <span data-ttu-id="6e440-200">Hola **ver SAML 2.0 extremos** sección **portal de administración de DocuSign**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6e440-200">In hello **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform hello following steps:</span></span>
   
    ![Configuración del inicio de sesión único][60]
   
    <span data-ttu-id="6e440-202">a.</span><span class="sxs-lookup"><span data-stu-id="6e440-202">a.</span></span> <span data-ttu-id="6e440-203">Hola copia **dirección URL del emisor de proveedor de servicio**y, a continuación, pegue en hello **identificador** en el cuadro de texto **DocuSign dominio y las direcciones URL** sección de hello Azure Hola siguiente portal patrón: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="6e440-203">Copy hello **Service Provider Issuer URL**, and then paste into hello **Identifier** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="6e440-204">b.</span><span class="sxs-lookup"><span data-stu-id="6e440-204">b.</span></span> <span data-ttu-id="6e440-205">Hola copia **dirección URL de inicio de sesión del proveedor de servicio**y, a continuación, pegue en hello **dirección URL de inicio de sesión** en el cuadro de texto **DocuSign dominio y las direcciones URL** sección de hello Azure Hola siguiente portal patrón: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="6e440-205">Copy hello **Service Provider Login URL**, and then paste into hello **Sign On URL** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="6e440-207">c.</span><span class="sxs-lookup"><span data-stu-id="6e440-207">c.</span></span>  <span data-ttu-id="6e440-208">Haga clic en **Close**</span><span class="sxs-lookup"><span data-stu-id="6e440-208">Click **Close**</span></span>
    
17. <span data-ttu-id="6e440-209">En el portal de Azure hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="6e440-209">On hello Azure portal, click **Save**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="6e440-211">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="6e440-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6e440-212">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="6e440-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6e440-213">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e440-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e440-214">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e440-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e440-215">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="6e440-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="6e440-217">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6e440-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e440-218">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6e440-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e440-220">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6e440-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e440-222">En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e440-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e440-224">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="6e440-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e440-226">a.</span><span class="sxs-lookup"><span data-stu-id="6e440-226">a.</span></span> <span data-ttu-id="6e440-227">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e440-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e440-228">b.</span><span class="sxs-lookup"><span data-stu-id="6e440-228">b.</span></span> <span data-ttu-id="6e440-229">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6e440-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e440-230">c.</span><span class="sxs-lookup"><span data-stu-id="6e440-230">c.</span></span> <span data-ttu-id="6e440-231">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6e440-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6e440-232">d.</span><span class="sxs-lookup"><span data-stu-id="6e440-232">d.</span></span> <span data-ttu-id="6e440-233">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6e440-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="6e440-234">Creación de un usuario de prueba de DocuSign</span><span class="sxs-lookup"><span data-stu-id="6e440-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="6e440-235">Admite la aplicación **sólo en el aprovisionamiento de usuarios de tiempo** y después de autenticar usuarios se crean automáticamente en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6e440-235">Application supports **Just in time user provisioning** and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6e440-236">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e440-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6e440-237">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooDocuSign de acceso.</span><span class="sxs-lookup"><span data-stu-id="6e440-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooDocuSign.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="6e440-239">**tooassign Britta Simon tooDocuSign, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6e440-239">**tooassign Britta Simon tooDocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e440-240">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6e440-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6e440-242">En la lista de aplicaciones de hello, seleccione **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="6e440-242">In hello applications list, select **DocuSign**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="6e440-244">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6e440-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="6e440-246">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6e440-246">Click **Add** button.</span></span> <span data-ttu-id="6e440-247">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6e440-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="6e440-249">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e440-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6e440-250">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6e440-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e440-251">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6e440-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e440-252">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="6e440-252">Testing single sign-on</span></span>

<span data-ttu-id="6e440-253">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6e440-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6e440-254">Al hacer clic en icono de DocuSign Hola Hola Panel de acceso, deberá obtener aplicaciones de DocuSign tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="6e440-254">When you click hello DocuSign tile in hello Access Panel, you should get automatically signed-on tooyour DocuSign application.</span></span>
<span data-ttu-id="6e440-255">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e440-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6e440-256">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6e440-256">Additional resources</span></span>

* [<span data-ttu-id="6e440-257">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e440-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e440-258">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e440-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="6e440-259">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="6e440-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

