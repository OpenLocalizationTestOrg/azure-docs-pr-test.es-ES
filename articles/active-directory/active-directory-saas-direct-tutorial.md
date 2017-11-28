---
title: "Tutorial: integración de Azure Active Directory con Direct | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y directo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ac663070b39e55eade2c43814b63a9d0374c7316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="c8b1c-103">Tutorial: integración de Azure Active Directory con Direct</span><span class="sxs-lookup"><span data-stu-id="c8b1c-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="c8b1c-104">En este tutorial, aprenderá cómo toointegrate directa con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c8b1c-104">In this tutorial, you learn how toointegrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c8b1c-105">Integración directa con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c8b1c-105">Integrating Direct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c8b1c-106">Puede controlar en Azure AD que tenga acceso tooDirect</span><span class="sxs-lookup"><span data-stu-id="c8b1c-106">You can control in Azure AD who has access tooDirect</span></span>
- <span data-ttu-id="c8b1c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooDirect (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8b1c-107">You can enable your users tooautomatically get signed-on tooDirect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c8b1c-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c8b1c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c8b1c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8b1c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8b1c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c8b1c-110">Prerequisites</span></span>

<span data-ttu-id="c8b1c-111">tooconfigure integración de Azure AD con Direct, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c8b1c-111">tooconfigure Azure AD integration with Direct, you need hello following items:</span></span>

- <span data-ttu-id="c8b1c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8b1c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c8b1c-113">Una suscripción habilitada para el inicio de sesión único en Direct</span><span class="sxs-lookup"><span data-stu-id="c8b1c-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c8b1c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c8b1c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c8b1c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c8b1c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c8b1c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8b1c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c8b1c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c8b1c-118">Scenario description</span></span>
<span data-ttu-id="c8b1c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8b1c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c8b1c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c8b1c-121">Agregar directamente desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c8b1c-121">Adding Direct from hello gallery</span></span>
2. <span data-ttu-id="c8b1c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8b1c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-hello-gallery"></a><span data-ttu-id="c8b1c-123">Agregar directamente desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c8b1c-123">Adding Direct from hello gallery</span></span>
<span data-ttu-id="c8b1c-124">integración de hello tooconfigure de directo en Azure AD, deberá tooadd directo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-124">tooconfigure hello integration of Direct into Azure AD, you need tooadd Direct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c8b1c-125">**tooadd directamente a través de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c8b1c-125">**tooadd Direct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8b1c-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c8b1c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c8b1c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c8b1c-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c8b1c-133">En el cuadro de búsqueda de hello, escriba **directa**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-133">In hello search box, type **Direct**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="c8b1c-135">En el panel de resultados de hello, seleccione **directa**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-135">In hello results panel, select **Direct**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c8b1c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8b1c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c8b1c-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Direct con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c8b1c-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c8b1c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en directo es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Direct is tooa user in Azure AD.</span></span> <span data-ttu-id="c8b1c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en toobe necesidades directo establecida.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-140">In other words, a link relationship between an Azure AD user and hello related user in Direct needs toobe established.</span></span>

