---
title: "Tutorial: Integración de Azure Active Directory con Greenhouse | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Greenhouse."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 1a7cdd00c4f2b15a1afc89522d79af22f4c5d866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="e2f3b-103">Tutorial: integración de Azure Active Directory con Greenhouse</span><span class="sxs-lookup"><span data-stu-id="e2f3b-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="e2f3b-104">En este tutorial, aprenderá cómo toointegrate efecto invernadero con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e2f3b-104">In this tutorial, you learn how toointegrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e2f3b-105">Integración efecto invernadero con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e2f3b-105">Integrating Greenhouse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e2f3b-106">Puede controlar en Azure AD que tenga acceso tooGreenhouse.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-106">You can control in Azure AD who has access tooGreenhouse.</span></span>
- <span data-ttu-id="e2f3b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooGreenhouse (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-107">You can enable your users tooautomatically get signed-on tooGreenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e2f3b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e2f3b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e2f3b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2f3b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e2f3b-110">Prerequisites</span></span>

<span data-ttu-id="e2f3b-111">integración de Azure AD con efecto invernadero tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e2f3b-111">tooconfigure Azure AD integration with Greenhouse, you need hello following items:</span></span>

- <span data-ttu-id="e2f3b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2f3b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e2f3b-113">Una suscripción habilitada para el inicio de sesión único en Greenhouse</span><span class="sxs-lookup"><span data-stu-id="e2f3b-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e2f3b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e2f3b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e2f3b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e2f3b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e2f3b-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e2f3b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e2f3b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e2f3b-118">Scenario description</span></span>
<span data-ttu-id="e2f3b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e2f3b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="e2f3b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e2f3b-121">Agregar efecto invernadero desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e2f3b-121">Adding Greenhouse from hello gallery</span></span>
2. <span data-ttu-id="e2f3b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2f3b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-hello-gallery"></a><span data-ttu-id="e2f3b-123">Agregar efecto invernadero desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e2f3b-123">Adding Greenhouse from hello gallery</span></span>
<span data-ttu-id="e2f3b-124">integración de hello tooconfigure de efecto invernadero en Azure AD, deberá tooadd efecto invernadero de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-124">tooconfigure hello integration of Greenhouse into Azure AD, you need tooadd Greenhouse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e2f3b-125">**tooadd efecto invernadero desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e2f3b-125">**tooadd Greenhouse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2f3b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="e2f3b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e2f3b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="e2f3b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="e2f3b-133">En el cuadro de búsqueda de hello, escriba **Greenhouse**, seleccione **Greenhouse** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-133">In hello search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Efecto invernadero en la lista de resultados de Hola](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e2f3b-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2f3b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e2f3b-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Greenhouse con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e2f3b-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e2f3b-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en efecto invernadero es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Greenhouse is tooa user in Azure AD.</span></span> <span data-ttu-id="e2f3b-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en efecto invernadero debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-138">In other words, a link relationship between an Azure AD user and hello related user in Greenhouse needs toobe established.</span></span>

<span data-ttu-id="e2f3b-139">En efecto invernadero, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-139">In Greenhouse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e2f3b-140">tooconfigure y prueba de inicio de sesión único en Azure AD con efecto invernadero, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e2f3b-140">tooconfigure and test Azure AD single sign-on with Greenhouse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e2f3b-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e2f3b-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e2f3b-143">**[Crear un usuario de prueba de Greenhouse](#create-a-greenhouse-test-user)**  -toohave un equivalente de Britta Simon en efecto invernadero que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - toohave a counterpart of Britta Simon in Greenhouse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e2f3b-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e2f3b-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e2f3b-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2f3b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e2f3b-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="e2f3b-148">**inicio de sesión único en tooconfigure Azure AD con efecto invernadero, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e2f3b-148">**tooconfigure Azure AD single sign-on with Greenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2f3b-149">En el portal de Azure, en Hola Hola **Greenhouse** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-149">In hello Azure portal, on hello **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="e2f3b-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="e2f3b-153">En hello **efecto invernadero dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e2f3b-153">On hello **Greenhouse Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Greenhouse](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="e2f3b-155">a.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-155">a.</span></span> <span data-ttu-id="e2f3b-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="e2f3b-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="e2f3b-157">b.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-157">b.</span></span> <span data-ttu-id="e2f3b-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="e2f3b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e2f3b-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-159">These values are not real.</span></span> <span data-ttu-id="e2f3b-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e2f3b-161">Póngase en contacto con [equipo de soporte técnico de Greenhouse cliente](https://www.greenhouse.io/contact) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) tooget these values.</span></span> 
 


4. <span data-ttu-id="e2f3b-162">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="e2f3b-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e2f3b-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e2f3b-166">tooconfigure inicio de sesión único en **Greenhouse** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de Greenhouse](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="e2f3b-166">tooconfigure single sign-on on **Greenhouse** side, you need toosend hello downloaded **Metadata XML** too[Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="e2f3b-167">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="e2f3b-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e2f3b-168">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e2f3b-169">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e2f3b-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e2f3b-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2f3b-170">Create an Azure AD test user</span></span>

<span data-ttu-id="e2f3b-171">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="e2f3b-173">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e2f3b-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2f3b-174">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e2f3b-176">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e2f3b-178">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e2f3b-180">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e2f3b-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e2f3b-182">a.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-182">a.</span></span> <span data-ttu-id="e2f3b-183">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e2f3b-184">b.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-184">b.</span></span> <span data-ttu-id="e2f3b-185">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e2f3b-186">c.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-186">c.</span></span> <span data-ttu-id="e2f3b-187">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e2f3b-188">d.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-188">d.</span></span> <span data-ttu-id="e2f3b-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="e2f3b-190">Creación de un usuario de prueba de Greenhouse</span><span class="sxs-lookup"><span data-stu-id="e2f3b-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="e2f3b-191">En orden tooenable toolog de los usuarios de Azure AD en Greenhouse, se les deben aprovisionar en Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-191">In order tooenable Azure AD users toolog into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="e2f3b-192">En caso de hello de Greenhouse, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-192">In hello case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e2f3b-193">Puede usar cualquier otro efecto invernadero herramienta cuentas de usuario creación o las API proporcionadas por efecto invernadero tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="e2f3b-194">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="e2f3b-194">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2f3b-195">Inicie sesión en tooyour **Greenhouse** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-195">Log in tooyour **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="e2f3b-196">En el menú de hello en la parte superior de hello, haga clic en **configurar**y, a continuación, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-196">In hello menu on hello top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="e2f3b-197">![Usuarios](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="e2f3b-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="e2f3b-198">Haga clic en **Nuevos usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="e2f3b-199">![Nuevo usuario](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="e2f3b-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="e2f3b-200">Hola **Agregar nuevo usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e2f3b-200">In hello **Add New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e2f3b-201">![Adición de un nuevo usuario](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Adición de un nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="e2f3b-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="e2f3b-202">a.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-202">a.</span></span> <span data-ttu-id="e2f3b-203">Hola **escribir correos electrónicos de usuario** cuadro de texto, dirección de correo electrónico de tipo hello de una cuenta válida de Azure Active Directory que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-203">In hello **Enter user emails** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision.</span></span>

   <span data-ttu-id="e2f3b-204">b.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-204">b.</span></span> <span data-ttu-id="e2f3b-205">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="e2f3b-206">los titulares de cuentas de Azure Active Directory Hola recibirá un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-206">hello Azure Active Directory account holders will receive an email including a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e2f3b-207">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2f3b-207">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e2f3b-208">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooGreenhouse.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGreenhouse.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="e2f3b-210">**tooassign Britta Simon tooGreenhouse, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e2f3b-210">**tooassign Britta Simon tooGreenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2f3b-211">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e2f3b-213">En la lista de aplicaciones de hello, seleccione **Greenhouse**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-213">In hello applications list, select **Greenhouse**.</span></span>

    ![vínculo de efecto invernadero Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="e2f3b-215">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="e2f3b-217">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-217">Click **Add** button.</span></span> <span data-ttu-id="e2f3b-218">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="e2f3b-220">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e2f3b-221">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e2f3b-222">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e2f3b-223">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="e2f3b-223">Test single sign-on</span></span>

<span data-ttu-id="e2f3b-224">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e2f3b-225">Al hacer clic en icono de efecto invernadero Hola Hola Panel de acceso, deberá obtener la aplicación de efecto invernadero tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="e2f3b-225">When you click hello Greenhouse tile in hello Access Panel, you should get automatically signed-on tooyour Greenhouse application.</span></span>
<span data-ttu-id="e2f3b-226">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e2f3b-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e2f3b-227">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e2f3b-227">Additional resources</span></span>

* [<span data-ttu-id="e2f3b-228">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2f3b-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2f3b-229">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e2f3b-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

