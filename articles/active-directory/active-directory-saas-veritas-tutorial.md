---
title: "Tutorial: Integración de Azure Active Directory con Veritas Enterprise Vault.cloud SSO | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Veritas Enterprise Vault.cloud SSO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 1037e70515686091460ac41e9e5a7951639bb520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veritas-enterprise-vaultcloud-sso"></a><span data-ttu-id="27b79-103">Tutorial: Integración de Azure Active Directory con Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="27b79-103">Tutorial: Azure Active Directory integration with Veritas Enterprise Vault.cloud SSO</span></span>

<span data-ttu-id="27b79-104">En este tutorial, aprenderá cómo toointegrate Veritas Enterprise Vault.cloud SSO con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="27b79-104">In this tutorial, you learn how toointegrate Veritas Enterprise Vault.cloud SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27b79-105">Integración Veritas Enterprise Vault.cloud SSO con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="27b79-105">Integrating Veritas Enterprise Vault.cloud SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="27b79-106">Puede controlar en Azure AD que tenga acceso tooVeritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="27b79-106">You can control in Azure AD who has access tooVeritas Enterprise Vault.cloud SSO</span></span>
- <span data-ttu-id="27b79-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooVeritas Enterprise Vault.cloud SSO (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b79-107">You can enable your users tooautomatically get signed-on tooVeritas Enterprise Vault.cloud SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="27b79-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="27b79-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="27b79-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="27b79-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27b79-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="27b79-110">Prerequisites</span></span>

<span data-ttu-id="27b79-111">tooconfigure integración de Azure AD con Veritas Enterprise Vault.cloud SSO, debe Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="27b79-111">tooconfigure Azure AD integration with Veritas Enterprise Vault.cloud SSO, you need hello following items:</span></span>

- <span data-ttu-id="27b79-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b79-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27b79-113">Una suscripción habilitada para inicio de sesión único en Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="27b79-113">A Veritas Enterprise Vault.cloud SSO single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27b79-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="27b79-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27b79-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="27b79-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27b79-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="27b79-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27b79-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27b79-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27b79-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="27b79-118">Scenario description</span></span>
<span data-ttu-id="27b79-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="27b79-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27b79-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="27b79-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27b79-121">Agregar Veritas Enterprise Vault.cloud SSO desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="27b79-121">Adding Veritas Enterprise Vault.cloud SSO from hello gallery</span></span>
2. <span data-ttu-id="27b79-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b79-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-veritas-enterprise-vaultcloud-sso-from-hello-gallery"></a><span data-ttu-id="27b79-123">Agregar Veritas Enterprise Vault.cloud SSO desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="27b79-123">Adding Veritas Enterprise Vault.cloud SSO from hello gallery</span></span>
<span data-ttu-id="27b79-124">integración de hello tooconfigure de Veritas Enterprise Vault.cloud SSO en Azure AD, deberá tooadd Veritas Enterprise Vault.cloud SSO de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="27b79-124">tooconfigure hello integration of Veritas Enterprise Vault.cloud SSO into Azure AD, you need tooadd Veritas Enterprise Vault.cloud SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27b79-125">**tooadd Veritas Enterprise Vault.cloud SSO de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27b79-125">**tooadd Veritas Enterprise Vault.cloud SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27b79-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="27b79-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="27b79-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="27b79-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="27b79-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="27b79-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="27b79-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27b79-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="27b79-133">En el cuadro de búsqueda de hello, escriba **Veritas Enterprise Vault.cloud SSO**.</span><span class="sxs-lookup"><span data-stu-id="27b79-133">In hello search box, type **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_search.png)

5. <span data-ttu-id="27b79-135">En el panel de resultados de hello, seleccione **Veritas Enterprise Vault.cloud SSO**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="27b79-135">In hello results panel, select **Veritas Enterprise Vault.cloud SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="27b79-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b79-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="27b79-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Veritas Enterprise Vault.cloud SSO con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="27b79-138">In this section, you configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27b79-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Veritas Enterprise Vault.cloud SSO es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27b79-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veritas Enterprise Vault.cloud SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="27b79-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Veritas Enterprise Vault.cloud SSO necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="27b79-140">In other words, a link relationship between an Azure AD user and hello related user in Veritas Enterprise Vault.cloud SSO needs toobe established.</span></span>

<span data-ttu-id="27b79-141">En Veritas Enterprise Vault.cloud SSO, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="27b79-141">In Veritas Enterprise Vault.cloud SSO, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="27b79-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Veritas Enterprise Vault.cloud SSO, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="27b79-142">tooconfigure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27b79-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="27b79-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27b79-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27b79-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27b79-145">**[Crear un usuario de prueba de SSO de Veritas empresarial Vault.cloud](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)**  -toohave un equivalente de Britta Simon en Veritas Enterprise Vault.cloud SSO que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="27b79-145">**[Creating a Veritas Enterprise Vault.cloud SSO test user](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)** - toohave a counterpart of Britta Simon in Veritas Enterprise Vault.cloud SSO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="27b79-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="27b79-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27b79-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="27b79-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="27b79-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b79-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="27b79-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="27b79-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veritas Enterprise Vault.cloud SSO application.</span></span>

