---
title: "Tutorial: integración de Azure Active Directory con Concur | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1012bf8c6f036306d0ca90689415d5e22e449989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="6afc8-103">Tutorial: Integración de Azure Active Directory con Concur</span><span class="sxs-lookup"><span data-stu-id="6afc8-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="6afc8-104">En este tutorial, aprenderá cómo toointegrate Concur con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6afc8-104">In this tutorial, you learn how toointegrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6afc8-105">Integración de Concur con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6afc8-105">Integrating Concur with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6afc8-106">Puede controlar en Azure AD que tenga acceso tooConcur</span><span class="sxs-lookup"><span data-stu-id="6afc8-106">You can control in Azure AD who has access tooConcur</span></span>
- <span data-ttu-id="6afc8-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooConcur (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afc8-107">You can enable your users tooautomatically get signed-on tooConcur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6afc8-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6afc8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6afc8-109">Si desea tooknow obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6afc8-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6afc8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6afc8-110">Prerequisites</span></span>

<span data-ttu-id="6afc8-111">integración de Azure AD con Concur tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6afc8-111">tooconfigure Azure AD integration with Concur, you need hello following items:</span></span>

- <span data-ttu-id="6afc8-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afc8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6afc8-113">Una suscripción habilitada para el inicio de sesión único en Concur</span><span class="sxs-lookup"><span data-stu-id="6afc8-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6afc8-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6afc8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6afc8-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6afc8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6afc8-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6afc8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6afc8-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6afc8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6afc8-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6afc8-118">Scenario description</span></span>
<span data-ttu-id="6afc8-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6afc8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6afc8-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="6afc8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6afc8-121">Adición de Concur de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6afc8-121">Adding Concur from hello gallery</span></span>
2. <span data-ttu-id="6afc8-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afc8-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="6afc8-123">configuración de saludo de la suscripción a Concur para SSO federado mediante SAMP es una tarea independiente, que debe ponerse en contacto con [equipo de soporte técnico de Concur cliente](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="6afc8-123">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 

## <a name="adding-concur-from-hello-gallery"></a><span data-ttu-id="6afc8-124">Adición de Concur de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6afc8-124">Adding Concur from hello gallery</span></span>
<span data-ttu-id="6afc8-125">integración de hello tooconfigure de Concur en Azure AD, deberá tooadd Concur de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="6afc8-125">tooconfigure hello integration of Concur into Azure AD, you need tooadd Concur from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6afc8-126">**tooadd Concur de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6afc8-126">**tooadd Concur from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6afc8-127">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6afc8-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6afc8-129">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6afc8-130">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-130">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="6afc8-132">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6afc8-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="6afc8-134">En el cuadro de búsqueda de hello, escriba **Concur**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-134">In hello search box, type **Concur**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="6afc8-136">En el panel de resultados de hello, seleccione **Concur**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6afc8-136">In hello results panel, select **Concur**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6afc8-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afc8-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6afc8-139">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con Concur con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6afc8-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6afc8-140">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Concur es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6afc8-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Concur is tooa user in Azure AD.</span></span> <span data-ttu-id="6afc8-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Concur debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="6afc8-141">In other words, a link relationship between an Azure AD user and hello related user in Concur needs toobe established.</span></span>

<span data-ttu-id="6afc8-142">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Concur.</span><span class="sxs-lookup"><span data-stu-id="6afc8-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Concur.</span></span>

