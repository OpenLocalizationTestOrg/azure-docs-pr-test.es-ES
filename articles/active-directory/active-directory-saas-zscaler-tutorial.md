---
title: "Tutorial: integración de Azure Active Directory con Zscaler | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Zscaler."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2894534f5d6711fd6af618cd699fa5837b5bf26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="12ad2-103">Tutorial: Integración de Azure Active Directory con Zscaler</span><span class="sxs-lookup"><span data-stu-id="12ad2-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="12ad2-104">En este tutorial, aprenderá cómo toointegrate Zscaler con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="12ad2-104">In this tutorial, you learn how toointegrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="12ad2-105">Integración Zscaler con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="12ad2-105">Integrating Zscaler with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="12ad2-106">Puede controlar en Azure AD que tenga acceso tooZscaler</span><span class="sxs-lookup"><span data-stu-id="12ad2-106">You can control in Azure AD who has access tooZscaler</span></span>
- <span data-ttu-id="12ad2-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZscaler (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="12ad2-107">You can enable your users tooautomatically get signed-on tooZscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="12ad2-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="12ad2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="12ad2-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="12ad2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12ad2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="12ad2-110">Prerequisites</span></span>

<span data-ttu-id="12ad2-111">integración de Azure AD con Zscaler tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="12ad2-111">tooconfigure Azure AD integration with Zscaler, you need hello following items:</span></span>

- <span data-ttu-id="12ad2-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="12ad2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="12ad2-113">Una suscripción habilitada para el inicio de sesión único en Zscaler</span><span class="sxs-lookup"><span data-stu-id="12ad2-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="12ad2-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="12ad2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="12ad2-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="12ad2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="12ad2-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="12ad2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="12ad2-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="12ad2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="12ad2-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="12ad2-118">Scenario description</span></span>
<span data-ttu-id="12ad2-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="12ad2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="12ad2-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="12ad2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="12ad2-121">Agregar Zscaler desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="12ad2-121">Adding Zscaler from hello gallery</span></span>
2. <span data-ttu-id="12ad2-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="12ad2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-hello-gallery"></a><span data-ttu-id="12ad2-123">Agregar Zscaler desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="12ad2-123">Adding Zscaler from hello gallery</span></span>
<span data-ttu-id="12ad2-124">integración de hello tooconfigure de Zscaler en Azure AD, deberá tooadd Zscaler de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="12ad2-124">tooconfigure hello integration of Zscaler into Azure AD, you need tooadd Zscaler from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="12ad2-125">**tooadd Zscaler de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="12ad2-125">**tooadd Zscaler from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="12ad2-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="12ad2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="12ad2-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="12ad2-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="12ad2-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="12ad2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="12ad2-133">En el cuadro de búsqueda de hello, escriba **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-133">In hello search box, type **Zscaler**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. <span data-ttu-id="12ad2-135">En el panel de resultados de hello, seleccione **Zscaler**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="12ad2-135">In hello results panel, select **Zscaler**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="12ad2-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="12ad2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="12ad2-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zscaler con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="12ad2-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="12ad2-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Zscaler es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12ad2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler is tooa user in Azure AD.</span></span> <span data-ttu-id="12ad2-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Zscaler debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="12ad2-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler needs toobe established.</span></span>

<span data-ttu-id="12ad2-141">En Zscaler, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="12ad2-141">In Zscaler, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="12ad2-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Zscaler, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="12ad2-142">tooconfigure and test Azure AD single sign-on with Zscaler, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="12ad2-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="12ad2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="12ad2-144">**[Configuración de proxy](#configuring-proxy-settings)**  -configuración de proxy de hello tooconfigure en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="12ad2-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="12ad2-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12ad2-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="12ad2-146">**[Crear un usuario de prueba de Zscaler](#creating-a-zscaler-test-user)**  -toohave un equivalente de Britta Simon en Zscaler que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="12ad2-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - toohave a counterpart of Britta Simon in Zscaler that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="12ad2-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="12ad2-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="12ad2-148">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="12ad2-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="12ad2-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="12ad2-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="12ad2-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Zscaler.</span><span class="sxs-lookup"><span data-stu-id="12ad2-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="12ad2-151">**inicio de sesión único en tooconfigure Azure AD con Zscaler, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="12ad2-151">**tooconfigure Azure AD single sign-on with Zscaler, perform hello following steps:**</span></span>