<span data-ttu-id="27b79-150">**tooconfigure inicio de sesión único en Azure AD con Veritas Enterprise Vault.cloud SSO, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27b79-150">**tooconfigure Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="27b79-151">En el portal de Azure, en Hola Hola **Veritas Enterprise Vault.cloud SSO** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="27b79-151">In hello Azure portal, on hello **Veritas Enterprise Vault.cloud SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="27b79-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="27b79-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_samlbase.png)

3. <span data-ttu-id="27b79-155">En hello **Veritas Enterprise Vault.cloud SSO dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27b79-155">On hello **Veritas Enterprise Vault.cloud SSO Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_url.png)

    <span data-ttu-id="27b79-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span><span class="sxs-lookup"><span data-stu-id="27b79-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="27b79-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="27b79-158">This value is not real.</span></span> <span data-ttu-id="27b79-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="27b79-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="27b79-160">Póngase en contacto con [equipo de soporte técnico de cliente de SSO de Veritas Enterprise Vault.cloud](https://www.veritas.com/support/.html) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="27b79-160">Contact [Veritas Enterprise Vault.cloud SSO Client support team](https://www.veritas.com/support/.html) tooget this value.</span></span> 

4. <span data-ttu-id="27b79-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="27b79-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_certificate.png) 

5. <span data-ttu-id="27b79-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="27b79-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-veritas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="27b79-165">En hello **configuración de SSO de Veritas Enterprise Vault.cloud** sección, haga clic en **configurar SSO de Veritas empresarial Vault.cloud** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="27b79-165">On hello **Veritas Enterprise Vault.cloud SSO Configuration** section, click **Configure Veritas Enterprise Vault.cloud SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="27b79-166">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="27b79-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_configure.png) 

7. <span data-ttu-id="27b79-168">tooconfigure inicio de sesión único en **Veritas Enterprise Vault.cloud SSO** lado, necesita hello toosend descargado **Certificate(Base64)** y **SAML Single Sign-On dirección URL del servicio**demasiado[equipo de soporte técnico de Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html).</span><span class="sxs-lookup"><span data-stu-id="27b79-168">tooconfigure single sign-on on **Veritas Enterprise Vault.cloud SSO** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html).</span></span>

> [!TIP]
> <span data-ttu-id="27b79-169">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="27b79-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="27b79-170">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="27b79-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="27b79-171">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27b79-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="27b79-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b79-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="27b79-173">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="27b79-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="27b79-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27b79-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27b79-176">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="27b79-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="27b79-178">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="27b79-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="27b79-180">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="27b79-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="27b79-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="27b79-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="27b79-184">a.</span><span class="sxs-lookup"><span data-stu-id="27b79-184">a.</span></span> <span data-ttu-id="27b79-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27b79-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27b79-186">b.</span><span class="sxs-lookup"><span data-stu-id="27b79-186">b.</span></span> <span data-ttu-id="27b79-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="27b79-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="27b79-188">c.</span><span class="sxs-lookup"><span data-stu-id="27b79-188">c.</span></span> <span data-ttu-id="27b79-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="27b79-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="27b79-190">d.</span><span class="sxs-lookup"><span data-stu-id="27b79-190">d.</span></span> <span data-ttu-id="27b79-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="27b79-191">Click **Create**.</span></span>
 
### <a name="creating-a-veritas-enterprise-vaultcloud-sso-test-user"></a><span data-ttu-id="27b79-192">Creación de un usuario de prueba de Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="27b79-192">Creating a Veritas Enterprise Vault.cloud SSO test user</span></span>

<span data-ttu-id="27b79-193">En esta sección, creará un usuario llamado Britta Simon en Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="27b79-193">In this section, you create a user called Britta Simon in Enterprise Vault.cloud SSO.</span></span> <span data-ttu-id="27b79-194">Trabajar con [equipo de soporte técnico de Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html) para agregar usuarios de hello en la plataforma de Enterprise Vault.cloud SSO Hola.</span><span class="sxs-lookup"><span data-stu-id="27b79-194">Work with [Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html) to add hello users in hello Enterprise Vault.cloud SSO platform.</span></span> <span data-ttu-id="27b79-195">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="27b79-195">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="27b79-196">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b79-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="27b79-197">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooVeritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="27b79-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeritas Enterprise Vault.cloud SSO.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="27b79-199">**tooassign Britta Simon tooVeritas empresarial Vault.cloud SSO, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27b79-199">**tooassign Britta Simon tooVeritas Enterprise Vault.cloud SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="27b79-200">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="27b79-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="27b79-202">En la lista de aplicaciones de hello, seleccione **Veritas Enterprise Vault.cloud SSO**.</span><span class="sxs-lookup"><span data-stu-id="27b79-202">In hello applications list, select **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_app.png) 

3. <span data-ttu-id="27b79-204">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="27b79-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="27b79-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="27b79-206">Click **Add** button.</span></span> <span data-ttu-id="27b79-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="27b79-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="27b79-209">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="27b79-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27b79-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="27b79-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27b79-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="27b79-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="27b79-212">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="27b79-212">Testing single sign-on</span></span>

<span data-ttu-id="27b79-213">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="27b79-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="27b79-214">Al hacer clic en icono de Veritas Enterprise Vault.cloud SSO Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="27b79-214">When you click hello Veritas Enterprise Vault.cloud SSO tile in hello Access Panel, you should get automatically signed-on tooyour Veritas Enterprise Vault.cloud SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="27b79-215">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="27b79-215">Additional resources</span></span>

* [<span data-ttu-id="27b79-216">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27b79-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27b79-217">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="27b79-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_203.png