<span data-ttu-id="6afc8-143">tooconfigure y prueba de inicio de sesión único en Azure AD con Concur, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6afc8-143">tooconfigure and test Azure AD single sign-on with Concur, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6afc8-144">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="6afc8-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6afc8-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6afc8-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6afc8-146">**[Crear un usuario de prueba de Concur](#creating-a-concur-test-user)**  -toohave un equivalente de Britta Simon en Concur que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="6afc8-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - toohave a counterpart of Britta Simon in Concur that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6afc8-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6afc8-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6afc8-148">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="6afc8-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6afc8-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afc8-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6afc8-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Concur.</span><span class="sxs-lookup"><span data-stu-id="6afc8-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="6afc8-151">**inicio de sesión único en tooconfigure Azure AD con Concur, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6afc8-151">**tooconfigure Azure AD single sign-on with Concur, perform hello following steps:**</span></span>

1. <span data-ttu-id="6afc8-152">En el portal de Azure, en Hola Hola **Concur** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-152">In hello Azure portal, on hello **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="6afc8-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6afc8-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="6afc8-156">En hello **Concur dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6afc8-156">On hello **Concur Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="6afc8-158">a.</span><span class="sxs-lookup"><span data-stu-id="6afc8-158">a.</span></span> <span data-ttu-id="6afc8-159">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="6afc8-159">In hello **Sign on URL** textbox, type hello value using hello following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="6afc8-160">b.</span><span class="sxs-lookup"><span data-stu-id="6afc8-160">b.</span></span> <span data-ttu-id="6afc8-161">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="6afc8-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6afc8-162">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="6afc8-162">These values are not hello real.</span></span> <span data-ttu-id="6afc8-163">Actualización de estos valores con hello real iniciar sesión en la dirección URL y el identificador.</span><span class="sxs-lookup"><span data-stu-id="6afc8-163">Update these values with hello actual Sign on URL and Identifier.</span></span> <span data-ttu-id="6afc8-164">Póngase en contacto con [equipo de soporte técnico de Concur cliente](https://www.concur.co.in/contact) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="6afc8-164">Contact [Concur Client support team](https://www.concur.co.in/contact) tooget these values.</span></span> 

4. <span data-ttu-id="6afc8-165">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6afc8-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="6afc8-167">Haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-167">Click **Save** button.</span></span>

    <span data-ttu-id="6afc8-168">![Configuración del inicio de sesión único](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="6afc8-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="6afc8-169">tooconfigure inicio de sesión único en **Concur** lado, necesita hello toosend descargado **Metadata XML** tooConcur soporte.</span><span class="sxs-lookup"><span data-stu-id="6afc8-169">tooconfigure single sign-on on **Concur** side, you need toosend hello downloaded **Metadata XML** tooConcur support.</span></span> <span data-ttu-id="6afc8-170">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="6afc8-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="6afc8-171">configuración de saludo de la suscripción a Concur para SSO federado mediante SAMP es una tarea independiente, que debe ponerse en contacto con [equipo de soporte técnico de Concur cliente](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="6afc8-171">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="6afc8-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="6afc8-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6afc8-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="6afc8-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6afc8-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6afc8-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6afc8-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afc8-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="6afc8-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="6afc8-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="6afc8-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6afc8-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6afc8-179">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6afc8-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6afc8-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6afc8-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6afc8-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6afc8-185">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="6afc8-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6afc8-187">a.</span><span class="sxs-lookup"><span data-stu-id="6afc8-187">a.</span></span> <span data-ttu-id="6afc8-188">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6afc8-189">b.</span><span class="sxs-lookup"><span data-stu-id="6afc8-189">b.</span></span> <span data-ttu-id="6afc8-190">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6afc8-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6afc8-191">c.</span><span class="sxs-lookup"><span data-stu-id="6afc8-191">c.</span></span> <span data-ttu-id="6afc8-192">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6afc8-193">d.</span><span class="sxs-lookup"><span data-stu-id="6afc8-193">d.</span></span> <span data-ttu-id="6afc8-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="6afc8-195">Creación de un usuario de prueba de Concur</span><span class="sxs-lookup"><span data-stu-id="6afc8-195">Creating a Concur test user</span></span>

<span data-ttu-id="6afc8-196">Aplicación admite Hola sólo en el aprovisionamiento de usuarios de tiempo y después de autenticar usuarios se crean automáticamente en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6afc8-196">Application supports hello Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6afc8-197">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afc8-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6afc8-198">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooConcur.</span><span class="sxs-lookup"><span data-stu-id="6afc8-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConcur.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="6afc8-200">**tooassign Britta Simon tooConcur, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6afc8-200">**tooassign Britta Simon tooConcur, perform hello following steps:**</span></span>

1. <span data-ttu-id="6afc8-201">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6afc8-203">En la lista de aplicaciones de hello, seleccione **Concur**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-203">In hello applications list, select **Concur**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="6afc8-205">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="6afc8-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-207">Click **Add** button.</span></span> <span data-ttu-id="6afc8-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="6afc8-210">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="6afc8-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6afc8-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6afc8-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6afc8-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6afc8-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="6afc8-213">Testing single sign-on</span></span>

<span data-ttu-id="6afc8-214">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6afc8-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6afc8-215">Al hacer clic en icono de Concur de Hola Hola Panel de acceso, deberá obtener la página de inicio de sesión de aplicación de Concur.</span><span class="sxs-lookup"><span data-stu-id="6afc8-215">When you click hello Concur tile in hello Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="6afc8-216">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6afc8-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6afc8-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6afc8-217">Additional resources</span></span>

* [<span data-ttu-id="6afc8-218">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6afc8-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6afc8-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6afc8-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="6afc8-220">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="6afc8-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

