---
title: "Tutorial: Integración de Azure Active Directory con LCVista | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y LCVista."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="9df76-103">Tutorial: Integración de Azure Active Directory con LCVista</span><span class="sxs-lookup"><span data-stu-id="9df76-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="9df76-104">En este tutorial, aprenderá cómo toointegrate LCVista con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9df76-104">In this tutorial, you learn how toointegrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9df76-105">Integración LCVista con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9df76-105">Integrating LCVista with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9df76-106">Puede controlar en Azure AD que tenga acceso tooLCVista</span><span class="sxs-lookup"><span data-stu-id="9df76-106">You can control in Azure AD who has access tooLCVista</span></span>
- <span data-ttu-id="9df76-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLCVista (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9df76-107">You can enable your users tooautomatically get signed-on tooLCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9df76-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9df76-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9df76-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9df76-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9df76-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9df76-110">Prerequisites</span></span>

<span data-ttu-id="9df76-111">integración de Azure AD con LCVista tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9df76-111">tooconfigure Azure AD integration with LCVista, you need hello following items:</span></span>

- <span data-ttu-id="9df76-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9df76-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9df76-113">Una suscripción habilitada para el inicio de sesión único en LCVista</span><span class="sxs-lookup"><span data-stu-id="9df76-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9df76-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9df76-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9df76-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9df76-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9df76-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9df76-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9df76-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9df76-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9df76-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9df76-118">Scenario description</span></span>
<span data-ttu-id="9df76-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9df76-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9df76-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9df76-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9df76-121">Agregar LCVista desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9df76-121">Adding LCVista from hello gallery</span></span>
2. <span data-ttu-id="9df76-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9df76-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-hello-gallery"></a><span data-ttu-id="9df76-123">Agregar LCVista desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9df76-123">Adding LCVista from hello gallery</span></span>
<span data-ttu-id="9df76-124">integración de hello tooconfigure de LCVista en Azure AD, deberá tooadd LCVista de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9df76-124">tooconfigure hello integration of LCVista into Azure AD, you need tooadd LCVista from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9df76-125">**tooadd LCVista de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9df76-125">**tooadd LCVista from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9df76-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9df76-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9df76-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9df76-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9df76-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9df76-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9df76-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9df76-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9df76-133">En el cuadro de búsqueda de hello, escriba **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="9df76-133">In hello search box, type **LCVista**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="9df76-135">En el panel de resultados de hello, seleccione **LCVista**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9df76-135">In hello results panel, select **LCVista**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9df76-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9df76-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9df76-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con LCVista con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9df76-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9df76-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en LCVista es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9df76-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LCVista is tooa user in Azure AD.</span></span> <span data-ttu-id="9df76-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en LCVista debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9df76-140">In other words, a link relationship between an Azure AD user and hello related user in LCVista needs toobe established.</span></span>

<span data-ttu-id="9df76-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en LCVista.</span><span class="sxs-lookup"><span data-stu-id="9df76-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LCVista.</span></span>

