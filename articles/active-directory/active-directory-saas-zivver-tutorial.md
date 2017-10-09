---
title: "Tutorial: integración de Azure Active Directory con ZIVVER | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ZIVVER."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 64cb7ea0-df6c-4963-84d8-6f435980e2de
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 0928abcc4dcbd97b892298f4919c8d44e1a058a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zivver"></a><span data-ttu-id="59e6b-103">Tutorial: integración de Azure Active Directory con ZIVVER</span><span class="sxs-lookup"><span data-stu-id="59e6b-103">Tutorial: Azure Active Directory integration with ZIVVER</span></span>

<span data-ttu-id="59e6b-104">En este tutorial, aprenderá cómo toointegrate ZIVVER con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59e6b-104">In this tutorial, you learn how toointegrate ZIVVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59e6b-105">Integración ZIVVER con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="59e6b-105">Integrating ZIVVER with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="59e6b-106">Puede controlar en Azure AD que tenga acceso tooZIVVER.</span><span class="sxs-lookup"><span data-stu-id="59e6b-106">You can control in Azure AD who has access tooZIVVER.</span></span>
- <span data-ttu-id="59e6b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZIVVER (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59e6b-107">You can enable your users tooautomatically get signed-on tooZIVVER (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="59e6b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="59e6b-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="59e6b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="59e6b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59e6b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="59e6b-110">Prerequisites</span></span>

<span data-ttu-id="59e6b-111">integración de Azure AD con ZIVVER tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="59e6b-111">tooconfigure Azure AD integration with ZIVVER, you need hello following items:</span></span>

- <span data-ttu-id="59e6b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59e6b-113">Una suscripción habilitada para el inicio de sesión único en ZIVVER</span><span class="sxs-lookup"><span data-stu-id="59e6b-113">A ZIVVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59e6b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="59e6b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59e6b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="59e6b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59e6b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="59e6b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59e6b-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59e6b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59e6b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="59e6b-118">Scenario description</span></span>
<span data-ttu-id="59e6b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="59e6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59e6b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="59e6b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59e6b-121">Agregar ZIVVER desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="59e6b-121">Adding ZIVVER from hello gallery</span></span>
2. <span data-ttu-id="59e6b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e6b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zivver-from-hello-gallery"></a><span data-ttu-id="59e6b-123">Agregar ZIVVER desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="59e6b-123">Adding ZIVVER from hello gallery</span></span>
<span data-ttu-id="59e6b-124">integración de hello tooconfigure de ZIVVER en Azure AD, deberá tooadd ZIVVER de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="59e6b-124">tooconfigure hello integration of ZIVVER into Azure AD, you need tooadd ZIVVER from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="59e6b-125">**tooadd ZIVVER de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="59e6b-125">**tooadd ZIVVER from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e6b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="59e6b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="59e6b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="59e6b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="59e6b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="59e6b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="59e6b-133">En el cuadro de búsqueda de hello, escriba **ZIVVER**, seleccione **ZIVVER** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="59e6b-133">In hello search box, type **ZIVVER**, select **ZIVVER** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ZIVVER en la lista de resultados de Hola](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="59e6b-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e6b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="59e6b-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ZIVVER con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="59e6b-136">In this section, you configure and test Azure AD single sign-on with ZIVVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="59e6b-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ZIVVER es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59e6b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ZIVVER is tooa user in Azure AD.</span></span> <span data-ttu-id="59e6b-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ZIVVER debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="59e6b-138">In other words, a link relationship between an Azure AD user and hello related user in ZIVVER needs toobe established.</span></span>

<span data-ttu-id="59e6b-139">En ZIVVER, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="59e6b-139">In ZIVVER, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="59e6b-140">tooconfigure y prueba de inicio de sesión único en Azure AD con ZIVVER, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="59e6b-140">tooconfigure and test Azure AD single sign-on with ZIVVER, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="59e6b-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="59e6b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="59e6b-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59e6b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59e6b-143">**[Crear un usuario de prueba ZIVVER](#create-a-zivver-test-user)**  -toohave un equivalente de Britta Simon en ZIVVER que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="59e6b-143">**[Create a ZIVVER test user](#create-a-zivver-test-user)** - toohave a counterpart of Britta Simon in ZIVVER that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="59e6b-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="59e6b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59e6b-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="59e6b-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="59e6b-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e6b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="59e6b-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="59e6b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ZIVVER application.</span></span>

<span data-ttu-id="59e6b-148">**inicio de sesión único en Azure AD tooconfigure con ZIVVER, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="59e6b-148">**tooconfigure Azure AD single sign-on with ZIVVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e6b-149">En el portal de Azure, en Hola Hola **ZIVVER** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-149">In hello Azure portal, on hello **ZIVVER** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="59e6b-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="59e6b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_samlbase.png)

3. <span data-ttu-id="59e6b-153">En hello **ZIVVER dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="59e6b-153">On hello **ZIVVER Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de ZIVVER](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_url.png)

    <span data-ttu-id="59e6b-155">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://app.zivver.com/SAML/Zivver`</span><span class="sxs-lookup"><span data-stu-id="59e6b-155">In hello **Identifier** textbox, type hello URL: `https://app.zivver.com/SAML/Zivver`</span></span>

