---
title: "Tutorial: Integración de Azure Active Directory con Rightscale | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="3576d-103">Tutorial: Integración de Azure Active Directory con Rightscale</span><span class="sxs-lookup"><span data-stu-id="3576d-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="3576d-104">En este tutorial, aprenderá cómo toointegrate Rightscale con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3576d-104">In this tutorial, you learn how toointegrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3576d-105">Integración Rightscale con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3576d-105">Integrating Rightscale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3576d-106">Puede controlar en Azure AD que tenga acceso tooRightscale</span><span class="sxs-lookup"><span data-stu-id="3576d-106">You can control in Azure AD who has access tooRightscale</span></span>
- <span data-ttu-id="3576d-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooRightscale (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3576d-107">You can enable your users tooautomatically get signed-on tooRightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3576d-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3576d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3576d-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3576d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3576d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3576d-110">Prerequisites</span></span>

<span data-ttu-id="3576d-111">integración de Azure AD con Rightscale tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3576d-111">tooconfigure Azure AD integration with Rightscale, you need hello following items:</span></span>

- <span data-ttu-id="3576d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3576d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3576d-113">Una suscripción habilitada para el inicio de sesión único en Rightscale</span><span class="sxs-lookup"><span data-stu-id="3576d-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3576d-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3576d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3576d-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3576d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3576d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3576d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3576d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3576d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3576d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3576d-118">Scenario description</span></span>
<span data-ttu-id="3576d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3576d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3576d-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="3576d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3576d-121">Agregar Rightscale desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3576d-121">Adding Rightscale from hello gallery</span></span>
2. <span data-ttu-id="3576d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3576d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-hello-gallery"></a><span data-ttu-id="3576d-123">Agregar Rightscale desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3576d-123">Adding Rightscale from hello gallery</span></span>
<span data-ttu-id="3576d-124">integración de hello tooconfigure de Rightscale en Azure AD, deberá tooadd Rightscale de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3576d-124">tooconfigure hello integration of Rightscale into Azure AD, you need tooadd Rightscale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3576d-125">**tooadd Rightscale de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3576d-125">**tooadd Rightscale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3576d-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3576d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3576d-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3576d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3576d-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3576d-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3576d-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3576d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3576d-133">En el cuadro de búsqueda de hello, escriba **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="3576d-133">In hello search box, type **Rightscale**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="3576d-135">En el panel de resultados de hello, seleccione **Rightscale**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3576d-135">In hello results panel, select **Rightscale**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3576d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3576d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3576d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Rightscale con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3576d-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3576d-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Rightscale es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3576d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rightscale is tooa user in Azure AD.</span></span> <span data-ttu-id="3576d-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Rightscale debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="3576d-140">In other words, a link relationship between an Azure AD user and hello related user in Rightscale needs toobe established.</span></span>

