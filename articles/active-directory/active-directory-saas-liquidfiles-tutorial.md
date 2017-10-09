---
title: "Tutorial: Integración de Azure Active Directory con LiquidFiles | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y LiquidFiles."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 67eb888090f81e0ceb791ed45d564b98fe1eb6d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="20d19-103">Tutorial: Integración de Azure Active Directory con LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="20d19-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="20d19-104">En este tutorial, aprenderá cómo toointegrate LiquidFiles con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="20d19-104">In this tutorial, you learn how toointegrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="20d19-105">Integración LiquidFiles con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="20d19-105">Integrating LiquidFiles with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="20d19-106">Puede controlar en Azure AD que tenga acceso tooLiquidFiles</span><span class="sxs-lookup"><span data-stu-id="20d19-106">You can control in Azure AD who has access tooLiquidFiles</span></span>
- <span data-ttu-id="20d19-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLiquidFiles (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="20d19-107">You can enable your users tooautomatically get signed-on tooLiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="20d19-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="20d19-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="20d19-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="20d19-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20d19-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="20d19-110">Prerequisites</span></span>

<span data-ttu-id="20d19-111">integración de Azure AD con LiquidFiles tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="20d19-111">tooconfigure Azure AD integration with LiquidFiles, you need hello following items:</span></span>

- <span data-ttu-id="20d19-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="20d19-112">An Azure AD subscription</span></span>
- <span data-ttu-id="20d19-113">Una suscripción habilitada para el inicio de sesión único en LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="20d19-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="20d19-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="20d19-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="20d19-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="20d19-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="20d19-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="20d19-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="20d19-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="20d19-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="20d19-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="20d19-118">Scenario description</span></span>
<span data-ttu-id="20d19-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="20d19-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="20d19-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="20d19-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="20d19-121">Agregar LiquidFiles desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="20d19-121">Adding LiquidFiles from hello gallery</span></span>
2. <span data-ttu-id="20d19-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="20d19-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-hello-gallery"></a><span data-ttu-id="20d19-123">Agregar LiquidFiles desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="20d19-123">Adding LiquidFiles from hello gallery</span></span>
<span data-ttu-id="20d19-124">integración de hello tooconfigure de LiquidFiles en Azure AD, deberá tooadd LiquidFiles de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="20d19-124">tooconfigure hello integration of LiquidFiles into Azure AD, you need tooadd LiquidFiles from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="20d19-125">**tooadd LiquidFiles de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="20d19-125">**tooadd LiquidFiles from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="20d19-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="20d19-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="20d19-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="20d19-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="20d19-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="20d19-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="20d19-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="20d19-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="20d19-133">En el cuadro de búsqueda de hello, escriba **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="20d19-133">In hello search box, type **LiquidFiles**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="20d19-135">En el panel de resultados de hello, seleccione **LiquidFiles**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="20d19-135">In hello results panel, select **LiquidFiles**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="20d19-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="20d19-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="20d19-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con LiquidFiles con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="20d19-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="20d19-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en LiquidFiles es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20d19-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LiquidFiles is tooa user in Azure AD.</span></span> <span data-ttu-id="20d19-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en LiquidFiles debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="20d19-140">In other words, a link relationship between an Azure AD user and hello related user in LiquidFiles needs toobe established.</span></span>