<span data-ttu-id="9df76-142">tooconfigure y prueba de inicio de sesión único en Azure AD con LCVista, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9df76-142">tooconfigure and test Azure AD single sign-on with LCVista, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9df76-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9df76-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9df76-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9df76-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9df76-145">**[Crear un usuario de prueba LCVista](#creating-a-lcvista-test-user)**  -toohave un equivalente de Britta Simon en LCVista que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9df76-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - toohave a counterpart of Britta Simon in LCVista that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9df76-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9df76-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9df76-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9df76-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9df76-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9df76-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9df76-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación LCVista.</span><span class="sxs-lookup"><span data-stu-id="9df76-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="9df76-150">**inicio de sesión único en Azure AD tooconfigure con LCVista, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9df76-150">**tooconfigure Azure AD single sign-on with LCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="9df76-151">En el portal de Azure, en Hola Hola **LCVista** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9df76-151">In hello Azure portal, on hello **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9df76-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9df76-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="9df76-155">En hello **LCVista dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9df76-155">On hello **LCVista Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="9df76-157">a.</span><span class="sxs-lookup"><span data-stu-id="9df76-157">a.</span></span> <span data-ttu-id="9df76-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="9df76-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="9df76-159">b.</span><span class="sxs-lookup"><span data-stu-id="9df76-159">b.</span></span> <span data-ttu-id="9df76-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="9df76-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="9df76-161">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="9df76-161">These values are not hello real.</span></span> <span data-ttu-id="9df76-162">Actualizar estos valores con hello real identificador y la dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9df76-162">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="9df76-163">Póngase en contacto con [equipo de soporte técnico de cliente de LCVista](https://lcvista.com/contact) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="9df76-163">Contact [LCVista Client support team](https://lcvista.com/contact) tooget these values.</span></span> 

4. <span data-ttu-id="9df76-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9df76-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="9df76-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9df76-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="9df76-168">En hello **LCVista configuración** sección, haga clic en **configurar LCVista** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="9df76-168">On hello **LCVista Configuration** section, click **Configure LCVista** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9df76-169">Hola copia **Id. de entidad SAML** y **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="9df76-169">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="9df76-171">Inicie sesión en tooyour LCVista aplicación como administrador.</span><span class="sxs-lookup"><span data-stu-id="9df76-171">Sign on tooyour LCVista application as an administrator.</span></span>

8. <span data-ttu-id="9df76-172">Hola **configuración de SAML** sección, compruebe hello **inicio de sesión SAML habilitar** y escriba los detalles de hello como se mencionó en por debajo de la imagen.</span><span class="sxs-lookup"><span data-stu-id="9df76-172">In hello **SAML Config** section, check hello **Enable SAML login** and enter hello details as mentioned in below image.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="9df76-174">a.</span><span class="sxs-lookup"><span data-stu-id="9df76-174">a.</span></span> <span data-ttu-id="9df76-175">Hola pegar **dirección URL del emisor** que haya copiado desde Azure AD en hello **Id. de entidad** sección.</span><span class="sxs-lookup"><span data-stu-id="9df76-175">Paste hello **Issuer URL** which you have copied from Azure AD in hello **Entity ID** section.</span></span> 

    <span data-ttu-id="9df76-176">b.</span><span class="sxs-lookup"><span data-stu-id="9df76-176">b.</span></span> <span data-ttu-id="9df76-177">Hola pegar **URL de servicio de inicio de sesión único** que haya copiado desde Azure AD en hello **URL** sección.</span><span class="sxs-lookup"><span data-stu-id="9df76-177">Paste hello **Single Sign-On Service URL** which you have copied from Azure AD in hello **URL** section.</span></span>

    <span data-ttu-id="9df76-178">c.</span><span class="sxs-lookup"><span data-stu-id="9df76-178">c.</span></span> <span data-ttu-id="9df76-179">De metadatos (XML) que ha descargado desde el portal de Azure, copie el valor de hello **X509Certificate** y péguelo en hello **x509 certificado** sección.</span><span class="sxs-lookup"><span data-stu-id="9df76-179">From Metadata (XML) which you have downloaded from Azure portal, copy hello value **X509Certificate** and paste it in hello **x509 Certificate** section.</span></span>

    <span data-ttu-id="9df76-180">d.</span><span class="sxs-lookup"><span data-stu-id="9df76-180">d.</span></span> <span data-ttu-id="9df76-181">Hola **atributo de nombre** cuadro de texto, pegue Hola valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="9df76-181">In hello **First name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="9df76-182">e.</span><span class="sxs-lookup"><span data-stu-id="9df76-182">e.</span></span> <span data-ttu-id="9df76-183">Hola **último atributo de nombre** cuadro de texto, pegue Hola valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="9df76-183">In hello **Last name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="9df76-184">f.</span><span class="sxs-lookup"><span data-stu-id="9df76-184">f.</span></span> <span data-ttu-id="9df76-185">Hola **atributo de correo electrónico** cuadro de texto, pegue Hola valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="9df76-185">In hello **Email attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="9df76-186">g.</span><span class="sxs-lookup"><span data-stu-id="9df76-186">g.</span></span> <span data-ttu-id="9df76-187">Hola **atributo Username** cuadro de texto, pegue Hola valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="9df76-187">In hello **Username attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="9df76-188">e.</span><span class="sxs-lookup"><span data-stu-id="9df76-188">e.</span></span> <span data-ttu-id="9df76-189">Haga clic en **guardar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="9df76-189">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="9df76-190">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9df76-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9df76-191">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9df76-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9df76-192">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9df76-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9df76-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9df76-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="9df76-194">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9df76-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9df76-196">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9df76-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9df76-197">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9df76-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9df76-199">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9df76-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9df76-201">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9df76-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9df76-203">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9df76-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9df76-205">a.</span><span class="sxs-lookup"><span data-stu-id="9df76-205">a.</span></span> <span data-ttu-id="9df76-206">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9df76-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9df76-207">b.</span><span class="sxs-lookup"><span data-stu-id="9df76-207">b.</span></span> <span data-ttu-id="9df76-208">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9df76-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9df76-209">c.</span><span class="sxs-lookup"><span data-stu-id="9df76-209">c.</span></span> <span data-ttu-id="9df76-210">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9df76-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9df76-211">d.</span><span class="sxs-lookup"><span data-stu-id="9df76-211">d.</span></span> <span data-ttu-id="9df76-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9df76-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="9df76-213">Creación de un usuario de prueba de LCVista</span><span class="sxs-lookup"><span data-stu-id="9df76-213">Creating a LCVista test user</span></span>

<span data-ttu-id="9df76-214">En esta sección, creará un usuario llamado Britta Simon en LCVista.</span><span class="sxs-lookup"><span data-stu-id="9df76-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="9df76-215">Necesita toocontact [equipo de soporte técnico de LCVista cliente](https://lcvista.com/contact) a los usuarios de tooadd Hola Hola LCVista aplicación.</span><span class="sxs-lookup"><span data-stu-id="9df76-215">You need toocontact [LCVista Client support team](https://lcvista.com/contact) tooadd hello users in hello LCVista application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9df76-216">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9df76-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9df76-217">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLCVista.</span><span class="sxs-lookup"><span data-stu-id="9df76-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLCVista.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9df76-219">**tooassign Britta Simon tooLCVista, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9df76-219">**tooassign Britta Simon tooLCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="9df76-220">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9df76-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9df76-222">En la lista de aplicaciones de hello, seleccione **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="9df76-222">In hello applications list, select **LCVista**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="9df76-224">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9df76-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9df76-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9df76-226">Click **Add** button.</span></span> <span data-ttu-id="9df76-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9df76-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9df76-229">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9df76-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9df76-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9df76-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9df76-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9df76-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9df76-232">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9df76-232">Testing single sign-on</span></span>

<span data-ttu-id="9df76-233">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9df76-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="9df76-234">Haga clic en el icono de LCVista Hola Hola Panel de acceso, será redirigido tooOrganization inicio de sesión en la página.</span><span class="sxs-lookup"><span data-stu-id="9df76-234">Click hello LCVista tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="9df76-235">Después de iniciar sesión correctamente, podrás ha iniciado sesión tooyour LCVista aplicación.</span><span class="sxs-lookup"><span data-stu-id="9df76-235">After successful login, you will be signed-on tooyour LCVista application.</span></span> <span data-ttu-id="9df76-236">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9df76-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9df76-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9df76-237">Additional resources</span></span>

* [<span data-ttu-id="9df76-238">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9df76-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9df76-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9df76-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

