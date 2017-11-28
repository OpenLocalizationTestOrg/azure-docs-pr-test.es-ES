---
title: "Tutorial: integración de Azure Active Directory con TigerText Secure Messenger | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y TigerText seguros Messenger."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: a3d7bb9598658c75c567c15751740d885fe4fc27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="8f783-103">Tutorial: integración de Azure Active Directory con TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="8f783-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="8f783-104">En este tutorial, aprenderá cómo toointegrate TigerText seguro Messenger con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f783-104">In this tutorial, you learn how toointegrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f783-105">Integración TigerText seguros Messenger con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8f783-105">Integrating TigerText Secure Messenger with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8f783-106">Puede controlar en Azure AD que tenga acceso tooTigerText Messenger segura</span><span class="sxs-lookup"><span data-stu-id="8f783-106">You can control in Azure AD who has access tooTigerText Secure Messenger</span></span>
- <span data-ttu-id="8f783-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTigerText seguros Messenger (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f783-107">You can enable your users tooautomatically get signed-on tooTigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f783-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8f783-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8f783-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f783-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f783-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8f783-110">Prerequisites</span></span>

<span data-ttu-id="8f783-111">tooconfigure integración de Azure AD con TigerText seguros Messenger, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8f783-111">tooconfigure Azure AD integration with TigerText Secure Messenger, you need hello following items:</span></span>

