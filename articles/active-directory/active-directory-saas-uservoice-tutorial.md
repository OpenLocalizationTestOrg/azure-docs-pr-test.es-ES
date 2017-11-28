---
title: "Tutorial: Integración de Azure Active Directory con UserVoice | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="c3841-103">Tutorial: Integración de Azure Active Directory con UserVoice</span><span class="sxs-lookup"><span data-stu-id="c3841-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="c3841-104">En este tutorial, aprenderá cómo toointegrate UserVoice con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3841-104">In this tutorial, you learn how toointegrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3841-105">Integración UserVoice con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c3841-105">Integrating UserVoice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c3841-106">Puede controlar en Azure AD que tenga acceso tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="c3841-106">You can control in Azure AD who has access tooUserVoice.</span></span>
- <span data-ttu-id="c3841-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooUserVoice (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3841-107">You can enable your users tooautomatically get signed-on tooUserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c3841-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3841-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c3841-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3841-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3841-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c3841-110">Prerequisites</span></span>

<span data-ttu-id="c3841-111">integración de Azure AD con UserVoice tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c3841-111">tooconfigure Azure AD integration with UserVoice, you need hello following items:</span></span>

- <span data-ttu-id="c3841-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3841-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3841-113">Una suscripción habilitada para el inicio de sesión único en UserVoice</span><span class="sxs-lookup"><span data-stu-id="c3841-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3841-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c3841-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3841-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c3841-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3841-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c3841-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3841-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3841-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3841-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c3841-118">Scenario description</span></span>
<span data-ttu-id="c3841-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c3841-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3841-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c3841-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3841-121">Agregar UserVoice desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c3841-121">Adding UserVoice from hello gallery</span></span>
2. <span data-ttu-id="c3841-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3841-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-hello-gallery"></a><span data-ttu-id="c3841-123">Agregar UserVoice desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c3841-123">Adding UserVoice from hello gallery</span></span>
<span data-ttu-id="c3841-124">integración de hello tooconfigure de UserVoice en Azure AD, deberá tooadd UserVoice de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c3841-124">tooconfigure hello integration of UserVoice into Azure AD, you need tooadd UserVoice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c3841-125">**tooadd UserVoice de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c3841-125">**tooadd UserVoice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3841-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c3841-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="c3841-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c3841-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c3841-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c3841-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="c3841-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c3841-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="c3841-133">En el cuadro de búsqueda de hello, escriba **UserVoice**, seleccione **UserVoice** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c3841-133">In hello search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de UserVoice en hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c3841-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3841-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c3841-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con UserVoice con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c3841-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c3841-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en UserVoice es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3841-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserVoice is tooa user in Azure AD.</span></span> <span data-ttu-id="c3841-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en UserVoice debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c3841-138">In other words, a link relationship between an Azure AD user and hello related user in UserVoice needs toobe established.</span></span>

