---
title: "Tutorial: Integración de Azure Active Directory con xMatters OnDemand | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y xMatters OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="3a93a-103">Tutorial: Integración de Azure Active Directory con xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="3a93a-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="3a93a-104">En este tutorial, aprenderá cómo toointegrate xMatters OnDemand con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a93a-104">In this tutorial, you learn how toointegrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a93a-105">Integración xMatters OnDemand con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3a93a-105">Integrating xMatters OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3a93a-106">Puede controlar en Azure AD que tenga acceso tooxMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="3a93a-106">You can control in Azure AD who has access tooxMatters OnDemand</span></span>
- <span data-ttu-id="3a93a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooxMatters OnDemand (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a93a-107">You can enable your users tooautomatically get signed-on tooxMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a93a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3a93a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3a93a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a93a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a93a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3a93a-110">Prerequisites</span></span>

<span data-ttu-id="3a93a-111">tooconfigure integración de Azure AD con xMatters OnDemand, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3a93a-111">tooconfigure Azure AD integration with xMatters OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="3a93a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a93a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a93a-113">Una suscripción habilitada para el inicio de sesión único en xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="3a93a-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a93a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3a93a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a93a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3a93a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a93a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3a93a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a93a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a93a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a93a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3a93a-118">Scenario description</span></span>
<span data-ttu-id="3a93a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3a93a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a93a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="3a93a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a93a-121">Agregar xMatters OnDemand desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3a93a-121">Adding xMatters OnDemand from hello gallery</span></span>
2. <span data-ttu-id="3a93a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a93a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a><span data-ttu-id="3a93a-123">Agregar xMatters OnDemand desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3a93a-123">Adding xMatters OnDemand from hello gallery</span></span>
<span data-ttu-id="3a93a-124">integración de hello tooconfigure de xMatters OnDemand en Azure AD, deberá tooadd xMatters OnDemand de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3a93a-124">tooconfigure hello integration of xMatters OnDemand into Azure AD, you need tooadd xMatters OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3a93a-125">**tooadd xMatters OnDemand de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3a93a-125">**tooadd xMatters OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a93a-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3a93a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3a93a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3a93a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3a93a-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3a93a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3a93a-133">En el cuadro de búsqueda de hello, escriba **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-133">In hello search box, type **xMatters OnDemand**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="3a93a-135">En el panel de resultados de hello, seleccione **xMatters OnDemand**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3a93a-135">In hello results panel, select **xMatters OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a93a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a93a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3a93a-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con xMatters OnDemand con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3a93a-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3a93a-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué Hola usuario equivalente en xMatters OnDemand es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a93a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in xMatters OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="3a93a-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en xMatters OnDemand debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="3a93a-140">In other words, a link relationship between an Azure AD user and hello related user in xMatters OnDemand needs toobe established.</span></span>

