---
title: "Tutorial: Integración de Azure Active Directory con Salesforce | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="48ff7-103">Tutorial: Integración de Azure Active Directory con Salesforce</span><span class="sxs-lookup"><span data-stu-id="48ff7-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="48ff7-104">En este tutorial, aprenderá cómo toointegrate Salesforce con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48ff7-104">In this tutorial, you learn how toointegrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48ff7-105">Integración de Salesforce con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="48ff7-105">Integrating Salesforce with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="48ff7-106">Puede controlar en Azure AD que tenga acceso tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="48ff7-106">You can control in Azure AD who has access tooSalesforce</span></span>
- <span data-ttu-id="48ff7-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSalesforce (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ff7-107">You can enable your users tooautomatically get signed-on tooSalesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48ff7-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="48ff7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="48ff7-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48ff7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48ff7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="48ff7-110">Prerequisites</span></span>

<span data-ttu-id="48ff7-111">tooconfigure integración de Azure AD con Salesforce, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="48ff7-111">tooconfigure Azure AD integration with Salesforce, you need hello following items:</span></span>

- <span data-ttu-id="48ff7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ff7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48ff7-113">Una suscripción habilitada para el inicio de sesión único en Salesforce</span><span class="sxs-lookup"><span data-stu-id="48ff7-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48ff7-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="48ff7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48ff7-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="48ff7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48ff7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="48ff7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48ff7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48ff7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48ff7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="48ff7-118">Scenario description</span></span>
<span data-ttu-id="48ff7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="48ff7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48ff7-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="48ff7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48ff7-121">Adición de Salesforce de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="48ff7-121">Adding Salesforce from hello gallery</span></span>
2. <span data-ttu-id="48ff7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ff7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-hello-gallery"></a><span data-ttu-id="48ff7-123">Adición de Salesforce de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="48ff7-123">Adding Salesforce from hello gallery</span></span>
<span data-ttu-id="48ff7-124">integración de hello tooconfigure de Salesforce en Azure AD, deberá tooadd Salesforce de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="48ff7-124">tooconfigure hello integration of Salesforce into Azure AD, you need tooadd Salesforce from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="48ff7-125">**tooadd Salesforce desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="48ff7-125">**tooadd Salesforce from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ff7-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="48ff7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="48ff7-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="48ff7-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="48ff7-131">Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="48ff7-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="48ff7-133">En el cuadro de búsqueda de hello, escriba **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-133">In hello search box, type **Salesforce**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="48ff7-135">En el panel de resultados de hello, seleccione **Salesforce**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="48ff7-135">In hello results panel, select **Salesforce**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48ff7-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ff7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48ff7-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Salesforce con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="48ff7-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="48ff7-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Salesforce es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48ff7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce is tooa user in Azure AD.</span></span> <span data-ttu-id="48ff7-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Salesforce debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="48ff7-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce needs toobe established.</span></span>

<span data-ttu-id="48ff7-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="48ff7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce.</span></span>

<span data-ttu-id="48ff7-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Salesforce, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="48ff7-142">tooconfigure and test Azure AD single sign-on with Salesforce, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="48ff7-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="48ff7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="48ff7-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48ff7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48ff7-145">**[Crear un usuario de prueba de Salesforce](#creating-a-salesforce-test-user)**  -toohave un equivalente de Britta Simon en Salesforce que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="48ff7-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - toohave a counterpart of Britta Simon in Salesforce that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="48ff7-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="48ff7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48ff7-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="48ff7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48ff7-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ff7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48ff7-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="48ff7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="48ff7-150">**inicio de sesión único en tooconfigure Azure AD con Salesforce, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="48ff7-150">**tooconfigure Azure AD single sign-on with Salesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ff7-151">En el portal de Azure, en Hola Hola **Salesforce** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-151">In hello Azure portal, on hello **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="48ff7-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="48ff7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="48ff7-155">En hello **dominio de Salesforce y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="48ff7-155">On hello **Salesforce Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="48ff7-157">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:</span><span class="sxs-lookup"><span data-stu-id="48ff7-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern:</span></span> 
   * <span data-ttu-id="48ff7-158">Cuenta de empresa: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="48ff7-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="48ff7-159">Cuenta de desarrollador: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="48ff7-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48ff7-160">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="48ff7-160">These values are not hello real.</span></span> <span data-ttu-id="48ff7-161">Actualizar estos valores con la URL de inicio de sesión real de Hola.</span><span class="sxs-lookup"><span data-stu-id="48ff7-161">Update these values with hello actual Sign-on URL.</span></span> <span data-ttu-id="48ff7-162">Póngase en contacto con [equipo de soporte técnico de Salesforce cliente](https://help.salesforce.com/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="48ff7-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="48ff7-163">En hello **el certificado de firma de SAML** sección, haga clic en **certificado** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="48ff7-163">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="48ff7-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="48ff7-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48ff7-167">En hello **configuración de Salesforce** sección, haga clic en **configurar Salesforce** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="48ff7-167">On hello **Salesforce Configuration** section, click **Configure Salesforce** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="48ff7-168">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="48ff7-168">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    <span data-ttu-id="48ff7-169">![Configuración del inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="48ff7-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="48ff7-170">Abra una nueva pestaña en el explorador e inicie sesión tooyour cuenta de administrador de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="48ff7-170">Open a new tab in your browser and log in tooyour Salesforce administrator account.</span></span>

