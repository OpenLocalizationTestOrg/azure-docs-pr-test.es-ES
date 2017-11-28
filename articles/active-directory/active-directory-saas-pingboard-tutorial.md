---
title: "Tutorial: Integración de Azure Active Directory con Pingboard | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Pingboard."
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
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="562cb-103">Tutorial: Integración de Azure Active Directory con Pingboard</span><span class="sxs-lookup"><span data-stu-id="562cb-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="562cb-104">En este tutorial, aprenderá cómo toointegrate Pingboard con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="562cb-104">In this tutorial, you learn how toointegrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="562cb-105">Integración Pingboard con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="562cb-105">Integrating Pingboard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="562cb-106">Puede controlar en Azure AD que tenga acceso tooPingboard</span><span class="sxs-lookup"><span data-stu-id="562cb-106">You can control in Azure AD who has access tooPingboard</span></span>
- <span data-ttu-id="562cb-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPingboard (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562cb-107">You can enable your users tooautomatically get signed-on tooPingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="562cb-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="562cb-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="562cb-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="562cb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="562cb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="562cb-110">Prerequisites</span></span>

<span data-ttu-id="562cb-111">integración de Azure AD con Pingboard tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="562cb-111">tooconfigure Azure AD integration with Pingboard, you need hello following items:</span></span>

