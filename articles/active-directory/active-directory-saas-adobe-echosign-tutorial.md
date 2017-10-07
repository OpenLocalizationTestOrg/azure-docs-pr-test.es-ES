---
title: "Tutorial: Integración de Azure Active Directory con Adobe Sign | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el inicio de sesión de Adobe."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="dc00e-103">Tutorial: integración de Azure Active Directory con Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="dc00e-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="dc00e-104">En este tutorial, aprenderá cómo toointegrate Adobe iniciar sesión con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc00e-104">In this tutorial, you learn how toointegrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc00e-105">Integración de inicio de sesión de Adobe con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="dc00e-105">Integrating Adobe Sign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dc00e-106">Puede controlar en Azure AD que tenga acceso tooAdobe inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="dc00e-106">You can control in Azure AD who has access tooAdobe Sign</span></span>
- <span data-ttu-id="dc00e-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAdobe inicio de sesión (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc00e-107">You can enable your users tooautomatically get signed-on tooAdobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc00e-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="dc00e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dc00e-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dc00e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc00e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dc00e-110">Prerequisites</span></span>

<span data-ttu-id="dc00e-111">tooconfigure integración de Azure AD con inicio de sesión de Adobe, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="dc00e-111">tooconfigure Azure AD integration with Adobe Sign, you need hello following items:</span></span>

- <span data-ttu-id="dc00e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc00e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc00e-113">Una suscripción habilitada para el inicio de sesión único en Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="dc00e-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc00e-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="dc00e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc00e-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="dc00e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc00e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="dc00e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc00e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc00e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc00e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="dc00e-118">Scenario description</span></span>
<span data-ttu-id="dc00e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="dc00e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc00e-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="dc00e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc00e-121">Agregar el inicio de sesión de Adobe desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="dc00e-121">Adding Adobe Sign from hello gallery</span></span>
2. <span data-ttu-id="dc00e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc00e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-hello-gallery"></a><span data-ttu-id="dc00e-123">Agregar el inicio de sesión de Adobe desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="dc00e-123">Adding Adobe Sign from hello gallery</span></span>
<span data-ttu-id="dc00e-124">integración de hello tooconfigure de inicio de sesión de Adobe en Azure AD, deberá tooadd inicio de sesión de Adobe en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="dc00e-124">tooconfigure hello integration of Adobe Sign into Azure AD, you need tooadd Adobe Sign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dc00e-125">**tooadd inicio de sesión de Adobe desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="dc00e-125">**tooadd Adobe Sign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc00e-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="dc00e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dc00e-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dc00e-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="dc00e-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc00e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="dc00e-133">En el cuadro de búsqueda de hello, escriba **inicio de sesión de Adobe**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-133">In hello search box, type **Adobe Sign**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="dc00e-135">En el panel de resultados de hello, seleccione **inicio de sesión de Adobe**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dc00e-135">In hello results panel, select **Adobe Sign**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc00e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc00e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc00e-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Adobe Sign con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dc00e-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dc00e-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el inicio de sesión de Adobe es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc00e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Sign is tooa user in Azure AD.</span></span> <span data-ttu-id="dc00e-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el inicio de sesión de Adobe debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="dc00e-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Sign needs toobe established.</span></span>

