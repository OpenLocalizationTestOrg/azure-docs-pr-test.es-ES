---
title: "Tutorial: integración de Azure Active Directory con EverBridge | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a260298279407ed709bc2e685a104410f9836a74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="c9a21-103">Tutorial: Integración de Azure Active Directory con EverBridge</span><span class="sxs-lookup"><span data-stu-id="c9a21-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="c9a21-104">En este tutorial, aprenderá cómo toointegrate EverBridge con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9a21-104">In this tutorial, you learn how toointegrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9a21-105">Integración EverBridge con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c9a21-105">Integrating EverBridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c9a21-106">Puede controlar en Azure AD que tenga acceso tooEverBridge</span><span class="sxs-lookup"><span data-stu-id="c9a21-106">You can control in Azure AD who has access tooEverBridge</span></span>
- <span data-ttu-id="c9a21-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooEverBridge (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9a21-107">You can enable your users tooautomatically get signed-on tooEverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9a21-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c9a21-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c9a21-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9a21-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9a21-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c9a21-110">Prerequisites</span></span>

<span data-ttu-id="c9a21-111">integración de Azure AD con EverBridge tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c9a21-111">tooconfigure Azure AD integration with EverBridge, you need hello following items:</span></span>

- <span data-ttu-id="c9a21-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9a21-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9a21-113">Una suscripción habilitada para el inicio de sesión único en EverBridge</span><span class="sxs-lookup"><span data-stu-id="c9a21-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9a21-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c9a21-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9a21-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c9a21-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9a21-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c9a21-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9a21-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9a21-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9a21-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c9a21-118">Scenario description</span></span>
<span data-ttu-id="c9a21-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c9a21-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9a21-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c9a21-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9a21-121">Agregar EverBridge desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c9a21-121">Adding EverBridge from hello gallery</span></span>
2. <span data-ttu-id="c9a21-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9a21-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-hello-gallery"></a><span data-ttu-id="c9a21-123">Agregar EverBridge desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c9a21-123">Adding EverBridge from hello gallery</span></span>
<span data-ttu-id="c9a21-124">integración de hello tooconfigure de EverBridge en Azure AD, deberá tooadd EverBridge de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c9a21-124">tooconfigure hello integration of EverBridge into Azure AD, you need tooadd EverBridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c9a21-125">**tooadd EverBridge de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9a21-125">**tooadd EverBridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9a21-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c9a21-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9a21-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c9a21-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c9a21-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9a21-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c9a21-133">En el cuadro de búsqueda de hello, escriba **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-133">In hello search box, type **EverBridge**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="c9a21-135">En el panel de resultados de hello, seleccione **EverBridge**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c9a21-135">In hello results panel, select **EverBridge**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c9a21-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9a21-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c9a21-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con EverBridge con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c9a21-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c9a21-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en EverBridge es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9a21-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EverBridge is tooa user in Azure AD.</span></span> <span data-ttu-id="c9a21-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en EverBridge debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c9a21-140">In other words, a link relationship between an Azure AD user and hello related user in EverBridge needs toobe established.</span></span>

