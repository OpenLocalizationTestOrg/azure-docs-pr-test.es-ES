---
title: "Tutorial: Integración de Azure Active Directory con TalentLMS | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 25538086602e58fbaab0fbf223f5b03908a74922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="19692-103">Tutorial: integración de Azure Active Directory con TalentLMS</span><span class="sxs-lookup"><span data-stu-id="19692-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="19692-104">En este tutorial, aprenderá cómo toointegrate TalentLMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19692-104">In this tutorial, you learn how toointegrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19692-105">Integración TalentLMS con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="19692-105">Integrating TalentLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="19692-106">Puede controlar en Azure AD que tenga acceso tooTalentLMS</span><span class="sxs-lookup"><span data-stu-id="19692-106">You can control in Azure AD who has access tooTalentLMS</span></span>
- <span data-ttu-id="19692-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTalentLMS (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19692-107">You can enable your users tooautomatically get signed-on tooTalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="19692-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="19692-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="19692-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="19692-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19692-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="19692-110">Prerequisites</span></span>

<span data-ttu-id="19692-111">integración de Azure AD con TalentLMS tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="19692-111">tooconfigure Azure AD integration with TalentLMS, you need hello following items:</span></span>

- <span data-ttu-id="19692-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19692-112">An Azure AD subscription</span></span>
- <span data-ttu-id="19692-113">Una suscripción habilitada para el inicio de sesión único en TalentLMS</span><span class="sxs-lookup"><span data-stu-id="19692-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="19692-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="19692-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="19692-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="19692-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19692-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="19692-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="19692-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19692-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19692-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="19692-118">Scenario description</span></span>
<span data-ttu-id="19692-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="19692-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="19692-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="19692-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19692-121">Agregar TalentLMS desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="19692-121">Adding TalentLMS from hello gallery</span></span>
2. <span data-ttu-id="19692-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19692-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-hello-gallery"></a><span data-ttu-id="19692-123">Agregar TalentLMS desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="19692-123">Adding TalentLMS from hello gallery</span></span>
<span data-ttu-id="19692-124">integración de hello tooconfigure de TalentLMS en Azure AD, deberá tooadd TalentLMS de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="19692-124">tooconfigure hello integration of TalentLMS into Azure AD, you need tooadd TalentLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="19692-125">**tooadd TalentLMS de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="19692-125">**tooadd TalentLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="19692-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="19692-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="19692-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="19692-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="19692-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="19692-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="19692-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="19692-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="19692-133">En el cuadro de búsqueda de hello, escriba **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="19692-133">In hello search box, type **TalentLMS**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="19692-135">En el panel de resultados de hello, seleccione **TalentLMS**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="19692-135">In hello results panel, select **TalentLMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="19692-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19692-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="19692-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TalentLMS con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="19692-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="19692-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TalentLMS es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19692-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TalentLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="19692-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TalentLMS debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="19692-140">In other words, a link relationship between an Azure AD user and hello related user in TalentLMS needs toobe established.</span></span>

