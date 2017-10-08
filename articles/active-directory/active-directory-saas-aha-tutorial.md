---
title: "Tutorial: Integración de Azure Active Directory con Aha! | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Aha!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="305f7-104">Tutorial: Integración de Azure Active Directory con Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="305f7-105">En este tutorial, aprenderá cómo toointegrate Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-105">In this tutorial, you learn how toointegrate Aha!</span></span> <span data-ttu-id="305f7-106">con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="305f7-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="305f7-107">Integración de Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-107">Integrating Aha!</span></span> <span data-ttu-id="305f7-108">con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="305f7-108">with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="305f7-109">Se puede controlar en Azure AD que tenga acceso tooAha!</span><span class="sxs-lookup"><span data-stu-id="305f7-109">You can control in Azure AD who has access tooAha!</span></span>
- <span data-ttu-id="305f7-110">¡Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAha!</span><span class="sxs-lookup"><span data-stu-id="305f7-110">You can enable your users tooautomatically get signed-on tooAha!</span></span> <span data-ttu-id="305f7-111">(inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="305f7-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="305f7-112">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="305f7-112">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="305f7-113">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="305f7-113">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="305f7-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="305f7-114">Prerequisites</span></span>

<span data-ttu-id="305f7-115">tooconfigure integración de Azure AD con Aha!, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="305f7-115">tooconfigure Azure AD integration with Aha!, you need hello following items:</span></span>

- <span data-ttu-id="305f7-116">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="305f7-116">An Azure AD subscription</span></span>
- <span data-ttu-id="305f7-117">Una</span><span class="sxs-lookup"><span data-stu-id="305f7-117">An Aha!</span></span> <span data-ttu-id="305f7-118">suscripción habilitada para inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="305f7-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="305f7-119">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="305f7-119">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="305f7-120">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="305f7-120">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="305f7-121">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="305f7-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="305f7-122">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="305f7-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="305f7-123">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="305f7-123">Scenario description</span></span>
<span data-ttu-id="305f7-124">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="305f7-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="305f7-125">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="305f7-125">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="305f7-126">Adición de Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-126">Adding Aha!</span></span> <span data-ttu-id="305f7-127">desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="305f7-127">from hello gallery</span></span>
2. <span data-ttu-id="305f7-128">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="305f7-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-hello-gallery"></a><span data-ttu-id="305f7-129">Adición de Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-129">Adding Aha!</span></span> <span data-ttu-id="305f7-130">desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="305f7-130">from hello gallery</span></span>
<span data-ttu-id="305f7-131">¡integración de hello tooconfigure de Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-131">tooconfigure hello integration of Aha!</span></span> <span data-ttu-id="305f7-132">¡en Azure AD, necesita tooadd Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-132">into Azure AD, you need tooadd Aha!</span></span> <span data-ttu-id="305f7-133">en lista de tooyour de hello Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="305f7-133">from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="305f7-134">**¡tooadd Aha! desde la Galería de hello, llevar a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="305f7-134">**tooadd Aha! from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="305f7-135">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="305f7-135">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="305f7-137">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="305f7-137">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="305f7-138">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="305f7-138">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="305f7-140">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="305f7-140">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="305f7-142">En el cuadro de búsqueda de hello, escriba **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="305f7-142">In hello search box, type **Aha!**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="305f7-144">En el panel de resultados de hello, seleccione **Aha!**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="305f7-144">In hello results panel, select **Aha!**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="305f7-146">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="305f7-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="305f7-147">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="305f7-148">en función de un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="305f7-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="305f7-149">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aha!</span></span> <span data-ttu-id="305f7-150">es usuario de tooa en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="305f7-150">is tooa user in Azure AD.</span></span> <span data-ttu-id="305f7-151">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-151">In other words, a link relationship between an Azure AD user and hello related user in Aha!</span></span> <span data-ttu-id="305f7-152">debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="305f7-152">needs toobe established.</span></span>

<span data-ttu-id="305f7-153">En Aha!, asignar un valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="305f7-153">In Aha!, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="305f7-154">prueba Azure AD y tooconfigure inicio de sesión único con Aha!, necesita hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="305f7-154">tooconfigure and test Azure AD single sign-on with Aha!, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="305f7-155">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="305f7-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="305f7-156">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="305f7-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="305f7-157">**[Crear un difíciles! usuario de prueba](#creating-an-aha-test-user)**  -toohave un equivalente de Britta Simon en Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - toohave a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="305f7-158">que está vinculado toohello representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="305f7-158">that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="305f7-159">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="305f7-159">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="305f7-160">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="305f7-160">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="305f7-161">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="305f7-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="305f7-162">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en su aplicación de Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-162">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="305f7-163">aplicación Aha!.</span><span class="sxs-lookup"><span data-stu-id="305f7-163">application.</span></span>

<span data-ttu-id="305f7-164">**tooconfigure inicio de sesión único en Azure AD con Aha!, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="305f7-164">**tooconfigure Azure AD single sign-on with Aha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="305f7-165">En el portal de Azure, en Hola Hola **Aha!**</span><span class="sxs-lookup"><span data-stu-id="305f7-165">In hello Azure portal, on hello **Aha!**</span></span> <span data-ttu-id="305f7-166">haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="305f7-166">application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="305f7-168">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="305f7-168">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="305f7-170">En hello **Aha! Dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="305f7-170">On hello **Aha! Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="305f7-172">a.</span><span class="sxs-lookup"><span data-stu-id="305f7-172">a.</span></span> <span data-ttu-id="305f7-173">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="305f7-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="305f7-174">b.</span><span class="sxs-lookup"><span data-stu-id="305f7-174">b.</span></span> <span data-ttu-id="305f7-175">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="305f7-175">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="305f7-176">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="305f7-176">These values are not real.</span></span> <span data-ttu-id="305f7-177">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="305f7-177">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="305f7-178">Póngase en contacto con el [equipo de soporte técnico de Aha! Equipo de soporte técnico de cliente](https://www.aha.io/company/contact) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="305f7-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="305f7-179">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="305f7-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="305f7-181">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="305f7-181">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="305f7-183">En una ventana del explorador web diferente, inicie sesión en tooyour Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-183">In a different web browser window, log in tooyour Aha!</span></span> <span data-ttu-id="305f7-184">como administrador.</span><span class="sxs-lookup"><span data-stu-id="305f7-184">company site as an administrator.</span></span>

7. <span data-ttu-id="305f7-185">En el menú de hello en la parte superior de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="305f7-185">In hello menu on hello top, click **Settings**.</span></span>

    <span data-ttu-id="305f7-186">![Configuración](./media/active-directory-saas-aha-tutorial/IC798950.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="305f7-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="305f7-187">Haga clic en **Cuenta**.</span><span class="sxs-lookup"><span data-stu-id="305f7-187">Click **Account**.</span></span>
   
    <span data-ttu-id="305f7-188">![Perfil](./media/active-directory-saas-aha-tutorial/IC798951.png "Perfil")</span><span class="sxs-lookup"><span data-stu-id="305f7-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="305f7-189">Haga clic en **Seguridad e inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="305f7-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="305f7-190">![Seguridad e inicio de sesión único](./media/active-directory-saas-aha-tutorial/IC798952.png "Seguridad e inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="305f7-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="305f7-191">En la sección **Inicio de sesión único**, en **Proveedor de identidades**, seleccione **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="305f7-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="305f7-192">![Seguridad e inicio de sesión único](./media/active-directory-saas-aha-tutorial/IC798953.png "Seguridad e inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="305f7-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="305f7-193">En hello **Single Sign-On** configuración, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="305f7-193">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
    
    <span data-ttu-id="305f7-194">![Inicio de sesión único](./media/active-directory-saas-aha-tutorial/IC798954.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="305f7-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="305f7-195">a.</span><span class="sxs-lookup"><span data-stu-id="305f7-195">a.</span></span> <span data-ttu-id="305f7-196">Hola **nombre** cuadro de texto, escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="305f7-196">In hello **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="305f7-197">b.</span><span class="sxs-lookup"><span data-stu-id="305f7-197">b.</span></span> <span data-ttu-id="305f7-198">En **Configurar con**, seleccione **Archivo de metadatos**.</span><span class="sxs-lookup"><span data-stu-id="305f7-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="305f7-199">c.</span><span class="sxs-lookup"><span data-stu-id="305f7-199">c.</span></span> <span data-ttu-id="305f7-200">tooupload el archivo de metadatos descargado, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="305f7-200">tooupload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="305f7-201">d.</span><span class="sxs-lookup"><span data-stu-id="305f7-201">d.</span></span> <span data-ttu-id="305f7-202">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="305f7-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="305f7-203">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="305f7-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="305f7-204">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="305f7-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="305f7-205">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="305f7-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="305f7-206">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="305f7-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="305f7-207">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="305f7-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="305f7-209">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="305f7-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="305f7-210">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="305f7-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="305f7-212">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="305f7-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="305f7-214">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="305f7-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="305f7-216">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="305f7-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="305f7-218">a.</span><span class="sxs-lookup"><span data-stu-id="305f7-218">a.</span></span> <span data-ttu-id="305f7-219">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="305f7-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="305f7-220">b.</span><span class="sxs-lookup"><span data-stu-id="305f7-220">b.</span></span> <span data-ttu-id="305f7-221">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="305f7-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="305f7-222">c.</span><span class="sxs-lookup"><span data-stu-id="305f7-222">c.</span></span> <span data-ttu-id="305f7-223">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="305f7-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="305f7-224">d.</span><span class="sxs-lookup"><span data-stu-id="305f7-224">d.</span></span> <span data-ttu-id="305f7-225">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="305f7-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="305f7-226">Creación de un</span><span class="sxs-lookup"><span data-stu-id="305f7-226">Creating an Aha!</span></span> <span data-ttu-id="305f7-227">usuario de prueba de Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-227">test user</span></span>

<span data-ttu-id="305f7-228">toolog de los usuarios de Azure AD tooenable en tooAha!, se les deben aprovisionar en Aha!.</span><span class="sxs-lookup"><span data-stu-id="305f7-228">tooenable Azure AD users toolog in tooAha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="305f7-229">En caso de hello de Aha!, el aprovisionamiento es una tarea automatizada.</span><span class="sxs-lookup"><span data-stu-id="305f7-229">In hello case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="305f7-230">No hay ningún elemento de acción para usted.</span><span class="sxs-lookup"><span data-stu-id="305f7-230">There is no action item for you.</span></span>

<span data-ttu-id="305f7-231">Los usuarios se crean automáticamente si es necesario durante Hola primer único inicio de sesión intento.</span><span class="sxs-lookup"><span data-stu-id="305f7-231">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="305f7-232">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-232">You can use any other Aha!</span></span> <span data-ttu-id="305f7-233">que proporcione Aha!</span><span class="sxs-lookup"><span data-stu-id="305f7-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="305f7-234">cuentas de usuario AAD tooprovision.</span><span class="sxs-lookup"><span data-stu-id="305f7-234">tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="305f7-235">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="305f7-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="305f7-236">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAha!.</span><span class="sxs-lookup"><span data-stu-id="305f7-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAha!.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="305f7-238">**tooassign Britta Simon tooAha!, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="305f7-238">**tooassign Britta Simon tooAha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="305f7-239">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="305f7-239">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="305f7-241">En la lista de aplicaciones de hello, seleccione **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="305f7-241">In hello applications list, select **Aha!**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="305f7-243">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="305f7-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="305f7-245">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="305f7-245">Click **Add** button.</span></span> <span data-ttu-id="305f7-246">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="305f7-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="305f7-248">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="305f7-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="305f7-249">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="305f7-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="305f7-250">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="305f7-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="305f7-251">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="305f7-251">Testing single sign-on</span></span>

<span data-ttu-id="305f7-252">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="305f7-252">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="305f7-253">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="305f7-253">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="305f7-254">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="305f7-254">Additional resources</span></span>

* [<span data-ttu-id="305f7-255">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="305f7-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="305f7-256">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="305f7-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