<span data-ttu-id="c9a21-141">En EverBridge, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9a21-141">In EverBridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c9a21-142">tooconfigure y prueba de inicio de sesión único en Azure AD con EverBridge, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c9a21-142">tooconfigure and test Azure AD single sign-on with EverBridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c9a21-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c9a21-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c9a21-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9a21-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9a21-145">**[Creación de un usuario de prueba EverBridge](#creating-an-everbridge-test-user)**  -toohave un equivalente de Britta Simon en EverBridge que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c9a21-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - toohave a counterpart of Britta Simon in EverBridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9a21-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c9a21-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9a21-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c9a21-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c9a21-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9a21-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c9a21-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación EverBridge.</span><span class="sxs-lookup"><span data-stu-id="c9a21-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="c9a21-150">**inicio de sesión único en Azure AD tooconfigure con EverBridge, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9a21-150">**tooconfigure Azure AD single sign-on with EverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9a21-151">En el portal de Azure, en Hola Hola **EverBridge** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-151">In hello Azure portal, on hello **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c9a21-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c9a21-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="c9a21-155">En hello **EverBridge dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c9a21-155">On hello **EverBridge Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="c9a21-157">a.</span><span class="sxs-lookup"><span data-stu-id="c9a21-157">a.</span></span> <span data-ttu-id="c9a21-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c9a21-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="c9a21-159">b.</span><span class="sxs-lookup"><span data-stu-id="c9a21-159">b.</span></span> <span data-ttu-id="c9a21-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="c9a21-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c9a21-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c9a21-161">These values are not real.</span></span> <span data-ttu-id="c9a21-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="c9a21-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c9a21-163">Póngase en contacto con [equipo de soporte técnico de EverBridge](mailto:support@everbridge.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="c9a21-163">Contact [EverBridge support team](mailto:support@everbridge.com) tooget these values.</span></span>
 
4. <span data-ttu-id="c9a21-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c9a21-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="c9a21-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c9a21-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c9a21-168">En hello **EverBridge configuración** sección, haga clic en **configurar EverBridge** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="c9a21-168">On hello **EverBridge Configuration** section, click **Configure EverBridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c9a21-169">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="c9a21-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="c9a21-171">tooget configurado para la aplicación de SSO, debe a toosign en tooyour Everbridge inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="c9a21-171">tooget SSO configured for your application, you need toosign-on tooyour Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="c9a21-172">En el menú de hello en la parte superior de hello, haga clic en hello **configuración** pestaña y seleccione **Single Sign-On** en **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="c9a21-174">a.</span><span class="sxs-lookup"><span data-stu-id="c9a21-174">a.</span></span> <span data-ttu-id="c9a21-175">Hola **nombre** cuadro de texto Nombre de Hola de tipo de identificador de proveedor (por ejemplo: nombre de su empresa).</span><span class="sxs-lookup"><span data-stu-id="c9a21-175">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="c9a21-176">b.</span><span class="sxs-lookup"><span data-stu-id="c9a21-176">b.</span></span> <span data-ttu-id="c9a21-177">Hola **nombre de la API** cuadro de texto, nombre de tipo hello de API.</span><span class="sxs-lookup"><span data-stu-id="c9a21-177">In hello **API Name** textbox, type hello name of API.</span></span>
   
    <span data-ttu-id="c9a21-178">c.</span><span class="sxs-lookup"><span data-stu-id="c9a21-178">c.</span></span> <span data-ttu-id="c9a21-179">Haga clic en **Elegir archivo** archivo de metadatos de Hola de tooupload de botón que descargó desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9a21-179">Click **Choose File** button tooupload hello metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="c9a21-180">d.</span><span class="sxs-lookup"><span data-stu-id="c9a21-180">d.</span></span> <span data-ttu-id="c9a21-181">En la ubicación de identidad SAML hello, seleccione **identidad está en el elemento NameIdentifier de Hola de hello instrucción Subject**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-181">In hello SAML Identity Location, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
   
    <span data-ttu-id="c9a21-182">e.</span><span class="sxs-lookup"><span data-stu-id="c9a21-182">e.</span></span> <span data-ttu-id="c9a21-183">Hola **URL de inicio de sesión del proveedor de identidades** cuadro de texto, pegue Hola valor de dirección URL de SSO de SAML de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9a21-183">In hello **Identity Provider Login URL** textbox, paste hello value of SAML SSO URL from Azure AD.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="c9a21-185">f.</span><span class="sxs-lookup"><span data-stu-id="c9a21-185">f.</span></span> <span data-ttu-id="c9a21-186">Hola proveedor iniciado por solicitud de enlace de servicio, seleccione **redirección HTTP**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-186">In hello Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="c9a21-187">g.</span><span class="sxs-lookup"><span data-stu-id="c9a21-187">g.</span></span> <span data-ttu-id="c9a21-188">Haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="c9a21-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="c9a21-189">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c9a21-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c9a21-190">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c9a21-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c9a21-191">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c9a21-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c9a21-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9a21-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="c9a21-193">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c9a21-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c9a21-195">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9a21-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9a21-196">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c9a21-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9a21-198">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9a21-200">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9a21-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9a21-202">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c9a21-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9a21-204">a.</span><span class="sxs-lookup"><span data-stu-id="c9a21-204">a.</span></span> <span data-ttu-id="c9a21-205">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9a21-206">b.</span><span class="sxs-lookup"><span data-stu-id="c9a21-206">b.</span></span> <span data-ttu-id="c9a21-207">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c9a21-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c9a21-208">c.</span><span class="sxs-lookup"><span data-stu-id="c9a21-208">c.</span></span> <span data-ttu-id="c9a21-209">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c9a21-210">d.</span><span class="sxs-lookup"><span data-stu-id="c9a21-210">d.</span></span> <span data-ttu-id="c9a21-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="c9a21-212">Creación de un usuario de prueba para EverBridge</span><span class="sxs-lookup"><span data-stu-id="c9a21-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="c9a21-213">En esta sección, creará una usuaria llamada Britta Simon en Everbridge.</span><span class="sxs-lookup"><span data-stu-id="c9a21-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="c9a21-214">Trabajar con [equipo de soporte técnico de EverBridge](mailto:support@everbridge.com) a los usuarios de tooadd hello en la plataforma de Everbridge Hola.</span><span class="sxs-lookup"><span data-stu-id="c9a21-214">Work with [EverBridge support team](mailto:support@everbridge.com) tooadd hello users in hello Everbridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c9a21-215">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9a21-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c9a21-216">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooEverBridge.</span><span class="sxs-lookup"><span data-stu-id="c9a21-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEverBridge.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c9a21-218">**tooassign Britta Simon tooEverBridge, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9a21-218">**tooassign Britta Simon tooEverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9a21-219">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c9a21-221">En la lista de aplicaciones de hello, seleccione **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-221">In hello applications list, select **EverBridge**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="c9a21-223">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c9a21-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-225">Click **Add** button.</span></span> <span data-ttu-id="c9a21-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c9a21-228">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9a21-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c9a21-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9a21-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c9a21-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c9a21-231">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c9a21-231">Testing single sign-on</span></span>

<span data-ttu-id="c9a21-232">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c9a21-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c9a21-233">Al hacer clic en icono de Everbridge Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Everbridge aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9a21-233">When you click hello Everbridge tile in hello Access Panel, you should get automatically signed-on tooyour Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9a21-234">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c9a21-234">Additional resources</span></span>

* [<span data-ttu-id="c9a21-235">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9a21-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9a21-236">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c9a21-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

