---
title: "Tutorial: Integración de Azure Active Directory con Deputy | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y adjunto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="2ae35-103">Tutorial: integración de Azure Active Directory con Deputy</span><span class="sxs-lookup"><span data-stu-id="2ae35-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="2ae35-104">En este tutorial, aprenderá cómo toointegrate adjunto con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ae35-104">In this tutorial, you learn how toointegrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ae35-105">Integración adjunto con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2ae35-105">Integrating Deputy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2ae35-106">Puede controlar en Azure AD que tenga acceso tooDeputy</span><span class="sxs-lookup"><span data-stu-id="2ae35-106">You can control in Azure AD who has access tooDeputy</span></span>
- <span data-ttu-id="2ae35-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooDeputy (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae35-107">You can enable your users tooautomatically get signed-on tooDeputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ae35-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2ae35-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2ae35-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ae35-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ae35-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2ae35-110">Prerequisites</span></span>

<span data-ttu-id="2ae35-111">tooconfigure integración de Azure AD con adjunto, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2ae35-111">tooconfigure Azure AD integration with Deputy, you need hello following items:</span></span>

- <span data-ttu-id="2ae35-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae35-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ae35-113">Una suscripción habilitada para el inicio de sesión único en Deputy</span><span class="sxs-lookup"><span data-stu-id="2ae35-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ae35-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2ae35-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ae35-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2ae35-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ae35-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2ae35-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ae35-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ae35-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ae35-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2ae35-118">Scenario description</span></span>
<span data-ttu-id="2ae35-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2ae35-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ae35-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="2ae35-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ae35-121">Agregar adjunto desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2ae35-121">Adding Deputy from hello gallery</span></span>
2. <span data-ttu-id="2ae35-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae35-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-hello-gallery"></a><span data-ttu-id="2ae35-123">Agregar adjunto desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2ae35-123">Adding Deputy from hello gallery</span></span>
<span data-ttu-id="2ae35-124">integración de hello tooconfigure de adjunto en Azure AD, deberá tooadd adjunto de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="2ae35-124">tooconfigure hello integration of Deputy into Azure AD, you need tooadd Deputy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2ae35-125">**tooadd adjunto de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ae35-125">**tooadd Deputy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ae35-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="2ae35-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2ae35-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2ae35-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2ae35-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2ae35-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2ae35-133">En el cuadro de búsqueda de hello, escriba **adjunto**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-133">In hello search box, type **Deputy**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="2ae35-135">En el panel de resultados de hello, seleccione **adjunto**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2ae35-135">In hello results panel, select **Deputy**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2ae35-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae35-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2ae35-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Deputy con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2ae35-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2ae35-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en adjunto es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ae35-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Deputy is tooa user in Azure AD.</span></span> <span data-ttu-id="2ae35-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en adjunto debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="2ae35-140">In other words, a link relationship between an Azure AD user and hello related user in Deputy needs toobe established.</span></span>

