---
title: "Tutorial: Integración de Azure Active Directory con Land Gorilla Client | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y terrenos Gorilla."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: e95a30551e636108fe22a7ab6d1827bc12d7f9a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="d904a-103">Tutorial: Integración de Azure Active Directory con Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="d904a-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="d904a-104">En este tutorial, aprenderá cómo toointegrate terrenos Gorilla cliente con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d904a-104">In this tutorial, you learn how toointegrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d904a-105">Integración de terrenos Gorilla cliente con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d904a-105">Integrating Land Gorilla Client with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d904a-106">Puede controlar en Azure AD que tenga acceso tooLand Gorilla cliente</span><span class="sxs-lookup"><span data-stu-id="d904a-106">You can control in Azure AD who has access tooLand Gorilla Client</span></span>
- <span data-ttu-id="d904a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLand cliente Gorilla (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d904a-107">You can enable your users tooautomatically get signed-on tooLand Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d904a-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="d904a-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d904a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d904a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d904a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d904a-110">Prerequisites</span></span>

<span data-ttu-id="d904a-111">integración de Azure AD con tierra Gorilla cliente tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d904a-111">tooconfigure Azure AD integration with Land Gorilla Client, you need hello following items:</span></span>

- <span data-ttu-id="d904a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d904a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d904a-113">Una suscripción habilitada para el inicio de sesión único en Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="d904a-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="d904a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d904a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="d904a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d904a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d904a-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d904a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d904a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d904a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="d904a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d904a-118">Scenario description</span></span>
<span data-ttu-id="d904a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d904a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d904a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="d904a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d904a-121">Agregar el cliente de Gorilla tierra de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="d904a-121">Adding Land Gorilla Client from hello gallery</span></span>
2. <span data-ttu-id="d904a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d904a-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-hello-gallery"></a><span data-ttu-id="d904a-123">Agregar el cliente de Gorilla tierra de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="d904a-123">Adding Land Gorilla Client from hello gallery</span></span>
<span data-ttu-id="d904a-124">integración de hello tooconfigure de tierra Gorilla cliente en Azure AD, deberá a tooadd terrenos Gorilla cliente de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="d904a-124">tooconfigure hello integration of Land Gorilla Client into Azure AD, you need tooadd Land Gorilla Client from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d904a-125">**tooadd terrenos Gorilla cliente desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d904a-125">**tooadd Land Gorilla Client from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d904a-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d904a-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d904a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d904a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d904a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d904a-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d904a-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d904a-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d904a-133">En el cuadro de búsqueda de hello, escriba **terrenos Gorilla cliente**.</span><span class="sxs-lookup"><span data-stu-id="d904a-133">In hello search box, type **Land Gorilla Client**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="d904a-135">En el panel de resultados de hello, seleccione **terrenos Gorilla cliente**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d904a-135">In hello results panel, select **Land Gorilla Client**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d904a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d904a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d904a-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Land Gorilla Client con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d904a-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d904a-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en tierra Gorilla cliente es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d904a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Land Gorilla Client is tooa user in Azure AD.</span></span> <span data-ttu-id="d904a-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en tierra Gorilla cliente necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="d904a-140">In other words, a link relationship between an Azure AD user and hello related user in Land Gorilla Client needs toobe established.</span></span>

