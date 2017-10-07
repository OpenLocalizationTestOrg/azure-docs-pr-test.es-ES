---
title: "Tutorial: integración de Azure Active Directory con EasyTerritory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y EasyTerritory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4f1e9fb4d615325f0d57bebaed955529d5dcd9b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="9061a-103">Tutorial: Integración de Azure Active Directory con EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="9061a-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="9061a-104">En este tutorial, aprenderá cómo toointegrate EasyTerritory con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9061a-104">In this tutorial, you learn how toointegrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9061a-105">Integración EasyTerritory con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9061a-105">Integrating EasyTerritory with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9061a-106">Puede controlar en Azure AD que tenga acceso tooEasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="9061a-106">You can control in Azure AD who has access tooEasyTerritory.</span></span>
- <span data-ttu-id="9061a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooEasyTerritory (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9061a-107">You can enable your users tooautomatically get signed-on tooEasyTerritory (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9061a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9061a-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="9061a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9061a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9061a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9061a-110">Prerequisites</span></span>

<span data-ttu-id="9061a-111">integración de Azure AD con EasyTerritory tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9061a-111">tooconfigure Azure AD integration with EasyTerritory, you need hello following items:</span></span>

- <span data-ttu-id="9061a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9061a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9061a-113">Una suscripción habilitada para el inicio de sesión único en EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="9061a-113">A EasyTerritory single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9061a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9061a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9061a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9061a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9061a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9061a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9061a-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9061a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9061a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9061a-118">Scenario description</span></span>
<span data-ttu-id="9061a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9061a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9061a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9061a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9061a-121">Agregar EasyTerritory desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9061a-121">Adding EasyTerritory from hello gallery</span></span>
2. <span data-ttu-id="9061a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9061a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-easyterritory-from-hello-gallery"></a><span data-ttu-id="9061a-123">Agregar EasyTerritory desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9061a-123">Adding EasyTerritory from hello gallery</span></span>
<span data-ttu-id="9061a-124">integración de hello tooconfigure de EasyTerritory en Azure AD, deberá tooadd EasyTerritory de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9061a-124">tooconfigure hello integration of EasyTerritory into Azure AD, you need tooadd EasyTerritory from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9061a-125">**tooadd EasyTerritory de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9061a-125">**tooadd EasyTerritory from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9061a-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9061a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="9061a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9061a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9061a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9061a-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="9061a-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9061a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="9061a-133">En el cuadro de búsqueda de hello, escriba **EasyTerritory**, seleccione **EasyTerritory** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9061a-133">In hello search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button tooadd hello application.</span></span>

    ![EasyTerritory en la lista de resultados de Hola](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9061a-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="9061a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9061a-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con EasyTerritory con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9061a-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9061a-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en EasyTerritory es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9061a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EasyTerritory is tooa user in Azure AD.</span></span> <span data-ttu-id="9061a-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en EasyTerritory debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9061a-138">In other words, a link relationship between an Azure AD user and hello related user in EasyTerritory needs toobe established.</span></span>

<span data-ttu-id="9061a-139">En EasyTerritory, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9061a-139">In EasyTerritory, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9061a-140">tooconfigure y prueba de inicio de sesión único en Azure AD con EasyTerritory, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9061a-140">tooconfigure and test Azure AD single sign-on with EasyTerritory, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9061a-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9061a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9061a-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9061a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9061a-143">**[Crear un usuario de prueba EasyTerritory](#create-a-easyterritory-test-user) ** -toohave un equivalente de Britta Simon en EasyTerritory que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9061a-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - toohave a counterpart of Britta Simon in EasyTerritory that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9061a-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9061a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9061a-145">**[Probar el inicio de sesión único](#test-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9061a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9061a-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9061a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9061a-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="9061a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EasyTerritory application.</span></span>

<span data-ttu-id="9061a-148">**inicio de sesión único en Azure AD tooconfigure con EasyTerritory, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9061a-148">**tooconfigure Azure AD single sign-on with EasyTerritory, perform hello following steps:**</span></span>

1. <span data-ttu-id="9061a-149">En el portal de Azure, en Hola Hola **EasyTerritory** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9061a-149">In hello Azure portal, on hello **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="9061a-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9061a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_samlbase.png)

3. <span data-ttu-id="9061a-153">En hello **EasyTerritory dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea que el modo de aplicación de hello tooconfigure en IDP iniciado:</span><span class="sxs-lookup"><span data-stu-id="9061a-153">On hello **EasyTerritory Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url.png)

    <span data-ttu-id="9061a-155">a.</span><span class="sxs-lookup"><span data-stu-id="9061a-155">a.</span></span> <span data-ttu-id="9061a-156">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://apps.easyterritory.com/<tenant id>/dev/`</span><span class="sxs-lookup"><span data-stu-id="9061a-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span></span>

    <span data-ttu-id="9061a-157">b.</span><span class="sxs-lookup"><span data-stu-id="9061a-157">b.</span></span> <span data-ttu-id="9061a-158">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span><span class="sxs-lookup"><span data-stu-id="9061a-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span></span>

4. <span data-ttu-id="9061a-159">Comprobar **mostrar avanzadas de configuración de direcciones URL** y realizar Hola siguiendo el paso si desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="9061a-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url1.png)

    <span data-ttu-id="9061a-161">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.easyterritory.com/`</span><span class="sxs-lookup"><span data-stu-id="9061a-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.easyterritory.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9061a-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9061a-162">These values are not real.</span></span> <span data-ttu-id="9061a-163">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9061a-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9061a-164">Póngase en contacto con [equipo de soporte técnico de cliente de EasyTerritory](mailto:sales@easyterritory.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="9061a-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) tooget these values.</span></span> 

5. <span data-ttu-id="9061a-165">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9061a-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_certificate.png) 

6. <span data-ttu-id="9061a-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9061a-167">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9061a-169">tooconfigure inicio de sesión único en **EasyTerritory** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de EasyTerritory](mailto:sales@easyterritory.com).</span><span class="sxs-lookup"><span data-stu-id="9061a-169">tooconfigure single sign-on on **EasyTerritory** side, you need toosend hello downloaded **Metadata XML** too[EasyTerritory support team](mailto:sales@easyterritory.com).</span></span> <span data-ttu-id="9061a-170">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="9061a-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9061a-171">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9061a-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9061a-172">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9061a-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9061a-173">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9061a-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9061a-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9061a-174">Create an Azure AD test user</span></span>

<span data-ttu-id="9061a-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9061a-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="9061a-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9061a-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9061a-178">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="9061a-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9061a-180">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9061a-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9061a-182">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9061a-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9061a-184">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9061a-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9061a-186">a.</span><span class="sxs-lookup"><span data-stu-id="9061a-186">a.</span></span> <span data-ttu-id="9061a-187">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9061a-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9061a-188">b.</span><span class="sxs-lookup"><span data-stu-id="9061a-188">b.</span></span> <span data-ttu-id="9061a-189">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9061a-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="9061a-190">c.</span><span class="sxs-lookup"><span data-stu-id="9061a-190">c.</span></span> <span data-ttu-id="9061a-191">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="9061a-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="9061a-192">d.</span><span class="sxs-lookup"><span data-stu-id="9061a-192">d.</span></span> <span data-ttu-id="9061a-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9061a-193">Click **Create**.</span></span>
 
### <a name="create-a-easyterritory-test-user"></a><span data-ttu-id="9061a-194">Creación de un usuario de prueba de EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="9061a-194">Create a EasyTerritory test user</span></span>

<span data-ttu-id="9061a-195">En esta sección, creará una usuaria llamada Britta Simon en EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="9061a-195">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="9061a-196">Trabaje con [equipo de soporte técnico de EasyTerritory](mailto:sales@easyterritory.com) a los usuarios de tooadd hello en la plataforma de EasyTerritory Hola.</span><span class="sxs-lookup"><span data-stu-id="9061a-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) tooadd hello users in hello EasyTerritory platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9061a-197">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9061a-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9061a-198">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooEasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="9061a-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEasyTerritory.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="9061a-200">**tooassign Britta Simon tooEasyTerritory, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9061a-200">**tooassign Britta Simon tooEasyTerritory, perform hello following steps:**</span></span>

1. <span data-ttu-id="9061a-201">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9061a-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9061a-203">En la lista de aplicaciones de hello, seleccione **EasyTerritory**.</span><span class="sxs-lookup"><span data-stu-id="9061a-203">In hello applications list, select **EasyTerritory**.</span></span>

    ![vínculo de EasyTerritory Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_app.png)  

3. <span data-ttu-id="9061a-205">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9061a-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="9061a-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9061a-207">Click **Add** button.</span></span> <span data-ttu-id="9061a-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9061a-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="9061a-210">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9061a-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9061a-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9061a-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9061a-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9061a-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9061a-213">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="9061a-213">Test single sign-on</span></span>

<span data-ttu-id="9061a-214">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9061a-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9061a-215">Al hacer clic en icono de EasyTerritory Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour EasyTerritory aplicación.</span><span class="sxs-lookup"><span data-stu-id="9061a-215">When you click hello EasyTerritory tile in hello Access Panel, you should get automatically signed-on tooyour EasyTerritory application.</span></span>
<span data-ttu-id="9061a-216">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9061a-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9061a-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9061a-217">Additional resources</span></span>

* [<span data-ttu-id="9061a-218">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9061a-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9061a-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9061a-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)




<!--Image references-->

[1]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png