<span data-ttu-id="20d19-141">En LiquidFiles, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="20d19-141">In LiquidFiles, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="20d19-142">tooconfigure y prueba de inicio de sesión único en Azure AD con LiquidFiles, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="20d19-142">tooconfigure and test Azure AD single sign-on with LiquidFiles, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="20d19-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="20d19-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="20d19-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="20d19-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="20d19-145">**[Crear un usuario de prueba LiquidFiles](#creating-a-liquidfiles-test-user)**  -toohave un equivalente de Britta Simon en LiquidFiles que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="20d19-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - toohave a counterpart of Britta Simon in LiquidFiles that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="20d19-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="20d19-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="20d19-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="20d19-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="20d19-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="20d19-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="20d19-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="20d19-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="20d19-150">**inicio de sesión único en Azure AD tooconfigure con LiquidFiles, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="20d19-150">**tooconfigure Azure AD single sign-on with LiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="20d19-151">En el portal de Azure, en Hola Hola **LiquidFiles** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="20d19-151">In hello Azure portal, on hello **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="20d19-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="20d19-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="20d19-155">En hello **LiquidFiles dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="20d19-155">On hello **LiquidFiles Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="20d19-157">a.</span><span class="sxs-lookup"><span data-stu-id="20d19-157">a.</span></span> <span data-ttu-id="20d19-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="20d19-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="20d19-159">b.</span><span class="sxs-lookup"><span data-stu-id="20d19-159">b.</span></span> <span data-ttu-id="20d19-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="20d19-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="20d19-161">c.</span><span class="sxs-lookup"><span data-stu-id="20d19-161">c.</span></span> <span data-ttu-id="20d19-162">b.</span><span class="sxs-lookup"><span data-stu-id="20d19-162">b.</span></span> <span data-ttu-id="20d19-163">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="20d19-163">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="20d19-164">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="20d19-164">These values are not real.</span></span> <span data-ttu-id="20d19-165">Actualización de estos valores con Hola URL de inicio de sesión real, identificador y dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="20d19-165">Update these values with hello actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="20d19-166">Póngase en contacto con [equipo de soporte técnico de cliente de LiquidFiles](https://www.liquidfiles.com/support.html) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="20d19-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="20d19-167">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="20d19-167">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="20d19-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="20d19-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="20d19-171">En hello **LiquidFiles configuración** sección, haga clic en **configurar LiquidFiles** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="20d19-171">On hello **LiquidFiles Configuration** section, click **Configure LiquidFiles** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="20d19-172">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="20d19-172">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="20d19-174">Sitio de empresa de LiquidFiles tooyour de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="20d19-174">Sign-on tooyour LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="20d19-175">Haga clic en **Single Sign-On** en hello **Administración > configuración** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="20d19-175">Click **Single Sign-On** in hello **Admin > Configuration** from hello menu.</span></span>

9. <span data-ttu-id="20d19-176">En hello **configuración de inicio de sesión único** , siga los pasos de Hola</span><span class="sxs-lookup"><span data-stu-id="20d19-176">On hello **Single Sign-On Configuration** page, perform hello following steps</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="20d19-178">a.</span><span class="sxs-lookup"><span data-stu-id="20d19-178">a.</span></span> <span data-ttu-id="20d19-179">Como **método de inicio de sesión único**, seleccione **SAML 2**.</span><span class="sxs-lookup"><span data-stu-id="20d19-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="20d19-180">b.</span><span class="sxs-lookup"><span data-stu-id="20d19-180">b.</span></span> <span data-ttu-id="20d19-181">Hola **dirección URL de inicio de sesión IDP** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="20d19-181">In hello **IDP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="20d19-182">c.</span><span class="sxs-lookup"><span data-stu-id="20d19-182">c.</span></span> <span data-ttu-id="20d19-183">Hola **IDP Logout URL** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="20d19-183">In hello **IDP Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="20d19-184">d.</span><span class="sxs-lookup"><span data-stu-id="20d19-184">d.</span></span> <span data-ttu-id="20d19-185">Hola **IDP Cert Fingerprint** cuadro de texto, pegue hello **huella digital** valor que haya copiado desde el portal de Azure...</span><span class="sxs-lookup"><span data-stu-id="20d19-185">In hello **IDP Cert Fingerprint** textbox, paste hello **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="20d19-186">e.</span><span class="sxs-lookup"><span data-stu-id="20d19-186">e.</span></span> <span data-ttu-id="20d19-187">En el cuadro de texto de formato de identificador de nombre de hello, escriba el valor de hello **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="20d19-187">In hello Name Identifier Format textbox, type hello value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="20d19-188">f.</span><span class="sxs-lookup"><span data-stu-id="20d19-188">f.</span></span> <span data-ttu-id="20d19-189">Hola cuadro de texto de contexto de autenticación, escriba el valor de hello **urn: oasis: nombres: tc: SAML:2.0:ac:classes:PasswordProtectedTransport**.</span><span class="sxs-lookup"><span data-stu-id="20d19-189">In hello Authn Context textbox, type hello value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="20d19-190">g.</span><span class="sxs-lookup"><span data-stu-id="20d19-190">g.</span></span> <span data-ttu-id="20d19-191">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="20d19-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="20d19-192">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="20d19-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="20d19-193">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="20d19-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="20d19-194">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="20d19-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="20d19-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="20d19-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="20d19-196">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="20d19-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="20d19-198">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="20d19-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="20d19-199">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="20d19-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="20d19-201">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="20d19-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="20d19-203">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="20d19-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="20d19-205">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="20d19-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="20d19-207">a.</span><span class="sxs-lookup"><span data-stu-id="20d19-207">a.</span></span> <span data-ttu-id="20d19-208">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="20d19-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="20d19-209">b.</span><span class="sxs-lookup"><span data-stu-id="20d19-209">b.</span></span> <span data-ttu-id="20d19-210">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="20d19-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="20d19-211">c.</span><span class="sxs-lookup"><span data-stu-id="20d19-211">c.</span></span> <span data-ttu-id="20d19-212">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="20d19-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="20d19-213">d.</span><span class="sxs-lookup"><span data-stu-id="20d19-213">d.</span></span> <span data-ttu-id="20d19-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="20d19-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="20d19-215">Creación de un usuario de prueba de LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="20d19-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="20d19-216">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en LiquidFiles toocreate.</span><span class="sxs-lookup"><span data-stu-id="20d19-216">hello objective of this section is toocreate a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="20d19-217">Trabajar con su tooget de administrador del servidor de LiquidFiles usted mismo agrega como un usuario antes de iniciar sesión tooyour LiquidFiles aplicación.</span><span class="sxs-lookup"><span data-stu-id="20d19-217">Work with your LiquidFiles server administrator tooget yourself added as a user before logging in tooyour LiquidFiles application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="20d19-218">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="20d19-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="20d19-219">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="20d19-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLiquidFiles.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="20d19-221">**tooassign Britta Simon tooLiquidFiles, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="20d19-221">**tooassign Britta Simon tooLiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="20d19-222">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="20d19-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="20d19-224">En la lista de aplicaciones de hello, seleccione **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="20d19-224">In hello applications list, select **LiquidFiles**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="20d19-226">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="20d19-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="20d19-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="20d19-228">Click **Add** button.</span></span> <span data-ttu-id="20d19-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="20d19-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="20d19-231">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="20d19-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="20d19-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="20d19-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="20d19-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="20d19-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="20d19-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="20d19-234">Testing single sign-on</span></span>

<span data-ttu-id="20d19-235">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="20d19-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="20d19-236">Al hacer clic en hello LiquidFiles el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour LiquidFiles aplicación.</span><span class="sxs-lookup"><span data-stu-id="20d19-236">When you click hello LiquidFiles tile in hello Access Panel, you should get automatically signed-on tooyour LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="20d19-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="20d19-237">Additional resources</span></span>

* [<span data-ttu-id="20d19-238">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="20d19-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="20d19-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="20d19-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png

