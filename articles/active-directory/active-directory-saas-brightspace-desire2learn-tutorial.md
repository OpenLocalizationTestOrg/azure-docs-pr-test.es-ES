---
title: "Tutorial: integración de Azure Active Directory con Brightspace by Desire2Learn | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Brightspace por Desire2Learn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 99d03dc50defcb291a651a5415e30baab39e1e77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="562f7-103">Tutorial: Integración de Azure Active Directory con Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="562f7-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>

<span data-ttu-id="562f7-104">En este tutorial, aprenderá cómo toointegrate Brightspace por Desire2Learn con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="562f7-104">In this tutorial, you learn how toointegrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="562f7-105">Integración de Brightspace por Desire2Learn con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="562f7-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="562f7-106">Puede controlar en Azure AD que tenga acceso tooBrightspace por Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="562f7-106">You can control in Azure AD who has access tooBrightspace by Desire2Learn</span></span>
- <span data-ttu-id="562f7-107">Puede habilitar la get ha iniciado sesión tooBrightspace de usuarios tooautomatically por Desire2Learn (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562f7-107">You can enable your users tooautomatically get signed-on tooBrightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="562f7-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="562f7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="562f7-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="562f7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="562f7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="562f7-110">Prerequisites</span></span>

<span data-ttu-id="562f7-111">integración de Azure AD con Brightspace por Desire2Learn tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="562f7-111">tooconfigure Azure AD integration with Brightspace by Desire2Learn, you need hello following items:</span></span>

- <span data-ttu-id="562f7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="562f7-113">Una suscripción habilitada para inicio de sesión único de Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="562f7-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="562f7-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="562f7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="562f7-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="562f7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="562f7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="562f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="562f7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="562f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="562f7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="562f7-118">Scenario description</span></span>
<span data-ttu-id="562f7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="562f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="562f7-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="562f7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="562f7-121">Agregar Brightspace por Desire2Learn desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="562f7-121">Adding Brightspace by Desire2Learn from hello gallery</span></span>
2. <span data-ttu-id="562f7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-brightspace-by-desire2learn-from-hello-gallery"></a><span data-ttu-id="562f7-123">Agregar Brightspace por Desire2Learn desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="562f7-123">Adding Brightspace by Desire2Learn from hello gallery</span></span>
<span data-ttu-id="562f7-124">integración de hello tooconfigure de Brightspace por Desire2Learn en Azure AD, deberá tooadd Brightspace por Desire2Learn de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="562f7-124">tooconfigure hello integration of Brightspace by Desire2Learn into Azure AD, you need tooadd Brightspace by Desire2Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="562f7-125">**tooadd Brightspace por Desire2Learn de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="562f7-125">**tooadd Brightspace by Desire2Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="562f7-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="562f7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="562f7-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="562f7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="562f7-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="562f7-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="562f7-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="562f7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="562f7-133">En el cuadro de búsqueda de hello, escriba **Brightspace por Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="562f7-133">In hello search box, type **Brightspace by Desire2Learn**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_search.png)

5. <span data-ttu-id="562f7-135">En el panel de resultados de hello, seleccione **Brightspace por Desire2Learn**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="562f7-135">In hello results panel, select **Brightspace by Desire2Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="562f7-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562f7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="562f7-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Brightspace by Desire2Learn con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="562f7-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="562f7-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Brightspace por Desire2Learn es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="562f7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Brightspace by Desire2Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="562f7-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Brightspace por Desire2Learn debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="562f7-140">In other words, a link relationship between an Azure AD user and hello related user in Brightspace by Desire2Learn needs toobe established.</span></span>

<span data-ttu-id="562f7-141">En Brightspace por Desire2Learn, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="562f7-141">In Brightspace by Desire2Learn, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="562f7-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Brightspace por Desire2Learn, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="562f7-142">tooconfigure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="562f7-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="562f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="562f7-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="562f7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="562f7-145">**[Crear un Brightspace por Desire2Learn prueba usuario](#creating-a-brightspace-by-desire2learn-test-user)**  -toohave un equivalente de Britta Simon en Brightspace por Desire2Learn que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="562f7-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - toohave a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="562f7-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="562f7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="562f7-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="562f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="562f7-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562f7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="562f7-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en Brightspace por Desire2Learn aplicación.</span><span class="sxs-lookup"><span data-stu-id="562f7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span></span>

<span data-ttu-id="562f7-150">**inicio de sesión único en Azure AD tooconfigure con Brightspace por Desire2Learn, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="562f7-150">**tooconfigure Azure AD single sign-on with Brightspace by Desire2Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="562f7-151">En el portal de Azure, en Hola Hola **Brightspace por Desire2Learn** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="562f7-151">In hello Azure portal, on hello **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="562f7-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="562f7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_samlbase.png)

