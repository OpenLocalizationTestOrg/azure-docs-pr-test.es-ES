---
title: "Tutorial: Integración de Azure Active Directory con Envoy | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Envoy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="2e35c-103">Tutorial: integración de Azure Active Directory con Envoy</span><span class="sxs-lookup"><span data-stu-id="2e35c-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="2e35c-104">En este tutorial, aprenderá cómo toointegrate Envoy con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e35c-104">In this tutorial, you learn how toointegrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e35c-105">Integración Envoy con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2e35c-105">Integrating Envoy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2e35c-106">Puede controlar en Azure AD que tenga acceso tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="2e35c-106">You can control in Azure AD who has access tooEnvoy.</span></span>
- <span data-ttu-id="2e35c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooEnvoy (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e35c-107">You can enable your users tooautomatically get signed-on tooEnvoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2e35c-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2e35c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="2e35c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e35c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e35c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2e35c-110">Prerequisites</span></span>

<span data-ttu-id="2e35c-111">integración de Azure AD con Envoy tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2e35c-111">tooconfigure Azure AD integration with Envoy, you need hello following items:</span></span>

- <span data-ttu-id="2e35c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e35c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e35c-113">Una suscripción habilitada para el inicio de sesión único en Envoy</span><span class="sxs-lookup"><span data-stu-id="2e35c-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e35c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2e35c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e35c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2e35c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e35c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2e35c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e35c-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e35c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e35c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2e35c-118">Scenario description</span></span>
<span data-ttu-id="2e35c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2e35c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e35c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="2e35c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e35c-121">Agregar Envoy desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2e35c-121">Adding Envoy from hello gallery</span></span>
2. <span data-ttu-id="2e35c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e35c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-hello-gallery"></a><span data-ttu-id="2e35c-123">Agregar Envoy desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2e35c-123">Adding Envoy from hello gallery</span></span>
<span data-ttu-id="2e35c-124">integración de hello tooconfigure de Envoy en Azure AD, deberá tooadd Envoy de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="2e35c-124">tooconfigure hello integration of Envoy into Azure AD, you need tooadd Envoy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2e35c-125">**tooadd Envoy desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2e35c-125">**tooadd Envoy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e35c-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="2e35c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="2e35c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2e35c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="2e35c-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e35c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="2e35c-133">En el cuadro de búsqueda de hello, escriba **Envoy**, seleccione **Envoy** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2e35c-133">In hello search box, type **Envoy**, select **Envoy** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de Envoy Hola](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2e35c-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e35c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2e35c-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Envoy con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2e35c-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e35c-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Envoy es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e35c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Envoy is tooa user in Azure AD.</span></span> <span data-ttu-id="2e35c-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Envoy debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="2e35c-138">In other words, a link relationship between an Azure AD user and hello related user in Envoy needs toobe established.</span></span>

<span data-ttu-id="2e35c-139">En Envoy, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2e35c-139">In Envoy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2e35c-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Envoy, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2e35c-140">tooconfigure and test Azure AD single sign-on with Envoy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2e35c-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="2e35c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2e35c-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e35c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e35c-143">**[Crear un usuario de prueba de Envoy](#create-an-envoy-test-user)**  -toohave un equivalente de Britta Simon en Envoy que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="2e35c-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - toohave a counterpart of Britta Simon in Envoy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2e35c-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2e35c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e35c-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2e35c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2e35c-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e35c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2e35c-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de envío.</span><span class="sxs-lookup"><span data-stu-id="2e35c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="2e35c-148">**inicio de sesión único en tooconfigure Azure AD con Envoy, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2e35c-148">**tooconfigure Azure AD single sign-on with Envoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e35c-149">En el portal de Azure, en Hola Hola **Envoy** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-149">In hello Azure portal, on hello **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="2e35c-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2e35c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="2e35c-153">En hello **Envoy dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2e35c-153">On hello **Envoy Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="2e35c-155">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="2e35c-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="2e35c-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="2e35c-156">This value is not real.</span></span> <span data-ttu-id="2e35c-157">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="2e35c-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="2e35c-158">Póngase en contacto con [equipo de soporte técnico de cliente de Envoy](https://envoy.com/contact/) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="2e35c-158">Contact [Envoy Client support team](https://envoy.com/contact/) tooget this value.</span></span>

4. <span data-ttu-id="2e35c-159">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado...</span><span class="sxs-lookup"><span data-stu-id="2e35c-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate..</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="2e35c-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2e35c-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2e35c-163">En hello **configuración Envoy** sección, haga clic en **configurar Envoy** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="2e35c-163">On hello **Envoy Configuration** section, click **Configure Envoy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2e35c-164">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="2e35c-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="2e35c-166">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Envoy como administrador.</span><span class="sxs-lookup"><span data-stu-id="2e35c-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="2e35c-167">En la barra de herramientas de hello en la parte superior de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-167">In hello toolbar on hello top, click **Settings**.</span></span>

    <span data-ttu-id="2e35c-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="2e35c-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="2e35c-169">Haga clic en **Compañía**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-169">Click **Company**.</span></span>

    <span data-ttu-id="2e35c-170">![Compañía](./media/active-directory-saas-envoy-tutorial/ic776783.png "Compañía")</span><span class="sxs-lookup"><span data-stu-id="2e35c-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="2e35c-171">Haga clic en **SAML**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-171">Click **SAML**.</span></span>

    <span data-ttu-id="2e35c-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="2e35c-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="2e35c-173">Hola **autenticación SAML** configuración sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2e35c-173">In hello **SAML Authentication** configuration section, perform hello following steps:</span></span>

    <span data-ttu-id="2e35c-174">![Autenticación de SAML](./media/active-directory-saas-envoy-tutorial/ic776785.png "Autenticación de SAML")</span><span class="sxs-lookup"><span data-stu-id="2e35c-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="2e35c-175">valor de Hello para el identificador de ubicación HQ hello es generados por la aplicación hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2e35c-175">hello value for hello HQ location ID is auto generated by hello application.</span></span>
    
    <span data-ttu-id="2e35c-176">a.</span><span class="sxs-lookup"><span data-stu-id="2e35c-176">a.</span></span> <span data-ttu-id="2e35c-177">En **huella digital** cuadro de texto, pegue hello **huella digital** valor de certificado en el que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2e35c-177">In **Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="2e35c-178">b.</span><span class="sxs-lookup"><span data-stu-id="2e35c-178">b.</span></span> <span data-ttu-id="2e35c-179">Pegar **SAML Single Sign-On dirección URL del servicio** valor, que ha copiado forman hello Azure portal en hello **URL SAML HTTP de proveedor de IDENTIDADES** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="2e35c-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form hello Azure portal into hello **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="2e35c-180">c.</span><span class="sxs-lookup"><span data-stu-id="2e35c-180">c.</span></span> <span data-ttu-id="2e35c-181">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="2e35c-182">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="2e35c-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2e35c-183">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="2e35c-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2e35c-184">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2e35c-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2e35c-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e35c-185">Create an Azure AD test user</span></span>

<span data-ttu-id="2e35c-186">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="2e35c-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="2e35c-188">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2e35c-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e35c-189">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="2e35c-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2e35c-191">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2e35c-193">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e35c-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2e35c-195">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2e35c-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2e35c-197">a.</span><span class="sxs-lookup"><span data-stu-id="2e35c-197">a.</span></span> <span data-ttu-id="2e35c-198">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e35c-199">b.</span><span class="sxs-lookup"><span data-stu-id="2e35c-199">b.</span></span> <span data-ttu-id="2e35c-200">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e35c-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="2e35c-201">c.</span><span class="sxs-lookup"><span data-stu-id="2e35c-201">c.</span></span> <span data-ttu-id="2e35c-202">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="2e35c-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="2e35c-203">d.</span><span class="sxs-lookup"><span data-stu-id="2e35c-203">d.</span></span> <span data-ttu-id="2e35c-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="2e35c-205">Creación de un usuario de prueba de Envoy</span><span class="sxs-lookup"><span data-stu-id="2e35c-205">Create an Envoy test user</span></span>

<span data-ttu-id="2e35c-206">No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="2e35c-206">There is no action item for you tooconfigure user provisioning tooEnvoy.</span></span> <span data-ttu-id="2e35c-207">Cuando un usuario asignado intenta toolog en Envoy a través de panel de acceso de hello, Envoy comprueba si existe el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2e35c-207">When an assigned user tries toolog into Envoy using hello access panel, Envoy checks whether hello user exists.</span></span> <span data-ttu-id="2e35c-208">Si no hay cuentas de usuario disponibles, Envoy crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2e35c-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2e35c-209">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e35c-209">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2e35c-210">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="2e35c-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEnvoy.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="2e35c-212">**tooassign Britta Simon tooEnvoy, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2e35c-212">**tooassign Britta Simon tooEnvoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e35c-213">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2e35c-215">En la lista de aplicaciones de hello, seleccione **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-215">In hello applications list, select **Envoy**.</span></span>

    ![vínculo de Envoy Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="2e35c-217">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="2e35c-219">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-219">Click **Add** button.</span></span> <span data-ttu-id="2e35c-220">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="2e35c-222">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="2e35c-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2e35c-223">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e35c-224">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2e35c-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2e35c-225">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="2e35c-225">Test single sign-on</span></span>

<span data-ttu-id="2e35c-226">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2e35c-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2e35c-227">Al hacer clic en icono de Envoy Hola Hola Panel de acceso, deberá obtener la aplicación de Envoy tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="2e35c-227">When you click hello Envoy tile in hello Access Panel, you should get automatically signed-on tooyour Envoy application.</span></span>
<span data-ttu-id="2e35c-228">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e35c-228">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2e35c-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2e35c-229">Additional resources</span></span>

* [<span data-ttu-id="2e35c-230">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e35c-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e35c-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2e35c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