<span data-ttu-id="d904a-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en tierras Gorilla cliente.</span><span class="sxs-lookup"><span data-stu-id="d904a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="d904a-142">tooconfigure y prueba de inicio de sesión único en Azure AD con tierra Gorilla cliente, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d904a-142">tooconfigure and test Azure AD single sign-on with Land Gorilla Client, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d904a-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="d904a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d904a-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en tootest Azure AD con grupo limitado.</span><span class="sxs-lookup"><span data-stu-id="d904a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="d904a-145">**[Crear un usuario de prueba de tierra Gorilla](#creating-a-land-gorilla-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d904a-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="d904a-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d904a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d904a-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d904a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d904a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d904a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d904a-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación cliente de Gorilla terrenos.</span><span class="sxs-lookup"><span data-stu-id="d904a-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="d904a-150">**tooconfigure inicio de sesión único en Azure AD con tierra Gorilla cliente, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d904a-150">**tooconfigure Azure AD single sign-on with Land Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="d904a-151">En el portal de administración de Azure de hello, en hello **terrenos Gorilla cliente** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d904a-151">In hello Azure Management portal, on hello **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d904a-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d904a-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="d904a-155">En hello **terrenos Gorilla cliente dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d904a-155">On hello **Land Gorilla Client Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="d904a-157">a.</span><span class="sxs-lookup"><span data-stu-id="d904a-157">a.</span></span> <span data-ttu-id="d904a-158">Hola **identificador** cuadro de texto, valor de tipo hello mediante uno de hello sigue el patrón:</span><span class="sxs-lookup"><span data-stu-id="d904a-158">In hello **Identifier** textbox, type hello value using one of hello following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="d904a-159">b.</span><span class="sxs-lookup"><span data-stu-id="d904a-159">b.</span></span> <span data-ttu-id="d904a-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando uno de hello siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="d904a-160">In hello **Reply URL** textbox, type a URL using one of hello following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="d904a-161">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="d904a-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="d904a-162">Tener tooupdate estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="d904a-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="d904a-163">Aquí le sugerimos toouse Hola único valor de cadena en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="d904a-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="d904a-164">Póngase en contacto con [equipo terrenos Gorilla clientes](https://www.landgorilla.com/support/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="d904a-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="d904a-165">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d904a-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="d904a-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d904a-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="d904a-169">configuración de SSO de tooget completa de la aplicación al final de la tierra Gorilla, póngase en contacto con [equipo de soporte técnico de tierra Gorilla cliente](https://www.landgorilla.com/support/) y proporcionarles Hola descargado **"Metadata XML** archivo.</span><span class="sxs-lookup"><span data-stu-id="d904a-169">tooget SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with hello downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d904a-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d904a-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="d904a-171">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="d904a-171">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d904a-173">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d904a-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d904a-174">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d904a-174">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d904a-176">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d904a-176">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d904a-178">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d904a-178">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d904a-180">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d904a-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d904a-182">a.</span><span class="sxs-lookup"><span data-stu-id="d904a-182">a.</span></span> <span data-ttu-id="d904a-183">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d904a-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d904a-184">b.</span><span class="sxs-lookup"><span data-stu-id="d904a-184">b.</span></span> <span data-ttu-id="d904a-185">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d904a-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d904a-186">c.</span><span class="sxs-lookup"><span data-stu-id="d904a-186">c.</span></span> <span data-ttu-id="d904a-187">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d904a-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d904a-188">d.</span><span class="sxs-lookup"><span data-stu-id="d904a-188">d.</span></span> <span data-ttu-id="d904a-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d904a-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="d904a-190">Creación de un usuario de prueba de Land Gorilla</span><span class="sxs-lookup"><span data-stu-id="d904a-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="d904a-191">Trabaje con [equipo de soporte técnico de tierra Gorilla](https://www.landgorilla.com/support/) a los usuarios de tooadd hello en la plataforma de tierra Gorilla Hola.</span><span class="sxs-lookup"><span data-stu-id="d904a-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) tooadd hello users in hello Land Gorilla platform.</span></span>
    
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d904a-192">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d904a-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d904a-193">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su cliente Gorilla tooLand de acceso.</span><span class="sxs-lookup"><span data-stu-id="d904a-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLand Gorilla Client.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d904a-195">**tooassign Britta Simon tooLand Gorilla cliente, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d904a-195">**tooassign Britta Simon tooLand Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="d904a-196">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d904a-196">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d904a-198">En la lista de aplicaciones de hello, seleccione **terrenos Gorilla cliente**.</span><span class="sxs-lookup"><span data-stu-id="d904a-198">In hello applications list, select **Land Gorilla Client**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="d904a-200">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d904a-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d904a-202">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d904a-202">Click **Add** button.</span></span> <span data-ttu-id="d904a-203">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d904a-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d904a-205">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d904a-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d904a-206">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d904a-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d904a-207">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d904a-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="d904a-208">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d904a-208">Testing single sign-on</span></span>

<span data-ttu-id="d904a-209">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d904a-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d904a-210">Al hacer clic en icono de tierra Gorilla cliente Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación terrenos Gorilla cliente.</span><span class="sxs-lookup"><span data-stu-id="d904a-210">When you click hello Land Gorilla Client tile in hello Access Panel, you should get automatically signed-on tooyour Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d904a-211">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d904a-211">Additional resources</span></span>

* [<span data-ttu-id="d904a-212">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d904a-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d904a-213">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d904a-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