<span data-ttu-id="3a93a-141">En xMatters OnDemand, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a93a-141">In xMatters OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3a93a-142">tooconfigure y prueba de inicio de sesión único en Azure AD con xMatters OnDemand, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3a93a-142">tooconfigure and test Azure AD single sign-on with xMatters OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3a93a-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="3a93a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3a93a-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a93a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a93a-145">**[Crear un usuario de prueba de xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)**  -toohave un equivalente de Britta Simon en xMatters OnDemand que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="3a93a-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - toohave a counterpart of Britta Simon in xMatters OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a93a-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3a93a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a93a-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3a93a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a93a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a93a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a93a-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en su xMatters OnDemand aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a93a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="3a93a-150">**inicio de sesión único en tooconfigure Azure AD con xMatters OnDemand, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3a93a-150">**tooconfigure Azure AD single sign-on with xMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a93a-151">En el portal de Azure, en Hola Hola **xMatters OnDemand** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-151">In hello Azure portal, on hello **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3a93a-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3a93a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="3a93a-155">En hello **xMatters OnDemand dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3a93a-155">On hello **xMatters OnDemand Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="3a93a-157">a.</span><span class="sxs-lookup"><span data-stu-id="3a93a-157">a.</span></span> <span data-ttu-id="3a93a-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="3a93a-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="3a93a-159">b.</span><span class="sxs-lookup"><span data-stu-id="3a93a-159">b.</span></span> <span data-ttu-id="3a93a-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="3a93a-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="3a93a-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3a93a-161">These values are not real.</span></span> <span data-ttu-id="3a93a-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="3a93a-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="3a93a-163">Póngase en contacto con [equipo de soporte técnico de xMatters OnDemand](https://www.xmatters.com/company/contact-us/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="3a93a-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="3a93a-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde Hola archivo del certificado localmente como **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="3a93a-166">Necesita tooforward Hola certificado toohello [equipo de soporte técnico de xMatters OnDemand](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="3a93a-166">You need tooforward hello certificate toohello [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="3a93a-167">certificado de Hello debe toobe cargada por el equipo de soporte técnico de xMatters Hola antes de finalizar la configuración de inicio de sesión único de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a93a-167">hello certificate needs toobe uploaded by hello xMatters support team before you can finalize hello single sign-on configuration.</span></span> 

5. <span data-ttu-id="3a93a-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3a93a-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3a93a-170">En hello **xMatters OnDemand configuración** sección, haga clic en **configurar xMatters OnDemand** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="3a93a-170">On hello **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3a93a-171">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="3a93a-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="3a93a-173">En una ventana del explorador web diferente, inicie sesión en tooyour sitio de la compañía de XMatters OnDemand como administrador.</span><span class="sxs-lookup"><span data-stu-id="3a93a-173">In a different web browser window, log in tooyour XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="3a93a-174">En la barra de herramientas de hello en la parte superior de hello, haga clic en **administración**y, a continuación, haga clic en **detalles de la compañía** en la barra de navegación de hello en el lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a93a-174">In hello toolbar on hello top, click **Admin**, and then click **Company Details** in hello navigation bar on hello left side.</span></span>
   
    <span data-ttu-id="3a93a-175">![Administración](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="3a93a-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="3a93a-176">En hello **configuración de SAML** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3a93a-176">On hello **SAML Configuration** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="3a93a-177">![Configuración de SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="3a93a-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="3a93a-178">a.</span><span class="sxs-lookup"><span data-stu-id="3a93a-178">a.</span></span> <span data-ttu-id="3a93a-179">Seleccione **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="3a93a-180">b.</span><span class="sxs-lookup"><span data-stu-id="3a93a-180">b.</span></span> <span data-ttu-id="3a93a-181">Pegar **Id. de entidad SAML**, que haya copiado desde Hola portal de Azure en hello **Id. de proveedor de identidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3a93a-181">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="3a93a-182">c.</span><span class="sxs-lookup"><span data-stu-id="3a93a-182">c.</span></span> <span data-ttu-id="3a93a-183">Pegar **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **inicio de sesión único en URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3a93a-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="3a93a-184">d.</span><span class="sxs-lookup"><span data-stu-id="3a93a-184">d.</span></span> <span data-ttu-id="3a93a-185">Pegar **dirección URL de cierre de sesión**, que haya copiado desde Hola portal de Azure en hello **dirección URL de cierre de sesión único** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3a93a-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="3a93a-186">e.</span><span class="sxs-lookup"><span data-stu-id="3a93a-186">e.</span></span> <span data-ttu-id="3a93a-187">En la página de detalles de la compañía de hello, en la parte superior de hello, haga clic en **guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-187">On hello Company Details page, at hello top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="3a93a-188">![Detalles de la compañía](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Detalles de la compañía")</span><span class="sxs-lookup"><span data-stu-id="3a93a-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="3a93a-189">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="3a93a-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3a93a-190">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="3a93a-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3a93a-191">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a93a-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a93a-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a93a-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a93a-193">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="3a93a-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3a93a-195">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3a93a-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a93a-196">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3a93a-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a93a-198">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a93a-200">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a93a-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a93a-202">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3a93a-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a93a-204">a.</span><span class="sxs-lookup"><span data-stu-id="3a93a-204">a.</span></span> <span data-ttu-id="3a93a-205">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a93a-206">b.</span><span class="sxs-lookup"><span data-stu-id="3a93a-206">b.</span></span> <span data-ttu-id="3a93a-207">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3a93a-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3a93a-208">c.</span><span class="sxs-lookup"><span data-stu-id="3a93a-208">c.</span></span> <span data-ttu-id="3a93a-209">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3a93a-210">d.</span><span class="sxs-lookup"><span data-stu-id="3a93a-210">d.</span></span> <span data-ttu-id="3a93a-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="3a93a-212">Creación de un usuario de prueba de xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="3a93a-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="3a93a-213">En orden tooenable toolog de los usuarios de Azure AD en tooXMatters OnDemand, les deben aprovisionar en XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="3a93a-213">In order tooenable Azure AD users toolog in tooXMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="3a93a-214">En caso de hello de XMatters OnDemand, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="3a93a-214">In hello case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="3a93a-215">tooprovision una cuenta de usuario, realizar Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3a93a-215">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="3a93a-216">Inicie sesión en tooyour **XMatters OnDemand** inquilino.</span><span class="sxs-lookup"><span data-stu-id="3a93a-216">Log in tooyour **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="3a93a-217">Haga clic en **usuarios** ficha y, a continuación, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-217">Click **Users** tab. and then click **Add User**.</span></span>
  
    <span data-ttu-id="3a93a-218">![Usuarios](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="3a93a-218">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="3a93a-219">Hola **agregar un usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3a93a-219">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="3a93a-220">![Agregar un usuario](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Agregar un usuario")</span><span class="sxs-lookup"><span data-stu-id="3a93a-220">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="3a93a-221">a.</span><span class="sxs-lookup"><span data-stu-id="3a93a-221">a.</span></span> <span data-ttu-id="3a93a-222">Seleccione **Active**(Activo).</span><span class="sxs-lookup"><span data-stu-id="3a93a-222">Select **Active**.</span></span>

    <span data-ttu-id="3a93a-223">b.</span><span class="sxs-lookup"><span data-stu-id="3a93a-223">b.</span></span> <span data-ttu-id="3a93a-224">Hola **Id. de usuario** cuadro de texto, Id. de usuario de tipo hello del usuario como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3a93a-224">In hello **User ID** textbox, type hello user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="3a93a-225">c.</span><span class="sxs-lookup"><span data-stu-id="3a93a-225">c.</span></span> <span data-ttu-id="3a93a-226">Hola **nombre** cuadro de texto Nombre de usuario de hello como Bárbara tipo.</span><span class="sxs-lookup"><span data-stu-id="3a93a-226">In hello **First Name** textbox, type first name of hello user like Britta.</span></span>

    <span data-ttu-id="3a93a-227">d.</span><span class="sxs-lookup"><span data-stu-id="3a93a-227">d.</span></span> <span data-ttu-id="3a93a-228">Hola **Last Name** cuadro de texto, escriba Apellidos del usuario de hello como Simon.</span><span class="sxs-lookup"><span data-stu-id="3a93a-228">In hello **Last Name** textbox, type last name of hello user like Simon.</span></span>
    
    <span data-ttu-id="3a93a-229">e.</span><span class="sxs-lookup"><span data-stu-id="3a93a-229">e.</span></span> <span data-ttu-id="3a93a-230">Hola **sitio** cuadro de texto, sitio válido de hello entrar un Azure válida que desee tooprovision de cuenta de AD.</span><span class="sxs-lookup"><span data-stu-id="3a93a-230">In hello **Site** textbox, Enter hello valid site of a valid Azure AD account you want tooprovision.</span></span>
    
    <span data-ttu-id="3a93a-231">f.</span><span class="sxs-lookup"><span data-stu-id="3a93a-231">f.</span></span> <span data-ttu-id="3a93a-232">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-232">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3a93a-233">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a93a-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3a93a-234">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooxMatters a petición.</span><span class="sxs-lookup"><span data-stu-id="3a93a-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooxMatters OnDemand.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3a93a-236">**tooassign Britta Simon tooxMatters OnDemand, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3a93a-236">**tooassign Britta Simon tooxMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a93a-237">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3a93a-239">En la lista de aplicaciones de hello, seleccione **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-239">In hello applications list, select **xMatters OnDemand**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="3a93a-241">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3a93a-243">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-243">Click **Add** button.</span></span> <span data-ttu-id="3a93a-244">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3a93a-246">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a93a-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3a93a-247">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a93a-248">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3a93a-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3a93a-249">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3a93a-249">Testing single sign-on</span></span>

<span data-ttu-id="3a93a-250">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3a93a-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3a93a-251">Al hacer clic en hello xMatters OnDemand icono en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour xMatters OnDemand aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a93a-251">When you click hello xMatters OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour xMatters OnDemand application.</span></span>
<span data-ttu-id="3a93a-252">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3a93a-252">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a93a-253">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3a93a-253">Additional resources</span></span>

* [<span data-ttu-id="3a93a-254">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a93a-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a93a-255">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3a93a-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

