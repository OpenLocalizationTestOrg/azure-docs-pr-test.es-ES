---
title: "Tutorial: Integración de Azure Active Directory con Zscaler Beta | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Zscaler Beta."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1471c2b51ca5684a11acd40f4e450521605bb786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a><span data-ttu-id="02d5a-103">Tutorial: Integración de Azure Active Directory con Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="02d5a-103">Tutorial: Azure Active Directory integration with Zscaler Beta</span></span>

<span data-ttu-id="02d5a-104">En este tutorial, aprenderá cómo toointegrate Zscaler Beta con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02d5a-104">In this tutorial, you learn how toointegrate Zscaler Beta with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02d5a-105">Integración de Zscaler Beta con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="02d5a-105">Integrating Zscaler Beta with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="02d5a-106">Puede controlar en Azure AD que tenga acceso tooZscaler Beta</span><span class="sxs-lookup"><span data-stu-id="02d5a-106">You can control in Azure AD who has access tooZscaler Beta</span></span>
- <span data-ttu-id="02d5a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZscaler Beta (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="02d5a-107">You can enable your users tooautomatically get signed-on tooZscaler Beta (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="02d5a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="02d5a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="02d5a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="02d5a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02d5a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="02d5a-110">Prerequisites</span></span>

<span data-ttu-id="02d5a-111">tooconfigure integración de Azure AD con Zscaler Beta, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="02d5a-111">tooconfigure Azure AD integration with Zscaler Beta, you need hello following items:</span></span>

- <span data-ttu-id="02d5a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="02d5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02d5a-113">Una suscripción habilitada para el inicio de sesión único en Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="02d5a-113">A Zscaler Beta single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02d5a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="02d5a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02d5a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="02d5a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02d5a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="02d5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="02d5a-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02d5a-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02d5a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="02d5a-118">Scenario description</span></span>
<span data-ttu-id="02d5a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="02d5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="02d5a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="02d5a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02d5a-121">Agregar Zscaler Beta de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="02d5a-121">Adding Zscaler Beta from hello gallery</span></span>
2. <span data-ttu-id="02d5a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="02d5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-beta-from-hello-gallery"></a><span data-ttu-id="02d5a-123">Agregar Zscaler Beta de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="02d5a-123">Adding Zscaler Beta from hello gallery</span></span>
<span data-ttu-id="02d5a-124">integración de hello tooconfigure de Zscaler Beta en Azure AD, deberá tooadd Zscaler Beta de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="02d5a-124">tooconfigure hello integration of Zscaler Beta into Azure AD, you need tooadd Zscaler Beta from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="02d5a-125">**tooadd Zscaler Beta de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="02d5a-125">**tooadd Zscaler Beta from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="02d5a-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="02d5a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="02d5a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="02d5a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="02d5a-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="02d5a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="02d5a-133">En el cuadro de búsqueda de hello, escriba **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-133">In hello search box, type **Zscaler Beta**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

5. <span data-ttu-id="02d5a-135">En el panel de resultados de hello, seleccione **Zscaler Beta**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="02d5a-135">In hello results panel, select **Zscaler Beta**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="02d5a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="02d5a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="02d5a-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zscaler Beta con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="02d5a-138">In this section, you configure and test Azure AD single sign-on with Zscaler Beta based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="02d5a-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Zscaler Beta es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02d5a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Beta is tooa user in Azure AD.</span></span> <span data-ttu-id="02d5a-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Zscaler Beta debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="02d5a-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Beta needs toobe established.</span></span>

<span data-ttu-id="02d5a-141">En Zscaler Beta, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="02d5a-141">In Zscaler Beta, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="02d5a-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Zscaler Beta, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="02d5a-142">tooconfigure and test Azure AD single sign-on with Zscaler Beta, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="02d5a-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="02d5a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="02d5a-144">**[Configuración de proxy](#configuring-proxy-settings)**  -configuración de proxy de hello tooconfigure en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="02d5a-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="02d5a-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02d5a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="02d5a-146">**[Crear un usuario de prueba de Zscaler Beta](#creating-a-zscaler-beta-test-user)**  -toohave un equivalente de Britta Simon en Zscaler Beta que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="02d5a-146">**[Creating a Zscaler Beta test user](#creating-a-zscaler-beta-test-user)** - toohave a counterpart of Britta Simon in Zscaler Beta that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="02d5a-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="02d5a-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="02d5a-148">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="02d5a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="02d5a-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="02d5a-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="02d5a-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="02d5a-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler Beta application.</span></span>

