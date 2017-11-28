---
title: "Tutorial: integración de Azure Active Directory con TOPdesk - Public | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Active Directory de Azure y TOPdesk - Public."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="0e3dc-103">Tutorial: Integración de Azure Active Directory con TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="0e3dc-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="0e3dc-104">En este tutorial, aprenderá cómo toointegrate TOPdesk - Public con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e3dc-104">In this tutorial, you learn how toointegrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e3dc-105">Integración de TOPdesk - Public con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-105">Integrating TOPdesk - Public with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e3dc-106">Puede controlar en Azure AD que tenga acceso tooTOPdesk - público.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-106">You can control in Azure AD who has access tooTOPdesk - Public.</span></span>
- <span data-ttu-id="0e3dc-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTOPdesk - Public (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-107">You can enable your users tooautomatically get signed-on tooTOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0e3dc-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="0e3dc-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e3dc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e3dc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0e3dc-110">Prerequisites</span></span>

<span data-ttu-id="0e3dc-111">tooconfigure integración de Azure AD con TOPdesk - Public, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-111">tooconfigure Azure AD integration with TOPdesk - Public, you need hello following items:</span></span>

- <span data-ttu-id="0e3dc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e3dc-113">Una suscripción habilitada para el inicio de sesión único en TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="0e3dc-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e3dc-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e3dc-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e3dc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e3dc-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e3dc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e3dc-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0e3dc-118">Scenario description</span></span>
<span data-ttu-id="0e3dc-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e3dc-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e3dc-121">Agregar TOPdesk - Public de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0e3dc-121">Adding TOPdesk - Public from hello gallery</span></span>
2. <span data-ttu-id="0e3dc-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-hello-gallery"></a><span data-ttu-id="0e3dc-123">Agregar TOPdesk - Public de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0e3dc-123">Adding TOPdesk - Public from hello gallery</span></span>
<span data-ttu-id="0e3dc-124">integración de hello tooconfigure de TOPdesk - Public en Azure AD, deberá tooadd TOPdesk - Public de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-124">tooconfigure hello integration of TOPdesk - Public into Azure AD, you need tooadd TOPdesk - Public from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e3dc-125">**tooadd TOPdesk - Public de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e3dc-125">**tooadd TOPdesk - Public from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e3dc-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="0e3dc-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e3dc-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="0e3dc-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="0e3dc-133">En el cuadro de búsqueda de hello, escriba **TOPdesk - Public**, seleccione **TOPdesk - Public** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-133">In hello search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de TOPdesk - Public Hola](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0e3dc-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3dc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0e3dc-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TOPdesk - Public con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0e3dc-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e3dc-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TOPdesk - Public es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TOPdesk - Public is tooa user in Azure AD.</span></span> <span data-ttu-id="0e3dc-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TOPdesk - Public debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-138">In other words, a link relationship between an Azure AD user and hello related user in TOPdesk - Public needs toobe established.</span></span>

<span data-ttu-id="0e3dc-139">En TOPdesk - Public, asignar Hola valo hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-139">In TOPdesk - Public, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0e3dc-140">tooconfigure y probar el inicio de sesión único en Azure AD con TOPdesk - Public, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-140">tooconfigure and test Azure AD single sign-on with TOPdesk - Public, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e3dc-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e3dc-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e3dc-143">**[Crear un usuario de prueba pública de TOPdesk -](#create-a-topdesk---public-test-user)**  - toohave un equivalente de Britta Simon en TOPdesk - Public que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - toohave a counterpart of Britta Simon in TOPdesk - Public that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e3dc-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e3dc-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0e3dc-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3dc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0e3dc-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="0e3dc-148">**tooconfigure inicio de sesión único en Azure AD con TOPdesk - Public, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e3dc-148">**tooconfigure Azure AD single sign-on with TOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e3dc-149">En el portal de Azure, en Hola Hola **TOPdesk - Public** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-149">In hello Azure portal, on hello **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="0e3dc-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="0e3dc-153">En hello **TOPdesk - dominio público y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-153">On hello **TOPdesk - Public Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="0e3dc-155">a.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-155">a.</span></span> <span data-ttu-id="0e3dc-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="0e3dc-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="0e3dc-157">b.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-157">b.</span></span> <span data-ttu-id="0e3dc-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="0e3dc-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="0e3dc-159">c.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-159">c.</span></span> <span data-ttu-id="0e3dc-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="0e3dc-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0e3dc-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-161">These values are not real.</span></span> <span data-ttu-id="0e3dc-162">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="0e3dc-163">La dirección URL de respuesta se explica más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="0e3dc-164">Póngase en contacto con [TOPdesk - equipo de soporte técnico de cliente público](https://help.topdesk.com/saas/enterprise/user/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) tooget these values.</span></span>  

4. <span data-ttu-id="0e3dc-165">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="0e3dc-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0e3dc-167">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="0e3dc-169">En hello **TOPdesk - Public Configuration** sección, haga clic en **configurar TOPdesk - Public** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-169">On hello **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0e3dc-170">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="0e3dc-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="0e3dc-172">Inicio de sesión tooyour **TOPdesk - Public** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-172">Sign on tooyour **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="0e3dc-173">Hola **TOPdesk** menú, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-173">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="0e3dc-174">![Configuración](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="0e3dc-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="0e3dc-175">Haga clic en **Login Settings**(Configuración de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="0e3dc-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="0e3dc-176">![Configuración de inicio de sesión](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Configuración de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="0e3dc-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="0e3dc-177">Expanda hello **configuración de inicio de sesión** menú y, a continuación, haga clic en **General**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-177">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="0e3dc-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="0e3dc-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="0e3dc-179">Hola **público** sección de hello **inicio de sesión SAML** configuración sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-179">In hello **Public** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0e3dc-180">![Configuración técnica](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Configuración técnica")</span><span class="sxs-lookup"><span data-stu-id="0e3dc-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="0e3dc-181">a.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-181">a.</span></span> <span data-ttu-id="0e3dc-182">Haga clic en **descargar** toodownload Hola archivo de metadatos públicos y, a continuación, guardarlo localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-182">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="0e3dc-183">b.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-183">b.</span></span> <span data-ttu-id="0e3dc-184">Abrir archivo de metadatos de hello descargado y, a continuación, busque hello **AssertionConsumerService** nodo.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-184">Open hello downloaded metadata file, and then locate hello **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="0e3dc-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="0e3dc-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="0e3dc-186">c.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-186">c.</span></span> <span data-ttu-id="0e3dc-187">Hola copia **AssertionConsumerService** valor, pegue este valor en hello **dirección URL de respuesta** en el cuadro de texto **TOPdesk - dominio público y las direcciones URL** sección.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-187">Copy hello **AssertionConsumerService** value, paste this value in hello **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="0e3dc-188">toocreate un archivo de certificado, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-188">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="0e3dc-189">![Certificado](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificado")</span><span class="sxs-lookup"><span data-stu-id="0e3dc-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="0e3dc-190">a.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-190">a.</span></span> <span data-ttu-id="0e3dc-191">Abra Hola descarga archivo de metadatos desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-191">Open hello downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="0e3dc-192">b.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-192">b.</span></span> <span data-ttu-id="0e3dc-193">Expanda hello **RoleDescriptor** nodo que tenga un **xsi: Type** de **fed: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-193">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="0e3dc-194">c.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-194">c.</span></span> <span data-ttu-id="0e3dc-195">Copiar valor de Hola de hello **X509Certificate** nodo.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-195">Copy hello value of hello **X509Certificate** node.</span></span>
    
    <span data-ttu-id="0e3dc-196">d.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-196">d.</span></span> <span data-ttu-id="0e3dc-197">Hola Guardar copia **X509Certificate** valor localmente en el equipo en un archivo.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-197">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="0e3dc-198">Hola **público** sección, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-198">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="0e3dc-199">![Inicio de sesión SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "Inicio de sesión SAML")</span><span class="sxs-lookup"><span data-stu-id="0e3dc-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="0e3dc-200">En hello **Asistente de configuración de SAML** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-200">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="0e3dc-201">![Asistente para configuración de SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Asistente de configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="0e3dc-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="0e3dc-202">a.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-202">a.</span></span> <span data-ttu-id="0e3dc-203">tooupload los metadatos descargados de archivos desde el portal de Azure, en **metadatos de federación**, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-203">tooupload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="0e3dc-204">b.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-204">b.</span></span> <span data-ttu-id="0e3dc-205">tooupload archivo su certificado, en **certificado (RSA)**, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-205">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="0e3dc-206">c.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-206">c.</span></span> <span data-ttu-id="0e3dc-207">que se obtuvo al equipo de soporte técnico de TOPdesk hello, en el archivo de logotipo de hello tooupload **icono del logotipo de**, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-207">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="0e3dc-208">d.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-208">d.</span></span> <span data-ttu-id="0e3dc-209">Hola **atributo de nombre de usuario** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-209">In hello **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="0e3dc-210">e.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-210">e.</span></span> <span data-ttu-id="0e3dc-211">Hola **nombre para mostrar** cuadro de texto, escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-211">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="0e3dc-212">f.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-212">f.</span></span> <span data-ttu-id="0e3dc-213">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0e3dc-214">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0e3dc-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0e3dc-215">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0e3dc-216">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e3dc-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0e3dc-217">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3dc-217">Create an Azure AD test user</span></span>

<span data-ttu-id="0e3dc-218">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="0e3dc-220">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e3dc-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e3dc-221">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-221">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0e3dc-223">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-223">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0e3dc-225">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-225">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0e3dc-227">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-227">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0e3dc-229">a.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-229">a.</span></span> <span data-ttu-id="0e3dc-230">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-230">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e3dc-231">b.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-231">b.</span></span> <span data-ttu-id="0e3dc-232">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-232">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="0e3dc-233">c.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-233">c.</span></span> <span data-ttu-id="0e3dc-234">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-234">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="0e3dc-235">d.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-235">d.</span></span> <span data-ttu-id="0e3dc-236">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="0e3dc-237">Creación de un usuario de prueba de TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="0e3dc-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="0e3dc-238">En orden tooenable Azure AD a los usuarios toolog en TOPdesk - Public, se les deben aprovisionar en TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-238">In order tooenable Azure AD users toolog into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="0e3dc-239">En caso de hello de TOPdesk - Public, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-239">In hello case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="0e3dc-240">tooconfigure aprovisionamiento de usuario, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-240">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="0e3dc-241">Inicio de sesión tooyour **TOPdesk - Public** como administrador.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-241">Sign on tooyour **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="0e3dc-242">En el menú de hello en la parte superior de hello, haga clic en **TOPdesk \> New \> archivos auxiliares \> persona**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-242">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="0e3dc-243">![Persona](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Persona")</span><span class="sxs-lookup"><span data-stu-id="0e3dc-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="0e3dc-244">En el cuadro de diálogo de hello nueva persona, realice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0e3dc-244">On hello New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="0e3dc-245">![Nueva persona](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Nueva persona")</span><span class="sxs-lookup"><span data-stu-id="0e3dc-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="0e3dc-246">a.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-246">a.</span></span> <span data-ttu-id="0e3dc-247">Haga clic en la ficha General de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-247">Click hello General tab.</span></span>

    <span data-ttu-id="0e3dc-248">b.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-248">b.</span></span> <span data-ttu-id="0e3dc-249">Hola **apellido** cuadro de texto, escriba el apellido del usuario de hello como Simon</span><span class="sxs-lookup"><span data-stu-id="0e3dc-249">In hello **Surname** textbox, type Surname of hello user like Simon</span></span>
 
    <span data-ttu-id="0e3dc-250">c.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-250">c.</span></span> <span data-ttu-id="0e3dc-251">Seleccione un **sitio** de cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-251">Select a **Site** for hello account.</span></span>
 
    <span data-ttu-id="0e3dc-252">d.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-252">d.</span></span> <span data-ttu-id="0e3dc-253">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="0e3dc-254">Puede usar cualquier otra TOPdesk - herramienta de creación de cuentas de usuario público o las API proporcionadas por TOPdesk - cuentas de usuario de tooprovision pública de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0e3dc-255">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3dc-255">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0e3dc-256">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTOPdesk - público.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-256">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTOPdesk - Public.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="0e3dc-258">**tooassign Britta Simon tooTOPdesk - Public, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e3dc-258">**tooassign Britta Simon tooTOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e3dc-259">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-259">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0e3dc-261">En la lista de aplicaciones de hello, seleccione **TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-261">In hello applications list, select **TOPdesk - Public**.</span></span>

    ![Hello TOPdesk - Public vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="0e3dc-263">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-263">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="0e3dc-265">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-265">Click **Add** button.</span></span> <span data-ttu-id="0e3dc-266">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="0e3dc-268">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-268">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e3dc-269">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e3dc-270">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0e3dc-271">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="0e3dc-271">Test single sign-on</span></span>

<span data-ttu-id="0e3dc-272">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-272">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0e3dc-273">Al hacer clic en hello TOPdesk - Public disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour TOPdesk - Public aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e3dc-273">When you click hello TOPdesk - Public tile in hello Access Panel, you should get automatically signed-on tooyour TOPdesk - Public application.</span></span>
<span data-ttu-id="0e3dc-274">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0e3dc-274">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0e3dc-275">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0e3dc-275">Additional resources</span></span>

* [<span data-ttu-id="0e3dc-276">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e3dc-276">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e3dc-277">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e3dc-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