<span data-ttu-id="3576d-141">En Rightscale, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3576d-141">In Rightscale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3576d-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Rightscale, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3576d-142">tooconfigure and test Azure AD single sign-on with Rightscale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3576d-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="3576d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3576d-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3576d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3576d-145">**[Crear un usuario de prueba Rightscale](#creating-a-rightscale-test-user)**  -toohave un equivalente de Britta Simon en Rightscale que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="3576d-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - toohave a counterpart of Britta Simon in Rightscale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3576d-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3576d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3576d-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3576d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3576d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3576d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3576d-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Rightscale.</span><span class="sxs-lookup"><span data-stu-id="3576d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="3576d-150">**inicio de sesión único en Azure AD tooconfigure con Rightscale, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3576d-150">**tooconfigure Azure AD single sign-on with Rightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="3576d-151">En el portal de Azure, en Hola Hola **Rightscale** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3576d-151">In hello Azure portal, on hello **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3576d-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3576d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="3576d-155">En hello **Rightscale dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado por IDP** no tiene tooperform todos los pasos tal y como aplicación hello ya está integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="3576d-155">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode** you do not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="3576d-157">En hello **Rightscale dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado en SP**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3576d-157">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="3576d-159">a.</span><span class="sxs-lookup"><span data-stu-id="3576d-159">a.</span></span> <span data-ttu-id="3576d-160">Haga clic en hello **mostrar avanzadas de configuración de la URL**.</span><span class="sxs-lookup"><span data-stu-id="3576d-160">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="3576d-161">b.</span><span class="sxs-lookup"><span data-stu-id="3576d-161">b.</span></span> <span data-ttu-id="3576d-162">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="3576d-162">In hello **Sign On URL** textbox, type hello URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="3576d-163">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3576d-163">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="3576d-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3576d-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="3576d-167">En hello **Rightscale configuración** sección, haga clic en **configurar Rightscale** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="3576d-167">On hello **Rightscale Configuration** section, click **Configure Rightscale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3576d-168">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="3576d-168">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="3576d-169">![Configuración del inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="3576d-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="3576d-170">tooget configurado para la aplicación de SSO, debe a toosign en tooyour RightScale inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="3576d-170">tooget SSO configured for your application, you need toosign-on tooyour RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="3576d-171">a.</span><span class="sxs-lookup"><span data-stu-id="3576d-171">a.</span></span> <span data-ttu-id="3576d-172">En el menú de hello en la parte superior de hello, haga clic en hello **configuración** pestaña y seleccione **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="3576d-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="3576d-174">b.</span><span class="sxs-lookup"><span data-stu-id="3576d-174">b.</span></span> <span data-ttu-id="3576d-175">Haga clic en hello "**nueva**" botón tooadd **los proveedores de identidad SAML**.</span><span class="sxs-lookup"><span data-stu-id="3576d-175">Click hello "**new**" button tooadd **Your SAML Identity Providers**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="3576d-177">c.</span><span class="sxs-lookup"><span data-stu-id="3576d-177">c.</span></span> <span data-ttu-id="3576d-178">En el cuadro de texto hello de **nombre para mostrar**, el nombre de la compañía de entrada.</span><span class="sxs-lookup"><span data-stu-id="3576d-178">In hello textbox of **Display Name**, input your company name.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="3576d-180">d.</span><span class="sxs-lookup"><span data-stu-id="3576d-180">d.</span></span> <span data-ttu-id="3576d-181">Seleccione **SSO iniciado por el RightScale permite usar una sugerencia de detección** y entrada su **nombre de dominio** Hola por debajo del cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3576d-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in hello below textbox.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="3576d-183">e.</span><span class="sxs-lookup"><span data-stu-id="3576d-183">e.</span></span> <span data-ttu-id="3576d-184">Pegue el valor de Hola de **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure en **punto de conexión de SSO de SAML** en RightScale.</span><span class="sxs-lookup"><span data-stu-id="3576d-184">Paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="3576d-186">f.</span><span class="sxs-lookup"><span data-stu-id="3576d-186">f.</span></span> <span data-ttu-id="3576d-187">Pegue el valor de Hola de **Id. de entidad SAML** que haya copiado desde el portal de Azure en **SAML EntityID** en RightScale.</span><span class="sxs-lookup"><span data-stu-id="3576d-187">Paste hello value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="3576d-189">g.</span><span class="sxs-lookup"><span data-stu-id="3576d-189">g.</span></span> <span data-ttu-id="3576d-190">Haga clic en **explorador** certificado de hello tooupload de botón que descargó desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3576d-190">Click **Browser** button tooupload hello certificate which you downloaded from Azure portal.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="3576d-192">h.</span><span class="sxs-lookup"><span data-stu-id="3576d-192">h.</span></span> <span data-ttu-id="3576d-193">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3576d-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="3576d-194">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="3576d-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3576d-195">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="3576d-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3576d-196">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3576d-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3576d-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3576d-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="3576d-198">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="3576d-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3576d-200">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3576d-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3576d-201">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3576d-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3576d-203">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3576d-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3576d-205">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3576d-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3576d-207">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3576d-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3576d-209">a.</span><span class="sxs-lookup"><span data-stu-id="3576d-209">a.</span></span> <span data-ttu-id="3576d-210">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3576d-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3576d-211">b.</span><span class="sxs-lookup"><span data-stu-id="3576d-211">b.</span></span> <span data-ttu-id="3576d-212">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3576d-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3576d-213">c.</span><span class="sxs-lookup"><span data-stu-id="3576d-213">c.</span></span> <span data-ttu-id="3576d-214">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3576d-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3576d-215">d.</span><span class="sxs-lookup"><span data-stu-id="3576d-215">d.</span></span> <span data-ttu-id="3576d-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3576d-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="3576d-217">Creación de un usuario de prueba de Rightscale</span><span class="sxs-lookup"><span data-stu-id="3576d-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="3576d-218">En esta sección, creará un usuario denominado Britta Simon en RightScale.</span><span class="sxs-lookup"><span data-stu-id="3576d-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="3576d-219">Trabajar con [equipo de soporte técnico de Rightscale cliente](mailto:support@rightscale.com) a los usuarios de tooadd hello en la plataforma de RightScale Hola.</span><span class="sxs-lookup"><span data-stu-id="3576d-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) tooadd hello users in hello RightScale platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3576d-220">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3576d-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3576d-221">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooRightscale.</span><span class="sxs-lookup"><span data-stu-id="3576d-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightscale.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3576d-223">**tooassign Britta Simon tooRightscale, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3576d-223">**tooassign Britta Simon tooRightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="3576d-224">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3576d-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3576d-226">En la lista de aplicaciones de hello, seleccione **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="3576d-226">In hello applications list, select **Rightscale**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="3576d-228">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3576d-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3576d-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3576d-230">Click **Add** button.</span></span> <span data-ttu-id="3576d-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3576d-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3576d-233">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3576d-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3576d-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3576d-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3576d-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3576d-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3576d-236">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3576d-236">Testing single sign-on</span></span>

<span data-ttu-id="3576d-237">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3576d-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="3576d-238">Al hacer clic en icono de RightScale Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour RightScale aplicación.</span><span class="sxs-lookup"><span data-stu-id="3576d-238">When you click hello RightScale tile in hello Access Panel, you should get automatically signed-on tooyour RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3576d-239">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3576d-239">Additional resources</span></span>

* [<span data-ttu-id="3576d-240">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3576d-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3576d-241">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3576d-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

