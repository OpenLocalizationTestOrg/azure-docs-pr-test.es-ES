---
title: "Tutorial: Integración de Azure Active Directory con CS Stars | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y CS estrellas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5704d151-afb8-40a4-b286-8bacd4f279ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: d84533e8a7e9bca2f7bdf4be7f3050bca2f18496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cs-stars"></a><span data-ttu-id="b42cf-103">Tutorial: Integración de Azure Active Directory con CS Stars</span><span class="sxs-lookup"><span data-stu-id="b42cf-103">Tutorial: Azure Active Directory integration with CS Stars</span></span>

<span data-ttu-id="b42cf-104">En este tutorial, aprenderá cómo toointegrate CS estrellas con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b42cf-104">In this tutorial, you learn how toointegrate CS Stars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b42cf-105">Integración CS estrellas con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b42cf-105">Integrating CS Stars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b42cf-106">Puede controlar en Azure AD que tenga acceso tooCS estrellas</span><span class="sxs-lookup"><span data-stu-id="b42cf-106">You can control in Azure AD who has access tooCS Stars</span></span>
- <span data-ttu-id="b42cf-107">Puede habilitar la tooautomatically a los usuarios obtener estrellas ha iniciado sesión tooCS (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b42cf-107">You can enable your users tooautomatically get signed-on tooCS Stars (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b42cf-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b42cf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b42cf-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b42cf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b42cf-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b42cf-110">Prerequisites</span></span>

<span data-ttu-id="b42cf-111">tooconfigure integración de Azure AD con CS estrellas, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b42cf-111">tooconfigure Azure AD integration with CS Stars, you need hello following items:</span></span>

- <span data-ttu-id="b42cf-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b42cf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b42cf-113">Una suscripción habilitada para el inicio de sesión único en CS Stars</span><span class="sxs-lookup"><span data-stu-id="b42cf-113">A CS Stars single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b42cf-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b42cf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b42cf-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b42cf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b42cf-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b42cf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b42cf-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b42cf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b42cf-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b42cf-118">Scenario description</span></span>
<span data-ttu-id="b42cf-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b42cf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b42cf-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="b42cf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b42cf-121">Agregar CS estrellas de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b42cf-121">Adding CS Stars from hello gallery</span></span>
2. <span data-ttu-id="b42cf-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b42cf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cs-stars-from-hello-gallery"></a><span data-ttu-id="b42cf-123">Agregar CS estrellas de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b42cf-123">Adding CS Stars from hello gallery</span></span>
<span data-ttu-id="b42cf-124">integración de hello tooconfigure de CS estrellas en Azure AD, deberá tooadd CS estrellas de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="b42cf-124">tooconfigure hello integration of CS Stars into Azure AD, you need tooadd CS Stars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b42cf-125">**tooadd CS estrellas de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b42cf-125">**tooadd CS Stars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b42cf-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b42cf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b42cf-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b42cf-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b42cf-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b42cf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b42cf-133">En el cuadro de búsqueda de hello, escriba **estrellas CS**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-133">In hello search box, type **CS Stars**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_search.png)

5. <span data-ttu-id="b42cf-135">En el panel de resultados de hello, seleccione **CS estrellas**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b42cf-135">In hello results panel, select **CS Stars**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b42cf-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b42cf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b42cf-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con CS Stars con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b42cf-138">In this section, you configure and test Azure AD single sign-on with CS Stars based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b42cf-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en CS estrellas es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b42cf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CS Stars is tooa user in Azure AD.</span></span> <span data-ttu-id="b42cf-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en CS estrellas debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="b42cf-140">In other words, a link relationship between an Azure AD user and hello related user in CS Stars needs toobe established.</span></span>

<span data-ttu-id="b42cf-141">En CS estrellas, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b42cf-141">In CS Stars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b42cf-142">tooconfigure y prueba de inicio de sesión único en Azure AD con CS estrellas, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b42cf-142">tooconfigure and test Azure AD single sign-on with CS Stars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b42cf-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="b42cf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b42cf-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b42cf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b42cf-145">**[Crear un usuario de prueba de estrellas CS](#creating-a-cs-stars-test-user) ** -toohave un equivalente de Britta Simon en CS estrellas que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="b42cf-145">**[Creating a CS Stars test user](#creating-a-cs-stars-test-user)** - toohave a counterpart of Britta Simon in CS Stars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b42cf-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b42cf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b42cf-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b42cf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b42cf-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b42cf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b42cf-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de CS estrellas.</span><span class="sxs-lookup"><span data-stu-id="b42cf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CS Stars application.</span></span>

<span data-ttu-id="b42cf-150">**inicio de sesión único en tooconfigure Azure AD con CS estrellas, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b42cf-150">**tooconfigure Azure AD single sign-on with CS Stars, perform hello following steps:**</span></span>

1. <span data-ttu-id="b42cf-151">En el portal de Azure, en Hola Hola **CS estrellas** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-151">In hello Azure portal, on hello **CS Stars** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b42cf-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b42cf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_samlbase.png)