<span data-ttu-id="c3841-139">En UserVoice, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3841-139">In UserVoice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c3841-140">tooconfigure y prueba de inicio de sesión único en Azure AD con UserVoice, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c3841-140">tooconfigure and test Azure AD single sign-on with UserVoice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c3841-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c3841-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c3841-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3841-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3841-143">**[Crear un usuario de prueba de UserVoice](#create-a-uservoice-test-user)**  -toohave un equivalente de Britta Simon en UserVoice que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c3841-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - toohave a counterpart of Britta Simon in UserVoice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3841-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c3841-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3841-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c3841-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c3841-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3841-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c3841-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de UserVoice.</span><span class="sxs-lookup"><span data-stu-id="c3841-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="c3841-148">**inicio de sesión único en Azure AD tooconfigure con UserVoice, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c3841-148">**tooconfigure Azure AD single sign-on with UserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3841-149">En el portal de Azure, en Hola Hola **UserVoice** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c3841-149">In hello Azure portal, on hello **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="c3841-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c3841-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="c3841-153">En hello **UserVoice dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c3841-153">On hello **UserVoice Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="c3841-155">a.</span><span class="sxs-lookup"><span data-stu-id="c3841-155">a.</span></span> <span data-ttu-id="c3841-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="c3841-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="c3841-157">b.</span><span class="sxs-lookup"><span data-stu-id="c3841-157">b.</span></span> <span data-ttu-id="c3841-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="c3841-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c3841-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c3841-159">These values are not real.</span></span> <span data-ttu-id="c3841-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="c3841-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c3841-161">Póngase en contacto con [equipo de soporte técnico de cliente de UserVoice](https://www.uservoice.com/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="c3841-161">Contact [UserVoice Client support team](https://www.uservoice.com/) tooget these values.</span></span>

4. <span data-ttu-id="c3841-162">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="c3841-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="c3841-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c3841-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c3841-166">En hello **configuración de UserVoice** sección, haga clic en **configurar UserVoice** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="c3841-166">On hello **UserVoice Configuration** section, click **Configure UserVoice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c3841-167">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="c3841-167">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="c3841-169">En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía UserVoice tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="c3841-169">In a different web browser window, log in tooyour UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="c3841-170">En la barra de herramientas de hello en la parte superior de hello, haga clic en **configuración**y, a continuación, seleccione **portal Web** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3841-170">In hello toolbar on hello top, click **Settings**, and then select **Web portal** from hello menu.</span></span>
   
    <span data-ttu-id="c3841-171">![Sección Configuración en la aplicación](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="c3841-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="c3841-172">En hello **portal Web** ficha Hola **autenticación de usuario** sección, haga clic en **editar** tooopen hello **Editar autenticación de usuario** cuadro de diálogo página.</span><span class="sxs-lookup"><span data-stu-id="c3841-172">On hello **Web portal** tab, in hello **User authentication** section, click **Edit** tooopen hello **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="c3841-173">![Pestaña Portal web](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span><span class="sxs-lookup"><span data-stu-id="c3841-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="c3841-174">En hello **Editar autenticación de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c3841-174">On hello **Edit User Authentication** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="c3841-175">![Editar autenticación de usuario](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Editar autenticación de usuario")</span><span class="sxs-lookup"><span data-stu-id="c3841-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="c3841-176">a.</span><span class="sxs-lookup"><span data-stu-id="c3841-176">a.</span></span> <span data-ttu-id="c3841-177">Haga clic en **Inicio de sesión único (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="c3841-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="c3841-178">b.</span><span class="sxs-lookup"><span data-stu-id="c3841-178">b.</span></span> <span data-ttu-id="c3841-179">Hola pegar **SAML Single Sign-On dirección URL del servicio** valor, que haya copiado desde Hola portal de Azure en hello **inicio de sesión remoto en SSO** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c3841-179">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="c3841-180">c.</span><span class="sxs-lookup"><span data-stu-id="c3841-180">c.</span></span> <span data-ttu-id="c3841-181">Hola pegar **dirección URL de cierre de sesión** valor, que haya copiado desde Hola portal de Azure en hello **cuadro de texto de cierre de sesión remoto SSO**.</span><span class="sxs-lookup"><span data-stu-id="c3841-181">Paste hello **Sign-Out URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="c3841-182">d.</span><span class="sxs-lookup"><span data-stu-id="c3841-182">d.</span></span> <span data-ttu-id="c3841-183">Hola pegar **huella digital** valor, que haya copiado desde el portal de Azure en la **huella digital de certificado SHA1 actual** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c3841-183">Paste hello **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="c3841-184">e.</span><span class="sxs-lookup"><span data-stu-id="c3841-184">e.</span></span> <span data-ttu-id="c3841-185">Haga clic en **Guardar configuración de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="c3841-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="c3841-186">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c3841-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c3841-187">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c3841-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c3841-188">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c3841-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c3841-189">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3841-189">Create an Azure AD test user</span></span>

<span data-ttu-id="c3841-190">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c3841-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="c3841-192">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c3841-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3841-193">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="c3841-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c3841-195">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c3841-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c3841-197">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c3841-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c3841-199">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c3841-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c3841-201">a.</span><span class="sxs-lookup"><span data-stu-id="c3841-201">a.</span></span> <span data-ttu-id="c3841-202">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3841-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3841-203">b.</span><span class="sxs-lookup"><span data-stu-id="c3841-203">b.</span></span> <span data-ttu-id="c3841-204">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3841-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c3841-205">c.</span><span class="sxs-lookup"><span data-stu-id="c3841-205">c.</span></span> <span data-ttu-id="c3841-206">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="c3841-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c3841-207">d.</span><span class="sxs-lookup"><span data-stu-id="c3841-207">d.</span></span> <span data-ttu-id="c3841-208">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c3841-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="c3841-209">Creación de un usuario de prueba de UserVoice</span><span class="sxs-lookup"><span data-stu-id="c3841-209">Create a UserVoice test user</span></span>

<span data-ttu-id="c3841-210">toolog de los usuarios de Azure AD tooenable en tooUserVoice, se les deben aprovisionar en UserVoice.</span><span class="sxs-lookup"><span data-stu-id="c3841-210">tooenable Azure AD users toolog in tooUserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="c3841-211">En caso de hello de UserVoice, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="c3841-211">In hello case of UserVoice, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="c3841-212">tooprovision una cuenta de usuario, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c3841-212">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="c3841-213">Inicie sesión en tooyour **UserVoice** inquilino.</span><span class="sxs-lookup"><span data-stu-id="c3841-213">Log in tooyour **UserVoice** tenant.</span></span>

2. <span data-ttu-id="c3841-214">Vaya demasiado**configuración**.</span><span class="sxs-lookup"><span data-stu-id="c3841-214">Go too**Settings**.</span></span>
   
    <span data-ttu-id="c3841-215">![Configuración](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="c3841-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="c3841-216">Haga clic en **General**.</span><span class="sxs-lookup"><span data-stu-id="c3841-216">Click **General**.</span></span>

4. <span data-ttu-id="c3841-217">Haga clic en **Agentes y permisos**.</span><span class="sxs-lookup"><span data-stu-id="c3841-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="c3841-218">![Agentes y permisos](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agentes y permisos")</span><span class="sxs-lookup"><span data-stu-id="c3841-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="c3841-219">Haga clic en **Agregar administradores**.</span><span class="sxs-lookup"><span data-stu-id="c3841-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="c3841-220">![Agregar administradores](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Agregar administradores")</span><span class="sxs-lookup"><span data-stu-id="c3841-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="c3841-221">En hello **invitar a administradores** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c3841-221">On hello **Invite admins** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="c3841-222">![Invitar a administradores](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invitar a administradores")</span><span class="sxs-lookup"><span data-stu-id="c3841-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="c3841-223">a.</span><span class="sxs-lookup"><span data-stu-id="c3841-223">a.</span></span> <span data-ttu-id="c3841-224">En el cuadro de texto de los correos electrónicos de hello, escriba la dirección de correo electrónico de Hola de cuenta de hello que desee tooprovision y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="c3841-224">In hello Emails textbox, type hello email address of hello account you want tooprovision, and then click **Add**.</span></span>
   
    <span data-ttu-id="c3841-225">b.</span><span class="sxs-lookup"><span data-stu-id="c3841-225">b.</span></span> <span data-ttu-id="c3841-226">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="c3841-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="c3841-227">Puede usar cualquier otra UserVoice usuario cuenta herramienta de creación o las API proporcionadas por UserVoice tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="c3841-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice tooprovision AAD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c3841-228">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3841-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c3841-229">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="c3841-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserVoice.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="c3841-231">**tooassign Britta Simon tooUserVoice, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c3841-231">**tooassign Britta Simon tooUserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3841-232">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c3841-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c3841-234">En la lista de aplicaciones de hello, seleccione **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="c3841-234">In hello applications list, select **UserVoice**.</span></span>

    ![vínculo de UserVoice de Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="c3841-236">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c3841-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="c3841-238">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c3841-238">Click **Add** button.</span></span> <span data-ttu-id="c3841-239">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c3841-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="c3841-241">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3841-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c3841-242">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c3841-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3841-243">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c3841-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c3841-244">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="c3841-244">Test single sign-on</span></span>

<span data-ttu-id="c3841-245">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c3841-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c3841-246">Al hacer clic en icono de UserVoice Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour UserVoice aplicación.</span><span class="sxs-lookup"><span data-stu-id="c3841-246">When you click hello UserVoice tile in hello Access Panel, you should get automatically signed-on tooyour UserVoice application.</span></span>
<span data-ttu-id="c3841-247">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c3841-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c3841-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c3841-248">Additional resources</span></span>

* [<span data-ttu-id="c3841-249">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3841-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3841-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c3841-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

