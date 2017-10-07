---
title: "Tutorial: integración de Azure Active Directory con Fuse | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y fusible."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 720ed8af0b5de1e3bee5a40353ca0ee661766864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="1fd7f-103">Tutorial: Integración de Azure Active Directory con Fuse</span><span class="sxs-lookup"><span data-stu-id="1fd7f-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="1fd7f-104">En este tutorial, aprenderá cómo toointegrate fusible con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1fd7f-104">In this tutorial, you learn how toointegrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1fd7f-105">Integración fusible con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1fd7f-105">Integrating Fuse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1fd7f-106">Puede controlar en Azure AD que tenga acceso tooFuse.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-106">You can control in Azure AD who has access tooFuse.</span></span>
- <span data-ttu-id="1fd7f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFuse (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-107">You can enable your users tooautomatically get signed-on tooFuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1fd7f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="1fd7f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1fd7f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fd7f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1fd7f-110">Prerequisites</span></span>

<span data-ttu-id="1fd7f-111">integración de Azure AD tooconfigure con fusible, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1fd7f-111">tooconfigure Azure AD integration with Fuse, you need hello following items:</span></span>

- <span data-ttu-id="1fd7f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fd7f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1fd7f-113">Una suscripción habilitada para el inicio de sesión único en Fuse</span><span class="sxs-lookup"><span data-stu-id="1fd7f-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1fd7f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1fd7f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1fd7f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1fd7f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1fd7f-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1fd7f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1fd7f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1fd7f-118">Scenario description</span></span>
<span data-ttu-id="1fd7f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1fd7f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="1fd7f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1fd7f-121">Agregar fusible de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1fd7f-121">Add Fuse from hello gallery</span></span>
2. <span data-ttu-id="1fd7f-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fd7f-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-hello-gallery"></a><span data-ttu-id="1fd7f-123">Agregar fusible de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1fd7f-123">Add Fuse from hello gallery</span></span>
<span data-ttu-id="1fd7f-124">integración de hello tooconfigure de fusible en Azure AD, deberá tooadd fusible de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-124">tooconfigure hello integration of Fuse into Azure AD, you need tooadd Fuse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1fd7f-125">**tooadd fusible de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1fd7f-125">**tooadd Fuse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1fd7f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="1fd7f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1fd7f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="1fd7f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="1fd7f-133">En el cuadro de búsqueda de hello, escriba **fusible**, seleccione **fusible** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-133">In hello search box, type **Fuse**, select **Fuse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Fusible en la lista de resultados de Hola](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1fd7f-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fd7f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1fd7f-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Fuse con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1fd7f-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1fd7f-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en fusible es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuse is tooa user in Azure AD.</span></span> <span data-ttu-id="1fd7f-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en fusible necesidades toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-138">In other words, a link relationship between an Azure AD user and hello related user in Fuse needs toobe established.</span></span>

<span data-ttu-id="1fd7f-139">En fusible, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-139">In Fuse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1fd7f-140">tooconfigure y prueba de inicio de sesión único en Azure AD con fusible, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1fd7f-140">tooconfigure and test Azure AD single sign-on with Fuse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1fd7f-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1fd7f-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1fd7f-143">**[Crear un usuario de prueba fusible](#create-a-fuse-test-user)**  -toohave un equivalente de Britta Simon en fusible que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - toohave a counterpart of Britta Simon in Fuse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1fd7f-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1fd7f-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1fd7f-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fd7f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1fd7f-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación fusible.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="1fd7f-148">**tooconfigure inicio de sesión único en Azure AD con fusible, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1fd7f-148">**tooconfigure Azure AD single sign-on with Fuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="1fd7f-149">En el portal de Azure, en Hola Hola **fusible** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-149">In hello Azure portal, on hello **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="1fd7f-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="1fd7f-153">En hello **fusible dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1fd7f-153">On hello **Fuse Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="1fd7f-155">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="1fd7f-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1fd7f-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-156">This value is not real.</span></span> <span data-ttu-id="1fd7f-157">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1fd7f-158">Póngase en contacto con [equipo de soporte técnico de cliente fusible](mailto:support@fusion-universal.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="1fd7f-159">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Raw)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-159">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="1fd7f-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1fd7f-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1fd7f-163">En hello **configuración fusible** sección, haga clic en **configurar fusible** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-163">On hello **Fuse Configuration** section, click **Configure Fuse** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1fd7f-164">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="1fd7f-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="1fd7f-166">tooget SSO configurado para la aplicación, póngase en contacto con [equipo de soporte técnico de fusible](mailto:support@fusion-universal.com) y proporcionarles siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="1fd7f-166">tooget SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with hello following:</span></span>

    * <span data-ttu-id="1fd7f-167">Hola descargado **archivo de certificado (Raw)**</span><span class="sxs-lookup"><span data-stu-id="1fd7f-167">hello downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="1fd7f-168">Hola **SAML Single Sign-On dirección URL del servicio**</span><span class="sxs-lookup"><span data-stu-id="1fd7f-168">hello **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="1fd7f-169">Hola **Id. de entidad de SAML**</span><span class="sxs-lookup"><span data-stu-id="1fd7f-169">hello **SAML Entity ID**</span></span>
    * <span data-ttu-id="1fd7f-170">Hola **dirección URL de cierre de sesión**</span><span class="sxs-lookup"><span data-stu-id="1fd7f-170">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="1fd7f-171">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="1fd7f-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1fd7f-172">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1fd7f-173">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1fd7f-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1fd7f-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fd7f-174">Create an Azure AD test user</span></span>

<span data-ttu-id="1fd7f-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="1fd7f-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1fd7f-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1fd7f-178">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1fd7f-180">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1fd7f-182">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1fd7f-184">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1fd7f-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1fd7f-186">a.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-186">a.</span></span> <span data-ttu-id="1fd7f-187">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1fd7f-188">b.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-188">b.</span></span> <span data-ttu-id="1fd7f-189">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="1fd7f-190">c.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-190">c.</span></span> <span data-ttu-id="1fd7f-191">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="1fd7f-192">d.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-192">d.</span></span> <span data-ttu-id="1fd7f-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="1fd7f-194">Creación de usuario de prueba de Fuse</span><span class="sxs-lookup"><span data-stu-id="1fd7f-194">Create a Fuse test user</span></span>

<span data-ttu-id="1fd7f-195">En esta sección, creará un usuario llamado Britta Simon en Fuse.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="1fd7f-196">Trabaje con [equipo de soporte técnico de fusible](mailto:support@fusion-universal.com) a los usuarios de tooadd hello en la plataforma de fusible Hola.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) tooadd hello users in hello Fuse platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1fd7f-197">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fd7f-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1fd7f-198">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooFuse.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFuse.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="1fd7f-200">**tooassign Britta Simon tooFuse, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1fd7f-200">**tooassign Britta Simon tooFuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="1fd7f-201">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1fd7f-203">En la lista de aplicaciones de hello, seleccione **fusible**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-203">In hello applications list, select **Fuse**.</span></span>

    ![vínculo de fusible Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="1fd7f-205">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="1fd7f-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-207">Click **Add** button.</span></span> <span data-ttu-id="1fd7f-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="1fd7f-210">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1fd7f-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1fd7f-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1fd7f-213">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="1fd7f-213">Test single sign-on</span></span>

<span data-ttu-id="1fd7f-214">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1fd7f-215">Al hacer clic en icono de fusible Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour fusible aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fd7f-215">When you click hello Fuse tile in hello Access Panel, you should get automatically signed-on tooyour Fuse application.</span></span>
<span data-ttu-id="1fd7f-216">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1fd7f-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1fd7f-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1fd7f-217">Additional resources</span></span>

* [<span data-ttu-id="1fd7f-218">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1fd7f-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1fd7f-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1fd7f-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

