---
title: "Tutorial: integración de Azure Active Directory con ZScaler ZSCloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="98aea-103">Tutorial: integración de Azure Active Directory con ZScaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="98aea-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="98aea-104">En este tutorial, aprenderá cómo toointegrate Zscaler ZSCloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="98aea-104">In this tutorial, you learn how toointegrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="98aea-105">Integración de Zscaler ZSCloud con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="98aea-105">Integrating Zscaler ZSCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="98aea-106">Puede controlar en Azure AD que tenga acceso tooZscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="98aea-106">You can control in Azure AD who has access tooZscaler ZSCloud</span></span>
- <span data-ttu-id="98aea-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZscaler ZSCloud (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98aea-107">You can enable your users tooautomatically get signed-on tooZscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="98aea-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="98aea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="98aea-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="98aea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98aea-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="98aea-110">Prerequisites</span></span>

<span data-ttu-id="98aea-111">integración de Azure AD con Zscaler ZSCloud tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="98aea-111">tooconfigure Azure AD integration with Zscaler ZSCloud, you need hello following items:</span></span>

- <span data-ttu-id="98aea-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98aea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="98aea-113">Una suscripción habilitada para el inicio de sesión único en ZScaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="98aea-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="98aea-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="98aea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="98aea-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="98aea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="98aea-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="98aea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="98aea-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98aea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="98aea-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="98aea-118">Scenario description</span></span>
<span data-ttu-id="98aea-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="98aea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="98aea-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="98aea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="98aea-121">Agregar Zscaler ZSCloud desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="98aea-121">Adding Zscaler ZSCloud from hello gallery</span></span>
2. <span data-ttu-id="98aea-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98aea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a><span data-ttu-id="98aea-123">Agregar Zscaler ZSCloud desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="98aea-123">Adding Zscaler ZSCloud from hello gallery</span></span>
<span data-ttu-id="98aea-124">integración de hello tooconfigure de Zscaler ZSCloud en Azure AD, deberá tooadd Zscaler ZSCloud de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="98aea-124">tooconfigure hello integration of Zscaler ZSCloud into Azure AD, you need tooadd Zscaler ZSCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="98aea-125">**tooadd Zscaler ZSCloud de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="98aea-125">**tooadd Zscaler ZSCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="98aea-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="98aea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="98aea-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="98aea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="98aea-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="98aea-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="98aea-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="98aea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="98aea-133">En el cuadro de búsqueda de hello, escriba **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="98aea-133">In hello search box, type **Zscaler ZSCloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="98aea-135">En el panel de resultados de hello, seleccione **Zscaler ZSCloud**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="98aea-135">In hello results panel, select **Zscaler ZSCloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="98aea-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98aea-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="98aea-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zscaler ZSCloud con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98aea-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="98aea-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Zscaler ZSCloud es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98aea-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler ZSCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="98aea-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Zscaler ZSCloud debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="98aea-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler ZSCloud needs toobe established.</span></span>