<span data-ttu-id="dc00e-141">En el inicio de sesión de Adobe, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc00e-141">In Adobe Sign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dc00e-142">tooconfigure y prueba de inicio de sesión único en Azure AD con inicio de sesión de Adobe, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="dc00e-142">tooconfigure and test Azure AD single sign-on with Adobe Sign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dc00e-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="dc00e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dc00e-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc00e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc00e-145">**[Creación de un usuario de prueba de inicio de sesión de Adobe](#creating-an-adobe-sign-test-user)**  -toohave un equivalente de Britta Simon en Inicio de sesión de Adobe es representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="dc00e-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - toohave a counterpart of Britta Simon in Adobe Sign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc00e-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="dc00e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc00e-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="dc00e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc00e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc00e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc00e-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de inicio de sesión de Adobe.</span><span class="sxs-lookup"><span data-stu-id="dc00e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="dc00e-150">**inicio de sesión único en Azure AD tooconfigure con inicio de sesión de Adobe, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="dc00e-150">**tooconfigure Azure AD single sign-on with Adobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc00e-151">En el portal de Azure, en Hola Hola **inicio de sesión de Adobe** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-151">In hello Azure portal, on hello **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="dc00e-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="dc00e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="dc00e-155">En hello **direcciones URL y el dominio de inicio de sesión de Adobe** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="dc00e-155">On hello **Adobe Sign Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="dc00e-157">a.</span><span class="sxs-lookup"><span data-stu-id="dc00e-157">a.</span></span> <span data-ttu-id="dc00e-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="dc00e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="dc00e-159">b.</span><span class="sxs-lookup"><span data-stu-id="dc00e-159">b.</span></span> <span data-ttu-id="dc00e-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="dc00e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dc00e-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="dc00e-161">These values are not real.</span></span> <span data-ttu-id="dc00e-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="dc00e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dc00e-163">Póngase en contacto con [equipo de soporte técnico de cliente de inicio de sesión de Adobe](https://helpx.adobe.com/in/contact/support.html) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="dc00e-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="dc00e-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="dc00e-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="dc00e-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="dc00e-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dc00e-168">En hello **configuración de inicio de sesión de Adobe** sección, haga clic en **configurar inicio de sesión de Adobe** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="dc00e-168">On hello **Adobe Sign Configuration** section, click **Configure Adobe Sign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dc00e-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="dc00e-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="dc00e-171">En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de inicio de sesión de Adobe tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="dc00e-171">In a different web browser window, log in tooyour Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="dc00e-172">En el menú de hello en la parte superior de hello, haga clic en **cuenta**y, a continuación, en panel de navegación de hello en el lado izquierdo de hello, haga clic en **configuración SAML** en **configuración de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-172">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="dc00e-173">![Cuenta](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Cuenta")</span><span class="sxs-lookup"><span data-stu-id="dc00e-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="dc00e-174">En la sección Configuración de SAML de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="dc00e-174">In hello SAML Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="dc00e-175">![Configuración de SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="dc00e-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="dc00e-176">a.</span><span class="sxs-lookup"><span data-stu-id="dc00e-176">a.</span></span> <span data-ttu-id="dc00e-177">En **SAML Mode** (Modo de SAML), seleccione **SAML Mandatory** (SAML obligatorio).</span><span class="sxs-lookup"><span data-stu-id="dc00e-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="dc00e-178">b.</span><span class="sxs-lookup"><span data-stu-id="dc00e-178">b.</span></span> <span data-ttu-id="dc00e-179">Seleccione **toolog de permitir que los administradores de cuentas de EchoSign con las credenciales de EchoSign**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-179">Select **Allow EchoSign Account Administrators toolog in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="dc00e-180">c.</span><span class="sxs-lookup"><span data-stu-id="dc00e-180">c.</span></span> <span data-ttu-id="dc00e-181">En **User Creation** (Creación de usuario), seleccione **Automatically add users authenticated through SAML** (Agregar automáticamente usuarios autenticados a través de SAML).</span><span class="sxs-lookup"><span data-stu-id="dc00e-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="dc00e-182">Desplazarse, realizar Hola siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="dc00e-182">Move on, performing hello following steps:</span></span>

       <span data-ttu-id="dc00e-183">![Configuración de SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="dc00e-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="dc00e-184">a.</span><span class="sxs-lookup"><span data-stu-id="dc00e-184">a.</span></span> <span data-ttu-id="dc00e-185">Pegar **Id. de entidad SAML**, que han copiado desde el portal de Azure en hello **Id. de entidad IdP** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="dc00e-185">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="dc00e-186">b.</span><span class="sxs-lookup"><span data-stu-id="dc00e-186">b.</span></span> <span data-ttu-id="dc00e-187">Pegar **SAML Single Sign-On dirección URL del servicio**, que han copiado desde el portal de Azure en hello **dirección URL de inicio de sesión IdP** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="dc00e-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into hello **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="dc00e-188">c.</span><span class="sxs-lookup"><span data-stu-id="dc00e-188">c.</span></span> <span data-ttu-id="dc00e-189">Pegar **dirección URL de cierre de sesión**, que han copiado desde el portal de Azure en hello **IdP Logout URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="dc00e-189">Paste **Sign-Out URL**, which you have copied from Azure portal into hello **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="dc00e-190">d.</span><span class="sxs-lookup"><span data-stu-id="dc00e-190">d.</span></span> <span data-ttu-id="dc00e-191">Abra su descargado **Certificate(Base64)** un archivo en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado IdP** cuadro de texto</span><span class="sxs-lookup"><span data-stu-id="dc00e-191">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Certificate** textbox</span></span>

    <span data-ttu-id="dc00e-192">e.</span><span class="sxs-lookup"><span data-stu-id="dc00e-192">e.</span></span> <span data-ttu-id="dc00e-193">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="dc00e-194">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="dc00e-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dc00e-195">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="dc00e-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dc00e-196">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dc00e-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc00e-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc00e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc00e-198">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="dc00e-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="dc00e-200">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="dc00e-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc00e-201">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="dc00e-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dc00e-203">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dc00e-205">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc00e-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dc00e-207">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="dc00e-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc00e-209">a.</span><span class="sxs-lookup"><span data-stu-id="dc00e-209">a.</span></span> <span data-ttu-id="dc00e-210">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc00e-211">b.</span><span class="sxs-lookup"><span data-stu-id="dc00e-211">b.</span></span> <span data-ttu-id="dc00e-212">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dc00e-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc00e-213">c.</span><span class="sxs-lookup"><span data-stu-id="dc00e-213">c.</span></span> <span data-ttu-id="dc00e-214">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dc00e-215">d.</span><span class="sxs-lookup"><span data-stu-id="dc00e-215">d.</span></span> <span data-ttu-id="dc00e-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="dc00e-217">Creación de un usuario de prueba de Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="dc00e-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="dc00e-218">toolog de los usuarios de Azure AD tooenable en tooAdobe inicio de sesión, se les deben aprovisionar en Inicio de sesión de Adobe.</span><span class="sxs-lookup"><span data-stu-id="dc00e-218">tooenable Azure AD users toolog in tooAdobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="dc00e-219">En caso de hello de inicio de sesión de Adobe, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="dc00e-219">In hello case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="dc00e-220">Puede usar cualquier otro inicio de sesión de Adobe herramienta cuentas de usuario creación o las API proporcionadas por el inicio de sesión de Adobe tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="dc00e-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="dc00e-221">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="dc00e-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc00e-222">Inicie sesión en tooyour **inicio de sesión de Adobe** como administrador.</span><span class="sxs-lookup"><span data-stu-id="dc00e-222">Log in tooyour **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="dc00e-223">En el menú de hello en la parte superior de hello, haga clic en **cuenta**y, a continuación, en panel de navegación de hello en el lado izquierdo de hello, haga clic en **usuarios y grupos**y, a continuación, haga clic en **crear un nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-223">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="dc00e-224">![Cuenta](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Cuenta")</span><span class="sxs-lookup"><span data-stu-id="dc00e-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="dc00e-225">Hola **crear nuevo usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="dc00e-225">In hello **Create New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="dc00e-226">![Creación de usuarios](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="dc00e-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="dc00e-227">a.</span><span class="sxs-lookup"><span data-stu-id="dc00e-227">a.</span></span> <span data-ttu-id="dc00e-228">Hola de tipo **dirección de correo electrónico**, **nombre**, y **Last Name** de una cuenta válida de AAD que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="dc00e-228">Type hello **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="dc00e-229">b.</span><span class="sxs-lookup"><span data-stu-id="dc00e-229">b.</span></span> <span data-ttu-id="dc00e-230">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="dc00e-231">titular de la cuenta de Hello Azure Active Directory recibe un correo electrónico que incluye una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="dc00e-231">hello Azure Active Directory account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dc00e-232">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc00e-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dc00e-233">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAdobe inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="dc00e-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdobe Sign.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="dc00e-235">**tooassign Britta Simon tooAdobe inicio de sesión, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="dc00e-235">**tooassign Britta Simon tooAdobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc00e-236">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="dc00e-238">En la lista de aplicaciones de hello, seleccione **inicio de sesión de Adobe**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-238">In hello applications list, select **Adobe Sign**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="dc00e-240">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="dc00e-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-242">Click **Add** button.</span></span> <span data-ttu-id="dc00e-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="dc00e-245">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc00e-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dc00e-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc00e-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dc00e-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc00e-248">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="dc00e-248">Testing single sign-on</span></span>

<span data-ttu-id="dc00e-249">Al hacer clic en hello Adobe signo disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación de inicio de sesión de Adobe.</span><span class="sxs-lookup"><span data-stu-id="dc00e-249">When you click hello Adobe Sign tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Sign application.</span></span>
<span data-ttu-id="dc00e-250">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dc00e-250">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc00e-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="dc00e-251">Additional resources</span></span>

* [<span data-ttu-id="dc00e-252">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc00e-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc00e-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc00e-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

