---
title: "Tutorial: Integración de Azure Active Directory con Ceridian Dayforce HCM | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y gestión de Dayforce Ceridian."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="3dc75-103">Tutorial: Integración de Azure Active Directory con Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="3dc75-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="3dc75-104">En este tutorial, aprenderá cómo toointegrate Ceridian Dayforce gestión con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3dc75-104">In this tutorial, you learn how toointegrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3dc75-105">Integración Ceridian Dayforce gestión con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3dc75-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3dc75-106">Puede controlar en Azure AD que tenga acceso tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="3dc75-106">You can control in Azure AD who has access tooCeridian Dayforce HCM.</span></span>
- <span data-ttu-id="3dc75-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCeridian Dayforce HCM (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dc75-107">You can enable your users tooautomatically get signed-on tooCeridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3dc75-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc75-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="3dc75-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3dc75-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3dc75-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3dc75-110">Prerequisites</span></span>

<span data-ttu-id="3dc75-111">integración de Azure AD con Ceridian Dayforce gestión tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3dc75-111">tooconfigure Azure AD integration with Ceridian Dayforce HCM, you need hello following items:</span></span>

- <span data-ttu-id="3dc75-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dc75-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3dc75-113">Una suscripción habilitada para el inicio de sesión único en Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="3dc75-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3dc75-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3dc75-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3dc75-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3dc75-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3dc75-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3dc75-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3dc75-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3dc75-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3dc75-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3dc75-118">Scenario description</span></span>
<span data-ttu-id="3dc75-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3dc75-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3dc75-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="3dc75-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3dc75-121">Agregar Ceridian Dayforce gestión de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3dc75-121">Adding Ceridian Dayforce HCM from hello gallery</span></span>
2. <span data-ttu-id="3dc75-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dc75-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a><span data-ttu-id="3dc75-123">Agregar Ceridian Dayforce gestión de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3dc75-123">Adding Ceridian Dayforce HCM from hello gallery</span></span>
<span data-ttu-id="3dc75-124">integración de hello tooconfigure de gestión de Dayforce Ceridian en Azure AD, deberá tooadd Ceridian Dayforce gestión de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3dc75-124">tooconfigure hello integration of Ceridian Dayforce HCM into Azure AD, you need tooadd Ceridian Dayforce HCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3dc75-125">**tooadd Ceridian Dayforce gestión de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3dc75-125">**tooadd Ceridian Dayforce HCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dc75-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3dc75-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="3dc75-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3dc75-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="3dc75-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3dc75-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="3dc75-133">En el cuadro de búsqueda de hello, escriba **Ceridian Dayforce gestión**, seleccione **Ceridian Dayforce gestión** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3dc75-133">In hello search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Gestión de Dayforce Ceridian en la lista de resultados de Hola](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3dc75-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dc75-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3dc75-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Ceridian Dayforce HCM con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3dc75-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3dc75-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Ceridian Dayforce gestión es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dc75-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ceridian Dayforce HCM is tooa user in Azure AD.</span></span> <span data-ttu-id="3dc75-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Ceridian Dayforce gestión debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="3dc75-138">In other words, a link relationship between an Azure AD user and hello related user in Ceridian Dayforce HCM needs toobe established.</span></span>

<span data-ttu-id="3dc75-139">En la gestión de Dayforce Ceridian, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dc75-139">In Ceridian Dayforce HCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3dc75-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Ceridian Dayforce gestión, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3dc75-140">tooconfigure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3dc75-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="3dc75-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3dc75-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3dc75-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3dc75-143">**[Crear un usuario de prueba de gestión de Dayforce Ceridian](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave un equivalente de Britta Simon en Ceridian Dayforce gestión que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="3dc75-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - toohave a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3dc75-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3dc75-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3dc75-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3dc75-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3dc75-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dc75-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3dc75-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de gestión de Dayforce Ceridian.</span><span class="sxs-lookup"><span data-stu-id="3dc75-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="3dc75-148">**tooconfigure inicio de sesión único en Azure AD con Ceridian Dayforce gestión, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3dc75-148">**tooconfigure Azure AD single sign-on with Ceridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dc75-149">En el portal de Azure, en Hola Hola **Ceridian Dayforce gestión** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-149">In hello Azure portal, on hello **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="3dc75-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3dc75-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="3dc75-153">En hello **Ceridian Dayforce gestión dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3dc75-153">On hello **Ceridian Dayforce HCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="3dc75-155">a.</span><span class="sxs-lookup"><span data-stu-id="3dc75-155">a.</span></span> <span data-ttu-id="3dc75-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por los usuarios en toosign tooyour aplicación de gestión de Dayforce Ceridian.</span><span class="sxs-lookup"><span data-stu-id="3dc75-156">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="3dc75-157">Environment</span><span class="sxs-lookup"><span data-stu-id="3dc75-157">Environment</span></span> | <span data-ttu-id="3dc75-158">URL</span><span class="sxs-lookup"><span data-stu-id="3dc75-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="3dc75-159">Para producción</span><span class="sxs-lookup"><span data-stu-id="3dc75-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="3dc75-160">Para pruebas</span><span class="sxs-lookup"><span data-stu-id="3dc75-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="3dc75-161">b.</span><span class="sxs-lookup"><span data-stu-id="3dc75-161">b.</span></span> <span data-ttu-id="3dc75-162">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="3dc75-162">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    
    | <span data-ttu-id="3dc75-163">Environment</span><span class="sxs-lookup"><span data-stu-id="3dc75-163">Environment</span></span> | <span data-ttu-id="3dc75-164">URL</span><span class="sxs-lookup"><span data-stu-id="3dc75-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="3dc75-165">Para producción</span><span class="sxs-lookup"><span data-stu-id="3dc75-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="3dc75-166">Para pruebas</span><span class="sxs-lookup"><span data-stu-id="3dc75-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="3dc75-167">c.</span><span class="sxs-lookup"><span data-stu-id="3dc75-167">c.</span></span> <span data-ttu-id="3dc75-168">Hola **dirección URL de respuesta** cuadro de texto, escriba Hola la dirección URL utilizada por la respuesta de Azure AD toopost Hola.</span><span class="sxs-lookup"><span data-stu-id="3dc75-168">In hello **Reply URL** textbox, type hello URL used by Azure AD toopost hello response.</span></span>
    
    | <span data-ttu-id="3dc75-169">Environment</span><span class="sxs-lookup"><span data-stu-id="3dc75-169">Environment</span></span> | <span data-ttu-id="3dc75-170">URL</span><span class="sxs-lookup"><span data-stu-id="3dc75-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="3dc75-171">Para producción</span><span class="sxs-lookup"><span data-stu-id="3dc75-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="3dc75-172">Para pruebas</span><span class="sxs-lookup"><span data-stu-id="3dc75-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="3dc75-173">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3dc75-173">These values are not real.</span></span> <span data-ttu-id="3dc75-174">Actualizar estos valores con hello real identificador, la dirección URL de respuesta y la dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3dc75-174">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="3dc75-175">Póngase en contacto con [equipo de soporte técnico de cliente de gestión de Ceridian Dayforce](https://www.ceridian.com/contact-us/index.html) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="3dc75-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) tooget these values.</span></span>

4. <span data-ttu-id="3dc75-176">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3dc75-176">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="3dc75-178">La aplicación de gestión de Dayforce Ceridian espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="3dc75-178">Your Ceridian Dayforce HCM application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="3dc75-179">Trabajar con [equipo de soporte técnico de gestión de Dayforce Ceridian](https://www.ceridian.com/contact-us/index.html) primer identificador de usuario correctos de hello tooidentify.</span><span class="sxs-lookup"><span data-stu-id="3dc75-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first tooidentify hello correct user identifier.</span></span> <span data-ttu-id="3dc75-180">Microsoft recomienda el uso de hello **"name"** atributo como identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="3dc75-180">Microsoft recommends using hello **"name"** attribute as user identifier.</span></span> <span data-ttu-id="3dc75-181">Puede administrar valores de hello de estos atributos de hello **atributos de usuario** sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3dc75-181">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="3dc75-182">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="3dc75-182">hello following screenshot shows an example for this.</span></span>  

    ![Configurar inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="3dc75-184">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3dc75-184">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="3dc75-185">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="3dc75-185">Attribute Name</span></span>  | <span data-ttu-id="3dc75-186">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="3dc75-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="3dc75-187">name</span><span class="sxs-lookup"><span data-stu-id="3dc75-187">name</span></span>  | <span data-ttu-id="3dc75-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="3dc75-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="3dc75-189">a.</span><span class="sxs-lookup"><span data-stu-id="3dc75-189">a.</span></span> <span data-ttu-id="3dc75-190">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3dc75-190">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="3dc75-193">b.</span><span class="sxs-lookup"><span data-stu-id="3dc75-193">b.</span></span> <span data-ttu-id="3dc75-194">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="3dc75-194">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="3dc75-195">c.</span><span class="sxs-lookup"><span data-stu-id="3dc75-195">c.</span></span> <span data-ttu-id="3dc75-196">Hola **valor** lista, atributo de usuario de hello seleccione desea toouse para su implementación.</span><span class="sxs-lookup"><span data-stu-id="3dc75-196">In hello **Value** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="3dc75-197">Por ejemplo, si desea toouse Hola EmployeeID como identificador de usuario único y lo ha almacenado el valor del atributo de Hola Hola ExtensionAttribute2, a continuación, seleccione **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-197">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="3dc75-198">d.</span><span class="sxs-lookup"><span data-stu-id="3dc75-198">d.</span></span> <span data-ttu-id="3dc75-199">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-199">Click **Ok**.</span></span>

7. <span data-ttu-id="3dc75-200">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3dc75-200">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="3dc75-202">En hello **Ceridian Dayforce gestión configuración** sección, haga clic en **configurar gestión de Dayforce Ceridian** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="3dc75-202">On hello **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3dc75-203">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="3dc75-203">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="3dc75-205">tooconfigure inicio de sesión único en **Ceridian Dayforce gestión** lado, necesita hello toosend descargado **Metadata XML** y **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** demasiado[equipo de soporte técnico de gestión de Dayforce Ceridian](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="3dc75-205">tooconfigure single sign-on on **Ceridian Dayforce HCM** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="3dc75-206">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="3dc75-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3dc75-207">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="3dc75-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3dc75-208">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3dc75-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3dc75-209">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dc75-209">Create an Azure AD test user</span></span>

<span data-ttu-id="3dc75-210">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="3dc75-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="3dc75-212">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3dc75-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dc75-213">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="3dc75-213">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3dc75-215">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-215">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3dc75-217">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3dc75-217">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3dc75-219">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3dc75-219">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3dc75-221">a.</span><span class="sxs-lookup"><span data-stu-id="3dc75-221">a.</span></span> <span data-ttu-id="3dc75-222">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-222">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3dc75-223">b.</span><span class="sxs-lookup"><span data-stu-id="3dc75-223">b.</span></span> <span data-ttu-id="3dc75-224">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3dc75-224">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="3dc75-225">c.</span><span class="sxs-lookup"><span data-stu-id="3dc75-225">c.</span></span> <span data-ttu-id="3dc75-226">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="3dc75-226">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="3dc75-227">d.</span><span class="sxs-lookup"><span data-stu-id="3dc75-227">d.</span></span> <span data-ttu-id="3dc75-228">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="3dc75-229">Crear un usuario de prueba de Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="3dc75-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="3dc75-230">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Ceridian Dayforce gestión toocreate.</span><span class="sxs-lookup"><span data-stu-id="3dc75-230">hello objective of this section is toocreate a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="3dc75-231">Trabajar con hello [equipo de soporte técnico de gestión de Dayforce Ceridian](https://www.ceridian.com/contact-us/index.html) tooget a los usuarios agregados en hello aplicación Ceridian Dayforce gestión.</span><span class="sxs-lookup"><span data-stu-id="3dc75-231">Work with hello [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) tooget users added in hello Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3dc75-232">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dc75-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3dc75-233">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="3dc75-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3dc75-235">**tooassign Britta Simon tooCeridian Dayforce HCM, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3dc75-235">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dc75-236">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3dc75-238">En la lista de aplicaciones de hello, seleccione **Ceridian Dayforce gestión**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-238">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="3dc75-240">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3dc75-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-242">Click **Add** button.</span></span> <span data-ttu-id="3dc75-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3dc75-245">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dc75-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3dc75-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3dc75-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3dc75-248">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dc75-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3dc75-249">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="3dc75-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="3dc75-251">**tooassign Britta Simon tooCeridian Dayforce HCM, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3dc75-251">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dc75-252">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3dc75-254">En la lista de aplicaciones de hello, seleccione **Ceridian Dayforce gestión**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-254">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![vínculo de Ceridian Dayforce gestión de Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="3dc75-256">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="3dc75-258">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-258">Click **Add** button.</span></span> <span data-ttu-id="3dc75-259">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="3dc75-261">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dc75-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3dc75-262">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3dc75-263">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3dc75-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3dc75-264">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="3dc75-264">Test single sign-on</span></span>

<span data-ttu-id="3dc75-265">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3dc75-265">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="3dc75-266">Al hacer clic en icono de gestión de Dayforce Ceridian Hola Hola Panel de acceso, deberá obtener la aplicación de gestión de Dayforce Ceridian tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="3dc75-266">When you click hello Ceridian Dayforce HCM tile in hello Access Panel, you should get automatically signed-on tooyour Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3dc75-267">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3dc75-267">Additional resources</span></span>

* [<span data-ttu-id="3dc75-268">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dc75-268">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3dc75-269">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3dc75-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

