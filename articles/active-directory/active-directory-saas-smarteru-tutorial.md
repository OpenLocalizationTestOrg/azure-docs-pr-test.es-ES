---
title: "Tutorial: Integración de Azure Active Directory con SmarterU | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SmarterU."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: a3b81b557c47e31f09e61bcf75dd23f370e642e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="a51fb-103">Tutorial: integración de Azure Active Directory con SmarterU</span><span class="sxs-lookup"><span data-stu-id="a51fb-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="a51fb-104">En este tutorial, aprenderá cómo toointegrate SmarterU con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a51fb-104">In this tutorial, you learn how toointegrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a51fb-105">Integración SmarterU con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a51fb-105">Integrating SmarterU with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a51fb-106">Puede controlar en Azure AD que tenga acceso tooSmarterU</span><span class="sxs-lookup"><span data-stu-id="a51fb-106">You can control in Azure AD who has access tooSmarterU</span></span>
- <span data-ttu-id="a51fb-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSmarterU (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a51fb-107">You can enable your users tooautomatically get signed-on tooSmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a51fb-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a51fb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a51fb-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a51fb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a51fb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a51fb-110">Prerequisites</span></span>

<span data-ttu-id="a51fb-111">integración de Azure AD con SmarterU tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a51fb-111">tooconfigure Azure AD integration with SmarterU, you need hello following items:</span></span>

- <span data-ttu-id="a51fb-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a51fb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a51fb-113">Una suscripción habilitada para el inicio de sesión único en SmarterU</span><span class="sxs-lookup"><span data-stu-id="a51fb-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a51fb-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a51fb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a51fb-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a51fb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a51fb-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a51fb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a51fb-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a51fb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a51fb-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a51fb-118">Scenario description</span></span>
<span data-ttu-id="a51fb-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a51fb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a51fb-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="a51fb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a51fb-121">Agregar SmarterU desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a51fb-121">Adding SmarterU from hello gallery</span></span>
2. <span data-ttu-id="a51fb-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a51fb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-hello-gallery"></a><span data-ttu-id="a51fb-123">Agregar SmarterU desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a51fb-123">Adding SmarterU from hello gallery</span></span>
<span data-ttu-id="a51fb-124">integración de hello tooconfigure de SmarterU en Azure AD, deberá tooadd SmarterU de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="a51fb-124">tooconfigure hello integration of SmarterU into Azure AD, you need tooadd SmarterU from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a51fb-125">**tooadd SmarterU de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a51fb-125">**tooadd SmarterU from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a51fb-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="a51fb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a51fb-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a51fb-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="a51fb-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a51fb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="a51fb-133">En el cuadro de búsqueda de hello, escriba **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-133">In hello search box, type **SmarterU**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="a51fb-135">En el panel de resultados de hello, seleccione **SmarterU**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a51fb-135">In hello results panel, select **SmarterU**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a51fb-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a51fb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a51fb-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SmarterU con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a51fb-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a51fb-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SmarterU es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a51fb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SmarterU is tooa user in Azure AD.</span></span> <span data-ttu-id="a51fb-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SmarterU debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="a51fb-140">In other words, a link relationship between an Azure AD user and hello related user in SmarterU needs toobe established.</span></span>

