---
title: "Tutorial: Integración de Azure Active Directory con Intralinks | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="03d56-103">Tutorial: integración de Azure Active Directory con Intralinks</span><span class="sxs-lookup"><span data-stu-id="03d56-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="03d56-104">En este tutorial, aprenderá cómo toointegrate Intralinks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="03d56-104">In this tutorial, you learn how toointegrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="03d56-105">Integración Intralinks con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="03d56-105">Integrating Intralinks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="03d56-106">Puede controlar en Azure AD que tenga acceso tooIntralinks</span><span class="sxs-lookup"><span data-stu-id="03d56-106">You can control in Azure AD who has access tooIntralinks</span></span>
- <span data-ttu-id="03d56-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooIntralinks (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="03d56-107">You can enable your users tooautomatically get signed-on tooIntralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="03d56-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="03d56-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="03d56-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="03d56-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03d56-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="03d56-110">Prerequisites</span></span>

<span data-ttu-id="03d56-111">integración de Azure AD con Intralinks tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="03d56-111">tooconfigure Azure AD integration with Intralinks, you need hello following items:</span></span>

- <span data-ttu-id="03d56-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="03d56-112">An Azure AD subscription</span></span>
- <span data-ttu-id="03d56-113">Una suscripción habilitada para el inicio de sesión único en Intralinks</span><span class="sxs-lookup"><span data-stu-id="03d56-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03d56-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="03d56-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="03d56-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="03d56-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="03d56-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="03d56-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="03d56-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03d56-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="03d56-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="03d56-118">Scenario description</span></span>
<span data-ttu-id="03d56-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="03d56-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="03d56-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="03d56-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="03d56-121">Agregar Intralinks desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="03d56-121">Adding Intralinks from hello gallery</span></span>
2. <span data-ttu-id="03d56-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="03d56-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-hello-gallery"></a><span data-ttu-id="03d56-123">Agregar Intralinks desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="03d56-123">Adding Intralinks from hello gallery</span></span>
<span data-ttu-id="03d56-124">integración de hello tooconfigure de Intralinks en Azure AD, deberá tooadd Intralinks de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="03d56-124">tooconfigure hello integration of Intralinks into Azure AD, you need tooadd Intralinks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="03d56-125">**tooadd Intralinks de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="03d56-125">**tooadd Intralinks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="03d56-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="03d56-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="03d56-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="03d56-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="03d56-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="03d56-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="03d56-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="03d56-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="03d56-133">En el cuadro de búsqueda de hello, escriba **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="03d56-133">In hello search box, type **Intralinks**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="03d56-135">En el panel de resultados de hello, seleccione **Intralinks**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="03d56-135">In hello results panel, select **Intralinks**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="03d56-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="03d56-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="03d56-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Intralinks con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="03d56-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="03d56-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Intralinks es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03d56-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intralinks is tooa user in Azure AD.</span></span> <span data-ttu-id="03d56-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Intralinks debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="03d56-140">In other words, a link relationship between an Azure AD user and hello related user in Intralinks needs toobe established.</span></span>