4. <span data-ttu-id="59e6b-156">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="59e6b-156">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_certificate.png) 

5. <span data-ttu-id="59e6b-158">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="59e6b-158">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-zivver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="59e6b-160">tooconfigure inicio de sesión único en **ZIVVER** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico ZIVVER](https://support.zivver.com).</span><span class="sxs-lookup"><span data-stu-id="59e6b-160">tooconfigure single sign-on on **ZIVVER** side, you need toosend hello downloaded **Metadata XML** too[ZIVVER support team](https://support.zivver.com).</span></span> <span data-ttu-id="59e6b-161">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="59e6b-161">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="59e6b-162">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="59e6b-162">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="59e6b-163">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="59e6b-163">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="59e6b-164">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59e6b-164">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="59e6b-165">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e6b-165">Create an Azure AD test user</span></span>

<span data-ttu-id="59e6b-166">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="59e6b-166">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="59e6b-168">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="59e6b-168">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e6b-169">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="59e6b-169">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-zivver-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="59e6b-171">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-171">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-zivver-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="59e6b-173">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="59e6b-173">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-zivver-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="59e6b-175">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="59e6b-175">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-zivver-tutorial/create_aaduser_04.png)

    <span data-ttu-id="59e6b-177">a.</span><span class="sxs-lookup"><span data-stu-id="59e6b-177">a.</span></span> <span data-ttu-id="59e6b-178">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-178">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59e6b-179">b.</span><span class="sxs-lookup"><span data-stu-id="59e6b-179">b.</span></span> <span data-ttu-id="59e6b-180">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59e6b-180">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="59e6b-181">c.</span><span class="sxs-lookup"><span data-stu-id="59e6b-181">c.</span></span> <span data-ttu-id="59e6b-182">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="59e6b-182">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="59e6b-183">d.</span><span class="sxs-lookup"><span data-stu-id="59e6b-183">d.</span></span> <span data-ttu-id="59e6b-184">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-184">Click **Create**.</span></span>
  
### <a name="create-a-zivver-test-user"></a><span data-ttu-id="59e6b-185">Creación de un usuario de prueba de ZIVVER</span><span class="sxs-lookup"><span data-stu-id="59e6b-185">Create a ZIVVER test user</span></span>

<span data-ttu-id="59e6b-186">En esta sección, creará un usuario llamado Britta Simon en ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="59e6b-186">In this section, you create a user called Britta Simon in ZIVVER.</span></span> <span data-ttu-id="59e6b-187">Trabajar con [equipo de soporte técnico ZIVVER](https://support.zivver.com) a los usuarios de tooadd hello en la plataforma ZIVVER Hola.</span><span class="sxs-lookup"><span data-stu-id="59e6b-187">Work with [ZIVVER support team](https://support.zivver.com) tooadd hello users in hello ZIVVER platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="59e6b-188">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e6b-188">Assign hello Azure AD test user</span></span>

<span data-ttu-id="59e6b-189">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooZIVVER.</span><span class="sxs-lookup"><span data-stu-id="59e6b-189">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZIVVER.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="59e6b-191">**tooassign Britta Simon tooZIVVER, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="59e6b-191">**tooassign Britta Simon tooZIVVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e6b-192">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-192">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="59e6b-194">En la lista de aplicaciones de hello, seleccione **ZIVVER**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-194">In hello applications list, select **ZIVVER**.</span></span>

    ![vínculo ZIVVER Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_app.png)  

3. <span data-ttu-id="59e6b-196">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-196">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="59e6b-198">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-198">Click **Add** button.</span></span> <span data-ttu-id="59e6b-199">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-199">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="59e6b-201">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="59e6b-201">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="59e6b-202">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-202">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59e6b-203">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="59e6b-203">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="59e6b-204">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="59e6b-204">Test single sign-on</span></span>

<span data-ttu-id="59e6b-205">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="59e6b-205">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="59e6b-206">Al hacer clic en hello ZIVVER el icono Panel de acceso de hello, deberá obtener la aplicación de ZIVVER tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="59e6b-206">When you click hello ZIVVER tile in hello Access Panel, you should get automatically signed-on tooyour ZIVVER application.</span></span>
<span data-ttu-id="59e6b-207">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59e6b-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="59e6b-208">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="59e6b-208">Additional resources</span></span>

* [<span data-ttu-id="59e6b-209">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59e6b-209">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59e6b-210">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59e6b-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_203.png