<span data-ttu-id="2ae35-141">En adjunto, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ae35-141">In Deputy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2ae35-142">tooconfigure y prueba de inicio de sesión único en Azure AD con adjunto, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2ae35-142">tooconfigure and test Azure AD single sign-on with Deputy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2ae35-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="2ae35-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2ae35-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ae35-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ae35-145">**[Crear un usuario de prueba adjunto](#creating-a-deputy-test-user)**  -toohave un equivalente de Britta Simon en adjunto que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="2ae35-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - toohave a counterpart of Britta Simon in Deputy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ae35-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2ae35-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ae35-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2ae35-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2ae35-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae35-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2ae35-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación adjunto.</span><span class="sxs-lookup"><span data-stu-id="2ae35-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="2ae35-150">**inicio de sesión único en Azure AD tooconfigure con adjunto, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ae35-150">**tooconfigure Azure AD single sign-on with Deputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ae35-151">En el portal de Azure, en Hola Hola **adjunto** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-151">In hello Azure portal, on hello **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2ae35-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2ae35-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="2ae35-155">En hello **adjunto dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="2ae35-155">On hello **Deputy Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="2ae35-157">a.</span><span class="sxs-lookup"><span data-stu-id="2ae35-157">a.</span></span> <span data-ttu-id="2ae35-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="2ae35-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="2ae35-159">b.</span><span class="sxs-lookup"><span data-stu-id="2ae35-159">b.</span></span> <span data-ttu-id="2ae35-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="2ae35-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="2ae35-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2ae35-162">Si desea que aplicación de hello tooconfigure en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="2ae35-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="2ae35-164">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="2ae35-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="2ae35-165">El sufijo de la región de Deputy es opcional o debe usar uno de los siguientes: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span><span class="sxs-lookup"><span data-stu-id="2ae35-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2ae35-166">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="2ae35-166">These values are not real.</span></span> <span data-ttu-id="2ae35-167">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="2ae35-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2ae35-168">Póngase en contacto con [equipo de soporte técnico de adjunto](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="2ae35-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget these values.</span></span> 

5. <span data-ttu-id="2ae35-169">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2ae35-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="2ae35-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2ae35-171">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2ae35-173">En hello **adjunto configuración** sección, haga clic en **configurar adjunto** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="2ae35-173">On hello **Deputy Configuration** section, click **Configure Deputy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2ae35-174">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="2ae35-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="2ae35-176">Navegue toohello después de la dirección URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="2ae35-176">Navigate toohello following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="2ae35-177">Vaya demasiado**configuración de seguridad** y haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-177">Go too**Security Settings** and click **Edit**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="2ae35-179">En esta página de **configuración de seguridad** , siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="2ae35-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="2ae35-181">a.</span><span class="sxs-lookup"><span data-stu-id="2ae35-181">a.</span></span> <span data-ttu-id="2ae35-182">Habilite el **inicio de sesión social**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="2ae35-183">b.</span><span class="sxs-lookup"><span data-stu-id="2ae35-183">b.</span></span> <span data-ttu-id="2ae35-184">Abra el certificado codificado en Base64 descargado desde el portal de Azure en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado OpenSSL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="2ae35-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="2ae35-185">c.</span><span class="sxs-lookup"><span data-stu-id="2ae35-185">c.</span></span> <span data-ttu-id="2ae35-186">En el cuadro de texto de dirección URL SSO SAML hello, escriba`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="2ae35-186">In hello SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="2ae35-187">d.</span><span class="sxs-lookup"><span data-stu-id="2ae35-187">d.</span></span> <span data-ttu-id="2ae35-188">En el cuadro de texto de dirección URL SSO SAML hello, reemplace `<your subdomain>` con el subdominio.</span><span class="sxs-lookup"><span data-stu-id="2ae35-188">In hello SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="2ae35-189">e.</span><span class="sxs-lookup"><span data-stu-id="2ae35-189">e.</span></span> <span data-ttu-id="2ae35-190">En el cuadro de texto de dirección URL SSO SAML hello, reemplace `<saml sso url>` con hello **SAML Single Sign-On dirección URL del servicio** haya copiado desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ae35-190">In hello SAML SSO URL textbox, replace `<saml sso url>` with hello **SAML Single Sign-On Service URL** you have copied from hello Azure portal.</span></span>
   
    <span data-ttu-id="2ae35-191">f.</span><span class="sxs-lookup"><span data-stu-id="2ae35-191">f.</span></span> <span data-ttu-id="2ae35-192">Haga clic en **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="2ae35-193">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="2ae35-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2ae35-194">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="2ae35-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2ae35-195">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ae35-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2ae35-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae35-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="2ae35-197">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="2ae35-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2ae35-199">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ae35-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ae35-200">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="2ae35-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ae35-202">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ae35-204">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ae35-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ae35-206">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="2ae35-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ae35-208">a.</span><span class="sxs-lookup"><span data-stu-id="2ae35-208">a.</span></span> <span data-ttu-id="2ae35-209">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ae35-210">b.</span><span class="sxs-lookup"><span data-stu-id="2ae35-210">b.</span></span> <span data-ttu-id="2ae35-211">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2ae35-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ae35-212">c.</span><span class="sxs-lookup"><span data-stu-id="2ae35-212">c.</span></span> <span data-ttu-id="2ae35-213">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2ae35-214">d.</span><span class="sxs-lookup"><span data-stu-id="2ae35-214">d.</span></span> <span data-ttu-id="2ae35-215">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="2ae35-216">Creación de usuario de prueba de Deputy</span><span class="sxs-lookup"><span data-stu-id="2ae35-216">Creating a Deputy test user</span></span>

<span data-ttu-id="2ae35-217">toolog de los usuarios de Azure AD tooenable en tooDeputy, se les deben aprovisionar en adjunto.</span><span class="sxs-lookup"><span data-stu-id="2ae35-217">tooenable Azure AD users toolog in tooDeputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="2ae35-218">En el caso de Deputy, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="2ae35-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="2ae35-219">tooprovision una cuenta de usuario, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ae35-219">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="2ae35-220">Inicie sesión en el sitio de la empresa tooyour adjunto como administrador.</span><span class="sxs-lookup"><span data-stu-id="2ae35-220">Log in tooyour Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="2ae35-221">En el panel de navegación superior de hello, haga clic en **personas**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-221">On hello top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="2ae35-222">![Personas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="2ae35-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="2ae35-223">Haga clic en hello **agregar personas** y haga clic en **agregar una sola persona**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-223">Click hello **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="2ae35-224">![Agregar personas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Agregar personas")</span><span class="sxs-lookup"><span data-stu-id="2ae35-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="2ae35-225">Realizar pasos de Hola y haga clic en **guardar e invitar**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-225">Perform hello following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="2ae35-226">![Nuevo usuario](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="2ae35-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="2ae35-227">a.</span><span class="sxs-lookup"><span data-stu-id="2ae35-227">a.</span></span> <span data-ttu-id="2ae35-228">Hola **nombre** cuadro de texto, nombre de tipo de usuario de hello como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-228">In hello **Name** textbox, type name of hello user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="2ae35-229">b.</span><span class="sxs-lookup"><span data-stu-id="2ae35-229">b.</span></span> <span data-ttu-id="2ae35-230">Hola **correo electrónico** cuadro de texto, dirección de correo electrónico de tipo hello de una cuenta de Azure AD que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="2ae35-230">In hello **Email** textbox, type hello email address of an Azure AD account you want tooprovision.</span></span>
   
   <span data-ttu-id="2ae35-231">c.</span><span class="sxs-lookup"><span data-stu-id="2ae35-231">c.</span></span> <span data-ttu-id="2ae35-232">Hola **trabajar en** cuadro de texto, nombre de tipo hello empresariales.</span><span class="sxs-lookup"><span data-stu-id="2ae35-232">In hello **Work at** textbox, type hello business name.</span></span>
   
   <span data-ttu-id="2ae35-233">d.</span><span class="sxs-lookup"><span data-stu-id="2ae35-233">d.</span></span> <span data-ttu-id="2ae35-234">Haga clic en el botón **Guardar e invitar**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="2ae35-235">titular de la cuenta de Hello AAD recibe un correo electrónico y sigue un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="2ae35-235">hello AAD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="2ae35-236">Puede usar cualquier otra adjunto usuario cuenta herramienta de creación o las API proporcionadas por adjunto tooprovision AAD cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="2ae35-236">You can use any other Deputy user account creation tools or APIs provided by Deputy tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2ae35-237">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ae35-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2ae35-238">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooDeputy.</span><span class="sxs-lookup"><span data-stu-id="2ae35-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDeputy.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2ae35-240">**tooassign Britta Simon tooDeputy, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ae35-240">**tooassign Britta Simon tooDeputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ae35-241">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2ae35-243">En la lista de aplicaciones de hello, seleccione **adjunto**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-243">In hello applications list, select **Deputy**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="2ae35-245">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2ae35-247">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-247">Click **Add** button.</span></span> <span data-ttu-id="2ae35-248">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2ae35-250">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ae35-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2ae35-251">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ae35-252">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2ae35-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2ae35-253">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2ae35-253">Testing single sign-on</span></span>

<span data-ttu-id="2ae35-254">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2ae35-254">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="2ae35-255">Al hacer clic en hello adjunto el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación adjunto.</span><span class="sxs-lookup"><span data-stu-id="2ae35-255">When you click hello Deputy tile in hello Access Panel, you should get automatically signed-on tooyour Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ae35-256">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2ae35-256">Additional resources</span></span>

* [<span data-ttu-id="2ae35-257">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ae35-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ae35-258">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2ae35-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