<span data-ttu-id="a51fb-141">En SmarterU, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a51fb-141">In SmarterU, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a51fb-142">tooconfigure y prueba de inicio de sesión único en Azure AD con SmarterU, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a51fb-142">tooconfigure and test Azure AD single sign-on with SmarterU, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a51fb-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="a51fb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a51fb-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a51fb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a51fb-145">**[Crear un usuario de prueba de SmarterU](#creating-a-smarteru-test-user)**  -toohave un equivalente de Britta Simon en SmarterU que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="a51fb-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - toohave a counterpart of Britta Simon in SmarterU that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a51fb-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a51fb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a51fb-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a51fb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a51fb-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a51fb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a51fb-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de SmarterU.</span><span class="sxs-lookup"><span data-stu-id="a51fb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="a51fb-150">**inicio de sesión único en tooconfigure Azure AD con SmarterU, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a51fb-150">**tooconfigure Azure AD single sign-on with SmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="a51fb-151">En el portal de Azure, en Hola Hola **SmarterU** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-151">In hello Azure portal, on hello **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="a51fb-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a51fb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="a51fb-155">En hello **SmarterU dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a51fb-155">On hello **SmarterU Domain and URLs** section, perform hello following steps:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="a51fb-157">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="a51fb-157">In hello **Identifier** textbox, type hello URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="a51fb-158">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a51fb-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="a51fb-160">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a51fb-160">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a51fb-162">En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía SmarterU tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="a51fb-162">In a different web browser window, log in tooyour SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="a51fb-163">En la barra de herramientas de hello en la parte superior de hello, haga clic en **configuración de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-163">In hello toolbar on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="a51fb-164">![Configuración de la cuenta](./media/active-directory-saas-smarteru-tutorial/IC777326.png "configuración de la cuenta")</span><span class="sxs-lookup"><span data-stu-id="a51fb-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="a51fb-165">En la página de configuración de la cuenta de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a51fb-165">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="a51fb-166">![Autorización externa](./media/active-directory-saas-smarteru-tutorial/IC777327.png "Autorización externa")</span><span class="sxs-lookup"><span data-stu-id="a51fb-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="a51fb-167">a.</span><span class="sxs-lookup"><span data-stu-id="a51fb-167">a.</span></span> <span data-ttu-id="a51fb-168">Seleccione **Habilitar autorización externa**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="a51fb-169">b.</span><span class="sxs-lookup"><span data-stu-id="a51fb-169">b.</span></span> <span data-ttu-id="a51fb-170">Hola **Control de inicio de sesión de Master** sección, seleccione hello **SmarterU** ficha.</span><span class="sxs-lookup"><span data-stu-id="a51fb-170">In hello **Master Login Control** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="a51fb-171">c.</span><span class="sxs-lookup"><span data-stu-id="a51fb-171">c.</span></span> <span data-ttu-id="a51fb-172">Hola **el inicio de sesión de usuario predeterminado** sección, seleccione hello **SmarterU** ficha.</span><span class="sxs-lookup"><span data-stu-id="a51fb-172">In hello **User Default Login** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="a51fb-173">d.</span><span class="sxs-lookup"><span data-stu-id="a51fb-173">d.</span></span> <span data-ttu-id="a51fb-174">Seleccione **Habilitar Okta**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="a51fb-175">e.</span><span class="sxs-lookup"><span data-stu-id="a51fb-175">e.</span></span> <span data-ttu-id="a51fb-176">Copiar el contenido de hello del archivo de metadatos descargado de hello y, a continuación, péguelo en hello **Okta Metadata** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="a51fb-176">Copy hello content of hello downloaded metadata file, and then paste it into hello **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="a51fb-177">f.</span><span class="sxs-lookup"><span data-stu-id="a51fb-177">f.</span></span> <span data-ttu-id="a51fb-178">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a51fb-179">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="a51fb-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a51fb-180">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="a51fb-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a51fb-181">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a51fb-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a51fb-182">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a51fb-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="a51fb-183">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="a51fb-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="a51fb-185">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a51fb-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a51fb-186">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="a51fb-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a51fb-188">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a51fb-190">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a51fb-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a51fb-192">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="a51fb-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a51fb-194">a.</span><span class="sxs-lookup"><span data-stu-id="a51fb-194">a.</span></span> <span data-ttu-id="a51fb-195">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a51fb-196">b.</span><span class="sxs-lookup"><span data-stu-id="a51fb-196">b.</span></span> <span data-ttu-id="a51fb-197">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a51fb-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a51fb-198">c.</span><span class="sxs-lookup"><span data-stu-id="a51fb-198">c.</span></span> <span data-ttu-id="a51fb-199">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a51fb-200">d.</span><span class="sxs-lookup"><span data-stu-id="a51fb-200">d.</span></span> <span data-ttu-id="a51fb-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="a51fb-202">Creación de un usuario de prueba de SmarterU</span><span class="sxs-lookup"><span data-stu-id="a51fb-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="a51fb-203">toolog de los usuarios de Azure AD tooenable en tooSmarterU, se les deben aprovisionar en SmarterU.</span><span class="sxs-lookup"><span data-stu-id="a51fb-203">tooenable Azure AD users toolog in tooSmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="a51fb-204">En el caso de SmarterU, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="a51fb-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="a51fb-205">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a51fb-205">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a51fb-206">Inicie sesión en tooyour **SmarterU** inquilino.</span><span class="sxs-lookup"><span data-stu-id="a51fb-206">Log in tooyour **SmarterU** tenant.</span></span>