- <span data-ttu-id="562cb-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="562cb-113">Una suscripción a Pingboard habilitada para inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="562cb-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="562cb-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="562cb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="562cb-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="562cb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="562cb-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="562cb-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="562cb-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="562cb-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="562cb-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="562cb-118">Scenario description</span></span>
<span data-ttu-id="562cb-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="562cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="562cb-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="562cb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="562cb-121">Agregar Pingboard desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="562cb-121">Adding Pingboard from hello gallery</span></span>
2. <span data-ttu-id="562cb-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562cb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-hello-gallery"></a><span data-ttu-id="562cb-123">Agregar Pingboard desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="562cb-123">Adding Pingboard from hello gallery</span></span>
<span data-ttu-id="562cb-124">integración de hello tooconfigure de Pingboard en Azure AD, deberá tooadd Pingboard de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="562cb-124">tooconfigure hello integration of Pingboard into Azure AD, you need tooadd Pingboard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="562cb-125">**tooadd Pingboard de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="562cb-125">**tooadd Pingboard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="562cb-126">Hola ** [Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="562cb-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="562cb-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="562cb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="562cb-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="562cb-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="562cb-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="562cb-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="562cb-133">En el cuadro de búsqueda de hello, escriba **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="562cb-133">In hello search box, type **Pingboard**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="562cb-135">En el panel de resultados de hello, seleccione **Pingboard**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="562cb-135">In hello results panel, select **Pingboard**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="562cb-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562cb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="562cb-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Pingboard con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="562cb-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="562cb-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Pingboard es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="562cb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pingboard is tooa user in Azure AD.</span></span> <span data-ttu-id="562cb-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Pingboard debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="562cb-140">In other words, a link relationship between an Azure AD user and hello related user in Pingboard needs toobe established.</span></span>

<span data-ttu-id="562cb-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Pingboard.</span><span class="sxs-lookup"><span data-stu-id="562cb-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Pingboard.</span></span>

<span data-ttu-id="562cb-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Pingboard, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="562cb-142">tooconfigure and test Azure AD single sign-on with Pingboard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="562cb-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="562cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="562cb-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="562cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="562cb-145">**[Crear un usuario de prueba Pingboard](#creating-a-pingboard-test-user) ** -toohave un equivalente de Britta Simon en Pingboard que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="562cb-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - toohave a counterpart of Britta Simon in Pingboard that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="562cb-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="562cb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="562cb-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="562cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="562cb-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562cb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="562cb-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Pingboard.</span><span class="sxs-lookup"><span data-stu-id="562cb-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="562cb-150">**inicio de sesión único en Azure AD tooconfigure con Pingboard, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="562cb-150">**tooconfigure Azure AD single sign-on with Pingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="562cb-151">En el portal de administración de Azure de hello, en hello **Pingboard** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="562cb-151">In hello Azure Management portal, on hello **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="562cb-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="562cb-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="562cb-155">En hello **Pingboard dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="562cb-155">On hello **Pingboard Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="562cb-157">a.</span><span class="sxs-lookup"><span data-stu-id="562cb-157">a.</span></span> <span data-ttu-id="562cb-158">Hola **identificador** cuadro de texto, valor de tipo hello como:`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="562cb-158">In hello **Identifier** textbox, type hello value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="562cb-159">b.</span><span class="sxs-lookup"><span data-stu-id="562cb-159">b.</span></span> <span data-ttu-id="562cb-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="562cb-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="562cb-161">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="562cb-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="562cb-162">Tener tooupdate estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="562cb-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="562cb-163">Aquí le sugerimos toouse Hola único valor de cadena en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="562cb-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="562cb-164">Póngase en contacto con [equipo de soporte técnico de cliente de Pingboard](https://support.pingboard.com/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="562cb-164">Contact [Pingboard Client support team](https://support.pingboard.com/) tooget these values.</span></span> 

4. <span data-ttu-id="562cb-165">Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="562cb-165">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="562cb-167">a.</span><span class="sxs-lookup"><span data-stu-id="562cb-167">a.</span></span> <span data-ttu-id="562cb-168">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello como:`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="562cb-168">In hello **Sign-on URL** textbox, type hello value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="562cb-169">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="562cb-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="562cb-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="562cb-171">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="562cb-173">tooconfigure SSO en el lado de Pingboard, abra una nueva ventana del explorador e inicie sesión tooyour Pingboard cuenta.</span><span class="sxs-lookup"><span data-stu-id="562cb-173">tooconfigure SSO on Pingboard side, open a new browser window and log in tooyour Pingboard Account.</span></span> <span data-ttu-id="562cb-174">Debe ser un tooset de administración de Pingboard seguridad de inicio de sesión único en.</span><span class="sxs-lookup"><span data-stu-id="562cb-174">You must be a Pingboard admin tooset up single sign on.</span></span>

8. <span data-ttu-id="562cb-175">En el menú superior Hola seleccione **aplicaciones > integraciones**</span><span class="sxs-lookup"><span data-stu-id="562cb-175">From hello top menu select **Apps > Integrations**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="562cb-177">En hello **integraciones** página, busque hello **"Azure Active Directory"** icono y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="562cb-177">On hello **Integrations** page, find hello **"Azure Active Directory"** tile, and click it.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="562cb-179">Hola modal que sigue a haga clic en **"Configurar"**</span><span class="sxs-lookup"><span data-stu-id="562cb-179">In hello modal that follows click **"Configure"**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="562cb-181">En hello después de la página, observará que "integración de Azure SSO está habilitada.".</span><span class="sxs-lookup"><span data-stu-id="562cb-181">On hello following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="562cb-182">Abra Hola descargado el archivo de Metadata XML en un Hola el Bloc de notas y pegar contenido en **metadatos de IDP**.</span><span class="sxs-lookup"><span data-stu-id="562cb-182">Open hello downloaded Metadata XML file in a notepad and paste hello content in **IDP Metadata**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="562cb-184">se validará el archivo Hello y, si todo es correcto, ahora se habilitará el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="562cb-184">hello file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="562cb-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562cb-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="562cb-186">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="562cb-186">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="562cb-188">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="562cb-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="562cb-189">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="562cb-189">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="562cb-191">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="562cb-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="562cb-193">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="562cb-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="562cb-195">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="562cb-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="562cb-197">a.</span><span class="sxs-lookup"><span data-stu-id="562cb-197">a.</span></span> <span data-ttu-id="562cb-198">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="562cb-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="562cb-199">b.</span><span class="sxs-lookup"><span data-stu-id="562cb-199">b.</span></span> <span data-ttu-id="562cb-200">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="562cb-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="562cb-201">c.</span><span class="sxs-lookup"><span data-stu-id="562cb-201">c.</span></span> <span data-ttu-id="562cb-202">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="562cb-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="562cb-203">d.</span><span class="sxs-lookup"><span data-stu-id="562cb-203">d.</span></span> <span data-ttu-id="562cb-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="562cb-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="562cb-205">Creación de un usuario de prueba de Pingboard</span><span class="sxs-lookup"><span data-stu-id="562cb-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="562cb-206">En orden tooenable toolog de los usuarios de Azure AD en Pingboard, se les deben aprovisionar en Pingboard.</span><span class="sxs-lookup"><span data-stu-id="562cb-206">In order tooenable Azure AD users toolog into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="562cb-207">En caso de hello de Pingboard, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="562cb-207">In hello case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="562cb-208">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="562cb-208">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="562cb-209">Inicie sesión en tooyour Pingboard sitio de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="562cb-209">Log in tooyour Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="562cb-210">Haga clic en el botón **“Add Employee”** (Agregar empleado) en la página **Directory** (Directorio).</span><span class="sxs-lookup"><span data-stu-id="562cb-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Agregar empleado](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="562cb-212">En hello **"Agregar empleado"** cuadro de diálogo, siga los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="562cb-212">On hello **“Add Employee”** dialog page, perform hello following steps.</span></span>

    ![Invitar a contactos](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="562cb-214">a.</span><span class="sxs-lookup"><span data-stu-id="562cb-214">a.</span></span> <span data-ttu-id="562cb-215">Hola **nombre completo** cuadro de texto, nombre completo de tipo hello de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="562cb-215">In hello **Full Name** textbox, type hello full name of Britta Simon.</span></span>

    <span data-ttu-id="562cb-216">b.</span><span class="sxs-lookup"><span data-stu-id="562cb-216">b.</span></span> <span data-ttu-id="562cb-217">Hola **correo electrónico** cuadro de texto, dirección de correo electrónico de Hola de tipo de cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="562cb-217">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="562cb-218">c.</span><span class="sxs-lookup"><span data-stu-id="562cb-218">c.</span></span> <span data-ttu-id="562cb-219">Hola **puesto** cuadro de texto, puesto de trabajo de tipo hello de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="562cb-219">In hello **Job Title** textbox, type hello job title of Britta Simon.</span></span>

    <span data-ttu-id="562cb-220">d.</span><span class="sxs-lookup"><span data-stu-id="562cb-220">d.</span></span> <span data-ttu-id="562cb-221">Hola **ubicación** ubicación seleccione Hola de Britta Simon de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="562cb-221">In hello **Location** dropdown, select hello location  of Britta Simon.</span></span>
    
    <span data-ttu-id="562cb-222">e.</span><span class="sxs-lookup"><span data-stu-id="562cb-222">e.</span></span> <span data-ttu-id="562cb-223">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="562cb-223">Click **Add**.</span></span>   

4. <span data-ttu-id="562cb-224">Adición de hello tooconfirm de usuario aparecerá una pantalla de confirmación.</span><span class="sxs-lookup"><span data-stu-id="562cb-224">A confirmation screen will come up tooconfirm hello addition of user.</span></span>
    
    ![confirmar](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="562cb-226">titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="562cb-226">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="562cb-227">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="562cb-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="562cb-228">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooPingboard de acceso.</span><span class="sxs-lookup"><span data-stu-id="562cb-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPingboard.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="562cb-230">**tooassign Britta Simon tooPingboard, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="562cb-230">**tooassign Britta Simon tooPingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="562cb-231">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="562cb-231">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="562cb-233">En la lista de aplicaciones de hello, seleccione **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="562cb-233">In hello applications list, select **Pingboard**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="562cb-235">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="562cb-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="562cb-237">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="562cb-237">Click **Add** button.</span></span> <span data-ttu-id="562cb-238">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="562cb-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="562cb-240">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="562cb-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="562cb-241">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="562cb-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="562cb-242">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="562cb-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="562cb-243">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="562cb-243">Testing single sign-on</span></span>

<span data-ttu-id="562cb-244">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="562cb-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="562cb-245">Al hacer clic en icono de Pingboard Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Pingboard aplicación.</span><span class="sxs-lookup"><span data-stu-id="562cb-245">When you click hello Pingboard tile in hello Access Panel, you should get automatically signed-on tooyour Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="562cb-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="562cb-246">Additional resources</span></span>

* [<span data-ttu-id="562cb-247">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="562cb-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="562cb-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="562cb-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