- <span data-ttu-id="8f783-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f783-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f783-113">Una suscripción habilitada para el inicio de sesión único en TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="8f783-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f783-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8f783-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f783-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8f783-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f783-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8f783-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f783-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f783-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f783-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8f783-118">Scenario description</span></span>
<span data-ttu-id="8f783-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8f783-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f783-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8f783-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f783-121">Agregar a TigerText seguros Messenger desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="8f783-121">Add TigerText Secure Messenger from hello gallery</span></span>
2. <span data-ttu-id="8f783-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f783-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-hello-gallery"></a><span data-ttu-id="8f783-123">Agregar a TigerText seguros Messenger desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="8f783-123">Add TigerText Secure Messenger from hello gallery</span></span>
<span data-ttu-id="8f783-124">integración de hello tooconfigure de TigerText proteger Messenger en Azure AD, deberá tooadd TigerText seguros Messenger en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="8f783-124">tooconfigure hello integration of TigerText Secure Messenger into Azure AD, you need tooadd TigerText Secure Messenger from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8f783-125">**tooadd TigerText seguros Messenger desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8f783-125">**tooadd TigerText Secure Messenger from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f783-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8f783-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8f783-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8f783-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8f783-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8f783-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8f783-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8f783-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8f783-133">En el cuadro de búsqueda de hello, escriba **TigerText seguros Messenger**, seleccione **TigerText seguros Messenger** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8f783-133">In hello search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Incorporación desde la galería](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8f783-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f783-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8f783-136">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con TigerText Secure Messenger con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8f783-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8f783-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TigerText seguros Messenger es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f783-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TigerText Secure Messenger is tooa user in Azure AD.</span></span> <span data-ttu-id="8f783-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TigerText seguros Messenger debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8f783-138">In other words, a link relationship between an Azure AD user and hello related user in TigerText Secure Messenger needs toobe established.</span></span>

<span data-ttu-id="8f783-139">En Messenger seguros TigerText, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f783-139">In TigerText Secure Messenger, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8f783-140">tooconfigure y prueba de inicio de sesión único en Azure AD con TigerText seguros Messenger, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8f783-140">tooconfigure and test Azure AD single sign-on with TigerText Secure Messenger, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8f783-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8f783-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8f783-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f783-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f783-143">**[Crear un usuario de prueba de TigerText proteger Messenger](#create-a-tigertext-secure-messenger-test-user)**  -toohave un equivalente de Britta Simon en TigerText seguros Messenger es representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8f783-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - toohave a counterpart of Britta Simon in TigerText Secure Messenger that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f783-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8f783-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f783-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8f783-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8f783-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f783-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8f783-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación TigerText seguros Messenger.</span><span class="sxs-lookup"><span data-stu-id="8f783-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="8f783-148">**tooconfigure inicio de sesión único en Azure AD con Messenger seguros TigerText, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8f783-148">**tooconfigure Azure AD single sign-on with TigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f783-149">En el portal de Azure, en Hola Hola **TigerText seguros Messenger** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8f783-149">In hello Azure portal, on hello **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8f783-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8f783-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="8f783-153">En hello **TigerText dominio de Messenger seguros y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8f783-153">On hello **TigerText Secure Messenger Domain and URLs** section, perform hello following steps:</span></span>

    ![Sección Dominio y direcciones URL de TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="8f783-155">a.</span><span class="sxs-lookup"><span data-stu-id="8f783-155">a.</span></span> <span data-ttu-id="8f783-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL como:`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="8f783-156">In hello **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="8f783-157">b.</span><span class="sxs-lookup"><span data-stu-id="8f783-157">b.</span></span> <span data-ttu-id="8f783-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="8f783-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8f783-159">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="8f783-159">This value is not real.</span></span> <span data-ttu-id="8f783-160">Actualice este valor con hello identificador real.</span><span class="sxs-lookup"><span data-stu-id="8f783-160">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="8f783-161">Póngase en contacto con [equipo de soporte técnico de cliente de mensajería segura TigerText](mailTo:prosupport@tigertext.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="8f783-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="8f783-162">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8f783-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Sección Certificado de firma SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="8f783-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8f783-164">Click **Save** button.</span></span>

    ![Botón Guardar](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8f783-166">tooget inicio de sesión único configurado para la aplicación, póngase en contacto con [equipo de soporte técnico de TigerText proteger Messenger](mailTo:prosupport@tigertext.com) y proporcióneles hello **metadatos descargados**.</span><span class="sxs-lookup"><span data-stu-id="8f783-166">tooget single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them hello **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="8f783-167">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8f783-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8f783-168">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8f783-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8f783-169">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f783-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8f783-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f783-170">Create an Azure AD test user</span></span>
<span data-ttu-id="8f783-171">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8f783-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8f783-173">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8f783-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f783-174">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8f783-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f783-176">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8f783-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Usuarios y grupos -> Todos los usuarios](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f783-178">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f783-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f783-180">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8f783-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Cuadro de diálogo usuario](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f783-182">a.</span><span class="sxs-lookup"><span data-stu-id="8f783-182">a.</span></span> <span data-ttu-id="8f783-183">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f783-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f783-184">b.</span><span class="sxs-lookup"><span data-stu-id="8f783-184">b.</span></span> <span data-ttu-id="8f783-185">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8f783-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f783-186">c.</span><span class="sxs-lookup"><span data-stu-id="8f783-186">c.</span></span> <span data-ttu-id="8f783-187">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8f783-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8f783-188">d.</span><span class="sxs-lookup"><span data-stu-id="8f783-188">d.</span></span> <span data-ttu-id="8f783-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8f783-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="8f783-190">Creación de un usuario de prueba de TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="8f783-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="8f783-191">En esta sección, creará un usuario llamado Britta Simon en TigerText.</span><span class="sxs-lookup"><span data-stu-id="8f783-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="8f783-192">Póngase en contacto demasiado[equipo de soporte técnico de cliente de mensajería segura TigerText](mailTo:prosupport@tigertext.com) a los usuarios de tooadd hello en la plataforma de TigerText Hola.</span><span class="sxs-lookup"><span data-stu-id="8f783-192">Please reach out too[TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooadd hello users in hello TigerText platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8f783-193">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f783-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8f783-194">En esta sección, habilitar Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTigerText Messenger seguros.</span><span class="sxs-lookup"><span data-stu-id="8f783-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTigerText Secure Messenger.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8f783-196">**tooassign Britta Simon tooTigerText Messenger seguros, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8f783-196">**tooassign Britta Simon tooTigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f783-197">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8f783-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8f783-199">En la lista de aplicaciones de hello, seleccione **TigerText seguros Messenger**.</span><span class="sxs-lookup"><span data-stu-id="8f783-199">In hello applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger en la lista de aplicaciones](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="8f783-201">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8f783-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8f783-203">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8f783-203">Click **Add** button.</span></span> <span data-ttu-id="8f783-204">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8f783-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8f783-206">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f783-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8f783-207">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8f783-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f783-208">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8f783-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8f783-209">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="8f783-209">Test single sign-on</span></span>

<span data-ttu-id="8f783-210">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8f783-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8f783-211">Al hacer clic en icono de TigerText Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour TigerText aplicación.</span><span class="sxs-lookup"><span data-stu-id="8f783-211">When you click hello TigerText tile in hello Access Panel, you should get automatically signed-on tooyour TigerText application.</span></span> <span data-ttu-id="8f783-212">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8f783-212">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f783-213">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8f783-213">Additional resources</span></span>

* [<span data-ttu-id="8f783-214">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f783-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f783-215">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8f783-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