<span data-ttu-id="98aea-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="98aea-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="98aea-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Zscaler ZSCloud, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="98aea-142">tooconfigure and test Azure AD single sign-on with Zscaler ZSCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="98aea-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="98aea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="98aea-144">**[Configuración de proxy](#configuring-proxy-settings)**  -configuración de proxy de hello tooconfigure en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="98aea-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="98aea-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98aea-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="98aea-146">**[Crear un usuario de prueba de Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave un equivalente de Britta Simon en Zscaler ZSCloud que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="98aea-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - toohave a counterpart of Britta Simon in Zscaler ZSCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="98aea-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="98aea-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="98aea-148">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="98aea-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="98aea-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98aea-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="98aea-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="98aea-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="98aea-151">**inicio de sesión único en tooconfigure Azure AD con Zscaler ZSCloud, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="98aea-151">**tooconfigure Azure AD single sign-on with Zscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="98aea-152">En el portal de Azure, en Hola Hola **Zscaler ZSCloud** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="98aea-152">In hello Azure portal, on hello **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="98aea-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="98aea-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="98aea-156">En hello **Zscaler ZSCloud dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="98aea-156">On hello **Zscaler ZSCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="98aea-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por los usuarios en toosign tooyour aplicación de ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="98aea-158">In hello **Sign-on URL** textbox, type hello URL used by your users toosign-on tooyour ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="98aea-159">Tiene este valor con hello tooupdate dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="98aea-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="98aea-160">Póngase en contacto con [equipo de soporte técnico de Zscaler ZSCloud cliente](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="98aea-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget this value.</span></span> 
 
4. <span data-ttu-id="98aea-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="98aea-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="98aea-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="98aea-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="98aea-165">En hello **configuración de Zscaler ZSCloud** sección, haga clic en **configurar Zscaler ZSCloud** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="98aea-165">On hello **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="98aea-166">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="98aea-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="98aea-168">En una ventana del explorador web diferente, inicie sesión en tooyour sitio de empresa de ZScaler ZSCloud como administrador.</span><span class="sxs-lookup"><span data-stu-id="98aea-168">In a different web browser window, log in tooyour ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="98aea-169">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="98aea-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="98aea-170">![Administración](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="98aea-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="98aea-171">En **Manage Administrators & Roles (Administrar administradores y roles)** haga clic en **Manage Users & Authentication (Administrar usuarios y autenticación)**.</span><span class="sxs-lookup"><span data-stu-id="98aea-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="98aea-172">![Administración de usuarios y autenticación](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Administración de usuarios y autenticación")</span><span class="sxs-lookup"><span data-stu-id="98aea-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="98aea-173">Hola **elegir opciones de autenticación para su organización** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="98aea-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="98aea-174">![Autenticación](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="98aea-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="98aea-175">a.</span><span class="sxs-lookup"><span data-stu-id="98aea-175">a.</span></span> <span data-ttu-id="98aea-176">Seleccione **Authenticate using SAML Single Sign-On**(Autenticarse mediante el inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="98aea-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="98aea-177">b.</span><span class="sxs-lookup"><span data-stu-id="98aea-177">b.</span></span> <span data-ttu-id="98aea-178">Haga clic en **Configure SAML Single Sign-On Parameters**(Configurar parámetros de inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="98aea-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="98aea-179">En hello **configurar SAML Single Sign-On parámetros** página del cuadro de diálogo, realizar pasos de hello y, a continuación, haga clic en **realiza**</span><span class="sxs-lookup"><span data-stu-id="98aea-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="98aea-180">![Inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="98aea-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="98aea-181">a.</span><span class="sxs-lookup"><span data-stu-id="98aea-181">a.</span></span> <span data-ttu-id="98aea-182">Hola pegar **SAML Single Sign-On dirección URL del servicio** valor en hello **dirección URL de los usuarios de toowhich del Portal de SAML de Hola se envía para autenticación** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="98aea-182">Paste hello **SAML Single Sign-On Service URL** value into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="98aea-183">b.</span><span class="sxs-lookup"><span data-stu-id="98aea-183">b.</span></span> <span data-ttu-id="98aea-184">Hola **atributo que contiene el nombre de inicio de sesión** cuadro de texto, tipo **NameID**.</span><span class="sxs-lookup"><span data-stu-id="98aea-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="98aea-185">c.</span><span class="sxs-lookup"><span data-stu-id="98aea-185">c.</span></span> <span data-ttu-id="98aea-186">tooupload el certificado descargado, haga clic en **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="98aea-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="98aea-187">d.</span><span class="sxs-lookup"><span data-stu-id="98aea-187">d.</span></span> <span data-ttu-id="98aea-188">Seleccione **Habilitar aprovisionamiento automático de SAML**.</span><span class="sxs-lookup"><span data-stu-id="98aea-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="98aea-189">En hello **configurar la autenticación de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="98aea-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="98aea-190">![Administración](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="98aea-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="98aea-191">a.</span><span class="sxs-lookup"><span data-stu-id="98aea-191">a.</span></span> <span data-ttu-id="98aea-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="98aea-192">Click **Save**.</span></span>

    <span data-ttu-id="98aea-193">b.</span><span class="sxs-lookup"><span data-stu-id="98aea-193">b.</span></span> <span data-ttu-id="98aea-194">Haga clic en **Activar ahora**.</span><span class="sxs-lookup"><span data-stu-id="98aea-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="98aea-195">Configuración de los valores de proxy</span><span class="sxs-lookup"><span data-stu-id="98aea-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="98aea-196">configuración de proxy de hello tooconfigure en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="98aea-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="98aea-197">Inicie **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="98aea-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="98aea-198">Seleccione **opciones de Internet** de hello **herramientas** menú Abrir hello **opciones de Internet** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="98aea-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="98aea-199">![Opciones de Internet](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Opciones de Internet")</span><span class="sxs-lookup"><span data-stu-id="98aea-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="98aea-200">Haga clic en hello **conexiones** ficha.</span><span class="sxs-lookup"><span data-stu-id="98aea-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="98aea-201">![Conexiones](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Conexiones")</span><span class="sxs-lookup"><span data-stu-id="98aea-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="98aea-202">Haga clic en **configuración de LAN** tooopen hello **configuración de LAN** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="98aea-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="98aea-203">En la sección servidor Proxy hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="98aea-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="98aea-204">![Servidor proxy](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Servidor proxy")</span><span class="sxs-lookup"><span data-stu-id="98aea-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="98aea-205">a.</span><span class="sxs-lookup"><span data-stu-id="98aea-205">a.</span></span> <span data-ttu-id="98aea-206">Seleccione **Usar un servidor proxy para la LAN**.</span><span class="sxs-lookup"><span data-stu-id="98aea-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="98aea-207">b.</span><span class="sxs-lookup"><span data-stu-id="98aea-207">b.</span></span> <span data-ttu-id="98aea-208">En el cuadro de texto de dirección de hello, escriba **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="98aea-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="98aea-209">c.</span><span class="sxs-lookup"><span data-stu-id="98aea-209">c.</span></span> <span data-ttu-id="98aea-210">En el cuadro de texto de puerto de hello, escriba **80**.</span><span class="sxs-lookup"><span data-stu-id="98aea-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="98aea-211">d.</span><span class="sxs-lookup"><span data-stu-id="98aea-211">d.</span></span> <span data-ttu-id="98aea-212">Seleccione **No usar servidor proxy para direcciones locales**.</span><span class="sxs-lookup"><span data-stu-id="98aea-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="98aea-213">e.</span><span class="sxs-lookup"><span data-stu-id="98aea-213">e.</span></span> <span data-ttu-id="98aea-214">Haga clic en **Aceptar** tooclose hello **configuración de red de área Local (LAN)** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="98aea-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="98aea-215">Haga clic en **Aceptar** tooclose hello **opciones de Internet** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="98aea-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="98aea-216">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="98aea-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="98aea-217">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="98aea-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="98aea-219">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="98aea-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="98aea-220">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="98aea-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="98aea-222">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="98aea-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="98aea-224">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="98aea-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="98aea-226">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="98aea-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="98aea-228">a.</span><span class="sxs-lookup"><span data-stu-id="98aea-228">a.</span></span> <span data-ttu-id="98aea-229">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="98aea-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="98aea-230">b.</span><span class="sxs-lookup"><span data-stu-id="98aea-230">b.</span></span> <span data-ttu-id="98aea-231">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="98aea-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="98aea-232">c.</span><span class="sxs-lookup"><span data-stu-id="98aea-232">c.</span></span> <span data-ttu-id="98aea-233">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="98aea-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="98aea-234">d.</span><span class="sxs-lookup"><span data-stu-id="98aea-234">d.</span></span> <span data-ttu-id="98aea-235">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="98aea-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="98aea-236">Creación de un usuario de prueba de ZScaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="98aea-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="98aea-237">toolog de los usuarios de Azure AD tooenable en tooZScaler ZSCloud, deben ser aprovisionado tooZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="98aea-237">tooenable Azure AD users toolog in tooZScaler ZSCloud, they must be provisioned tooZScaler ZSCloud.</span></span>  
<span data-ttu-id="98aea-238">En caso de hello de ZScaler ZSCloud, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="98aea-238">In hello case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="98aea-239">tooconfigure aprovisionamiento de usuario, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="98aea-239">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="98aea-240">Inicie sesión en tooyour **Zscaler** inquilino.</span><span class="sxs-lookup"><span data-stu-id="98aea-240">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="98aea-241">Haga clic en **Administración**.</span><span class="sxs-lookup"><span data-stu-id="98aea-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="98aea-242">![Administración](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="98aea-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="98aea-243">Haga clic en **User Management**(Administración de usuarios).</span><span class="sxs-lookup"><span data-stu-id="98aea-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="98aea-244">![Agregar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="98aea-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="98aea-245">Hola **usuarios** , haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="98aea-245">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="98aea-246">![Agregar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="98aea-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="98aea-247">En la sección Agregar usuario hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="98aea-247">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="98aea-248">![Agregar usuario](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="98aea-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="98aea-249">a.</span><span class="sxs-lookup"><span data-stu-id="98aea-249">a.</span></span> <span data-ttu-id="98aea-250">Hola de tipo **UserID**, **usuario DisplayName**, **contraseña**, **Confirmar contraseña**y, a continuación, seleccione **grupos**hello y **departamento** de una cuenta válida de AAD que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="98aea-250">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="98aea-251">b.</span><span class="sxs-lookup"><span data-stu-id="98aea-251">b.</span></span> <span data-ttu-id="98aea-252">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="98aea-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="98aea-253">Puede usar cualquier otra ZScaler ZSCloud usuario cuenta herramienta de creación o las API proporcionadas por ZScaler ZSCloud tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="98aea-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="98aea-254">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="98aea-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="98aea-255">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooZscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="98aea-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler ZSCloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="98aea-257">**tooassign tooZscaler Britta Simon ZSCloud, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="98aea-257">**tooassign Britta Simon tooZscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="98aea-258">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="98aea-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="98aea-260">En la lista de aplicaciones de hello, seleccione **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="98aea-260">In hello applications list, select **Zscaler ZSCloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="98aea-262">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="98aea-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="98aea-264">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="98aea-264">Click **Add** button.</span></span> <span data-ttu-id="98aea-265">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="98aea-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="98aea-267">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="98aea-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="98aea-268">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="98aea-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="98aea-269">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="98aea-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="98aea-270">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="98aea-270">Testing single sign-on</span></span>

<span data-ttu-id="98aea-271">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="98aea-271">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>

<span data-ttu-id="98aea-272">Al hacer clic en hello Zscaler ZSCloud disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación de Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="98aea-272">When you click hello Zscaler ZSCloud tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler ZSCloud application.</span></span>

<span data-ttu-id="98aea-273">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="98aea-273">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="98aea-274">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="98aea-274">Additional resources</span></span>

* [<span data-ttu-id="98aea-275">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98aea-275">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="98aea-276">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="98aea-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

