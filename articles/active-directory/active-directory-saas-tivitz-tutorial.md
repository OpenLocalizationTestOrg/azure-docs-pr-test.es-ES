---
title: "Tutorial: Integración de Azure Active Directory con TiViTz | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y TiViTz."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b97ed88f-7888-4185-be22-41d1f62cbbf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: e915c31d317c4713720a4db07b23764d91f26a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tivitz"></a><span data-ttu-id="8242c-103">Tutorial: Integración de Azure Active Directory con TiViTz</span><span class="sxs-lookup"><span data-stu-id="8242c-103">Tutorial: Azure Active Directory integration with TiViTz</span></span>

<span data-ttu-id="8242c-104">En este tutorial, aprenderá cómo toointegrate TiViTz con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8242c-104">In this tutorial, you learn how toointegrate TiViTz with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8242c-105">Integración TiViTz con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8242c-105">Integrating TiViTz with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8242c-106">Puede controlar en Azure AD que tenga acceso tooTiViTz</span><span class="sxs-lookup"><span data-stu-id="8242c-106">You can control in Azure AD who has access tooTiViTz</span></span>
- <span data-ttu-id="8242c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTiViTz (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8242c-107">You can enable your users tooautomatically get signed-on tooTiViTz (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8242c-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8242c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8242c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8242c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8242c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8242c-110">Prerequisites</span></span>

<span data-ttu-id="8242c-111">integración de Azure AD con TiViTz tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8242c-111">tooconfigure Azure AD integration with TiViTz, you need hello following items:</span></span>

- <span data-ttu-id="8242c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8242c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8242c-113">Una suscripción habilitada para inicio de sesión único en TiViTz</span><span class="sxs-lookup"><span data-stu-id="8242c-113">A TiViTz single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8242c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8242c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8242c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8242c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8242c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8242c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8242c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8242c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8242c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8242c-118">Scenario description</span></span>
<span data-ttu-id="8242c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8242c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8242c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8242c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8242c-121">Agregar TiViTz desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8242c-121">Adding TiViTz from hello gallery</span></span>
2. <span data-ttu-id="8242c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8242c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tivitz-from-hello-gallery"></a><span data-ttu-id="8242c-123">Agregar TiViTz desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8242c-123">Adding TiViTz from hello gallery</span></span>
<span data-ttu-id="8242c-124">integración de hello tooconfigure de TiViTz en Azure AD, deberá tooadd TiViTz de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="8242c-124">tooconfigure hello integration of TiViTz into Azure AD, you need tooadd TiViTz from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8242c-125">**tooadd TiViTz de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8242c-125">**tooadd TiViTz from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8242c-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8242c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8242c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8242c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8242c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8242c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8242c-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8242c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8242c-133">En el cuadro de búsqueda de hello, escriba **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="8242c-133">In hello search box, type **TiViTz**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_search.png)

5. <span data-ttu-id="8242c-135">En el panel de resultados de hello, seleccione **TiViTz**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8242c-135">In hello results panel, select **TiViTz**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8242c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8242c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8242c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TiViTz con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8242c-138">In this section, you configure and test Azure AD single sign-on with TiViTz based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8242c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TiViTz es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8242c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TiViTz is tooa user in Azure AD.</span></span> <span data-ttu-id="8242c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TiViTz debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8242c-140">In other words, a link relationship between an Azure AD user and hello related user in TiViTz needs toobe established.</span></span>

<span data-ttu-id="8242c-141">En TiViTz, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8242c-141">In TiViTz, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8242c-142">tooconfigure y prueba de inicio de sesión único en Azure AD con TiViTz, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8242c-142">tooconfigure and test Azure AD single sign-on with TiViTz, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8242c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8242c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8242c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8242c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8242c-145">**[Crear un usuario de prueba TiViTz](#creating-a-tivitz-test-user) ** -toohave un equivalente de Britta Simon en TiViTz que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8242c-145">**[Creating a TiViTz test user](#creating-a-tivitz-test-user)** - toohave a counterpart of Britta Simon in TiViTz that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8242c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8242c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8242c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8242c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8242c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8242c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8242c-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación TiViTz.</span><span class="sxs-lookup"><span data-stu-id="8242c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TiViTz application.</span></span>

<span data-ttu-id="8242c-150">**inicio de sesión único en Azure AD tooconfigure con TiViTz, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8242c-150">**tooconfigure Azure AD single sign-on with TiViTz, perform hello following steps:**</span></span>

1. <span data-ttu-id="8242c-151">En el portal de Azure, en Hola Hola **TiViTz** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8242c-151">In hello Azure portal, on hello **TiViTz** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8242c-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8242c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_samlbase.png)

3. <span data-ttu-id="8242c-155">En hello **TiViTz dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8242c-155">On hello **TiViTz Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_url.png)

    <span data-ttu-id="8242c-157">a.</span><span class="sxs-lookup"><span data-stu-id="8242c-157">a.</span></span> <span data-ttu-id="8242c-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="8242c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    <span data-ttu-id="8242c-159">b.</span><span class="sxs-lookup"><span data-stu-id="8242c-159">b.</span></span> <span data-ttu-id="8242c-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="8242c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8242c-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="8242c-161">These values are not real.</span></span> <span data-ttu-id="8242c-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="8242c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8242c-163">Póngase en contacto con [equipo de soporte técnico de cliente de TiViTz](mailto:info@tivitz.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="8242c-163">Contact [TiViTz Client support team](mailto:info@tivitz.com) tooget these values.</span></span> 

4. <span data-ttu-id="8242c-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8242c-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_certificate.png) 

5. <span data-ttu-id="8242c-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8242c-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tivitz-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8242c-168">tooconfigure inicio de sesión único en **TiViTz** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de TiViTz](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="8242c-168">tooconfigure single sign-on on **TiViTz** side, you need toosend hello downloaded **Metadata XML** too[TiViTz support team](mailto:info@tivitz.com).</span></span>

> [!TIP]
> <span data-ttu-id="8242c-169">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8242c-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8242c-170">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8242c-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8242c-171">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8242c-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8242c-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8242c-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="8242c-173">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8242c-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8242c-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8242c-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8242c-176">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8242c-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8242c-178">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8242c-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8242c-180">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8242c-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8242c-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8242c-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8242c-184">a.</span><span class="sxs-lookup"><span data-stu-id="8242c-184">a.</span></span> <span data-ttu-id="8242c-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8242c-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8242c-186">b.</span><span class="sxs-lookup"><span data-stu-id="8242c-186">b.</span></span> <span data-ttu-id="8242c-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8242c-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8242c-188">c.</span><span class="sxs-lookup"><span data-stu-id="8242c-188">c.</span></span> <span data-ttu-id="8242c-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8242c-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8242c-190">d.</span><span class="sxs-lookup"><span data-stu-id="8242c-190">d.</span></span> <span data-ttu-id="8242c-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8242c-191">Click **Create**.</span></span>
 
### <a name="creating-a-tivitz-test-user"></a><span data-ttu-id="8242c-192">Creación de un usuario de prueba de TiViTz</span><span class="sxs-lookup"><span data-stu-id="8242c-192">Creating a TiViTz test user</span></span>

<span data-ttu-id="8242c-193">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en TiViTz toocreate.</span><span class="sxs-lookup"><span data-stu-id="8242c-193">hello objective of this section is toocreate a user called Britta Simon in TiViTz.</span></span> <span data-ttu-id="8242c-194">TiViTz admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8242c-194">TiViTz supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="8242c-195">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="8242c-195">There is no action item for you in this section.</span></span> <span data-ttu-id="8242c-196">Se crea un nuevo usuario durante un tooaccess intento TiViTz si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="8242c-196">A new user is created during an attempt tooaccess TiViTz if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="8242c-197">Si necesita un usuario toocreate manualmente, necesita toocontact [equipo de soporte técnico de TiViTz](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="8242c-197">If you need toocreate an user manually, you need toocontact [TiViTz support team](mailto:info@tivitz.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8242c-198">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8242c-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8242c-199">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTiViTz.</span><span class="sxs-lookup"><span data-stu-id="8242c-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTiViTz.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8242c-201">**tooassign Britta Simon tooTiViTz, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8242c-201">**tooassign Britta Simon tooTiViTz, perform hello following steps:**</span></span>

1. <span data-ttu-id="8242c-202">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8242c-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8242c-204">En la lista de aplicaciones de hello, seleccione **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="8242c-204">In hello applications list, select **TiViTz**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_app.png) 

3. <span data-ttu-id="8242c-206">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8242c-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8242c-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8242c-208">Click **Add** button.</span></span> <span data-ttu-id="8242c-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8242c-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8242c-211">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8242c-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8242c-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8242c-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8242c-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8242c-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8242c-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8242c-214">Testing single sign-on</span></span>

<span data-ttu-id="8242c-215">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8242c-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8242c-216">Al hacer clic en icono de TiViTz Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour TiViTz aplicación.</span><span class="sxs-lookup"><span data-stu-id="8242c-216">When you click hello TiViTz tile in hello Access Panel, you should get automatically signed-on tooyour TiViTz application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8242c-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8242c-217">Additional resources</span></span>

* [<span data-ttu-id="8242c-218">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8242c-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8242c-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8242c-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_203.png