1. <span data-ttu-id="12ad2-152">En el portal de Azure, en Hola Hola **Zscaler** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-152">In hello Azure portal, on hello **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="12ad2-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="12ad2-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. <span data-ttu-id="12ad2-156">En hello **Zscaler dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="12ad2-156">On hello **Zscaler Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="12ad2-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.zsclaer.net`</span><span class="sxs-lookup"><span data-stu-id="12ad2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="12ad2-159">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="12ad2-159">This value is not real.</span></span> <span data-ttu-id="12ad2-160">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="12ad2-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="12ad2-161">Póngase en contacto con [equipo de soporte técnico de Zscaler cliente](https://www.zscaler.com/company/contact) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="12ad2-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) tooget this value.</span></span> 

4. <span data-ttu-id="12ad2-162">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="12ad2-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. <span data-ttu-id="12ad2-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="12ad2-164">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="12ad2-166">En hello **configuración de Zscaler** sección, haga clic en **configurar Zscaler** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="12ad2-166">On hello **Zscaler Configuration** section, click **Configure Zscaler** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="12ad2-167">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="12ad2-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. <span data-ttu-id="12ad2-169">En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de ZScaler tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="12ad2-169">In a different web browser window, log in tooyour ZScaler company site as an administrator.</span></span>

8. <span data-ttu-id="12ad2-170">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-170">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="12ad2-171">![Administración](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="12ad2-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="12ad2-172">En **Manage Administrators & Roles (Administrar administradores y roles)** haga clic en **Manage Users & Authentication (Administrar usuarios y autenticación)**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="12ad2-173">![Administración de usuarios y autenticación](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Administración de usuarios y autenticación")</span><span class="sxs-lookup"><span data-stu-id="12ad2-173">![Manage Users & Authentication](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="12ad2-174">Hola **elegir opciones de autenticación para su organización** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="12ad2-174">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="12ad2-175">![Autenticación](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="12ad2-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="12ad2-176">a.</span><span class="sxs-lookup"><span data-stu-id="12ad2-176">a.</span></span> <span data-ttu-id="12ad2-177">Seleccione **Authenticate using SAML Single Sign-On**(Autenticarse mediante el inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="12ad2-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="12ad2-178">b.</span><span class="sxs-lookup"><span data-stu-id="12ad2-178">b.</span></span> <span data-ttu-id="12ad2-179">Haga clic en **Configure SAML Single Sign-On Parameters**(Configurar parámetros de inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="12ad2-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="12ad2-180">En hello **configurar SAML Single Sign-On parámetros** página del cuadro de diálogo, realizar pasos de hello y, a continuación, haga clic en **realiza**</span><span class="sxs-lookup"><span data-stu-id="12ad2-180">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="12ad2-181">![Inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="12ad2-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="12ad2-182">a.</span><span class="sxs-lookup"><span data-stu-id="12ad2-182">a.</span></span> <span data-ttu-id="12ad2-183">Hola pegar **SAML Single Sign-On dirección URL del servicio** valor, que haya copiado desde Hola portal de Azure en hello **dirección URL de los usuarios de toowhich del Portal de SAML de Hola se envía para autenticación** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="12ad2-183">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="12ad2-184">b.</span><span class="sxs-lookup"><span data-stu-id="12ad2-184">b.</span></span> <span data-ttu-id="12ad2-185">Hola **atributo que contiene el nombre de inicio de sesión** cuadro de texto, tipo **NameID**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-185">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="12ad2-186">c.</span><span class="sxs-lookup"><span data-stu-id="12ad2-186">c.</span></span> <span data-ttu-id="12ad2-187">tooupload el certificado descargado, haga clic en **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-187">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="12ad2-188">d.</span><span class="sxs-lookup"><span data-stu-id="12ad2-188">d.</span></span> <span data-ttu-id="12ad2-189">Seleccione **Habilitar aprovisionamiento automático de SAML**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-189">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="12ad2-190">En hello **configurar la autenticación de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="12ad2-190">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="12ad2-191">![Administración](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="12ad2-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="12ad2-192">a.</span><span class="sxs-lookup"><span data-stu-id="12ad2-192">a.</span></span> <span data-ttu-id="12ad2-193">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-193">Click **Save**.</span></span>

    <span data-ttu-id="12ad2-194">b.</span><span class="sxs-lookup"><span data-stu-id="12ad2-194">b.</span></span> <span data-ttu-id="12ad2-195">Haga clic en **Activar ahora**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="12ad2-196">Configuración de los valores de proxy</span><span class="sxs-lookup"><span data-stu-id="12ad2-196">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="12ad2-197">configuración de proxy de hello tooconfigure en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="12ad2-197">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="12ad2-198">Inicie **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-198">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="12ad2-199">Seleccione **opciones de Internet** de hello **herramientas** menú Abrir hello **opciones de Internet** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="12ad2-199">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="12ad2-200">![Opciones de Internet](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Opciones de Internet")</span><span class="sxs-lookup"><span data-stu-id="12ad2-200">![Internet Options](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="12ad2-201">Haga clic en hello **conexiones** ficha.</span><span class="sxs-lookup"><span data-stu-id="12ad2-201">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="12ad2-202">![Conexiones](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Conexiones")</span><span class="sxs-lookup"><span data-stu-id="12ad2-202">![Connections](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="12ad2-203">Haga clic en **configuración de LAN** tooopen hello **configuración de LAN** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="12ad2-203">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="12ad2-204">En la sección servidor Proxy hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="12ad2-204">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="12ad2-205">![Servidor proxy](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Servidor proxy")</span><span class="sxs-lookup"><span data-stu-id="12ad2-205">![Proxy server](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="12ad2-206">a.</span><span class="sxs-lookup"><span data-stu-id="12ad2-206">a.</span></span> <span data-ttu-id="12ad2-207">Seleccione **Usar un servidor proxy para la LAN**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="12ad2-208">b.</span><span class="sxs-lookup"><span data-stu-id="12ad2-208">b.</span></span> <span data-ttu-id="12ad2-209">En el cuadro de texto de dirección de hello, escriba **gateway.zscaler.net**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-209">In hello Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="12ad2-210">c.</span><span class="sxs-lookup"><span data-stu-id="12ad2-210">c.</span></span> <span data-ttu-id="12ad2-211">En el cuadro de texto de puerto de hello, escriba **80**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-211">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="12ad2-212">d.</span><span class="sxs-lookup"><span data-stu-id="12ad2-212">d.</span></span> <span data-ttu-id="12ad2-213">Seleccione **No usar servidor proxy para direcciones locales**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="12ad2-214">e.</span><span class="sxs-lookup"><span data-stu-id="12ad2-214">e.</span></span> <span data-ttu-id="12ad2-215">Haga clic en **Aceptar** tooclose hello **configuración de red de área Local (LAN)** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="12ad2-215">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="12ad2-216">Haga clic en **Aceptar** tooclose hello **opciones de Internet** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="12ad2-216">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="12ad2-217">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="12ad2-217">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="12ad2-218">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="12ad2-218">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="12ad2-219">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="12ad2-219">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="12ad2-220">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="12ad2-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="12ad2-221">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="12ad2-221">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="12ad2-223">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="12ad2-223">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="12ad2-224">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="12ad2-224">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="12ad2-226">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-226">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="12ad2-228">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="12ad2-228">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="12ad2-230">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="12ad2-230">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="12ad2-232">a.</span><span class="sxs-lookup"><span data-stu-id="12ad2-232">a.</span></span> <span data-ttu-id="12ad2-233">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-233">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="12ad2-234">b.</span><span class="sxs-lookup"><span data-stu-id="12ad2-234">b.</span></span> <span data-ttu-id="12ad2-235">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="12ad2-235">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="12ad2-236">c.</span><span class="sxs-lookup"><span data-stu-id="12ad2-236">c.</span></span> <span data-ttu-id="12ad2-237">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-237">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="12ad2-238">d.</span><span class="sxs-lookup"><span data-stu-id="12ad2-238">d.</span></span> <span data-ttu-id="12ad2-239">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="12ad2-240">Creación de un usuario de prueba de Zscaler</span><span class="sxs-lookup"><span data-stu-id="12ad2-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="12ad2-241">toolog de los usuarios de Azure AD tooenable en tooZScaler, deben ser tooZScaler aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="12ad2-241">tooenable Azure AD users toolog in tooZScaler, they must be provisioned tooZScaler.</span></span>  
<span data-ttu-id="12ad2-242">En caso de hello de ZScaler, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="12ad2-242">In hello case of ZScaler, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="12ad2-243">tooconfigure aprovisionamiento de usuario, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="12ad2-243">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="12ad2-244">Inicie sesión en tooyour **Zscaler** inquilino.</span><span class="sxs-lookup"><span data-stu-id="12ad2-244">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="12ad2-245">Haga clic en **Administración**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="12ad2-246">![Administración](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="12ad2-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="12ad2-247">Haga clic en **User Management**(Administración de usuarios).</span><span class="sxs-lookup"><span data-stu-id="12ad2-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="12ad2-248">![Agregar](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="12ad2-248">![Add](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="12ad2-249">Hola **usuarios** , haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-249">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="12ad2-250">![Agregar](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="12ad2-250">![Add](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="12ad2-251">En la sección Agregar usuario hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="12ad2-251">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="12ad2-252">![Agregar usuario](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="12ad2-252">![Add User](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="12ad2-253">a.</span><span class="sxs-lookup"><span data-stu-id="12ad2-253">a.</span></span> <span data-ttu-id="12ad2-254">Hola de tipo **UserID**, **usuario DisplayName**, **contraseña**, **Confirmar contraseña**y, a continuación, seleccione **grupos**hello y **departamento** de una cuenta válida de AAD que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="12ad2-254">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="12ad2-255">b.</span><span class="sxs-lookup"><span data-stu-id="12ad2-255">b.</span></span> <span data-ttu-id="12ad2-256">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="12ad2-257">Puede usar cualquier otra ZScaler usuario cuenta herramienta de creación o las API proporcionadas por ZScaler tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="12ad2-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="12ad2-258">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="12ad2-258">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="12ad2-259">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooZscaler.</span><span class="sxs-lookup"><span data-stu-id="12ad2-259">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="12ad2-261">**tooassign Britta Simon tooZscaler, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="12ad2-261">**tooassign Britta Simon tooZscaler, perform hello following steps:**</span></span>

1. <span data-ttu-id="12ad2-262">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-262">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="12ad2-264">En la lista de aplicaciones de hello, seleccione **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-264">In hello applications list, select **Zscaler**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. <span data-ttu-id="12ad2-266">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-266">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="12ad2-268">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-268">Click **Add** button.</span></span> <span data-ttu-id="12ad2-269">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="12ad2-271">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="12ad2-271">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="12ad2-272">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-272">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="12ad2-273">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="12ad2-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="12ad2-274">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="12ad2-274">Testing single sign-on</span></span>

<span data-ttu-id="12ad2-275">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="12ad2-275">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="12ad2-276">Al hacer clic en icono de Zscaler Hola Hola Panel de acceso, deberá obtener la aplicación de Zscaler tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="12ad2-276">When you click hello Zscaler tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler application.</span></span>
<span data-ttu-id="12ad2-277">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="12ad2-277">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12ad2-278">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="12ad2-278">Additional resources</span></span>

* [<span data-ttu-id="12ad2-279">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12ad2-279">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12ad2-280">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="12ad2-280">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