2. <span data-ttu-id="a51fb-207">Vaya demasiado**usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-207">Go too**Users**.</span></span>

3. <span data-ttu-id="a51fb-208">En la sección de usuario de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a51fb-208">In hello user section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a51fb-209">![Nuevo usuario](./media/active-directory-saas-smarteru-tutorial/IC777329.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="a51fb-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="a51fb-210">a.</span><span class="sxs-lookup"><span data-stu-id="a51fb-210">a.</span></span> <span data-ttu-id="a51fb-211">Haga clic en **+Usuario**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-211">Click **+User**.</span></span>
    
    <span data-ttu-id="a51fb-212">b.</span><span class="sxs-lookup"><span data-stu-id="a51fb-212">b.</span></span> <span data-ttu-id="a51fb-213">Hola de tipo relacionados con los valores de atributo de cuenta de usuario de hello Azure AD en hello siguientes cuadros de texto: **correo electrónico principal**, **Id. de empleado**, **contraseña**,  **Comprobar contraseña**, **nombre dado**, **apellido**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-213">Type hello related attribute values of hello Azure AD user account into hello following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="a51fb-214">c.</span><span class="sxs-lookup"><span data-stu-id="a51fb-214">c.</span></span> <span data-ttu-id="a51fb-215">Haga clic en **Activo**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="a51fb-216">d.</span><span class="sxs-lookup"><span data-stu-id="a51fb-216">d.</span></span> <span data-ttu-id="a51fb-217">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="a51fb-218">Puede usar cualquier otra SmarterU usuario cuenta herramienta de creación o las API proporcionadas por SmarterU tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="a51fb-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a51fb-219">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a51fb-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a51fb-220">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSmarterU.</span><span class="sxs-lookup"><span data-stu-id="a51fb-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmarterU.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="a51fb-222">**tooassign Britta Simon tooSmarterU, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a51fb-222">**tooassign Britta Simon tooSmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="a51fb-223">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a51fb-225">En la lista de aplicaciones de hello, seleccione **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-225">In hello applications list, select **SmarterU**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="a51fb-227">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="a51fb-229">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-229">Click **Add** button.</span></span> <span data-ttu-id="a51fb-230">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="a51fb-232">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="a51fb-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a51fb-233">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a51fb-234">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a51fb-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a51fb-235">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="a51fb-235">Testing single sign-on</span></span>

<span data-ttu-id="a51fb-236">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a51fb-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="a51fb-237">Al hacer clic en icono de SmarterU Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour SmarterU aplicación.</span><span class="sxs-lookup"><span data-stu-id="a51fb-237">When you click hello SmarterU tile in hello Access Panel, you should get automatically signed-on tooyour SmarterU application.</span></span>
<span data-ttu-id="a51fb-238">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a51fb-238">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="a51fb-239">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a51fb-239">Additional resources</span></span>

* [<span data-ttu-id="a51fb-240">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a51fb-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a51fb-241">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a51fb-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