<span data-ttu-id="03d56-141">En Intralinks, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="03d56-141">In Intralinks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="03d56-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Intralinks, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="03d56-142">tooconfigure and test Azure AD single sign-on with Intralinks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="03d56-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="03d56-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="03d56-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03d56-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="03d56-145">**[Creación de un usuario de prueba Intralinks](#creating-an-intralinks-test-user)**  -toohave un equivalente de Britta Simon en Intralinks que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="03d56-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - toohave a counterpart of Britta Simon in Intralinks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="03d56-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="03d56-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="03d56-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="03d56-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="03d56-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="03d56-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="03d56-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Intralinks.</span><span class="sxs-lookup"><span data-stu-id="03d56-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="03d56-150">**inicio de sesión único en Azure AD tooconfigure con Intralinks, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="03d56-150">**tooconfigure Azure AD single sign-on with Intralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="03d56-151">En el portal de Azure, en Hola Hola **Intralinks** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="03d56-151">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="03d56-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="03d56-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="03d56-155">En hello **Intralinks dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="03d56-155">On hello **Intralinks Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="03d56-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="03d56-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="03d56-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="03d56-158">This value is not real.</span></span> <span data-ttu-id="03d56-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="03d56-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="03d56-160">Póngase en contacto con [equipo de soporte técnico de cliente de Intralinks](https://www.intralinks.com/contact-1) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="03d56-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) tooget this value.</span></span> 
 
4. <span data-ttu-id="03d56-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="03d56-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="03d56-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="03d56-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="03d56-165">tooconfigure inicio de sesión único en **Intralinks** lado, necesita hello toosend descargado **Metadata XML** [equipo de soporte técnico Intralinks](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="03d56-165">tooconfigure single sign-on on **Intralinks** side, you need toosend hello downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="03d56-166">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="03d56-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="03d56-167">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="03d56-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="03d56-168">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="03d56-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="03d56-169">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="03d56-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="03d56-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="03d56-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="03d56-171">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="03d56-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="03d56-173">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="03d56-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="03d56-174">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="03d56-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="03d56-176">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="03d56-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="03d56-178">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="03d56-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="03d56-180">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="03d56-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="03d56-182">a.</span><span class="sxs-lookup"><span data-stu-id="03d56-182">a.</span></span> <span data-ttu-id="03d56-183">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="03d56-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="03d56-184">b.</span><span class="sxs-lookup"><span data-stu-id="03d56-184">b.</span></span> <span data-ttu-id="03d56-185">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="03d56-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="03d56-186">c.</span><span class="sxs-lookup"><span data-stu-id="03d56-186">c.</span></span> <span data-ttu-id="03d56-187">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="03d56-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="03d56-188">d.</span><span class="sxs-lookup"><span data-stu-id="03d56-188">d.</span></span> <span data-ttu-id="03d56-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="03d56-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="03d56-190">Creación de un usuario de prueba de Intralinks</span><span class="sxs-lookup"><span data-stu-id="03d56-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="03d56-191">En esta sección, creará un usuario llamado Britta Simon en Intralinks.</span><span class="sxs-lookup"><span data-stu-id="03d56-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="03d56-192">Trabaje con [equipo de soporte técnico Intralinks](https://www.intralinks.com/contact-1) a los usuarios de tooadd hello en la plataforma de Intralinks Hola.</span><span class="sxs-lookup"><span data-stu-id="03d56-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) tooadd hello users in hello Intralinks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="03d56-193">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="03d56-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="03d56-194">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooIntralinks.</span><span class="sxs-lookup"><span data-stu-id="03d56-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntralinks.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="03d56-196">**tooassign Britta Simon tooIntralinks, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="03d56-196">**tooassign Britta Simon tooIntralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="03d56-197">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="03d56-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="03d56-199">En la lista de aplicaciones de hello, seleccione **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="03d56-199">In hello applications list, select **Intralinks**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="03d56-201">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="03d56-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="03d56-203">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="03d56-203">Click **Add** button.</span></span> <span data-ttu-id="03d56-204">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="03d56-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="03d56-206">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="03d56-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="03d56-207">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="03d56-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="03d56-208">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="03d56-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="03d56-209">Adición de la aplicación VIA o Elite de Intralinks</span><span class="sxs-lookup"><span data-stu-id="03d56-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="03d56-210">Usa Intralinks Hola misma plataforma de identidad SSO para todas las demás aplicaciones de Intralinks Excluir aplicación Nexus de acuerdo.</span><span class="sxs-lookup"><span data-stu-id="03d56-210">Intralinks uses hello same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="03d56-211">Por lo que si tiene previsto toouse cualquier otra aplicación Intralinks, a continuación, en primer lugar tiene tooconfigure SSO para una aplicación Intralinks principal mediante el procedimiento de Hola que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="03d56-211">So if you plan toouse any other Intralinks application then first you have tooconfigure SSO for one Primary Intralinks application using hello procedure described above.</span></span>

<span data-ttu-id="03d56-212">Después de que puede seguir hello debajo de procedimiento tooadd otra aplicación Intralinks en el inquilino que puede aprovechar esta aplicación principal de SSO.</span><span class="sxs-lookup"><span data-stu-id="03d56-212">After that you can follow hello below procedure tooadd another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="03d56-213">Esta característica está disponible sólo tooAzure AD Premium SKU los clientes y no está disponible para los clientes gratuito o SKU básica.</span><span class="sxs-lookup"><span data-stu-id="03d56-213">This feature is available only tooAzure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="03d56-214">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="03d56-214">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="03d56-216">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="03d56-216">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="03d56-217">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="03d56-217">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="03d56-219">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="03d56-219">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="03d56-221">En el cuadro de búsqueda de hello, escriba **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="03d56-221">In hello search box, type **Intralinks**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="03d56-223">En **Intralinks Agregar aplicación** realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="03d56-223">On **Intralinks Add app** perform hello following steps:</span></span>

    ![Adición de la aplicación VIA o Elite de Intralinks](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="03d56-225">a.</span><span class="sxs-lookup"><span data-stu-id="03d56-225">a.</span></span> <span data-ttu-id="03d56-226">En **nombre** cuadro de texto, escriba un nombre adecuado de la aplicación hello p. ej. **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="03d56-226">In **Name** textbox, enter appropriate name of hello application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="03d56-227">b.</span><span class="sxs-lookup"><span data-stu-id="03d56-227">b.</span></span> <span data-ttu-id="03d56-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="03d56-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="03d56-229">En el portal de Azure, en Hola Hola **Intralinks** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="03d56-229">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

7. <span data-ttu-id="03d56-231">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **en el inicio de sesión vinculado**.</span><span class="sxs-lookup"><span data-stu-id="03d56-231">On hello **Single sign-on** dialog, select **Mode** as   **Linked Sign-on**.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="03d56-233">Obtener URL de SSO de Hola Hola SP iniciado desde [Intralinks equipo](https://www.intralinks.com/contact-1) para Hola otra aplicación Intralinks y escríbala de nuevo en **configurar inicio de sesión en la dirección URL** tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="03d56-233">Get hello hello SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for hello other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="03d56-235">En el cuadro de texto de inicio de sesión en la dirección URL de hello, escriba Hola URL que se usa la aplicación de Intralinks de toosign en tooyour de usuarios usando Hola sigue el patrón:</span><span class="sxs-lookup"><span data-stu-id="03d56-235">In hello Sign On URL textbox, type hello URL used by your users toosign-on tooyour Intralinks application using hello following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="03d56-236">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="03d56-236">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="03d56-238">Asignación de toouser de aplicación Hola o grupos como se muestra en la sección de hello  **[usuario de prueba de hello Azure AD asignar](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="03d56-238">Assign hello application toouser or groups as shown in hello section **[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="03d56-239">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="03d56-239">Testing single sign-on</span></span>

<span data-ttu-id="03d56-240">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="03d56-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="03d56-241">Al hacer clic en hello Intralinks el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour Intralinks aplicación.</span><span class="sxs-lookup"><span data-stu-id="03d56-241">When you click hello Intralinks tile in hello Access Panel, you should get automatically signed-on tooyour Intralinks application.</span></span>
<span data-ttu-id="03d56-242">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="03d56-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="03d56-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="03d56-243">Additional resources</span></span>

* [<span data-ttu-id="03d56-244">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03d56-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="03d56-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="03d56-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

