---
title: "Tutorial: Integración de Azure Active Directory con Adobe Creative Cloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Adobe creativa en la nube."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="0cf07-103">Tutorial: Integración de Azure Active Directory con Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="0cf07-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="0cf07-104">En este tutorial, aprenderá cómo toointegrate Adobe Creative en la nube con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0cf07-104">In this tutorial, you learn how toointegrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0cf07-105">Integración de Adobe creativa en la nube con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0cf07-105">Integrating Adobe Creative Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0cf07-106">Puede controlar en Azure AD que tenga acceso tooAdobe creativa en la nube</span><span class="sxs-lookup"><span data-stu-id="0cf07-106">You can control in Azure AD who has access tooAdobe Creative Cloud</span></span>
- <span data-ttu-id="0cf07-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAdobe creativa en la nube (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf07-107">You can enable your users tooautomatically get signed-on tooAdobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0cf07-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="0cf07-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="0cf07-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0cf07-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cf07-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0cf07-110">Prerequisites</span></span>

<span data-ttu-id="0cf07-111">tooconfigure integración de Azure AD con Adobe creativa en la nube, debe Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0cf07-111">tooconfigure Azure AD integration with Adobe Creative Cloud, you need hello following items:</span></span>

- <span data-ttu-id="0cf07-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf07-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0cf07-113">Una suscripción habilitada para el inicio de sesión único en Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="0cf07-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0cf07-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0cf07-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0cf07-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0cf07-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0cf07-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0cf07-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0cf07-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0cf07-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0cf07-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0cf07-118">Scenario description</span></span>
<span data-ttu-id="0cf07-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0cf07-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0cf07-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0cf07-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0cf07-121">Agregar Adobe creativa en la nube desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0cf07-121">Adding Adobe Creative Cloud from hello gallery</span></span>
2. <span data-ttu-id="0cf07-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf07-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a><span data-ttu-id="0cf07-123">Agregar Adobe creativa en la nube desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0cf07-123">Adding Adobe Creative Cloud from hello gallery</span></span>
<span data-ttu-id="0cf07-124">integración de hello tooconfigure de Adobe creativa en la nube en Azure AD, deberá tooadd Adobe creativa en la nube de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0cf07-124">tooconfigure hello integration of Adobe Creative Cloud into Azure AD, you need tooadd Adobe Creative Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0cf07-125">**tooadd Adobe creativa en la nube de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0cf07-125">**tooadd Adobe Creative Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cf07-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0cf07-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0cf07-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0cf07-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0cf07-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cf07-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0cf07-133">En el cuadro de búsqueda de hello, escriba **Adobe Creative nube**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-133">In hello search box, type **Adobe Creative Cloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="0cf07-135">En el panel de resultados de hello, seleccione **Adobe Creative nube**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0cf07-135">In hello results panel, select **Adobe Creative Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0cf07-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf07-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0cf07-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Adobe Creative Cloud utilizando usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0cf07-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0cf07-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Adobe creativa en la nube es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0cf07-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Creative Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="0cf07-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Adobe creativa en la nube debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0cf07-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Creative Cloud needs toobe established.</span></span>

