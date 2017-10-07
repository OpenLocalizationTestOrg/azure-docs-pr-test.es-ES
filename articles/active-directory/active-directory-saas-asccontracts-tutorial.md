---
title: "Tutorial: Integración de Azure Active Directory con ASC Contracts | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y los contratos de ASC."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 8320af8acfda3e3d37e589c9887cd697d5ab651c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="39298-103">Tutorial: Integración de Azure Active Directory con ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="39298-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="39298-104">En este tutorial, aprenderá cómo toointegrate ASC contratos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39298-104">In this tutorial, you learn how toointegrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39298-105">Integración ASC contratos con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="39298-105">Integrating ASC Contracts with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="39298-106">Puede controlar en Azure AD que tenga acceso tooASC contratos</span><span class="sxs-lookup"><span data-stu-id="39298-106">You can control in Azure AD who has access tooASC Contracts</span></span>
- <span data-ttu-id="39298-107">Puede habilitar la tooautomatically a los usuarios obtener contratos tooASC ha iniciado sesión (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="39298-107">You can enable your users tooautomatically get signed-on tooASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="39298-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="39298-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="39298-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39298-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39298-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="39298-110">Prerequisites</span></span>

<span data-ttu-id="39298-111">tooconfigure integración de Azure AD con contratos de ASC, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="39298-111">tooconfigure Azure AD integration with ASC Contracts, you need hello following items:</span></span>

- <span data-ttu-id="39298-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="39298-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39298-113">Una suscripción habilitada para inicio de sesión único en ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="39298-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39298-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="39298-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39298-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="39298-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39298-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="39298-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="39298-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39298-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39298-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="39298-118">Scenario description</span></span>
<span data-ttu-id="39298-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="39298-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39298-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="39298-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39298-121">Adición de contratos de ASC desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="39298-121">Adding ASC Contracts from hello gallery</span></span>
2. <span data-ttu-id="39298-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="39298-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-hello-gallery"></a><span data-ttu-id="39298-123">Adición de contratos de ASC desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="39298-123">Adding ASC Contracts from hello gallery</span></span>
<span data-ttu-id="39298-124">integración de hello tooconfigure de ASC contratos en Azure AD, deberá tooadd ASC contratos de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="39298-124">tooconfigure hello integration of ASC Contracts into Azure AD, you need tooadd ASC Contracts from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="39298-125">**tooadd ASC contratos de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="39298-125">**tooadd ASC Contracts from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="39298-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="39298-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="39298-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="39298-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="39298-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="39298-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="39298-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39298-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="39298-133">En el cuadro de búsqueda de hello, escriba **ASC contratos**.</span><span class="sxs-lookup"><span data-stu-id="39298-133">In hello search box, type **ASC Contracts**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="39298-135">En el panel de resultados de hello, seleccione **ASC contratos**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="39298-135">In hello results panel, select **ASC Contracts**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="39298-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="39298-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="39298-138">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con ASC Contracts con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="39298-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="39298-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en contratos de ASC es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39298-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ASC Contracts is tooa user in Azure AD.</span></span> <span data-ttu-id="39298-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en contratos de ASC debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="39298-140">In other words, a link relationship between an Azure AD user and hello related user in ASC Contracts needs toobe established.</span></span>

<span data-ttu-id="39298-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en contratos de ASC.</span><span class="sxs-lookup"><span data-stu-id="39298-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ASC Contracts.</span></span>

<span data-ttu-id="39298-142">tooconfigure y prueba de inicio de sesión único en Azure AD con contratos de ASC, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="39298-142">tooconfigure and test Azure AD single sign-on with ASC Contracts, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="39298-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="39298-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="39298-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39298-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="39298-145">**[Creación de un usuario de prueba de contratos de ASC](#creating-an-asc-contracts-test-user)**  -toohave un equivalente de Britta Simon en contratos de ASC es representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="39298-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - toohave a counterpart of Britta Simon in ASC Contracts that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="39298-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="39298-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39298-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="39298-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="39298-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="39298-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="39298-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de contratos de ASC.</span><span class="sxs-lookup"><span data-stu-id="39298-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="39298-150">**inicio de sesión único en Azure AD tooconfigure con contratos de ASC, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="39298-150">**tooconfigure Azure AD single sign-on with ASC Contracts, perform hello following steps:**</span></span>

1. <span data-ttu-id="39298-151">En el portal de Azure, en Hola Hola **ASC contratos** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="39298-151">In hello Azure portal, on hello **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="39298-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="39298-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="39298-155">En hello **ASC contratos de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="39298-155">On hello **ASC Contracts Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="39298-157">a.</span><span class="sxs-lookup"><span data-stu-id="39298-157">a.</span></span> <span data-ttu-id="39298-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="39298-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="39298-159">b.</span><span class="sxs-lookup"><span data-stu-id="39298-159">b.</span></span> <span data-ttu-id="39298-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="39298-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="39298-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="39298-161">These values are not real.</span></span> <span data-ttu-id="39298-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="39298-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="39298-163">Póngase en contacto con el equipo de ASC redes Inc. (ASC) en **613.599.6178** tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="39298-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** tooget these values.</span></span>

4. <span data-ttu-id="39298-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="39298-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="39298-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="39298-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="39298-168">tooconfigure inicio de sesión único en **ASC contratos** cara, llame al soporte técnico de ASC redes Inc. (ASC) en **613.599.6178** y proporcionarles Hola descargado **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="39298-168">tooconfigure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with hello downloaded **Metadata XML**.</span></span> <span data-ttu-id="39298-169">Establecen esta aplicación se pueden instalar toohave Hola configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="39298-169">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="39298-170">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="39298-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="39298-171">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="39298-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="39298-172">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="39298-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="39298-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="39298-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="39298-174">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="39298-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="39298-176">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="39298-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="39298-177">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="39298-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="39298-179">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="39298-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="39298-181">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="39298-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="39298-183">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="39298-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="39298-185">a.</span><span class="sxs-lookup"><span data-stu-id="39298-185">a.</span></span> <span data-ttu-id="39298-186">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39298-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39298-187">b.</span><span class="sxs-lookup"><span data-stu-id="39298-187">b.</span></span> <span data-ttu-id="39298-188">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="39298-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="39298-189">c.</span><span class="sxs-lookup"><span data-stu-id="39298-189">c.</span></span> <span data-ttu-id="39298-190">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="39298-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="39298-191">d.</span><span class="sxs-lookup"><span data-stu-id="39298-191">d.</span></span> <span data-ttu-id="39298-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="39298-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="39298-193">Creación de un usuario de prueba de ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="39298-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="39298-194">Trabajar con el equipo de soporte técnico de ASC redes Inc. (ASC) en **613.599.6178** usuarios de hello tooget agregados en la plataforma de contratos de ASC Hola.</span><span class="sxs-lookup"><span data-stu-id="39298-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** tooget hello users added in hello ASC Contracts platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="39298-195">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="39298-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="39298-196">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooASC contratos.</span><span class="sxs-lookup"><span data-stu-id="39298-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooASC Contracts.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="39298-198">**tooassign Britta Simon tooASC contratos, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="39298-198">**tooassign Britta Simon tooASC Contracts, perform hello following steps:**</span></span>

1. <span data-ttu-id="39298-199">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="39298-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="39298-201">En la lista de aplicaciones de hello, seleccione **ASC contratos**.</span><span class="sxs-lookup"><span data-stu-id="39298-201">In hello applications list, select **ASC Contracts**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="39298-203">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="39298-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="39298-205">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="39298-205">Click **Add** button.</span></span> <span data-ttu-id="39298-206">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="39298-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="39298-208">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="39298-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="39298-209">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="39298-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="39298-210">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="39298-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="39298-211">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="39298-211">Testing single sign-on</span></span>

<span data-ttu-id="39298-212">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="39298-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="39298-213">Al hacer clic en hello ASC contratos disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación ASC contratos.</span><span class="sxs-lookup"><span data-stu-id="39298-213">When you click hello ASC Contracts tile in hello Access Panel, you should get automatically signed-on tooyour ASC Contracts application.</span></span> <span data-ttu-id="39298-214">Para obtener más información sobre el panel de acceso, consulte</span><span class="sxs-lookup"><span data-stu-id="39298-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="39298-215">[Introducción al panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="39298-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39298-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="39298-216">Additional resources</span></span>

* [<span data-ttu-id="39298-217">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39298-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39298-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="39298-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

