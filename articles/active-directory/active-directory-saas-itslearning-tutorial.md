---
title: "Tutorial: Integración de Azure Active Directory con itslearning | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y itslearning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 60587ba3-1396-4b8a-9ac1-e22a98e5e0ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 4ee6c8d450cc3972a87da67fc79890473cfa498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itslearning"></a><span data-ttu-id="cdfd7-103">Tutorial: Integración de Azure Active Directory con itslearning</span><span class="sxs-lookup"><span data-stu-id="cdfd7-103">Tutorial: Azure Active Directory integration with itslearning</span></span>

<span data-ttu-id="cdfd7-104">En este tutorial, aprenderá cómo toointegrate itslearning con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cdfd7-104">In this tutorial, you learn how toointegrate itslearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cdfd7-105">Integración itslearning con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="cdfd7-105">Integrating itslearning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cdfd7-106">Puede controlar en Azure AD que tenga acceso tooitslearning</span><span class="sxs-lookup"><span data-stu-id="cdfd7-106">You can control in Azure AD who has access tooitslearning</span></span>
- <span data-ttu-id="cdfd7-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooitslearning (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdfd7-107">You can enable your users tooautomatically get signed-on tooitslearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cdfd7-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cdfd7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cdfd7-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cdfd7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdfd7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cdfd7-110">Prerequisites</span></span>

<span data-ttu-id="cdfd7-111">integración de Azure AD con itslearning tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="cdfd7-111">tooconfigure Azure AD integration with itslearning, you need hello following items:</span></span>

- <span data-ttu-id="cdfd7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdfd7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cdfd7-113">Una suscripción habilitada para el inicio de sesión único en itslearning</span><span class="sxs-lookup"><span data-stu-id="cdfd7-113">An itslearning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cdfd7-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cdfd7-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="cdfd7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cdfd7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cdfd7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cdfd7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cdfd7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cdfd7-118">Scenario description</span></span>
<span data-ttu-id="cdfd7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cdfd7-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="cdfd7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cdfd7-121">Agregar itslearning desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cdfd7-121">Adding itslearning from hello gallery</span></span>
2. <span data-ttu-id="cdfd7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdfd7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itslearning-from-hello-gallery"></a><span data-ttu-id="cdfd7-123">Agregar itslearning desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cdfd7-123">Adding itslearning from hello gallery</span></span>
<span data-ttu-id="cdfd7-124">integración de hello tooconfigure de itslearning en Azure AD, deberá tooadd itslearning de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-124">tooconfigure hello integration of itslearning into Azure AD, you need tooadd itslearning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cdfd7-125">**tooadd itslearning de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cdfd7-125">**tooadd itslearning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdfd7-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cdfd7-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cdfd7-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="cdfd7-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="cdfd7-133">En el cuadro de búsqueda de hello, escriba **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-133">In hello search box, type **itslearning**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_search.png)

5. <span data-ttu-id="cdfd7-135">En el panel de resultados de hello, seleccione **itslearning**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-135">In hello results panel, select **itslearning**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cdfd7-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdfd7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cdfd7-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con itslearning utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cdfd7-138">In this section, you configure and test Azure AD single sign-on with itslearning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cdfd7-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en itslearning es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in itslearning is tooa user in Azure AD.</span></span> <span data-ttu-id="cdfd7-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en itslearning debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-140">In other words, a link relationship between an Azure AD user and hello related user in itslearning needs toobe established.</span></span>

<span data-ttu-id="cdfd7-141">En itslearning, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-141">In itslearning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cdfd7-142">tooconfigure y prueba de inicio de sesión único en Azure AD con itslearning, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="cdfd7-142">tooconfigure and test Azure AD single sign-on with itslearning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cdfd7-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cdfd7-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cdfd7-145">**[Creación de un usuario de prueba itslearning](#creating-an-itslearning-test-user) ** -toohave un equivalente de Britta Simon en itslearning que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-145">**[Creating an itslearning test user](#creating-an-itslearning-test-user)** - toohave a counterpart of Britta Simon in itslearning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cdfd7-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cdfd7-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cdfd7-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdfd7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cdfd7-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación itslearning.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your itslearning application.</span></span>

<span data-ttu-id="cdfd7-150">**inicio de sesión único en Azure AD tooconfigure con itslearning, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cdfd7-150">**tooconfigure Azure AD single sign-on with itslearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdfd7-151">En el portal de Azure, en Hola Hola **itslearning** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-151">In hello Azure portal, on hello **itslearning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="cdfd7-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_samlbase.png)