<span data-ttu-id="0cf07-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Adobe creativa en la nube.</span><span class="sxs-lookup"><span data-stu-id="0cf07-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="0cf07-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Adobe creativa en la nube, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0cf07-142">tooconfigure and test Azure AD single sign-on with Adobe Creative Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0cf07-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0cf07-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0cf07-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0cf07-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0cf07-145">**[Creación de un usuario de prueba en la nube Adobe Creative](#creating-an-adobe-creative-cloud-test-user)**  -toohave un equivalente de Britta Simon en Adobe creativa en la nube que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="0cf07-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - toohave a counterpart of Britta Simon in Adobe Creative Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="0cf07-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0cf07-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0cf07-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0cf07-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0cf07-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf07-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0cf07-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Adobe creativa en la nube.</span><span class="sxs-lookup"><span data-stu-id="0cf07-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="0cf07-150">**tooconfigure inicio de sesión único en Azure AD con Adobe creativa en la nube, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0cf07-150">**tooconfigure Azure AD single sign-on with Adobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cf07-151">En el portal de administración de Azure de hello, en hello **Adobe Creative nube** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-151">In hello Azure Management portal, on hello **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0cf07-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0cf07-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="0cf07-155">En hello **Adobe Creative nube dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="0cf07-155">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="0cf07-157">a.</span><span class="sxs-lookup"><span data-stu-id="0cf07-157">a.</span></span> <span data-ttu-id="0cf07-158">Hola **identificador** cuadro de texto, valor de tipo hello como:`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="0cf07-158">In hello **Identifier** textbox, type hello value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="0cf07-159">b.</span><span class="sxs-lookup"><span data-stu-id="0cf07-159">b.</span></span> <span data-ttu-id="0cf07-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="0cf07-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0cf07-161">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cf07-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="0cf07-162">Tener tooupdate estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="0cf07-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="0cf07-163">Aquí le sugerimos toouse Hola único valor de cadena en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="0cf07-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="0cf07-164">Si necesita un usuario toocreate manualmente, debe equipo de soporte técnico de toocontact hello Adobe creativa en la nube.</span><span class="sxs-lookup"><span data-stu-id="0cf07-164">If you need toocreate an user manually, you need toocontact hello Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="0cf07-165">En hello **Adobe Creative nube dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="0cf07-165">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="0cf07-167">a.</span><span class="sxs-lookup"><span data-stu-id="0cf07-167">a.</span></span> <span data-ttu-id="0cf07-168">Haga clic en hello **mostrar avanzadas de configuración de direcciones URL** opción</span><span class="sxs-lookup"><span data-stu-id="0cf07-168">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="0cf07-169">b.</span><span class="sxs-lookup"><span data-stu-id="0cf07-169">b.</span></span> <span data-ttu-id="0cf07-170">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello como:`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="0cf07-170">In hello **Sign-on URL** textbox, type hello value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="0cf07-171">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0cf07-171">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="0cf07-173">En hello **configuración de nube de Adobe Creative** sección, haga clic en **configurar Adobe creativa en la nube** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="0cf07-173">On hello **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0cf07-174">Copie hello **Id. de entidad SAML** y **dirección URL del servicio de SSO de SAML** desde la sección de referencia rápida.</span><span class="sxs-lookup"><span data-stu-id="0cf07-174">Please copy hello **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="0cf07-176">En una ventana del explorador web diferente, inquilinos de nube creativa de Adobe tooyour inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="0cf07-176">In a different web browser window, sign-on tooyour Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="0cf07-177">Vaya demasiado**identidad** Hola panel de navegación izquierdo y haga clic en el dominio.</span><span class="sxs-lookup"><span data-stu-id="0cf07-177">Go too**Identity** on hello left navigation pane and click your domain.</span></span> <span data-ttu-id="0cf07-178">A continuación, realizar Hola seguir pasos de **inicio de sesión único en requiere una configuración** sección.</span><span class="sxs-lookup"><span data-stu-id="0cf07-178">Then perform hello following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="0cf07-179">![Configuración](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="0cf07-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="0cf07-180">Haga clic en **examinar** hello tooupload descarga certificado de Azure AD demasiado**certificado IDP**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-180">Click **Browse** tooupload hello downloaded certificate from Azure AD too**IDP Certificate**.</span></span>

10. <span data-ttu-id="0cf07-181">Hola **emisor IDP** cuadro de texto, coloque valor Hola de **Id. de entidad SAML** que copió de **configurar inicio de sesión** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cf07-181">In hello **IDP issuer** textbox, put hello value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="0cf07-182">Hola **dirección URL de inicio de sesión IDP** cuadro de texto, coloque valor Hola de **dirección URL del servicio de SSO de SAML** que copió de **configurar inicio de sesión** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cf07-182">In hello **IDP Login URL** textbox, put hello value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="0cf07-183">Seleccione **HTTP - Redirect** (HTTP - Redireccionamiento) como **IDP Binding** (Enlace IDP).</span><span class="sxs-lookup"><span data-stu-id="0cf07-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="0cf07-184">Seleccione **Email Address** (Dirección de correo electrónico) como **User Login Setting** (Configuración de inicio de sesión de usuario).</span><span class="sxs-lookup"><span data-stu-id="0cf07-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="0cf07-185">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0cf07-185">Click **Save** button.</span></span>

15. <span data-ttu-id="0cf07-186">panel de Hello presentará ahora Hola XML **"Descargar los metadatos"** archivo.</span><span class="sxs-lookup"><span data-stu-id="0cf07-186">hello dashboard will now present hello XML **"Download Metadata"** file.</span></span> <span data-ttu-id="0cf07-187">Contiene la URL de EntityDescriptor y la URL de AssertionConsumerService de Adobe.</span><span class="sxs-lookup"><span data-stu-id="0cf07-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="0cf07-188">Por favor, abra el archivo hello y configurarlos en hello aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0cf07-188">Please open hello file and configure them in hello Azure AD application.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="0cf07-191">a.</span><span class="sxs-lookup"><span data-stu-id="0cf07-191">a.</span></span> <span data-ttu-id="0cf07-192">Hola uso EntityDescriptor valor Adobe proporcionado para **identificador** en hello **configurar opciones de aplicación** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0cf07-192">Use hello EntityDescriptor value Adobe provided you for **Identifier** on hello **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="0cf07-193">b.</span><span class="sxs-lookup"><span data-stu-id="0cf07-193">b.</span></span> <span data-ttu-id="0cf07-194">Hola de uso AssertionConsumerService valor Adobe proporcionado para **dirección URL de respuesta** en hello **configurar opciones de aplicación** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0cf07-194">Use hello AssertionConsumerService value Adobe provided you for **Reply URL** on hello **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0cf07-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf07-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="0cf07-196">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0cf07-196">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0cf07-198">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0cf07-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cf07-199">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0cf07-199">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0cf07-201">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0cf07-201">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0cf07-203">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0cf07-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0cf07-205">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0cf07-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0cf07-207">a.</span><span class="sxs-lookup"><span data-stu-id="0cf07-207">a.</span></span> <span data-ttu-id="0cf07-208">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0cf07-209">b.</span><span class="sxs-lookup"><span data-stu-id="0cf07-209">b.</span></span> <span data-ttu-id="0cf07-210">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0cf07-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0cf07-211">c.</span><span class="sxs-lookup"><span data-stu-id="0cf07-211">c.</span></span> <span data-ttu-id="0cf07-212">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0cf07-213">d.</span><span class="sxs-lookup"><span data-stu-id="0cf07-213">d.</span></span> <span data-ttu-id="0cf07-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="0cf07-215">Creación de un usuario de prueba de Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="0cf07-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="0cf07-216">En orden tooenable toolog de los usuarios de Azure AD en Adobe creativa en la nube, se les deben aprovisionar en Adobe creativa en la nube.</span><span class="sxs-lookup"><span data-stu-id="0cf07-216">In order tooenable Azure AD users toolog into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="0cf07-217">En caso de hello de Adobe creativa en la nube, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="0cf07-217">In hello case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="0cf07-218">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="0cf07-218">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cf07-219">Inicie sesión en tooyour sitio de la compañía de Adobe creativa en la nube como administrador.</span><span class="sxs-lookup"><span data-stu-id="0cf07-219">Log in tooyour Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="0cf07-220">Haga clic en **Contactos**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-220">Click **People**.</span></span>

    <span data-ttu-id="0cf07-221">![Personas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="0cf07-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="0cf07-222">Haga clic en **Invitar a usuario**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-222">Click **Invite User**.</span></span>

    <span data-ttu-id="0cf07-223">![Invitación de usuarios](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invitación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="0cf07-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="0cf07-224">En hello **invitar personas** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0cf07-224">On hello **Invite People** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="0cf07-225">![Invitar a personas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invitar a personas")</span><span class="sxs-lookup"><span data-stu-id="0cf07-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="0cf07-226">a.</span><span class="sxs-lookup"><span data-stu-id="0cf07-226">a.</span></span> <span data-ttu-id="0cf07-227">Hola **correo electrónico** cuadro de texto, dirección de correo electrónico de Hola de tipo de cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0cf07-227">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="0cf07-228">b.</span><span class="sxs-lookup"><span data-stu-id="0cf07-228">b.</span></span> <span data-ttu-id="0cf07-229">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0cf07-230">titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="0cf07-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0cf07-231">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cf07-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0cf07-232">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooAdobe acceso creativa en la nube.</span><span class="sxs-lookup"><span data-stu-id="0cf07-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAdobe Creative Cloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0cf07-234">**tooassign Britta Simon tooAdobe creativa en la nube, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0cf07-234">**tooassign Britta Simon tooAdobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="0cf07-235">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-235">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0cf07-237">En la lista de aplicaciones de hello, seleccione **Adobe Creative nube**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-237">In hello applications list, select **Adobe Creative Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="0cf07-239">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0cf07-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-241">Click **Add** button.</span></span> <span data-ttu-id="0cf07-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0cf07-244">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cf07-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0cf07-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0cf07-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0cf07-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0cf07-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0cf07-247">Testing single sign-on</span></span>

<span data-ttu-id="0cf07-248">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0cf07-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0cf07-249">Al hacer clic en icono de Adobe creativa en la nube de Hola Hola Panel de acceso, deberá obtener la aplicación en la nube creativa de Adobe tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="0cf07-249">When you click hello Adobe Creative Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0cf07-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0cf07-250">Additional resources</span></span>

* [<span data-ttu-id="0cf07-251">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0cf07-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0cf07-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0cf07-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png