<span data-ttu-id="02d5a-151">**inicio de sesión único en tooconfigure Azure AD con Zscaler Beta, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="02d5a-151">**tooconfigure Azure AD single sign-on with Zscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="02d5a-152">En el portal de Azure, en Hola Hola **Zscaler Beta** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-152">In hello Azure portal, on hello **Zscaler Beta** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="02d5a-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="02d5a-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

3. <span data-ttu-id="02d5a-156">En hello **Zscaler Beta dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="02d5a-156">On hello **Zscaler Beta Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    <span data-ttu-id="02d5a-158">En cuadro de texto de dirección URL de hello inicio de sesión, escriba dirección URL de hello utilizada por los usuarios en toosign tooyour aplicación de Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="02d5a-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour Zscaler Beta application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="02d5a-159">Tiene este valor con hello tooupdate dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="02d5a-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="02d5a-160">Póngase en contacto con [equipo de soporte técnico de Zscaler Beta cliente](https://www.zscaler.com/company/contact) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="02d5a-160">Contact [Zscaler Beta Client support team](https://www.zscaler.com/company/contact) tooget this value.</span></span> 

4. <span data-ttu-id="02d5a-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="02d5a-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

5. <span data-ttu-id="02d5a-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="02d5a-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="02d5a-165">En hello **Zscaler Beta configuración** sección, haga clic en **configurar Zscaler Beta** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="02d5a-165">On hello **Zscaler Beta Configuration** section, click **Configure Zscaler Beta** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="02d5a-166">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="02d5a-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

7. <span data-ttu-id="02d5a-168">En una ventana del explorador web diferente, inicie sesión en tooyour sitio de empresa de Zscaler Beta como administrador.</span><span class="sxs-lookup"><span data-stu-id="02d5a-168">In a different web browser window, log in tooyour Zscaler Beta company site as an administrator.</span></span>

8. <span data-ttu-id="02d5a-169">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="02d5a-170">![Administración](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="02d5a-170">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="02d5a-171">En **Manage Administrators & Roles (Administrar administradores y roles)** haga clic en **Manage Users & Authentication (Administrar usuarios y autenticación)**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="02d5a-172">![Administración de usuarios y autenticación](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Administración de usuarios y autenticación")</span><span class="sxs-lookup"><span data-stu-id="02d5a-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="02d5a-173">Hola **elegir opciones de autenticación para su organización** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="02d5a-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="02d5a-174">![Autenticación](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="02d5a-174">![Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="02d5a-175">a.</span><span class="sxs-lookup"><span data-stu-id="02d5a-175">a.</span></span> <span data-ttu-id="02d5a-176">Seleccione **Authenticate using SAML Single Sign-On**(Autenticarse mediante el inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="02d5a-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="02d5a-177">b.</span><span class="sxs-lookup"><span data-stu-id="02d5a-177">b.</span></span> <span data-ttu-id="02d5a-178">Haga clic en **Configure SAML Single Sign-On Parameters**(Configurar parámetros de inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="02d5a-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="02d5a-179">En hello **configurar SAML Single Sign-On parámetros** página del cuadro de diálogo, realizar pasos de hello y, a continuación, haga clic en **realiza**</span><span class="sxs-lookup"><span data-stu-id="02d5a-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="02d5a-180">![Inicio de sesión único](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="02d5a-180">![Single Sign-On](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="02d5a-181">a.</span><span class="sxs-lookup"><span data-stu-id="02d5a-181">a.</span></span> <span data-ttu-id="02d5a-182">Hola pegar **SAML Single Sign-On dirección URL del servicio** valor, que haya copiado desde Hola portal de Azure en hello **dirección URL de los usuarios de toowhich del Portal de SAML de Hola se envía para autenticación** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="02d5a-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="02d5a-183">b.</span><span class="sxs-lookup"><span data-stu-id="02d5a-183">b.</span></span> <span data-ttu-id="02d5a-184">Hola **atributo que contiene el nombre de inicio de sesión** cuadro de texto, tipo **NameID**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="02d5a-185">c.</span><span class="sxs-lookup"><span data-stu-id="02d5a-185">c.</span></span> <span data-ttu-id="02d5a-186">tooupload el certificado descargado, haga clic en **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="02d5a-187">d.</span><span class="sxs-lookup"><span data-stu-id="02d5a-187">d.</span></span> <span data-ttu-id="02d5a-188">Seleccione **Habilitar aprovisionamiento automático de SAML**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="02d5a-189">En hello **configurar la autenticación de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="02d5a-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="02d5a-190">![Administración](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="02d5a-190">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="02d5a-191">a.</span><span class="sxs-lookup"><span data-stu-id="02d5a-191">a.</span></span> <span data-ttu-id="02d5a-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-192">Click **Save**.</span></span>

    <span data-ttu-id="02d5a-193">b.</span><span class="sxs-lookup"><span data-stu-id="02d5a-193">b.</span></span> <span data-ttu-id="02d5a-194">Haga clic en **Activar ahora**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="02d5a-195">Configuración de los valores de proxy</span><span class="sxs-lookup"><span data-stu-id="02d5a-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="02d5a-196">configuración de proxy de hello tooconfigure en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="02d5a-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="02d5a-197">Inicie **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="02d5a-198">Seleccione **opciones de Internet** de hello **herramientas** menú Abrir hello **opciones de Internet** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="02d5a-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="02d5a-199">![Opciones de Internet](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Opciones de Internet")</span><span class="sxs-lookup"><span data-stu-id="02d5a-199">![Internet Options](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="02d5a-200">Haga clic en hello **conexiones** ficha.</span><span class="sxs-lookup"><span data-stu-id="02d5a-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="02d5a-201">![Conexiones](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Conexiones")</span><span class="sxs-lookup"><span data-stu-id="02d5a-201">![Connections](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="02d5a-202">Haga clic en **configuración de LAN** tooopen hello **configuración de LAN** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="02d5a-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="02d5a-203">En la sección servidor Proxy hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="02d5a-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="02d5a-204">![Servidor proxy](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Servidor proxy")</span><span class="sxs-lookup"><span data-stu-id="02d5a-204">![Proxy server](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="02d5a-205">a.</span><span class="sxs-lookup"><span data-stu-id="02d5a-205">a.</span></span> <span data-ttu-id="02d5a-206">Seleccione **Usar un servidor proxy para la LAN**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="02d5a-207">b.</span><span class="sxs-lookup"><span data-stu-id="02d5a-207">b.</span></span> <span data-ttu-id="02d5a-208">En el cuadro de texto de dirección de hello, escriba **gateway.zscalerbeta.net**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-208">In hello Address textbox, type **gateway.zscalerbeta.net**.</span></span>

    <span data-ttu-id="02d5a-209">c.</span><span class="sxs-lookup"><span data-stu-id="02d5a-209">c.</span></span> <span data-ttu-id="02d5a-210">En el cuadro de texto de puerto de hello, escriba **80**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="02d5a-211">d.</span><span class="sxs-lookup"><span data-stu-id="02d5a-211">d.</span></span> <span data-ttu-id="02d5a-212">Seleccione **No usar servidor proxy para direcciones locales**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="02d5a-213">e.</span><span class="sxs-lookup"><span data-stu-id="02d5a-213">e.</span></span> <span data-ttu-id="02d5a-214">Haga clic en **Aceptar** tooclose hello **configuración de red de área Local (LAN)** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="02d5a-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="02d5a-215">Haga clic en **Aceptar** tooclose hello **opciones de Internet** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="02d5a-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="02d5a-216">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="02d5a-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="02d5a-217">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="02d5a-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="02d5a-218">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="02d5a-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="02d5a-219">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="02d5a-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="02d5a-220">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="02d5a-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="02d5a-222">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="02d5a-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="02d5a-223">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="02d5a-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="02d5a-225">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="02d5a-227">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="02d5a-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="02d5a-229">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="02d5a-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="02d5a-231">a.</span><span class="sxs-lookup"><span data-stu-id="02d5a-231">a.</span></span> <span data-ttu-id="02d5a-232">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02d5a-233">b.</span><span class="sxs-lookup"><span data-stu-id="02d5a-233">b.</span></span> <span data-ttu-id="02d5a-234">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="02d5a-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="02d5a-235">c.</span><span class="sxs-lookup"><span data-stu-id="02d5a-235">c.</span></span> <span data-ttu-id="02d5a-236">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="02d5a-237">d.</span><span class="sxs-lookup"><span data-stu-id="02d5a-237">d.</span></span> <span data-ttu-id="02d5a-238">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-beta-test-user"></a><span data-ttu-id="02d5a-239">Creación de un usuario de prueba de Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="02d5a-239">Creating a Zscaler Beta test user</span></span>

<span data-ttu-id="02d5a-240">toolog de los usuarios de Azure AD tooenable en tooZscaler Beta, deben ser aprovisionado tooZscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="02d5a-240">tooenable Azure AD users toolog in tooZscaler Beta, they must be provisioned tooZscaler Beta.</span></span> <span data-ttu-id="02d5a-241">En caso de hello de Zscaler Beta, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="02d5a-241">In hello case of Zscaler Beta, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="02d5a-242">tooconfigure aprovisionamiento de usuario, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="02d5a-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="02d5a-243">Inicie sesión en tooyour **Zscaler Beta** inquilino.</span><span class="sxs-lookup"><span data-stu-id="02d5a-243">Log in tooyour **Zscaler Beta** tenant.</span></span>

2. <span data-ttu-id="02d5a-244">Haga clic en **Administración**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="02d5a-245">![Administración](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="02d5a-245">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="02d5a-246">Haga clic en **User Management**(Administración de usuarios).</span><span class="sxs-lookup"><span data-stu-id="02d5a-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="02d5a-247">![Agregar](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="02d5a-247">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="02d5a-248">Hola **usuarios** , haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="02d5a-249">![Agregar](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="02d5a-249">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="02d5a-250">En la sección Agregar usuario hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="02d5a-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="02d5a-251">![Agregar usuario](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="02d5a-251">![Add User](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="02d5a-252">a.</span><span class="sxs-lookup"><span data-stu-id="02d5a-252">a.</span></span> <span data-ttu-id="02d5a-253">Hola de tipo **UserID**, **usuario DisplayName**, **contraseña**, **Confirmar contraseña**y, a continuación, seleccione **grupos**hello y **departamento** de un Azure válida que desee tooprovision de cuenta de AD.</span><span class="sxs-lookup"><span data-stu-id="02d5a-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="02d5a-254">b.</span><span class="sxs-lookup"><span data-stu-id="02d5a-254">b.</span></span> <span data-ttu-id="02d5a-255">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="02d5a-256">Puede usar cualquier otra Zscaler Beta usuario cuenta herramienta de creación o las API proporcionadas por Zscaler Beta tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02d5a-256">You can use any other Zscaler Beta user account creation tools or APIs provided by Zscaler Beta tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="02d5a-257">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="02d5a-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="02d5a-258">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooZscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="02d5a-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler Beta.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="02d5a-260">**tooassign Britta Simon tooZscaler Beta, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="02d5a-260">**tooassign Britta Simon tooZscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="02d5a-261">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="02d5a-263">En la lista de aplicaciones de hello, seleccione **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-263">In hello applications list, select **Zscaler Beta**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

3. <span data-ttu-id="02d5a-265">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="02d5a-267">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-267">Click **Add** button.</span></span> <span data-ttu-id="02d5a-268">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="02d5a-270">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="02d5a-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="02d5a-271">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02d5a-272">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="02d5a-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="02d5a-273">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="02d5a-273">Testing single sign-on</span></span>

<span data-ttu-id="02d5a-274">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="02d5a-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="02d5a-275">Al hacer clic en hello Zscaler Beta disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación de Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="02d5a-275">When you click hello Zscaler Beta tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Beta application.</span></span>
<span data-ttu-id="02d5a-276">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="02d5a-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="02d5a-277">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="02d5a-277">Additional resources</span></span>

* [<span data-ttu-id="02d5a-278">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02d5a-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02d5a-279">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="02d5a-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_203.png