3. <span data-ttu-id="cdfd7-155">En hello **itslearning dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cdfd7-155">On hello **itslearning Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_url.png)

    <span data-ttu-id="cdfd7-157">a.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-157">a.</span></span> <span data-ttu-id="cdfd7-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL como:</span><span class="sxs-lookup"><span data-stu-id="cdfd7-158">In hello **Sign-on URL** textbox, type a URL as:</span></span>
    | |
    |--| 
    | `https://www.itslearning.com/index.aspx`|
    | `https://us1.itslearning.com/index.aspx`|

    <span data-ttu-id="cdfd7-159">b.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-159">b.</span></span> <span data-ttu-id="cdfd7-160">Hola **identificador** cuadro de texto, escriba una dirección URL como:`urn:mace:saml2v2.no:services:com.itslearning`</span><span class="sxs-lookup"><span data-stu-id="cdfd7-160">In hello **Identifier** textbox, type a URL as: `urn:mace:saml2v2.no:services:com.itslearning`</span></span>

4. <span data-ttu-id="cdfd7-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_certificate.png) 

5. <span data-ttu-id="cdfd7-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="cdfd7-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itslearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cdfd7-165">tooconfigure inicio de sesión único en **itslearning** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de itslearning](mailto:support@itslearning.com).</span><span class="sxs-lookup"><span data-stu-id="cdfd7-165">tooconfigure single sign-on on **itslearning** side, you need toosend hello downloaded **Metadata XML** too[itslearning support team](mailto:support@itslearning.com).</span></span> <span data-ttu-id="cdfd7-166">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="cdfd7-167">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="cdfd7-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cdfd7-168">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cdfd7-169">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cdfd7-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cdfd7-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdfd7-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="cdfd7-171">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="cdfd7-173">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cdfd7-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdfd7-174">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cdfd7-176">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cdfd7-178">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cdfd7-180">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cdfd7-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cdfd7-182">a.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-182">a.</span></span> <span data-ttu-id="cdfd7-183">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cdfd7-184">b.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-184">b.</span></span> <span data-ttu-id="cdfd7-185">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cdfd7-186">c.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-186">c.</span></span> <span data-ttu-id="cdfd7-187">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cdfd7-188">d.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-188">d.</span></span> <span data-ttu-id="cdfd7-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-189">Click **Create**.</span></span>
 
### <a name="creating-an-itslearning-test-user"></a><span data-ttu-id="cdfd7-190">Creación de un usuario de prueba de itslearning</span><span class="sxs-lookup"><span data-stu-id="cdfd7-190">Creating an itslearning test user</span></span>

<span data-ttu-id="cdfd7-191">En esta sección, creará un usuario llamado Britta Simon en itslearning.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-191">In this section, you create a user called Britta Simon in itslearning.</span></span> <span data-ttu-id="cdfd7-192">Trabajar con [itslearning equipo de soporte técnico de cliente](mailto:support@itslearning.com) para agregar usuarios de hello en la plataforma de itslearning Hola.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-192">Work with [itslearning Client support team](mailto:support@itslearning.com) to add hello users in hello itslearning platform.</span></span> <span data-ttu-id="cdfd7-193">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cdfd7-194">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdfd7-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cdfd7-195">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooitslearning.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooitslearning.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="cdfd7-197">**tooassign Britta Simon tooitslearning, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cdfd7-197">**tooassign Britta Simon tooitslearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdfd7-198">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="cdfd7-200">En la lista de aplicaciones de hello, seleccione **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-200">In hello applications list, select **itslearning**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_app.png) 

3. <span data-ttu-id="cdfd7-202">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="cdfd7-204">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-204">Click **Add** button.</span></span> <span data-ttu-id="cdfd7-205">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="cdfd7-207">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cdfd7-208">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cdfd7-209">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cdfd7-210">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="cdfd7-210">Testing single sign-on</span></span>

<span data-ttu-id="cdfd7-211">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cdfd7-212">Al hacer clic en icono de itslearning Hola Hola Panel de acceso, deberá obtener la página de inicio de sesión de la aplicación itslearning.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-212">When you click hello itslearning tile in hello Access Panel, you should get login page of itslearning application.</span></span> <span data-ttu-id="cdfd7-213">Haga clic en **iniciar sesión con Windows Azure ACS1** para inicio de sesión correcto en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="cdfd7-213">Click **Log in with Windows Azure ACS1** for successful login into hello application.</span></span>

  ![Inicio de sesión](./media/active-directory-saas-itslearning-tutorial/login.png)

<span data-ttu-id="cdfd7-215">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cdfd7-215">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cdfd7-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cdfd7-216">Additional resources</span></span>

* [<span data-ttu-id="cdfd7-217">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cdfd7-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cdfd7-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cdfd7-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_203.png