3. <span data-ttu-id="562f7-155">En hello **Brightspace por Desire2Learn dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="562f7-155">On hello **Brightspace by Desire2Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_url.png)

    <span data-ttu-id="562f7-157">a.</span><span class="sxs-lookup"><span data-stu-id="562f7-157">a.</span></span> <span data-ttu-id="562f7-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="562f7-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.tenants.brightspace.com/samlLogin`|
    | `https://<companyname>.desire2learn.com/shibboleth-sp`|

    <span data-ttu-id="562f7-159">b.</span><span class="sxs-lookup"><span data-stu-id="562f7-159">b.</span></span> <span data-ttu-id="562f7-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span><span class="sxs-lookup"><span data-stu-id="562f7-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="562f7-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="562f7-161">These values are not real.</span></span> <span data-ttu-id="562f7-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="562f7-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="562f7-163">Póngase en contacto con [Brightspace por Desire2Learn equipo de soporte técnico](https://www.d2l.com/contact/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="562f7-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) tooget these values.</span></span>
 


4. <span data-ttu-id="562f7-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="562f7-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_certificate.png) 

5. <span data-ttu-id="562f7-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="562f7-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="562f7-168">inicio de sesión único en tooconfigure en **Brightspace por Desire2Learn** lado, necesita hello toosend descargado **Metadata XML** demasiado[Brightspace por Desire2Learn equipo de soporte técnico](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="562f7-168">tooconfigure single sign-on on **Brightspace by Desire2Learn** side, you need toosend hello downloaded **Metadata XML** too[Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="562f7-169">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="562f7-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="562f7-170">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="562f7-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="562f7-171">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="562f7-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="562f7-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="562f7-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="562f7-173">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="562f7-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="562f7-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="562f7-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="562f7-176">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="562f7-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="562f7-178">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="562f7-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="562f7-180">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="562f7-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="562f7-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="562f7-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="562f7-184">a.</span><span class="sxs-lookup"><span data-stu-id="562f7-184">a.</span></span> <span data-ttu-id="562f7-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="562f7-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="562f7-186">b.</span><span class="sxs-lookup"><span data-stu-id="562f7-186">b.</span></span> <span data-ttu-id="562f7-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="562f7-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="562f7-188">c.</span><span class="sxs-lookup"><span data-stu-id="562f7-188">c.</span></span> <span data-ttu-id="562f7-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="562f7-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="562f7-190">d.</span><span class="sxs-lookup"><span data-stu-id="562f7-190">d.</span></span> <span data-ttu-id="562f7-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="562f7-191">Click **Create**.</span></span>
 
### <a name="creating-a-brightspace-by-desire2learn-test-user"></a><span data-ttu-id="562f7-192">Creación de un usuario de prueba de Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="562f7-192">Creating a Brightspace by Desire2Learn test user</span></span>

<span data-ttu-id="562f7-193">En orden tooenable Azure AD a los usuarios toolog en Brightspace por Desire2Learn, se les deben aprovisionar en Brightspace por Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="562f7-193">In order tooenable Azure AD users toolog into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="562f7-194">En caso de hello de Brightspace por Desire2Learn, cuentas de usuario de hello debe toobe creado por la [Brightspace por Desire2Learn equipo de soporte técnico](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="562f7-194">In hello case of Brightspace by Desire2Learn, hello user accounts need toobe created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

>[!NOTE]
><span data-ttu-id="562f7-195">Puede usar cualquiera mediante la herramienta de creación de cuentas de usuario de Desire2Learn o las API proporcionadas por Brightspace por Desire2Learn tooprovision Azure Active Directory las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="562f7-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="562f7-196">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="562f7-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="562f7-197">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBrightspace por Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="562f7-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBrightspace by Desire2Learn.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="562f7-199">**tooassign Britta Simon tooBrightspace por Desire2Learn, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="562f7-199">**tooassign Britta Simon tooBrightspace by Desire2Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="562f7-200">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="562f7-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="562f7-202">En la lista de aplicaciones de hello, seleccione **Brightspace por Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="562f7-202">In hello applications list, select **Brightspace by Desire2Learn**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_app.png) 

3. <span data-ttu-id="562f7-204">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="562f7-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="562f7-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="562f7-206">Click **Add** button.</span></span> <span data-ttu-id="562f7-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="562f7-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="562f7-209">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="562f7-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="562f7-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="562f7-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="562f7-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="562f7-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="562f7-212">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="562f7-212">Testing single sign-on</span></span>

<span data-ttu-id="562f7-213">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="562f7-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="562f7-214">Al hacer clic en hello Brightspace por Desire2Learn mosaico Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Brightspace por Desire2Learn aplicación.</span><span class="sxs-lookup"><span data-stu-id="562f7-214">When you click hello Brightspace by Desire2Learn tile in hello Access Panel, you should get automatically signed-on tooyour Brightspace by Desire2Learn application.</span></span>
<span data-ttu-id="562f7-215">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="562f7-215">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="562f7-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="562f7-216">Additional resources</span></span>

* [<span data-ttu-id="562f7-217">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="562f7-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="562f7-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="562f7-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_203.png