8.  <span data-ttu-id="48ff7-171">En hello **administrador** panel de navegación, haga clic en **controles de seguridad** tooexpand Hola relacionados con la sección.</span><span class="sxs-lookup"><span data-stu-id="48ff7-171">Under hello **Administrator** navigation pane, click **Security Controls** tooexpand hello related section.</span></span> <span data-ttu-id="48ff7-172">A continuación, haga clic en **Configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-172">Then click **Single Sign-On Settings**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="48ff7-174">En hello **configuración de inicio de sesión único** página, haga clic en hello **editar** botón.</span><span class="sxs-lookup"><span data-stu-id="48ff7-174">On hello **Single Sign-On Settings** page, click hello **Edit** button.</span></span>
    <span data-ttu-id="48ff7-175">![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="48ff7-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="48ff7-176">Si está configuración de Single Sign-On no se puede tooenable para su cuenta de Salesforce, puede que necesite toocontact [equipo de soporte técnico de Salesforce cliente](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="48ff7-176">If you are unable tooenable Single Sign-On settings for your Salesforce account, you may need toocontact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="48ff7-177">Seleccione **SAML habilitado** y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="48ff7-179">tooconfigure su SAML único inicio de sesión en configuración, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-179">tooconfigure your SAML single sign-on settings, click **New**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="48ff7-181">En hello **SAML Single Sign-On editar la configuración de** página, asegúrese de hello siguiendo configuraciones:</span><span class="sxs-lookup"><span data-stu-id="48ff7-181">On hello **SAML Single Sign-On Setting Edit** page, make hello following configurations:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="48ff7-183">a.</span><span class="sxs-lookup"><span data-stu-id="48ff7-183">a.</span></span> <span data-ttu-id="48ff7-184">Para hello **nombre** , escriba un nombre descriptivo para esta configuración.</span><span class="sxs-lookup"><span data-stu-id="48ff7-184">For hello **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="48ff7-185">Proporciona un valor para **nombre** rellenar automáticamente hello **nombre de la API** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="48ff7-185">Providing a value for **Name** automatically populate hello **API Name** textbox.</span></span>

    <span data-ttu-id="48ff7-186">b.</span><span class="sxs-lookup"><span data-stu-id="48ff7-186">b.</span></span> <span data-ttu-id="48ff7-187">Pegar **Id. de entidad Small** valor en hello **emisor** campo Salesforce.</span><span class="sxs-lookup"><span data-stu-id="48ff7-187">Paste **SMAL Entity ID** value into hello **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="48ff7-188">c.</span><span class="sxs-lookup"><span data-stu-id="48ff7-188">c.</span></span> <span data-ttu-id="48ff7-189">Hola **cuadro de texto Id. de entidad**, escriba el nombre de dominio de Salesforce con hello sigue el patrón:</span><span class="sxs-lookup"><span data-stu-id="48ff7-189">In hello **Entity Id textbox**, type your Salesforce domain name using hello following pattern:</span></span>
      
      * <span data-ttu-id="48ff7-190">Cuenta de empresa: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="48ff7-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="48ff7-191">Cuenta de desarrollador: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="48ff7-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="48ff7-192">d.</span><span class="sxs-lookup"><span data-stu-id="48ff7-192">d.</span></span> <span data-ttu-id="48ff7-193">Haga clic en **examinar** o **Elegir archivo** tooopen hello **tooUpload Elegir archivo** cuadro de diálogo, seleccione el certificado de Salesforce y, a continuación, haga clic en **abrir**certificado de hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="48ff7-193">Click **Browse** or **Choose File** tooopen hello **Choose File tooUpload** dialog, select your Salesforce certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="48ff7-194">e.</span><span class="sxs-lookup"><span data-stu-id="48ff7-194">e.</span></span> <span data-ttu-id="48ff7-195">En **SAML Identity Type** (Tipo de identidad de SAML), seleccione **Assertion contains User's salesforce.com username** (La aserción contiene el nombre de usuario de salesforce.com del usuario).</span><span class="sxs-lookup"><span data-stu-id="48ff7-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="48ff7-196">f.</span><span class="sxs-lookup"><span data-stu-id="48ff7-196">f.</span></span> <span data-ttu-id="48ff7-197">Para **ubicación de identidad SAML**, seleccione **identidad está en el elemento NameIdentifier de Hola de hello instrucción Subject**</span><span class="sxs-lookup"><span data-stu-id="48ff7-197">For **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**</span></span>

    <span data-ttu-id="48ff7-198">g.</span><span class="sxs-lookup"><span data-stu-id="48ff7-198">g.</span></span> <span data-ttu-id="48ff7-199">Pegar **URL de servicio de inicio de sesión único** en hello **URL de inicio de sesión del proveedor de identidades** campo Salesforce.</span><span class="sxs-lookup"><span data-stu-id="48ff7-199">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="48ff7-200">h.</span><span class="sxs-lookup"><span data-stu-id="48ff7-200">h.</span></span> <span data-ttu-id="48ff7-201">En **Service Provider Initiated Request Binding** (Vinculación de solicitud iniciada del proveedor de servicios), seleccione **HTTP Redirect** (Redirección HTTP).</span><span class="sxs-lookup"><span data-stu-id="48ff7-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="48ff7-202">i.</span><span class="sxs-lookup"><span data-stu-id="48ff7-202">i.</span></span> <span data-ttu-id="48ff7-203">Por último, haga clic en **guardar** tooapply las opciones de inicio de sesión único de SAML.</span><span class="sxs-lookup"><span data-stu-id="48ff7-203">Finally, click **Save** tooapply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="48ff7-204">En el panel de navegación izquierdo de hello en Salesforce, haga clic en **Domain Management** tooexpand Hola sección relacionada y, a continuación, haga clic en **mi dominio**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-204">On hello left navigation pane in Salesforce, click **Domain Management** tooexpand hello related section, and then click **My Domain**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="48ff7-206">Desplácese hacia abajo toohello **configuración de autenticación** sección y haga clic en hello **editar** botón.</span><span class="sxs-lookup"><span data-stu-id="48ff7-206">Scroll down toohello **Authentication Configuration** section, and click hello **Edit** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="48ff7-208">Hola **servicio de autenticación** sección, seleccione Hola nombre descriptivo de la configuración de SSO de SAML y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-208">In hello **Authentication Service** section, select hello friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="48ff7-210">Si se selecciona más de un servicio de autenticación, los usuarios son solicitada tooselect qué servicio de autenticación que deseen toosign sesión al iniciar el entorno de Salesforce tooyour de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="48ff7-210">If more than one authentication service is selected, users are prompted tooselect which authentication service they like toosign in with while initiating single sign-on tooyour Salesforce environment.</span></span> <span data-ttu-id="48ff7-211">Si no desea toohappen, entonces debe **dejar sin seleccionar todos los demás servicios de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-211">If you don’t want it toohappen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="48ff7-212">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="48ff7-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="48ff7-213">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="48ff7-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="48ff7-214">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48ff7-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48ff7-215">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ff7-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="48ff7-216">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="48ff7-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="48ff7-218">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="48ff7-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ff7-219">En el panel de navegación izquierdo de Hola Hola **portal de Azure**, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="48ff7-219">On hello left navigation pane in hello **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48ff7-221">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-221">toodisplay hello list of users, Go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48ff7-223">En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="48ff7-223">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48ff7-225">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="48ff7-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48ff7-227">a.</span><span class="sxs-lookup"><span data-stu-id="48ff7-227">a.</span></span> <span data-ttu-id="48ff7-228">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48ff7-229">b.</span><span class="sxs-lookup"><span data-stu-id="48ff7-229">b.</span></span> <span data-ttu-id="48ff7-230">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="48ff7-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48ff7-231">c.</span><span class="sxs-lookup"><span data-stu-id="48ff7-231">c.</span></span> <span data-ttu-id="48ff7-232">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="48ff7-233">d.</span><span class="sxs-lookup"><span data-stu-id="48ff7-233">d.</span></span> <span data-ttu-id="48ff7-234">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="48ff7-235">Creación de un usuario de prueba de Salesforce</span><span class="sxs-lookup"><span data-stu-id="48ff7-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="48ff7-236">En esta sección, creará un usuario llamado a Britta Simon en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="48ff7-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="48ff7-237">Salesforce admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="48ff7-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="48ff7-238">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="48ff7-238">There is no action item for you in this section.</span></span> <span data-ttu-id="48ff7-239">Si un usuario ya no existe en Salesforce, se crea uno nuevo si intentas tooaccess Salesforce.</span><span class="sxs-lookup"><span data-stu-id="48ff7-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt tooaccess Salesforce.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="48ff7-240">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ff7-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="48ff7-241">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="48ff7-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="48ff7-243">**tooassign Britta Simon tooSalesforce, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="48ff7-243">**tooassign Britta Simon tooSalesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ff7-244">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="48ff7-246">En la lista de aplicaciones de hello, seleccione **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-246">In hello applications list, select **Salesforce**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="48ff7-248">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="48ff7-250">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-250">Click **Add** button.</span></span> <span data-ttu-id="48ff7-251">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="48ff7-253">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="48ff7-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="48ff7-254">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48ff7-255">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48ff7-256">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="48ff7-256">Testing single sign-on</span></span>

<span data-ttu-id="48ff7-257">tootest Hola de su inicio de sesión configuración de inicio único, abra Panel de acceso en [https://myapps.microsoft.com](https://myapps.microsoft.com/), a continuación, inicie sesión en la cuenta de prueba de Hola y haga clic en **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="48ff7-257">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into hello test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48ff7-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="48ff7-258">Additional resources</span></span>

* [<span data-ttu-id="48ff7-259">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48ff7-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48ff7-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48ff7-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="48ff7-261">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="48ff7-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