<span data-ttu-id="c8b1c-141">En Direct, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-141">In Direct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c8b1c-142">prueba Azure AD y tooconfigure inicio de sesión único con Direct, necesita hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c8b1c-142">tooconfigure and test Azure AD single sign-on with Direct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c8b1c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c8b1c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8b1c-145">**[Crear un usuario de prueba directa](#creating-a-direct-test-user)**  -toohave un equivalente de Britta Simon en directo que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - toohave a counterpart of Britta Simon in Direct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c8b1c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8b1c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c8b1c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8b1c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c8b1c-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación directa.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="c8b1c-150">**tooconfigure inicio de sesión único en Azure AD con Direct, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c8b1c-150">**tooconfigure Azure AD single sign-on with Direct, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8b1c-151">En el portal de Azure, en Hola Hola **directa** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-151">In hello Azure portal, on hello **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c8b1c-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="c8b1c-155">En hello **directa del dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="c8b1c-155">On hello **Direct Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="c8b1c-157">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="c8b1c-157">In hello **Identifier** textbox, type hello URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="c8b1c-158">Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="c8b1c-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="c8b1c-160">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="c8b1c-160">In hello **Sign-on URL** textbox, type hello URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="c8b1c-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="c8b1c-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c8b1c-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c8b1c-165">tooconfigure inicio de sesión único en **directa** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico directo](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="c8b1c-165">tooconfigure single sign-on on **Direct** side, you need toosend hello downloaded **Metadata XML** too[Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="c8b1c-166">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c8b1c-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c8b1c-167">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c8b1c-168">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c8b1c-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c8b1c-169">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8b1c-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="c8b1c-170">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c8b1c-172">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c8b1c-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8b1c-173">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c8b1c-175">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c8b1c-177">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c8b1c-179">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c8b1c-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c8b1c-181">a.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-181">a.</span></span> <span data-ttu-id="c8b1c-182">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8b1c-183">b.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-183">b.</span></span> <span data-ttu-id="c8b1c-184">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c8b1c-185">c.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-185">c.</span></span> <span data-ttu-id="c8b1c-186">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c8b1c-187">d.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-187">d.</span></span> <span data-ttu-id="c8b1c-188">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="c8b1c-189">Creación de un usuario de prueba de Direct</span><span class="sxs-lookup"><span data-stu-id="c8b1c-189">Creating a Direct test user</span></span>

<span data-ttu-id="c8b1c-190">En esta sección, creará un usuario llamado Britta Simon en Direct.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="c8b1c-191">Trabajar con [equipo de soporte técnico directo](https://direct4b.com/ja/support.html#inquiry) para agregar usuarios de hello en plataforma directo Hola.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add hello users in hello Direct platform.</span></span> <span data-ttu-id="c8b1c-192">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c8b1c-193">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8b1c-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c8b1c-194">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooDirect.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirect.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c8b1c-196">**tooassign Britta Simon tooDirect, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c8b1c-196">**tooassign Britta Simon tooDirect, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8b1c-197">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c8b1c-199">En la lista de aplicaciones de hello, seleccione **directa**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-199">In hello applications list, select **Direct**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="c8b1c-201">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c8b1c-203">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-203">Click **Add** button.</span></span> <span data-ttu-id="c8b1c-204">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c8b1c-206">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c8b1c-207">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c8b1c-208">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c8b1c-209">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c8b1c-209">Testing single sign-on</span></span>

<span data-ttu-id="c8b1c-210">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="c8b1c-211">Si desea tootest en **modo a iniciado por IDP**:</span><span class="sxs-lookup"><span data-stu-id="c8b1c-211">If you wish tootest in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="c8b1c-212">Al hacer clic en hello **directa** Hola de mosaico en el Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour **directa** aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-212">When you click hello **Direct** tile in hello Access Panel, you should get automatically signed-on tooyour **Direct** application.</span></span>

2. <span data-ttu-id="c8b1c-213">Si desea tootest en **iniciado en modo SP**:</span><span class="sxs-lookup"><span data-stu-id="c8b1c-213">If you wish tootest in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="c8b1c-214">a.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-214">a.</span></span> <span data-ttu-id="c8b1c-215">Haga clic en hello **directa** el icono Panel de acceso de Hola y será la página de inicio de sesión de aplicaciones de toohello redirigida.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-215">Click on hello **Direct** tile in hello Access Panel and you will be redirected toohello application sign-on page.</span></span>

    <span data-ttu-id="c8b1c-216">b.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-216">b.</span></span> <span data-ttu-id="c8b1c-217">Entrada su `subdomain` en cuadro de texto hello muestra y presione '次へ (siguiente)' y se debe obtener automáticamente ha iniciado sesión tooyour **directa** aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8b1c-217">Input your `subdomain` in hello textbox displayed and press '次へ (Next)' and you should get automatically signed-on tooyour **Direct** application .</span></span>
    
<span data-ttu-id="c8b1c-218">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8b1c-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c8b1c-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c8b1c-219">Additional resources</span></span>

* [<span data-ttu-id="c8b1c-220">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8b1c-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8b1c-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c8b1c-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