<span data-ttu-id="19692-141">En TalentLMS, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19692-141">In TalentLMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="19692-142">tooconfigure y prueba de inicio de sesión único en Azure AD con TalentLMS, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="19692-142">tooconfigure and test Azure AD single sign-on with TalentLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="19692-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="19692-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="19692-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19692-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19692-145">**[Crear un usuario de prueba de TalentLMS](#creating-a-talentlms-test-user)**  -toohave un equivalente de Britta Simon en TalentLMS que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="19692-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - toohave a counterpart of Britta Simon in TalentLMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="19692-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="19692-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19692-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="19692-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="19692-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19692-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="19692-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="19692-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="19692-150">**inicio de sesión único en tooconfigure Azure AD con TalentLMS, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="19692-150">**tooconfigure Azure AD single sign-on with TalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="19692-151">En el portal de Azure, en Hola Hola **TalentLMS** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="19692-151">In hello Azure portal, on hello **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="19692-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="19692-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="19692-155">En hello **TalentLMS dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="19692-155">On hello **TalentLMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="19692-157">a.</span><span class="sxs-lookup"><span data-stu-id="19692-157">a.</span></span> <span data-ttu-id="19692-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="19692-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="19692-159">b.</span><span class="sxs-lookup"><span data-stu-id="19692-159">b.</span></span> <span data-ttu-id="19692-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="19692-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="19692-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="19692-161">These values are not real.</span></span> <span data-ttu-id="19692-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="19692-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="19692-163">Póngase en contacto con [equipo de soporte técnico de cliente de TalentLMS](https://www.talentlms.com/contact) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="19692-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="19692-164">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** valor de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="19692-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="19692-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="19692-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="19692-168">En hello **configuración de TalentLMS** sección, haga clic en **configurar TalentLMS** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="19692-168">On hello **TalentLMS Configuration** section, click **Configure TalentLMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="19692-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="19692-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="19692-171">En una ventana del explorador web diferente, inicie sesión en el sitio de la empresa TalentLMS tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="19692-171">In a different web browser window, log in tooyour TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="19692-172">Hola **cuenta de & configuración** sección, haga clic en hello **usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="19692-172">In hello **Account & Settings** section, click hello **Users** tab.</span></span>
   
    <span data-ttu-id="19692-173">![Cuenta y configuración](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Cuenta y configuración")</span><span class="sxs-lookup"><span data-stu-id="19692-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="19692-174">Haga clic en **Inicio de sesión único (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="19692-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="19692-175">Hola sección Single Sign-On, realice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="19692-175">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="19692-176">![Inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="19692-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="19692-177">a.</span><span class="sxs-lookup"><span data-stu-id="19692-177">a.</span></span> <span data-ttu-id="19692-178">De hello **tipo de integración de SSO** lista, seleccione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="19692-178">From hello **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="19692-179">b.</span><span class="sxs-lookup"><span data-stu-id="19692-179">b.</span></span> <span data-ttu-id="19692-180">Hola **proveedor de identidades (IDP)** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="19692-180">In hello **Identity provider (IDP)** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="19692-181">c.</span><span class="sxs-lookup"><span data-stu-id="19692-181">c.</span></span> <span data-ttu-id="19692-182">Hola pegar **huella digital** valor desde el portal de Azure en hello **huella digital de certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="19692-182">Paste hello **Thumbprint** value from Azure portal into hello **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="19692-183">d.</span><span class="sxs-lookup"><span data-stu-id="19692-183">d.</span></span>  <span data-ttu-id="19692-184">Hola **dirección URL de inicio de sesión remoto** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="19692-184">In hello **Remote sign-in URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="19692-185">e.</span><span class="sxs-lookup"><span data-stu-id="19692-185">e.</span></span> <span data-ttu-id="19692-186">Hola **dirección URL de cierre de sesión remoto** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="19692-186">In hello **Remote sign-out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="19692-187">f.</span><span class="sxs-lookup"><span data-stu-id="19692-187">f.</span></span> <span data-ttu-id="19692-188">Rellene los siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="19692-188">Fill in hello following:</span></span> 

    * <span data-ttu-id="19692-189">Hola **Id. dirigido** cuadro de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="19692-189">In hello **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="19692-190">Hola **nombre** cuadro de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="19692-190">In hello **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="19692-191">Hola **apellidos** cuadro de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="19692-191">In hello **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="19692-192">Hola **correo electrónico** cuadro de texto, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="19692-192">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="19692-193">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="19692-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="19692-194">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="19692-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="19692-195">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="19692-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="19692-196">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="19692-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="19692-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19692-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="19692-198">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="19692-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="19692-200">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="19692-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="19692-201">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="19692-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="19692-203">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="19692-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="19692-205">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19692-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="19692-207">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="19692-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="19692-209">a.</span><span class="sxs-lookup"><span data-stu-id="19692-209">a.</span></span> <span data-ttu-id="19692-210">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="19692-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="19692-211">b.</span><span class="sxs-lookup"><span data-stu-id="19692-211">b.</span></span> <span data-ttu-id="19692-212">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="19692-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="19692-213">c.</span><span class="sxs-lookup"><span data-stu-id="19692-213">c.</span></span> <span data-ttu-id="19692-214">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="19692-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="19692-215">d.</span><span class="sxs-lookup"><span data-stu-id="19692-215">d.</span></span> <span data-ttu-id="19692-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="19692-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="19692-217">Creación de un usuario de prueba de TalentLMS</span><span class="sxs-lookup"><span data-stu-id="19692-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="19692-218">toolog de los usuarios de Azure AD tooenable en tooTalentLMS, se les deben aprovisionar en TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="19692-218">tooenable Azure AD users toolog in tooTalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="19692-219">En caso de hello de TalentLMS, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="19692-219">In hello case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="19692-220">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="19692-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="19692-221">Inicie sesión en tooyour **TalentLMS** inquilino.</span><span class="sxs-lookup"><span data-stu-id="19692-221">Log in tooyour **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="19692-222">Haga clic en **Users** (Usuarios) y, luego, en **Add User** (Agregar usuario).</span><span class="sxs-lookup"><span data-stu-id="19692-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="19692-223">En hello **para agregar un usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="19692-223">On hello **Add user** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="19692-224">![Agregar usuario](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="19692-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="19692-225">a.</span><span class="sxs-lookup"><span data-stu-id="19692-225">a.</span></span> <span data-ttu-id="19692-226">Hola **nombre** cuadro de texto, escriba Hola nombre de usuario como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="19692-226">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="19692-227">b.</span><span class="sxs-lookup"><span data-stu-id="19692-227">b.</span></span> <span data-ttu-id="19692-228">Hola **apellidos** cuadro de texto, escriba Hola último nombre de usuario como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="19692-228">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="19692-229">c.</span><span class="sxs-lookup"><span data-stu-id="19692-229">c.</span></span> <span data-ttu-id="19692-230">Hola **dirección de correo electrónico** cuadro de texto, escriba el correo electrónico de saludo del usuario como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="19692-230">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="19692-231">d.</span><span class="sxs-lookup"><span data-stu-id="19692-231">d.</span></span> <span data-ttu-id="19692-232">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="19692-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="19692-233">Puede usar cualquier otra TalentLMS usuario cuenta herramienta de creación o las API proporcionadas por TalentLMS tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="19692-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="19692-234">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="19692-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="19692-235">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTalentLMS.</span><span class="sxs-lookup"><span data-stu-id="19692-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTalentLMS.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="19692-237">**tooassign Britta Simon tooTalentLMS, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="19692-237">**tooassign Britta Simon tooTalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="19692-238">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="19692-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="19692-240">En la lista de aplicaciones de hello, seleccione **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="19692-240">In hello applications list, select **TalentLMS**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="19692-242">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="19692-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="19692-244">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="19692-244">Click **Add** button.</span></span> <span data-ttu-id="19692-245">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="19692-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="19692-247">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="19692-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="19692-248">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="19692-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="19692-249">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="19692-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="19692-250">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="19692-250">Testing single sign-on</span></span>

<span data-ttu-id="19692-251">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="19692-251">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="19692-252">Al hacer clic en hello TalentLMS disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour TalentLMS aplicación</span><span class="sxs-lookup"><span data-stu-id="19692-252">When you click hello TalentLMS tile in hello Access Panel, you should get automatically signed-on tooyour TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19692-253">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="19692-253">Additional resources</span></span>

* [<span data-ttu-id="19692-254">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19692-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19692-255">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="19692-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