3. <span data-ttu-id="b42cf-155">En hello **CS estrellas dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b42cf-155">On hello **CS Stars Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_url.png)

    <span data-ttu-id="b42cf-157">a.</span><span class="sxs-lookup"><span data-stu-id="b42cf-157">a.</span></span> <span data-ttu-id="b42cf-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="b42cf-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span></span>

    <span data-ttu-id="b42cf-159">b.</span><span class="sxs-lookup"><span data-stu-id="b42cf-159">b.</span></span> <span data-ttu-id="b42cf-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.csstars.com/enterprise/`</span><span class="sxs-lookup"><span data-stu-id="b42cf-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.csstars.com/enterprise/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b42cf-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="b42cf-161">These values are not real.</span></span> <span data-ttu-id="b42cf-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="b42cf-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b42cf-163">Póngase en contacto con [equipo de soporte técnico de cliente de estrellas CS](http://www.marshclearsight.com/support/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="b42cf-163">Contact [CS Stars Client support team](http://www.marshclearsight.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="b42cf-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b42cf-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_certificate.png) 

5. <span data-ttu-id="b42cf-166">Haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-166">Click **Save** button.</span></span>

    <span data-ttu-id="b42cf-167">![Configuración del inicio de sesión único](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="b42cf-167">![Configure Single Sign-On](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span></span>
6. <span data-ttu-id="b42cf-168">tooconfigure inicio de sesión único en **CS estrellas** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de estrellas CS](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="b42cf-168">tooconfigure single sign-on on **CS Stars** side, you need toosend hello downloaded **Metadata XML** too[CS Stars support team](http://www.marshclearsight.com/support/).</span></span> 
<CE>

> [!TIP]
> <span data-ttu-id="b42cf-169">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="b42cf-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b42cf-170">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="b42cf-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b42cf-171">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b42cf-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b42cf-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b42cf-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="b42cf-173">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="b42cf-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b42cf-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b42cf-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b42cf-176">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b42cf-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b42cf-178">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b42cf-180">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b42cf-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b42cf-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="b42cf-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b42cf-184">a.</span><span class="sxs-lookup"><span data-stu-id="b42cf-184">a.</span></span> <span data-ttu-id="b42cf-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b42cf-186">b.</span><span class="sxs-lookup"><span data-stu-id="b42cf-186">b.</span></span> <span data-ttu-id="b42cf-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b42cf-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b42cf-188">c.</span><span class="sxs-lookup"><span data-stu-id="b42cf-188">c.</span></span> <span data-ttu-id="b42cf-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b42cf-190">d.</span><span class="sxs-lookup"><span data-stu-id="b42cf-190">d.</span></span> <span data-ttu-id="b42cf-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-191">Click **Create**.</span></span>
 
### <a name="creating-a-cs-stars-test-user"></a><span data-ttu-id="b42cf-192">Creación de un usuario de prueba de CS Stars</span><span class="sxs-lookup"><span data-stu-id="b42cf-192">Creating a CS Stars test user</span></span>

<span data-ttu-id="b42cf-193">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en CS estrellas.</span><span class="sxs-lookup"><span data-stu-id="b42cf-193">hello objective of this section is toocreate a user called Britta Simon in CS Stars.</span></span>

<span data-ttu-id="b42cf-194">tooget un usuario creado en el CS estrellas, necesita toocontact su [equipo de soporte técnico de estrellas CS](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="b42cf-194">tooget a user created in CS Stars, you need toocontact your [CS Stars support team](http://www.marshclearsight.com/support/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b42cf-195">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b42cf-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b42cf-196">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCS estrellas.</span><span class="sxs-lookup"><span data-stu-id="b42cf-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCS Stars.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b42cf-198">**tooassign Britta Simon tooCS estrellas, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="b42cf-198">**tooassign Britta Simon tooCS Stars, perform hello following steps:**</span></span>

1. <span data-ttu-id="b42cf-199">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b42cf-201">En la lista de aplicaciones de hello, seleccione **estrellas CS**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-201">In hello applications list, select **CS Stars**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_app.png) 

3. <span data-ttu-id="b42cf-203">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b42cf-205">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-205">Click **Add** button.</span></span> <span data-ttu-id="b42cf-206">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b42cf-208">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="b42cf-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b42cf-209">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b42cf-210">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b42cf-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b42cf-211">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b42cf-211">Testing single sign-on</span></span>

<span data-ttu-id="b42cf-212">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b42cf-212">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="b42cf-213">Al hacer clic en hello CS estrellas disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación CS estrellas.</span><span class="sxs-lookup"><span data-stu-id="b42cf-213">When you click hello CS Stars tile in hello Access Panel, you should get automatically signed-on tooyour CS Stars application.</span></span>
 

## <a name="additional-resources"></a><span data-ttu-id="b42cf-214">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b42cf-214">Additional resources</span></span>

* [<span data-ttu-id="b42cf-215">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b42cf-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b42cf-216">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b42cf-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_203.png

